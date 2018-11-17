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

0 - Indicators off
1 - Caps Lock on
2 - Num Lock on
3 - Caps Lock on and Num Lock on
4 - Scroll Lock on
5 - Caps Lock on and Scroll Lock on
6 - Num Lock on and Scroll Lock on
7 - Caps Lock on, Num Lock on, and Scroll Lock on 