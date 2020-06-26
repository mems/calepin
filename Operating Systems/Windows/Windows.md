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

	*\Thumbs.db
	*\ehthumbs.db
	*\ehthumbs_vista.db

Windows XP Media Center Edition:

	#%USERPROFILE%\Local Settings\Application Data\Microsoft\Ehome\Image.db
	#%LOCALAPPDATA%\Microsoft\Ehome\Video.db
	#%USERPROFILE%\Local Settings\Application Data\Microsoft\Ehome\Video.db
	#%LOCALAPPDATA%\Microsoft\Ehome\musicThumbs.db
	#%USERPROFILE%\Local Settings\Application Data\Microsoft\Ehome\musicThumbs.db
	#%ALLUSERSPROFILE%\Microsoft\eHome\thmb\TVThumb.db
	#%ALLUSERSPROFILE%\Application Data\Microsoft\eHome\thmb\TVThumb.db
	#%LOCALAPPDATA%\VirtualStore\ProgramData\Microsoft\eHome\thmb\TVThumb.db
	#%USERPROFILE%\Local Settings\Application Data\VirtualStore\ProgramData\Microsoft\eHome\thmb\TVThumb.db

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
