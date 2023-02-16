## Android SDK

- [How to install Android SDK and setup AVD Emulator without Android Studio](https://medium.com/michael-wallace/how-to-install-android-sdk-and-setup-avd-emulator-without-android-studio-aeb55c014264)
- [Start the emulator from the command line  |  Développeurs Android](https://developer.android.com/studio/run/emulator-commandline)

### Emulator

Start `./android`, then tools > Mangage AVDs...

```sh
cd ~/Library/Android/sdk/tools/bin && ./avdmanager list avd
```

- HAXM `sudo kextload /Library/Extensions/intelhaxm.kext` (Need to allow it: Settings > Security & Privacy)
- `kextstat | grep intel`, `ls /dev/HAX`
- `sudo /Library/Extensions/intelhaxm.kext/Contents/Resources/uninstall.sh`
- `sudo /Library/Android/sdk/tools/bin/sdkmanager --update --sdk_root=/Library/Android/sdk`
- [gitlab ci - Android Command line tools sdkmanager always shows: Warning: Could not create settings - Stack Overflow](https://stackoverflow.com/questions/60440509/android-command-line-tools-sdkmanager-always-shows-warning-could-not-create-se)
- [Installation Instructions on macOS · intel/haxm Wiki](https://github.com/intel/haxm/wiki/Installation-Instructions-on-macOS)
- [Run Apps on the Android Emulator | Android Studio](https://developer.android.com/studio/run/emulator.html)
- [Control the Emulator from the Command Line | Android Studio](https://developer.android.com/studio/run/emulator-commandline.html)
- [Android* - Intel® Hardware Accelerated Execution Manager (Intel® HAXM) | Intel® Software](https://software.intel.com/en-us/android/articles/intel-hardware-accelerated-execution-manager)

### Virtual machine

- [how to change the resolution of android x86 to 1080p - YouTube](https://www.youtube.com/watch?v=JoMs-4bsygs)
- [Android 4.3 running on VMWare and resolution change to 1080p - YouTube](https://www.youtube.com/watch?v=62bMiL-o_OU)
- [virtualbox - Switch android x86 screen resolution - Stack Overflow](https://stackoverflow.com/questions/6202342/switch-android-x86-screen-resolution)
- [Setup Hardware OpenGL for Linux Android x86 VirtualBox (also runs ARM apps) | Keyables](http://www.keyables.com/2012/06/setup-hardware-opengl-for-linux-android.html)

Setup Proxy (when using Emulator, or not) http://www.techverse.net/how-to-setup-proxy-server-3g-4g-data-connection-android-phone/

`UVESA_MODE=1336x768 DPI=96` `UVESA_MODE=1920x1080 DPI=340`

## Virtualization

- [BlueStacks](https://www.bluestacks.com/) - use VirtualBox and run Android x64 binaries
	- [rooting - How to gain root on BlueStacks Android emulator - Android Enthusiasts Stack Exchange](https://android.stackexchange.com/questions/224119/how-to-gain-root-on-bluestacks-android-emulator)
	- [How to enable Virtualization (VT) on Windows 10 for BlueStacks 4 – BlueStacks Support](https://web.archive.org/web/20201110163832/https://support.bluestacks.com/hc/en-us/articles/115003174386-How-to-enable-Virtualization-VT-on-Windows-10-for-BlueStacks-4)
- [MEmu](https://www.memuplay.com/)
- [NoxPlayer](https://www.bignox.com/)
- [Android SKD Emulator](#emulator)
- [Anbox - Android in a Box](https://anbox.io/) - use Linux Containers to run on GNU/Linux distributions
- Android-x86
	- [Installation Howto | Android-x86](https://www.android-x86.org/installhowto.html)
	- [How to Install Android Lineage OS on VMware Workstation | XpertsTec](https://web.archive.org/web/20201122184440/https://www.xpertstec.com/how-to-install-android-lineage-os-on-vmware-workstation/)
	- [How to Install Android in VirtualBox](https://web.archive.org/web/20201112022000/http://www.howtogeek.com/164570/how-to-install-android-in-virtualbox/)

## Interoperability

- [cinit/WSAPatch: Make WSA(Windows Subsystem for Android) run on Windows 10.](https://github.com/cinit/WSAPatch)
- [A patch to enable Windows Subsystem for Android to run on Windows 10 | Hacker News](https://news.ycombinator.com/item?id=34664223)

## APK

- [APK](../../Formats,%20encoding%20and%20protocols/APK/APK.md)
- [processor - How to tell what architecture an APK is intended for? - Android Enthusiasts Stack Exchange](https://android.stackexchange.com/questions/168302/how-to-tell-what-architecture-an-apk-is-intended-for)
- [How do you install an APK file in the Android emulator? - Stack Overflow](https://stackoverflow.com/questions/3480201/how-do-you-install-an-apk-file-in-the-android-emulator/3480235#3480235)

## Kiosk mode

- [Kiosk Mode - Android 5.0 (Lollipop) or Higher | QuickTapSurvey : Help Center](http://support.quicktapsurvey.com/support/solutions/articles/208386-kiosk-mode-android-5-0-lollipop-or-higher)
- [Kiosk Mode - Android | QuickTapSurvey : Help Center](http://support.quicktapsurvey.com/support/solutions/articles/197934-kiosk-mode-android)

## Reverse tethering

Use the host network

- [Introducing “gnirehtet”, a reverse tethering tool for Android](https://medium.com/genymobile/gnirehtet-reverse-tethering-android-2afacdbdaec7)

## Android TV apps

- [APKMirror - Free APK Downloads - Download Free Android APKs #APKPLZ](https://www.apkmirror.com/)
- [\[Tutorial\] How to Modify Android TV and FireOS Apps to Work with Regular Android - WeTek Community Forum](http://www.wetekforums.com/v/index.php?p=/discussion/28075/tutorial-how-to-modify-android-tv-and-fireos-apps-to-work-with-regular-android)

Regular app (mobile or table) could no work properly with a remote, and could require the use of a mouse (via USB), could also not appreas in TV launcher (can be reach via Settings > Applications > Downloaded applications)

## SSH server

With [SimpleSSHD](http://www.galexander.org/software/simplesshd/).

Install from:

- [SimpleSSHD - Apps on Google Play](https://play.google.com/store/apps/details?id=org.galexander.sshd)
- [SimpleSSHD | F-Droid - Free and Open Source Android App Repository](https://f-droid.org/en/packages/org.galexander.sshd/)

Add public auth key:

```sh
ssh -p 2222 user@<androiddeviceip>
# use the onetime password given in the SimpleSSHD's console
# ssh-keyscan -p 2222 -t ecdsa-sha2-nistp256 192.168.3.20

# Add public key for further connections
echo "<userpublickey>" > /data/data/org.galexander.sshd/files/authorized_keys

# create symlink to easy access (SFTP), for ex. to list other app data: /sdcard/Android/data/<appid>
ln -s /sdcard /data/data/org.galexander.sshd/files/sdcard
```

Files are in:

```
/data/user/0/org.galexander.sshd/files/
/data/data/org.galexander.sshd/files/authorized_keys
```
