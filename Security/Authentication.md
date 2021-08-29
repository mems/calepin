- [Authentication Cheat Sheet - OWASP](https://www.owasp.org/index.php/Authentication_Cheat_Sheet)
- [The Current State Of Authentication: We Have A Password Problem – Smashing Magazine](https://www.smashingmagazine.com/2016/06/the-current-state-of-authentication-we-have-a-password-problem/)
- [Security token — Wikipedia](https://en.wikipedia.org/wiki/Security_token)
- [Password — Wikipedia](https://en.wikipedia.org/wiki/Password#Alternatives_to_passwords_for_authentication)
- [GRC's | SQRL Secure Quick Reliable Login  ](https://www.grc.com/sqrl/sqrl.htm)
- [Authentication — Wikipedia](https://en.wikipedia.org/wiki/Authentication)
- [Category:Authentication methods — Wikipedia](https://en.wikipedia.org/wiki/Category:Authentication_methods)
- [teesloane/Auth-Boss: Become an Auth Boss. Learn about different authentication methodologies on the web.](https://github.com/teesloane/Auth-Boss)

What happend if a user use products where with a domain used to redirect him, could be owned after some time by a third party: [Bugtraq: Logic security flaw in TP-LINK - tplinklogin.net](http://seclists.org/bugtraq/2016/Jul/3)

## JSON Web Tokens

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

## Login with email

> If you are storing email addresses then you probably should store them in their original case (the recipient at least) to be safe. However, always compare them case-insensitively in order to avoid duplicates.
– [I it ok to use uppercase letter in email address? - Webmaster Stack Exchange](https://webmasters.stackexchange.com/questions/34056/is-it-ok-to-use-uppercase-letters-in-email-address/34058#34058)

> The local mailbox part (the username), however, is case sensitive. The email address ReCipiENt@eXaMPle.cOm is indeed different from recipient@example.com (but it the same as ReCipiENt@example.com).
>
> Simply put: Only the username itself is case sensitive. Email addresses are not affected by the case.
— [Are email addresse case sensitive? - Quora](https://www.quora.com/Are-email-addresses-case-sensitive)

> The local-part of a mailbox MUST BE treated as case sensitive. Therefore, SMTP implementations MUST take care to preserve the case of mailbox local-parts. Mailbox domains are not case sensitive. In particular, for some hosts the user "smith" is different from the user "Smith". However, exploiting the case sensitivity of mailbox local-parts impedes interoperability and is discouraged.
— https://www.rfc-editor.org/rfc/rfc2821.txt

## “Invalid Username or Password”, a useless security measure

You can confirm if an username exist by trying to create an new account with the same username.

https://kev.inburke.com/kevin/invalid-username-or-password-useless/

> - Rate limiting can go a fair way to preventing brute force attacks. To find email addresses, an attacker is going to need to try a lot of email addresses and/or a lot of passwords, and get a lot of them wrong. Consider throttling invalid login attempts by IP address or subnet. Check submitted passwords against a dictionary of common passwords (123456, monkey, etc) and ban that traffic extra hard. Exponential backoff (forcing attackers to try again after 1, 2, 4, 8, 16.. seconds) is useful.
> - Give guidance to users about creating strong passwords. Allow easy integration with LastPass or 1Password.
> - Add a 2-factor auth option to your website. Encourage users to use it.
> - Warn users about malicious behavior ("someone is trying to snoop your password") and contact them about suspicious logins.

## Graphical password

- [Cyberspace of Shujun LI - Graphical Passwords](http://www.hooklee.com/default.asp?t=Graphical%20Passwords)
- [Mot de passe visuel : pas la panacée - ZDNet](http://www.zdnet.fr/actualites/mot-de-passe-visuel-pas-la-panacee-39794074.htm)

## Password

- [Password storage](./Data%20access%20and%20integrity/Data%20access%20and%20integrity.md#password-storage)
- [Password Guidance: Simplifying Your Approach | CESG Site](https://www.cesg.gov.uk/guidance/password-guidance-simplifying-your-approach)
- [Offensive Passwords – Tim MalcomVetter – Medium](https://medium.com/@malcomvetter/offensive-passwords-451371ccd02e)
- [Password — Wikipedia](https://en.wikipedia.org/wiki/Password)
- [CmosPwd - CGSecurity](http://www.cgsecurity.org/wiki/CmosPwd) decrypts password stored in cmos (for BIOS SETUP)
- [Creating Secure Password Resets With JSON Web Tokens – Smashing Magazine](https://www.smashingmagazine.com/2017/11/safe-password-resets-with-json-web-tokens/) - Password reset workflow

- [AgileBits Blog | Security](https://blog.agilebits.com/category/security/)
- [The 1Password Emergency Kit: Version 3.0 - Productivityist](https://productivityist.com/1password-emergency-kit-3/) - Emergency Kit for recover passwords and keys (ex: in case something happen to you)

Be carefull with renew password links send by email. See [Password-less login problems](#password-less-login).

Use a password manager:

- [Password Manager for Families, Businesses, Teams | 1Password](https://1password.com/)
- [Open Source Password Management Solutions | Bitwarden](https://bitwarden.com/)

More informations about password managers:

- [Switching from 1Password to Bitwarden | joshua stein](https://jcs.org/2017/11/17/bitwarden)
- [rubywarden/API.md at master · jcs/rubywarden](https://github.com/jcs/rubywarden/blob/master/API.md)
- [jcs/rubywarden: An unofficial, mostly Bitwarden-compatible API server written in Ruby (Sinatra and ActiveRecord)](https://github.com/jcs/rubywarden)
- [vvondra/bitwarden-serverless: Implementation of the Bitwarden API using an AWS serverless stack](https://github.com/vvondra/bitwarden-serverless)
- [rubywarden/1password_import.rb at master · jcs/rubywarden](https://github.com/jcs/rubywarden/blob/master/tools/1password_import.rb)

### Password reuse

![Du bruker ikke samme børste overalt, hvorfor bruke samme passord?](brush-password-reuse.png)

> You don’t use the same brush everywhere, so why do you reuse the same password?
> — [Robert Malmgren on Twitter: "Awesome, and very graphical, Norwegian info card about password security - ”You don’t use the same brush everywhere, so why do you reuse the same password?”. An excellent question!… https://t.co/WDSJHlJ7Jw"](https://twitter.com/mitt_nya_nym/status/1009350180766928896)

- [Musematte - børster - NorSIS nettbutikk](https://norsis.no/nettbutikk/produkt/musematte/)
- [Plakat 1 - børster - NorSIS nettbutikk](https://norsis.no/nettbutikk/produkt/plakat-1/)

### Password rules

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

### Password leaks

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

### SSO

Aka Single sign-on.

If credentials leak, this could give access to more than one application/website.

Note: If for any reason (a good or not) the SSO provider could disable/delete the account. Some implementation don't provide a way to use an other method to sign-in, that means the user will be locked out. [Never Use Google to Sign-In | Gurjeet Singh](https://web.archive.org/web/20201114181850/https://gurjeet.singh.im/blog/never-use-google-to-sign-in)

Examples: OAuth, Google, Facebook, Twitter, LinkedIn, Github, etc.

### Password hash cracking

- [Your Password is Too Damn Short](http://blog.codinghorror.com/your-password-is-too-damn-short/)
- [Rainbow table — Wikipédia](https://fr.wikipedia.org/wiki/Rainbow_table)

### Fcrack zip

```
-l (#-#): specify the minimum and maximum length of passwords to check
-b : use brute force to crack the password
-c (charset): specify the character set to use
-u : unzip / filter incorrect passwords
```

- [fcrackzip- Port | MacPorts](https://ports.macports.org/port/fcrackzip/summary)

### John the ripper

```sh
zip2john /path/to/file.zip > zip_hash.txt
john –wordlist=/path/to/wordlist.txt zip_hash.txt
```

- [john-jumbo- Port | MacPorts](https://ports.macports.org/port/john-jumbo/summary)
- [RaiderSec: Cracking Unix Password Hashes with John the Ripper (JTR)](http://raidersec.blogspot.fr/2013/01/cracking-unix-passwords-with-john.html)

## Password-less login

Use an access token or a public-private key (ex: SSH key)

> provide only your email address and a link is sent to that email address. You click the link, which contains a special login code, and the website logs you in and deactivates the code so it can no longer be used. Subsequent visits to that URL just give a 403. In other words, every login is treated like a password reset. For many use cases, this could be a real pain, but for the case of, say, a site where a handful of internal users need access to an admin panel, it’s really nice to not have to deal with one more password.
> — http://jon.smajda.com/2014/10/20/mailbox-and-facebook-app-links/

**[But use POST not GET!](http://blog.teamtreehouse.com/the-definitive-guide-to-get-vs-post)** 15min lifetime, 1 usage, only sent by a user request (from the app/website)

- [Passwordless SSH using public-private key pairs | Enable Sysadmin](https://www.redhat.com/sysadmin/passwordless-ssh)
- [Understanding SSH Key Pairs :: WinSCP](https://winscp.net/eng/docs/ssh_keys)
- [Generating a new SSH key and adding it to the ssh-agent - GitHub Help](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Suppression des mots de passe : des paroles de Google aux actes de Medium - Next INpact](http://www.nextinpact.com/news/95657-supprimer-mots-passe-google-en-parle-medium-propose-alternative.htm)
- [Le mot de passe, espèce en voie de disparition](http://www.lemonde.fr/pixels/article/2015/03/19/le-mot-de-passe-espece-en-voie-de-disparition_4596536_4408996.html)

Problems:

- This unique URL can leak
	- [Why you shouldn’t share links on Facebook — Medium](https://medium.com/@intideceukelaire/why-you-shouldnt-share-links-on-facebook-f317ba4aa58b)
	- [Password-less login – Find Work – Medium](https://medium.com/findworkco/password-less-login-df0354c3f3ee)
- links could be visited by robots (search engine, anti-virus scanner) or browser (prebrowser: prerender, preload, etc.)
	> BingPreview in Outlook webmail scans links when users open their email - invalidating one-time use links.
	— https://twitter.com/simonw/status/841090452543561729

## TOTP

Should not used to authentificate users, but only validate the auth request (2 factor auth) because secret key can be stolen on the client or the server side.

Can be use to open a port for SSH login: https://github.com/benjojo/totp-ssh-fluxer

- [Time-based One-time Password Algorithm — Wikipedia](https://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm)
- [Activation de la double authentification - Bienvenue sur le wiki Gandi - Gandi Docs](https://wiki.gandi.net/fr/contacts/login/2-factor-activation#des_applications_totp)
- [Google TOTP Two-factor Authentication for PHP | Application Security](https://www.idontplaydarts.com/2011/07/google-totp-two-factor-authentication-for-php/) - implementation of Google TOTP

## Client certificate

Authenticate clients with certificates

- [SSL/TLS Strong Encryption: How-To - Apache HTTP Server Version 2.2](https://httpd.apache.org/docs/2.2/ssl/ssl_howto.html#accesscontrol)
- [Technology/KnowledgeBase/ClientCerts - CAcert Wiki](http://wiki.cacert.org/Technology/KnowledgeBase/ClientCerts)
- [FAQ/ImportRootCert - CAcert Wiki](http://wiki.cacert.org/FAQ/ImportRootCert)
- [FAQ/BrowserClients - CAcert Wiki](http://wiki.cacert.org/FAQ/BrowserClients#Importing_the_CAcert_Root_Certificate)
- [Installing the Certificate through the Web Browser](http://help-icc.untangle.com/Content/User%20Guide/UI_Tabs/SSLCertificateGPO_v4/Appendix%20B%20Installing%20the.htm) and [Using client side ssl certificates in firefox and chrome](http://www.binarytides.com/client-side-ssl-certificates-firefox-chrome/)
- [ssl - How to install trusted CA certificate on Android device? - Stack Overflow](https://stackoverflow.com/questions/4461360/how-to-install-trusted-ca-certificate-on-android-device/)

## Biometrics

Face, fingerprint, iris/retina and DNA

**Never use biometrics as authentification, because we can't change it if it's compromised (biometric thieft).** And also because not everyone own it (inherited gene mutation / defect) or it could be lost / altered after an accident, a disease, etc.

> Biometrics are a username, not a password.
>
> — https://twitter.com/netik/status/924333873252646914

> It is plain stupid to use something that you can't change and that you leave everywhere every day as a security token
>
> — Frank Rieger from Chaos Computer Club: [CCC | Chaos Computer Club breaks Apple TouchID](http://www.ccc.de/en/updates/2013/ccc-breaks-apple-touchid)

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
- [The family with no fingerprints - BBC News](https://web.archive.org/web/20201227092611/https://www.bbc.com/news/world-asia-55301200)
- cosmetic iris

## Two-factor authentication

Aka 2FA

> My Twitter account, two email addresses, & my phone. It was not due to passwords, they hacked my phone account itself.
> Someone called @verizon impersonating me and successfully changed my SIM & unsuccessfully attempted to change my phone number.
> By calling @verizon and successfully changing my phone's SIM, the hacker bypassed two-factor verification which I have on all accounts.
> The hacker got access by changing my SIM which redirected texts, then resetting my passwords to trigger two-factor authentication.
— https://twitter.com/deray/status/741356147479842816

- [Two-factor authentication — Wikipedia](https://en.wikipedia.org/wiki/Two-factor_authentication)
- [Two Factor Auth List](https://twofactorauth.org/)

## Software keys

Each version has private key to decode unique certificat from software version + user name encoded with public key (specific for a version of the software)

## Usurpation & social engineering

- [TIL that someone can change your Facebook email, password, and two step verification just by asking Facebook to turn off login approvals, and sending in a fake ID. (Happened to me lost all my business pages) : technology](https://www.reddit.com/r/technology/comments/4q8ywp/til_that_someone_can_change_your_facebook_email/)
- [Amazon’s customer service backdoor — Medium](https://medium.com/@espringe/amazon-s-customer-service-backdoor-be375b3428c4#.vfpvsk8yl)
- [Social engineering (security) — Wikipedia](https://en.wikipedia.org/wiki/Social_engineering_(security))
- [Thermal Attacks on Mobile-based User Authentication](http://www.mkhamis.com/data/papers/abdelrahman2017chi.pdf) - See also [Thermal Cameras Can See How You Enter Your Smartphone PIN - The Atlantic](https://www.theatlantic.com/amp/article/519069/)
