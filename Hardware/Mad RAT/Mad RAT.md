Mad Catz RAT

## Rollover issue

The mouse have issue with hover state in macOS, **use USBOverdrive** to fix this issue.
Note: Mad Catz RAT official driver is not anymore available (2017)

Some times the issue with the hover state can occur (again, doesn't appears in USBOverdrive Status), just unplug then plug again with the wire.

See:

- [macos - No hover feedback in OS X Yosemite - Ask Different](https://apple.stackexchange.com/questions/151308/no-hover-feedback-in-os-x-yosemite)
- [macos - How do I resolve the MADCATZ R.A.T 9 cursor bug in El Capitan? - Ask Different](https://apple.stackexchange.com/questions/200274/how-do-i-resolve-the-madcatz-r-a-t-9-cursor-bug-in-el-capitan)
- [Mad Catz M.O.U.S.9 and OS X Mavericks not playing nice - AnandTech Forums: Technology, Hardware, Software, and Deals](https://forums.anandtech.com/threads/mad-catz-m-o-u-s-9-and-os-x-mavericks-not-playing-nice.2360002/)
- [Mad Catz : OSXElCapitan](https://www.reddit.com/r/OSXElCapitan/comments/3n6ajf/mad_catz/)

## ?

ftp://ftp.saitek.com/pub/
ftp://ftp.saitek.com/pub/support/.hg.zip


/Applications/Mad Catz Editor.app
/System/Library/CyborgRAT.kext
/Library/PreferencePanes/MadCatzRAT.prefPane
/Library/PrivilegedHelperTools/MadCatzSmartTechnology.app
/Library/Application Support/Smart Technology/Devices/CyborgRAT.bundle
/Library/Application Support/Smart Technology/Devices/CyborgRAT.bundle/Contents/Resources/Default.pr0
~/Library/Application Support/Smart Technology/RAT/%CUSTOM_PROFILE_%.pr0

/Library/Application Support/Smart Technology/Devices/CyborgRAT.bundle/Contents/Resources/js/js.h : Base64 JS

- [osx - No hover feedback in OS X Yosemite - Ask Different](http://apple.stackexchange.com/questions/151308/no-hover-feedback-in-os-x-yosemite)
- [Cyborg RAT 7 - It has NEVER worked on my Mac! | MacRumors Forums](http://forums.macrumors.com/threads/cyborg-rat-7-it-has-never-worked-on-my-mac.1433546/)
- https://twitter.com/MadCatz
- https://github.com/quarterto/Dotfiles/blob/master/cyborgrat/install.sh
- https://github.com/Darkstrumn/MadCatz_AutoProfiler
- https://github.com/martinhovorka/config-x11-rat7-rat9
- https://github.com/MayeulC/Saitek
- https://github.com/MayeulC/Saitek/wiki/R.A.T-9-USB-Documentation
- https://gist.github.com/kureshii/be2f5235346f98d47bf8
- https://delightlylinux.wordpress.com/2012/03/07/using-the-cyborg-r-a-t-7-with-ubuntu/
- https://wiki.archlinux.org/index.php/Mad_Catz_Mouse
- https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-input-evdev/+bug/615892
- https://github.com/xwavex/pyRAT
- https://github.com/fisadev/system-install/tree/master/rat7
- https://github.com/greg-js/arch-wiki-md-repo/blob/master/wiki/_content/english/Mad%20Catz%20Mouse.md
- https://github.com/rkruk/R.A.T.-Cyborg-Mouse-on-Linux
- https://github.com/UserXXX/Claw/tree/master and https://github.com/UserXXX/Claw/wiki/The-pr0-file-format

	Section "InputClass"
		Identifier "R.A.T."
		MatchProduct "R.A.T.7|R.A.T.9"
		MatchDevicePath "/dev/input/event*"
		Option "Buttons" "17"
		Option "ButtonMapping" "1 2 3 4 5 0 0 8 9 7 6 12 0 0 0 16 17"
		Option "AutoReleaseButtons" "13 14 15"
		Option "ZAxisMapping" "4 5 6 7"
	EndSection