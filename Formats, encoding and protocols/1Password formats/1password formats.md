- [Import from Lastpass - Import all entries, but added all information in Notes sections also — AgileBits Support Forum](https://discussions.agilebits.com/discussion/comment/99557/)
- [Importing Acrylic Wallet data into 1Password — AgileBits Support Forum](https://discussions.agilebits.com/discussion/comment/114976/#Comment_114976)

- [Feature requests and pointing out some general shortcomings of 1password... — AgileBits Support Forum](https://discussions.agilebits.com/discussion/34541/feature-requests-and-pointing-out-some-general-shortcomings-of-1password)

## Other formats

Unencrypted data

- 1PIF is a JSON
- CSV

- [Mac to Linux: 1Password to KeePassX – We Saw a Chicken …](http://scruss.com/blog/2013/04/24/mac-to-linux-1password-to-keepassx/) - [scruss/1pw2kpxxml: A program to convert 1Password Interchange File data to KeePassX XML data](https://github.com/scruss/1pw2kpxxml)
- [1PIF file format documentation? — AgileBits Support Forum](https://discussions.agilebits.com/discussion/32993/1pif-file-format-documentation)

## Agile Keychain

**Don't use this format, but [OPVault](#opvault) instead**

`.agilekeychain` and `.cloudKeychain`

Older format, use 1 Password to version 4

1PasswordAnywhere: an html file that decrypt your agil keychain in a browser

- https://com-agilebits-users.s3.amazonaws.com/brenty/1PasswordAnywhere.zip
- [MrC's Convert to 1Password Utility — AgileBits Support Forum](https://discussions.agilebits.com/discussion/30286/mrcs-convert-to-1password-utility/p1)
- [Hello all, I'm the Chief Defender Against the Dark Arts at AgileBits, the makers... | Hacker News](https://news.ycombinator.com/item?id=10410247)
- [Roguelazer/onepasswordpy: Python implementation of 1Password keychains](https://github.com/Roguelazer/onepasswordpy)
- [stayradiated/onepasswordjs: JavaScript implementation of the 1Password cloud keychain](https://github.com/stayradiated/onepasswordjs) - based on OnePasswordPy
- [The continuing evolution of security in 1Password 4](http://wayback.archive.org/web/20140328051731/http://learn.agilebits.com/1Password4/Security/1P4-security-changes.html)
- [Agile Keychain Design | 1Password 3 User Guide](http://wayback.archive.org/web/20140411204743/http://help.agilebits.com:80/1Password3/agile_keychain_design.html)
- [1Password 4 Cloud Keychain design](http://wayback.archive.org/web/20140406224234/http://learn.agilebits.com:80/1Password4/Security/keychain-design.html)
- [passwords - Is 1Password more secure than an AES encrypted text file? - Information Security Stack Exchange](https://security.stackexchange.com/questions/41073/is-1password-more-secure-than-an-aes-encrypted-text-file)
- [Agile Keychain design - 1Password Support](https://support.1password.com/agile-keychain-design/)
- [john-users - Cracking 1Password Agile Keychain files with JtR!](http://www.openwall.com/lists/john-users/2012/07/20/3) - [gwik / agilekeychain — Bitbucket](https://bitbucket.org/gwik/agilekeychain)
	> Password Agile Keychain is very similar (functionality / concept wise) to OS X Keychain. It uses PBKDF2-SHA1 with 1,000 iterations and AES-128 in CBC mode. Cracking speeds are almost same as OS X Keychain cracking speeds. The format scales almost linearly with number of cores
- [alsemyonov/one_password: Decryptor of 1Password Agile Keychain](https://github.com/alsemyonov/one_password)
- [Bitcrack's Bl0g: Cracking the 1Password Master Password](http://blog.bitcrack.net/2013/04/cracking-1password-master-password-it.html) - [rurapenthe/1pass2hashcat: The 1Pass 2 Hashcat Tool that Extracts the Master Password in a format Hashcat can process.](https://github.com/rurapenthe/1pass2hashcat)

## OPVault

`.opvault`

Replace [Agile Keychain](#agile-keychain)

- [How to switch to the OPVault format from Agile Keychain - 1Password Support](https://support.1password.com/cs/switch-to-opvault/)
- [OPVault design - 1Password Support](https://support.1password.com/opvault-design/)
- [Additional files related to 1Password security documents](https://cache.agilebits.com/security-kb/)
- [OPVault implementation details — AgileBits Support Forum](https://discussions.agilebits.com/discussion/77406/opvault-implementation-details)
- [keanulee/opvault-viewer](https://github.com/keanulee/opvault-viewer)
- [miquella/opvault: Go package for reading the 1Password OPVault format](https://github.com/miquella/opvault)
- [OblivionCloudControl/opvault: Python library to access 1Password OPVault stores](https://github.com/OblivionCloudControl/opvault)
- [Search · opvault](https://github.com/search?utf8=%E2%9C%93&q=opvault&type=)
- [rnml / opvault — Bitbucket](https://bitbucket.org/rnml/opvault)

## Importers

- [MrC's Convert to 1Password Utility — AgileBits Support Forum](https://discussions.agilebits.com/discussion/30286/mrcs-convert-to-1password-utility/p1)
- [agilebits/onepassword-utilities: Utilities for 1Password](https://github.com/agilebits/onepassword-utilities)

## 1Password network sync

- [About the 1Password security model - 1Password Support](https://support.1password.com/1password-security/)
- [The 1Password for Teams security design - 1Password for Teams White Paper.pdf](https://1password.com/files/1Password%20for%20Teams%20White%20Paper.pdf)

- [OPVault design - 1Password Support](https://support.1password.com/opvault-design/)

- [WLAN Server with multiple Macs, Folder sync options — AgileBits Support Forum](https://discussions.agilebits.com/discussion/76296/wlan-server-with-multiple-macs-folder-sync-options)
- [Automatic Backup of 1Password Data to a Thumb Drive](http://chauncey.io/posts/automatic-backup-of-1password-data-to-a-thumb-drive/)
- [Folder sync completely broke recently — AgileBits Support Forum](https://discussions.agilebits.com/discussion/76231/folder-sync-completely-broke-recently)
- [Folder sync: please clarify the instructions — AgileBits Support Forum](https://discussions.agilebits.com/discussion/25427/folder-sync-please-clarify-the-instructions)
- [Problem with Folder Sync on Network Drive — AgileBits Support Forum](https://discussions.agilebits.com/discussion/56873/problem-with-folder-sync-on-network-drive)

- [bash - RSync only if filesystem is mounted - Stack Overflow](https://stackoverflow.com/questions/27359/rsync-only-if-filesystem-is-mounted/27370#27370)
- [linux - What's the best way to check if a volume is mounted in a Bash script? - Server Fault](https://serverfault.com/questions/50585/whats-the-best-way-to-check-if-a-volume-is-mounted-in-a-bash-script/50601#50601)