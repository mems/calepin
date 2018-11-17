## Maildir

- [MailboxFormat/Maildir - Dovecot Wiki](http://wiki2.dovecot.org/MailboxFormat/Maildir)
- [Maildir — Wikipedia](https://en.wikipedia.org/wiki/Maildir)

See [mbox — Wikipedia](https://en.wikipedia.org/wiki/Mbox)

### Thunderbird

- https://gist.github.com/mems/802213a81ab819afda66083e25e85684
- [Thunderbird/Maildir - MozillaWiki](https://wiki.mozilla.org/Thunderbird/Maildir)
- [Maildir in Thunderbird | Thunderbird Help](https://support.mozilla.org/en-US/kb/maildir-thunderbird)

Email file name is the timestamp when the email is stored, moved (in microseconds). Example: `1466698612265640`, start with `From - Thu Jun 23 18:16:52 2016` (`Thu Jun 23 2016 18:16:52 GMT+0200 (CEST)`) 

Use NodeJS to convert mbox to maildir:

	// Note: this script not work properly if an email contains "\n\nFrom - "
	const fs = require('fs');
	const path = require('path');
	const readline = require('readline');
	
	let file = process.argv[2];
	let tmpFile = file + ".tmp";
	fs.renameSync(file, tmpFile);
	let folder = file;
	fs.mkdirSync(folder);
	let curFolder = folder + path.sep + "cur";
	fs.mkdirSync(curFolder);
	fs.mkdirSync(folder + path.sep + "tmp");
	
	let rl = readline.createInterface({
		input: fs.createReadStream(tmpFile)
	});
	// each entry is separated by "\n\n" (or "\r\n", "\n\r", "\r\r")
	let emptyLines = 0;//consecutive empty lines
	let buffer = "";
	let count = 0;
	
	function writeEntry(data = ""){
		//if(!data.startWith("From - ")){
		if(!data.substr(0, 7) === "From - "){
			throw new Error(`Invalid entry "${data.substr(0, 10)}…"`);
		}
		
		data += "\n";// newline at the end
		let date = data.substring(7, data.indexOf("\n"));//"From - (.*)"
		let timestamp = Date.parse(date);// What about timezone?
		if(Number.isNaN(timestamp)){
			throw new Error(`Invalid entry date "${date}"`);
		}
		timestamp *= 1000;// in microseconds
		timestamp += Math.round(Math.random() * 999999);//add random milliseconds + microseconds
		fs.writeFile(curFolder + "/" + timestamp, data, "utf8", error => error && console.warn(error));
	}
	
	// Each line
	rl.on("line", (line) => {
		// If an empty line
		if(line === ""){
			emptyLines++;
		}
		// If previous lines are empty
		else{
			// End of previous entry
			// What happend a message contains "\n\nFrom - " ? like embedded emails
			//if(emptyLines >= 1 && line.startWith("From - ")){
			if(emptyLines >= 1 && line.substr(0, 7) === "From - "){
				count++;
				writeEntry(buffer.trim());
				buffer = "";
			}
		
			emptyLines = 0;
		}
		
		buffer += line + "\n";
	});
	rl.on("close", () => {
		// For the last entry
		buffer = buffer.trim();
		if(buffer !== ""){
			count++;
			writeEntry(buffer);
		}
		
		console.log(`${count} entrie(s) founded in "${file}"`);
	});

- [mbox2maildir Perl script](http://untroubled.org/mbox2maildir)
- [Converting Mbox mailboxes to Maildir format with mb2md.pl](http://batleth.sapienti-sat.org/projects/mb2md/)
- [Thunderbird/MBOX to IMAP/Maildir migration done easy with mb2md](http://realtechtalk.com/thunderbirdmbox_to_imapmaildir_migration_done_easy_with_mb2md-1134-articles)
- [Migration/MailFormat - Dovecot Wiki](http://wiki2.dovecot.org/Migration/MailFormat)
- [Importing and exporting your mail - MozillaZine Knowledge Base](http://kb.mozillazine.org/Importing_and_exporting_your_mail)
- [Migrating local Thunderbird mail folders to an IMAP server | barncrew.com](http://www.barncrew.com/migrating-local-thunderbird-mail-folders-to-an-imap-server/)