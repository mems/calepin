## Kiosk mode

Aka Assigned Access

Only Professional, Enterprise or Education version

- `Windows + Shift + Enter` (fullscreen mode), like `F11`
- `Set-AssignedAccess  -AppName Microsoft.MicrosoftEdge  -UserName test`
- [Create a Kiosk Experience | Microsoft Docs](https://docs.microsoft.com/en-us/windows-hardware/customize/enterprise/create-a-kiosk-image)
- [Guidelines for choosing an app for assigned access (Windows 10) | Microsoft Docs](https://docs.microsoft.com/en-US/windows/configuration/guidelines-for-assigned-access-app)
- [Set up a kiosk on Windows 10 Pro, Enterprise, or Education (Windows 10) | Microsoft Docs](https://docs.microsoft.com/en-us/windows/configuration/set-up-a-kiosk-for-windows-10-for-desktop-editions)
- [How to Easily Put a Windows PC into Kiosk Mode With Assigned Access](https://www.howtogeek.com/173562/how-to-easily-put-a-windows-pc-into-kiosk-mode-with-assigned-access/)
- [How to Open Internet Explorer in Full Screen or Kiosk Mode](https://www.online-tech-tips.com/internet-explorer-tips/internet-explorer-full-screen/)

## Set up backup

- http://windows.microsoft.com/en-us/windows/back-up-files
- http://windows.microsoft.com/en-us/windows/back-up-restore-faq
- http://windows.microsoft.com/en-us/windows7/How-does-Windows-choose-which-files-to-back-up

## Thumbnail caches

Windows XP, 2000

```
*\Thumbs.db
*\ehthumbs.db
*\ehthumbs_vista.db
```

Windows XP Media Center Edition:

```
#%USERPROFILE%\Local Settings\Application Data\Microsoft\Ehome\Image.db
#%LOCALAPPDATA%\Microsoft\Ehome\Video.db
#%USERPROFILE%\Local Settings\Application Data\Microsoft\Ehome\Video.db
#%LOCALAPPDATA%\Microsoft\Ehome\musicThumbs.db
#%USERPROFILE%\Local Settings\Application Data\Microsoft\Ehome\musicThumbs.db
#%ALLUSERSPROFILE%\Microsoft\eHome\thmb\TVThumb.db
#%ALLUSERSPROFILE%\Application Data\Microsoft\eHome\thmb\TVThumb.db
#%LOCALAPPDATA%\VirtualStore\ProgramData\Microsoft\eHome\thmb\TVThumb.db
#%USERPROFILE%\Local Settings\Application Data\VirtualStore\ProgramData\Microsoft\eHome\thmb\TVThumb.db
```

Windows Vista, 7, 8, 10:

1024, 256, 96 and 32 shows the size of cached thumnails of an image

`thumbcache_*`, `iconcache_*` in `%USERPROFILE%\AppData\Local\Microsoft\Windows\Explorer\*`

- [Windows thumbnail cache — Wikipedia](https://en.wikipedia.org/wiki/Windows_thumbnail_cache)
- [File extension DB - Windows thumbnail database](https://www.file-extensions.org/db-file-extension-windows-thumbnail-database)
- [All you need to know about thumbnail cache files in Windows - gHacks Tech News](http://www.ghacks.net/2014/03/12/thumbnail-cache-files-windows/)
- [Delete Thumbnail Cache thumbcache Files on Windows 7](http://www.kodyaz.com/articles/delete-thumbnail-cache-thumbcache-files-on-windows-7.aspx)
- [Thumbcache Viewer - Extract thumbnail images from the thumbcache_*.db and iconcache_*.db database files.](https://thumbcacheviewer.github.io/)
- [Thumbs Viewer - Extract thumbnail images from the Thumbs.db, ehthumbs.db, ehthumbs_vista.db, Image.db, Video.db, TVThumb.db, and musicThumbs.db database files.](https://thumbsviewer.github.io/)

## Set Keyboard Status at Boot

num lock, scroll lock, caps lock

Navigate to `HKEY_USERS\.DEFAULT\Control Panel\Keyboard`

The value of InitialKeyboardIndicators controls the state of num lock, caps lock and scroll lock:

- 0 = Indicators off
- 1 = Caps Lock on
- 2 = Num Lock on
- 3 = Caps Lock on and Num Lock on
- 4 = Scroll Lock on
- 5 = Caps Lock on and Scroll Lock on
- 6 = Num Lock on and Scroll Lock on
- 7 = Caps Lock on, Num Lock on, and Scroll Lock on

## Install Windows

[Create installation media for Windows - Windows Help](https://support.microsoft.com/en-us/help/15088/windows-10-create-installation-media)

### Variant N and KN

- [Windows 10 editions — Wikipedia](https://en.wikipedia.org/wiki/Windows_10_editions#Variations)

Install the Media Feature Pack:

- [Download Media Feature Pack for N and KN versions of Windows 10 from Official Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=48231)
- [Download Windows 10 Media Feature Pack](https://www.microsoft.com/en-us/software-download/mediafeaturepack)
- [Media Feature Pack list for Windows N editions](https://support.microsoft.com/en-us/help/3145500/media-feature-pack-list-for-windows-n-editions)

## Create a dot file

Or rename, write `.gitignore.` or `.htaccess.` (with both dots). The trailing dot will be removed.

- [How do I manually create a file with a . (dot) prefix in Windows? For example, .htaccess - Stack Overflow](https://stackoverflow.com/questions/5004633/how-do-i-manually-create-a-file-with-a-dot-prefix-in-windows-for-example/38425947#38425947)

## Bash shell on Windows

On Windows 10, [Install the Linux Subsystem](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
Or on Windows 8 install [MSYS2](http://www.msys2.org/) (install in the default folder) (check or update env var `PATH` `C:\msys64\usr\bin`)

```
cmd.exe
> bash
```

Or open command line (in Start > All programms > MSYS2 64bit > MSYS2 MSYS): `C:\msys64\msys2_shell.cmd -msys`
Or:`cmd /c set HOME=%USERPROFILE% & set MSYSTEM=MINGW64 & bash.exe --login -i` where `MSYSTEM` can be `MINGW64`, `MINGW32` or `MSYS`

Alternatively you can use also:

- Cygwin
    - [Cygwin Packages](https://www.cygwin.com/packages/)
    - to choose which package to (re)install, use the setup: [Cygwin Installation](https://cygwin.com/install.html)
- Git for Windows comes with MinGW64 (`%GIT_INSTALL_PATH%/usr/bin`, `%GIT_INSTALL_PATH%/bin`, `%GIT_INSTALL_PATH%/mingw64/bin`)
	- [Git for Windows](https://gitforwindows.org/)
	- [The difference between MINGW and MSYS2 · git-for-windows/git Wiki](https://github.com/git-for-windows/git/wiki/The-difference-between-MINGW-and-MSYS2)
	- [What is Git Bash for Windows anyway? - Super User](https://superuser.com/questions/1053633/what-is-git-bash-for-windows-anyway/1053657#1053657)

	In `C:\Program Files\Git`:
	> `/bin/bash.exe` refers to a redirector that sets up some environment variables and then hands off to `/usr/bin/bash.exe`. This redirector was only invented for backwards compatibility, but apparently is needed for eternity.
	>
	> To sum it up: `/bin/bash.exe` is not the Bash, but relies on `/usr/bin/bash.exe` to do the hard lifting.
	> [...]
	> Use `git-bash.exe` and just use the mintty that comes with Git for Windows
	> - [CTRL -C event is closing the ConsoleZ window instead of returning to a prompt · Issue #262 · cbucher/console](https://github.com/cbucher/console/issues/262#issuecomment-183875609)

	To start bash, in different terminal emulators (interactive shell):

	- [Mintty](https://github.com/mintty/mintty) (that comes with Git for Windows): `C:\Program Files\Git\git-bash.exe`. See [windows - How can I find out the command line options for git-bash.exe? - Super User](https://superuser.com/questions/1104567/how-can-i-find-out-the-command-line-options-for-git-bash-exe)
		[CTRL + C & CTRL + V copy paste · Issue #602 · mintty/mintty](https://github.com/mintty/mintty/issues/602)
	- Windows CMD: `C:\Windows\System32\cmd.exe /c "C:\Program Files\Git\usr\bin\bash.exe" --login -i`
	- PowerShell: `C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -Command "Set-Location -Path (Get-Location); & \"C:\\Program Files\\Git\\usr\\bin\\bash.exe\" --login -i"`

	See also:

	- `pacman -S <package-name>`, [Package management · git-for-windows/git Wiki](https://github.com/git-for-windows/git/wiki/Package-management)
	- [batch file - How to start MingW Console (GitBash) from Command Line on Windows? - Stack Overflow](https://stackoverflow.com/questions/34252265/how-to-start-mingw-console-gitbash-from-command-line-on-windows)
	- [windows 7 - Git: Open Git-Bash in specific directory - Super User](https://superuser.com/questions/1310814/git-open-git-bash-in-specific-directory)
	- [FAQ · git-for-windows/git Wiki](https://github.com/git-for-windows/git/wiki/FAQ#what-is-the-relationship-between-git-for-windows-and-msysgit)
	- [git-for-windows/build-extra: Additional files and scripts to help build Git for Windows on MSYS2.](https://github.com/git-for-windows/build-extra#msys2)
- MinGW64 http://mingw-w64.org/doku.php/start
- MinGW "MSYS" package https://sourceforge.net/projects/mingw/
- GnuWin https://sourceforge.net/projects/gnuwin32/
- Unxutils (check or update env var PATH for both `%WHERE_UNXUTILS_IS%\bin` and `%WHERE_UNXUTILS_IS%\usr\local\wbin`) http://unxutils.sourceforge.net/ `C:\Program Files (x86)\UnxUtils`
	Not updated since 2003
	But sh (zsh) doesn't work propely

For write to clipboard:

`clip` (from `C:\Windows\system32\clip.exe`)

- [Little-known command line utility: clip – The Old New Thing](https://blogs.msdn.microsoft.com/oldnewthing/20091110-00/?p=16093)

## Network

> Run it as administrator, crank up the connection to 100, select the network adapter you're using, choose "Optimal" and hit Save.

> Pro tip: run TCP Analyser (link on homepage) first.
> The MTU and RWIN are the things that get tweaked.

> main win here was actually switching the congestion protocol.

> Most internet connections are PPPoE also, so afterwards select "custom" and click the checkbox. That way correct fragment size is sent to your router and he doesn't have to do splitting (= reduced overhead). Test with "MTU/Latency"

- [SpeedGuide.net :: TCP Optimizer / Downloads](https://www.speedguide.net/downloads.php)
- [35. What are the best TCP Optimizer settings for gaming ? :: SG FAQ](https://www.speedguide.net/faq/35-what-are-the-best-tcp-optimizer-settings-for-474)
- [Secret Tricks To Fix Lag? MTU, TCP Optimizer, Leatrix Lag Fix - YouTube](https://www.youtube.com/watch?v=9J3xZ6hpTXk)

## Keyboard layout

"When using Remote Desktop the keyboard layout always defaults to EN (English)":

```reg
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
"IgnoreRemoteKeyboardLayout"=dword:00000001
```

- [c# - Extracting keyboard layouts from windows - Stack Overflow](https://stackoverflow.com/questions/661722/extracting-keyboard-layouts-from-windows/44392188#44392188)
- [randyrants/sharpkeys: SharpKeys is a utility that manages a Registry key that allows Windows to remap one key to any other key.](https://github.com/randyrants/sharpkeys)
- [Keyboard Manager Overview · microsoft/PowerToys Wiki](https://github.com/microsoft/PowerToys/wiki/Keyboard-Manager-Overview)

- Microsoft Keyboard Layout Creator use .Net
- [grompe/kbdasm: Assembler/disassembler of Windows keyboard layouts in flat assembler](https://github.com/grompe/kbdasm) - Disassemble kayboard layout DLLs
- [ijprest/keyboard-layout-editor: Web application to enable the design & editing of keyboard layouts](https://github.com/ijprest/keyboard-layout-editor)
- [Windows-driver-samples/input/layout at master · microsoft/Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples/tree/master/input/layout)
- [HOWTO: Build keyboard layouts for Windows x64 - Levicki's Tech Spot - levicki.net](https://web.archive.org/web/20200211103320/https://levicki.net/articles/2006/09/29/HOWTO_Build_keyboard_layouts_for_Windows_x64.php)
- [KbdEdit - The Best Keyboard Layout Editor For Windows 10, 8, 7, Vista, XP and 2003 (32- and 64-bit)](http://kbdedit.com/)

### Apple keyboard layout

Useful when you use a remote desktop connection. The host doesn't have the Apple keyboard layout.

```reg
Windows Registry Editor Version 5.00

; Layouts installed by Boot Camp Support driver package
; Layout files are relative to "C:\Windows\System32"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000404]
"Layout Component ID"="7F611C89DF564F01AE5B4A405192D1FB"
"Layout File"="ChinaTA.dll"
"Layout ID"="00e2"
"Layout Text"="Chinese Traditional (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000405]
"Layout Component ID"="0C8DA389245B4792B4960E336F62AC3E"
"Layout File"="CzechA.dll"
"Layout ID"="00d4"
"Layout Text"="Czech (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000406]
"Layout Component ID"="C3996498F423440FB9CE2732A821E7D9"
"Layout File"="DanishA.dll"
"Layout ID"="00cc"
"Layout Text"="Danish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000407]
"Layout Component ID"="B616E2191BF048D4A554E5C6BE224AB4"
"Layout File"="GermanA.dll"
"Layout ID"="00c3"
"Layout Text"="German (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000409]
"Layout Component ID"="B422390FE3C04f3a917D15AD1ACD710F"
"Layout File"="USA.dll"
"Layout ID"="00d1"
"Layout Text"="United States (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000040a]
"Layout Component ID"="C3364C7C44BC444A88A50459135D35B5"
"Layout File"="SpanishA.dll"
"Layout ID"="00c5"
"Layout Text"="Spanish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000040b]
"Layout Component ID"="ECE9937799D242F5AE0CAA446EDEDC62"
"Layout File"="FinnishA.dll"
"Layout ID"="00cb"
"Layout Text"="Finnish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000040c]
"Layout Component ID"="2ECD3C77364749B18E910F9196B420FA"
"Layout File"="FrenchA.dll"
"Layout ID"="00c2"
"Layout Text"="French (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000040e]
"Layout Component ID"="725BE97D2AD14042BA539D96030F93AA"
"Layout File"="HungaryA.dll"
"Layout ID"="00d5"
"Layout Text"="Hungarian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000410]
"Layout Component ID"="6401AAA6058F431181B445C26BEF22D9"
"Layout File"="ItalianA.dll"
"Layout ID"="00c4"
"Layout Text"="Italian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000413]
"Layout Component ID"="3844B95343FB43D68E9695D6E88F016E"
"Layout File"="DutchA.dll"
"Layout ID"="00c1"
"Layout Text"="Dutch (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000414]
"Layout Component ID"="74BE397ABD8143E4960D38111394D1A3"
"Layout File"="NorwayA.dll"
"Layout ID"="00c9"
"Layout Text"="Norwegian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000415]
"Layout Component ID"="D3D2841618E34D09ABBCA0DA34A60FAE"
"Layout File"="PolishA.dll"
"Layout ID"="00cf"
"Layout Text"="Polish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000416]
"Layout Component ID"="326773935C8C4597B0738FE2084D44AD"
"Layout File"="PortuguA.dll"
"Layout ID"="00ce"
"Layout Text"="Portuguese (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000419]
"Layout Component ID"="B0F62A69BE9446488ED502E800DBC36C"
"Layout File"="RussianA.dll"
"Layout ID"="00c8"
"Layout Text"="Russian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000041d]
"Layout Component ID"="8CC8067A1BFF4A0FAD38708DE4CD4BF1"
"Layout File"="SwedishA.dll"
"Layout ID"="00c7"
"Layout Text"="Swedish (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000041f]
"Layout Component ID"="2513D09A670B4d9bA8F1BDAAAA32176F"
"Layout File"="TurkeyQA.dll"
"Layout ID"="00d3"
"Layout Text"="Turkish Q (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000804]
"Layout Component ID"="472ECFB106AE4249B0ADCF62F91D8AEE"
"Layout File"="ChinaSA.dll"
"Layout ID"="00e1"
"Layout Text"="Chinese Simplified (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000809]
"Layout Component ID"="1A4D378083AD454BB4FE02F208614EB6"
"Layout File"="BritishA.dll"
"Layout ID"="00c0"
"Layout Text"="United Kingdom (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000813]
"Layout Component ID"="D70C1682E8F24ED4B5B70AAD37B1BA42"
"Layout File"="BelgiumA.dll"
"Layout ID"="00cd"
"Layout Text"="Belgian (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0000c0c]
"Layout Component ID"="517A729DDEC543E3A7F392E3F130C25F"
"Layout File"="CanadaA.dll"
"Layout ID"="00ca"
"Layout Text"="Canadian Multilingual (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a000100c]
"Layout Component ID"="CE4C7E2419DE400B8A553E1A5C3DCD04"
"Layout File"="SwissA.dll"
"Layout ID"="00c6"
"Layout Text"="Swiss (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a0020409]
"Layout Component ID"="241A34D0-06DB-405e-8B4E-8CA2FC34D1C7"
"Layout File"="IntlEngA.dll"
"Layout ID"="00d0"
"Layout Text"="United States-International (Apple)"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layouts\a100041f]
"Layout Component ID"="D1502D2EF02F4e4b8D313D3C0B0457D0"
"Layout File"="TurkeyA.dll"
"Layout ID"="00d2"
"Layout Text"="Turkish F (Apple)"
```

- [Download and install Windows support software on your Mac - Apple Support](https://support.apple.com/en-us/HT204923)
- [timsutton/brigadier: Fetch and install Boot Camp ESDs with ease.](https://github.com/timsutton/brigadier) - `brigadier -m MacBookPro11,1 -o Bootcamp-MBP11.1`
- [Utiliser un clavier Apple avec Connexion Bureau à distance* – i3idouille](https://web.archive.org/web/20200914101629/https://www.i3idouille.fr/index.php/2011/12/sys-utiliser-un-clavier-apple-avec-connexion-bureau-a-distance/)
- [Use your Apple Keyboard in Windows with Boot Camp - Apple Support](https://support.apple.com/en-us/HT202676)
- [Keyboard mappings using a PC keyboard on a Macintosh](https://support.microsoft.com/en-us/help/970299/keyboard-mappings-using-a-pc-keyboard-on-a-macintosh)
- [Apple - Support - Downloads](https://support.apple.com/downloads/boot-camp)

## Minimal Install

Aka lightweight

- [Download Windows 10 Disc Image (ISO File)](https://www.microsoft.com/en-us/software-download/windows10ISO) - You need a webbrowser on a non Windows OS (you can fake it with the browser dev tools)

- [MSMG Toolkit](https://msmgtoolkit.in/) - Batch command script to install or remove components `(echo A & echo. & echo 1 & echo 3 & echo Y) | toolkit.cmd` `toolkit.cmd <answers.txt` https://stackoverflow.com/a/53421091/470117
- [WinReducer ES Wim Converter - WINREDUCER.NET](https://www.winreducer.net/winreducer-es-wim-converter.html) - convert ESD file to WIM
- [prclaunchky/Windows-10-Super-Minimal](https://github.com/prclaunchky/Windows-10-Super-Minimal)
- [Sycnex/Windows10Debloater: Script to remove Windows 10 bloatware.](https://github.com/Sycnex/Windows10Debloater)
- [Windows 10 Lite (Better Privacy) download | SourceForge.net](https://sourceforge.net/projects/windows-10-lite/)
- [Setting up a Minimal Windows 10 Installation • Archives | Nico Verbruggen](https://web.archive.org/web/20200929053833/https://nicoverbruggen.be/archives/mindows-10)

```
dism /Image:X:ToolKit\Mount\Install /Cleanup-Image /ScanHealth
dism /Image:X:ToolKit\Mount\Install /Cleanup-Image /StartComponentCleanup /ResetBase
```
