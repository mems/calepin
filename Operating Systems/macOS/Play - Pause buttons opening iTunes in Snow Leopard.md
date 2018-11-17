Quit iTunes
Locate iTunes.app in Finder (In Finder: Menu › Go › Applications...)
Ctrl-click on the iTunes.app-file and select 'Compress "iTunes.app"' (for backup)
Ctrl-click on the iTunes.app-file and select 'Show Package Contents'
Locate the file 'Info.plist' inside the folder 'Contents'
Ctrl-click 'Info-plist' and select 'Open with..' and select 'TextEdit' (or your favourite text-editor. Not Word tho.)

Near the bottom of the file locate the following segment:

    <key>CFBundleIdentifier</key>
    <string>com.apple.iTunes</string>

Change the last 's' in the word 'iTunes' to 'z', like so:

    <key>CFBundleIdentifier</key>
    <string>com.apple.iTunez</string>

Save the file
IMPORTANT: Drag the file 'iTunes.app' out of the Applications-folder and on to the Desktop
Drag the file 'iTunes.app' back into the Applications folder
(You should probably disable the iTunesHelper. This can be done by going to System Preferences › Accounts › (Your account) › Login Items and remove the 'iTunesHelper'.)
Log out and log in

- http://forums.macgeneration.com/mac-os-x/patch-pour-les-touches-play-pause-sous-snow-leopard-300962.html -> http://nomitsu-kronos.hd.free.fr/contents/MMFix.tgz
- http://superuser.com/questions/31925/stop-play-pause-button-opening-itunes-in-snow-leopard