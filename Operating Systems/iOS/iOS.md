- [Test if native application installed](Security#test-if-native-application-installed)
- [About Apple Configurator 2.3 - Apple Support](https://support.apple.com/en-us/HT207133)

- [iMazing | iPhone, iPad & iPod Manager for Mac & PC](https://imazing.com/en)
- [iTools - Provide the most useful tools for iOS users (thinkskysoft)](https://www.thinkskysoft.com/itools/)

## Application

Download native application IPA

- [iphone - How do I download an iOS App (IPA) file to my Mac after iTunes 12.7 update? - Ask Different](https://apple.stackexchange.com/questions/298391/how-do-i-download-an-ios-app-ipa-file-to-my-mac-after-itunes-12-7-update/298455#298455)
- [iOSEmus - iOS App Freedom!](http://iosem.us/)
- [Hollr2099.net - iOS IPA Library](https://www.hollr2099.net/ipas.html)
- [Cracked iOS & Mac App Store Apps Free Download | AppCake](https://www.iphonecake.com/)

## Firmware

`~/Library/iTunes/iPhone Software Updates/*_Restore.ipsw`

	$ md5 iPhone3,1_7.1.2_11D257_Restore.ipsw
	MD5 (iPhone3,1_7.1.2_11D257_Restore.ipsw) = 6ed6cb1c2eac7177f96c9fbcf04a4f34

- [Download iPhone Software (IPSW firmware files)](http://www.iphonehacks.com/download-iphone-ios-firmware)
- [Firmware - The iPhone Wiki](https://www.theiphonewiki.com/wiki/Firmware)

## Screen record

1. quit QuickTime on your Mac if it is open
2. connect your device to your Mac via a cable
3. open QuickTime on your Mac, and select File > New Movie Recording
4. a window will appear
5. click the arrow next to the record button, and select your device from the dropdown menu that appears
6. the window will show a live preview of you device screen

If you want to record:

1. click the record button and go about your business on your iPhone
2. once you're done, click the stop button and save the video

- [macos - How do I AirPlay mirror my iPhone screen to my MacBook Pro? - Ask Different](https://apple.stackexchange.com/questions/139989/how-do-i-airplay-mirror-my-iphone-screen-to-my-macbook-pro)
- [quicktime - Enable touch indicator for iOS app demo video recording - Ask Different](https://apple.stackexchange.com/questions/203044/enable-touch-indicator-for-ios-app-demo-video-recording/250290#250290)

## Screen mirror

You can use:

- AirPlay
- Quicktime on a connected Mac, see [Record screen](#Screen-record)
- third party app like AirServer or Reflector

## Record phone call

Works better with visual voicemail

Note: voicemail duration could be limited

Use the conference with you voicemail:

1. call your self (you should get your voicemail "leave a message after the bip")
2. call the person
3. merge calls, conversation will be recorded by the voicemail
4. end the call
5. you should now have a new voicemail, with visual voicemail you save it with share button

Or use the speaker an record with an external recorder (or a Mac with QuickTime Player, File > New Audio Recoding, using internal microphone)

It's possible to develop an app that use CallKit to fake a call, and use conference mode?

## Phone Codes

	Any command can be preceded by *#, ** or ##.
	
	*# is INTERROGATION.
	** is SETUP.
	## is CANCEL / DELETE.
	
	*#5005*78283#           This dumps a baseband log in /Library/Logs/Baseband/ - Note 1
	**5005*78283#           This dumps a baseband log in /Library/Logs/Baseband/ - Note 1
	##5005*78283#           This dumps a baseband log in /Library/Logs/Baseband/ - Note 1
	*#5005*62#              "Error performing request - No Network Service" - Note 2
	*#5005*62255#           "Error performing request - No Network Service" - Note 2
	*#5005*87223#           "Error performing request - No Network Service" - Note 2
	*#5005*86#              Displays the Voice Mail dial-in number.
	**5005*86*VOICEMAIL#    Sets the Voice Mail number to VOICEMAIL (international format).
	##5005*86#              Erases the Voice Mail number from phone.
	*#5005*7672#            Display the SMSC Setting. 
	**5005*7672*SMSCNUMBER# Sets the SMSC to SMSCNUMBER (international format).
	##5005*7672#            Erases the SMSC number from phone.
	*#5005*22#              "Error performing request - No Network Service" - Note 2
	**5005*22#              Unknown. Displays "Please wait"; returns to dialpad - Note 2
	##5005*22#              Unknown. Displays "Please wait"; returns to dialpad - Note 2
	*#5005*5264#            This reads LANG and tells you the "actual language" (en).
	*#5005#                 "Error performing request - No Network Service" - Note 2
	##5005*22*12345678#     Function unknown, displays "please wait"...; power-off to exit.
	
	'
	Note 1: It may be necessary to change the prefix from the set of (*#, **, ##) to
	        initiate a new log dump.  The logs are not "tail" able, since this is a single
	        dump, with no additional data written.  So far, these logs appear to always
	        remain the same size.  Logfiles are stamped with the current date.
	
	Note 2: These tests were performed with a stock phone on the AT&T network.  It is
	        possible that these errors represent debugging features that are only
	        available on a special debug cellular base-station (CONJECTURE only!)'

	international format: start with 0 instead +
	
	#302#,#303#,#304#,#305#,#306#,#307# is a call loop into the iphone, it makes a call to itself.
	
	the number codes correspond to the alphabets to spell out the service, i.e.
	Voicemail: #5005*86# => 86 = VM
	SMSC: #5005*7672# => 7672 = SMSC
	
	"#31# number" to hide caller id(to call and not show your call number)

	- If you have an iPhone 3GS or iPhone 4 (GSM), to enable the logging, follow steps 1 and 2 below:
	
	1) Dial: *KOOL*CSI# (*5005*274#) and hit Dismiss button 2) Dial: *KOOL*MA# (*5005*62#)
	
	Once this is done, proceed to step 3 below.
	
	- If you have an iPhone 4 (CDMA), iPhone 4S (GSM/CDMA) or iPhone 5, to enable logging, follow steps 1 and 2 below:
	
	1) Dial: *KOOL*CSI# (*5005*274#) and hit Dismiss button 2) Dial: **KOOL*DIAG# (*5005*3424#) and hit Dismiss button
	
	Once this is done, proceed to step 3 below.
	
	3) Wait a few moments for the command to process. 4) Power off the device by holding down the power button and swiping to turn it off. 5) Power on the device again 6) At this point, CSI and MA or CSI and DIAG logging should be enabled, depending on which device you're using.
	
	- When the issue occurs, follow the steps below to capture the logs:
	
	1) Dial: *KOOL*STATE# (*5005*78283#) 2) Press "Reply" (big green button) 3) Enter a description of the problem 4) Press "Reply" (upper right corner)
	
	Note: The buffer to hold the logs is only 1.5 MB so, make sure to enable logging when you see the issue.
	
	After an iTunes sync to your computer, csi and ma or diag baseband log files should appear in the following locations, depending on what OS you're using:
	
	OS X:
	
	~/Library/Logs/CrashReporter/MobileDevice/<your device's name here>/Baseband
	
	Use Terminal (/Applications/Utilities/Terminal.app) to view this folder and copy the files from there to your desktop like this (replace your device name here with the name of your device in the MobileDevice folder which is unique for each device):
	
	cp -R ~/Library/Logs/CrashReporter/MobileDevice/<your device name here>/Baseband ~/Desktop
	
	Windows 7 and Vista:
	
	C:\Users\User Name\AppData\Roaming\Apple Computer\Logs\CrashReporter\MobileDevice\<device-name>\Baseband\ Note: The AppData folder is hidden by default. Choose Folder and Search Options from the Organize menu in the file browser window, then click the View tab and change the "Hidden files and folders" option to "Show hidden files and folders".
	
	Windows XP: C:\Documents and Settings\User Name\Application Data\Apple Computer\Logs\CrashReporter\MobileDevice\<device-name>\Baseband\ Note: The Application Data folder is hidden by default. Choose Tools > Folder Options in the file browser window, then click the View tab and change the "Hidden files and folders" option to "Show hidden files and folders".
	
	--- Disabling Baseband Logging ---
	
	To disable logging, replace the leading asterisk (*) with a pound character (#), like the example below, for each item you enabled:
	
	- If you have an iPhone 3GS or iPhone 4 (GSM), to disable the logging, follow steps 1 and 2 below:
	
	1) #5005*274# (#KOOL*CSI#) 2) #5005*62# (#KOOL*MA#)
	
	- If you have an iPhone 4 (CDMA), iPhone 4S (GSM/CDMA) or iPhone 5, to disable logging, follow steps 1 and 2 below:
	
	1) #5005*274# (#KOOL*CSI#) 2) #5005*3424# (#KOOL*DIAG#)

- [Phone.app codes - The iPhone Wiki](https://www.theiphonewiki.com/wiki/Phone.app_codes)
- [Google Code Archive - Long-term storage for Google Code Project Hosting.](https://code.google.com/archive/p/iphone-elite/wikis/iPhoneCodes.wiki)

## Reset

1. press the lock button and hold it down for 3 seconds
2. still holding the power button, hold down the home button for 10 seconds

## Mockup

- [iOS 8 Illustrator Vector UI Kit Update « Mercury Intermedia | Premium mobile apps | iOS & Android](http://mercury.io/blog/ios-8-illustrator-vector-ui-kit-update)
- [iOS 9 GUI for Sketch - Design+Code](https://designcode.io/ios9)
- [iOS 9 GUI (iPhone) — Facebook Design Resources](http://facebook.github.io/design/ios9.html)
- [iOS 9 Design Guidelines for iPhone and iPad - Design+Code](https://designcode.io/iosdesign-guidelines)

## Accounts

- [ios - App Store asking for other Apple ID when updating apps - Ask Different](http://apple.stackexchange.com/questions/135930/app-store-asking-for-other-apple-id-when-updating-apps)

## Kiosk mode

> use Guided Access (Settings > General > Accessibility > Guided Access on and Accessibility Shortcut on), and turn on every option except for Sleep/Wake button.
> Prior to that, turn on Do Not Disturb so people won't see your notifications. To turn off Guided Access, just press the home button three times, press End on the top left corner and enter the password you've set.

- [About Apple Configurator 2.3 - Apple Support](https://support.apple.com/en-us/HT207133)
- [Disabling the Home and Sleep/Wake Buttons - iPad | QuickTapSurvey : Help Center](http://support.quicktapsurvey.com/support/solutions/articles/198517-disabling-the-home-and-sleep-wake-buttons-)

## Use Network Link Conditioner

1. Connect with USB
2. open XCode
3. Window > Devices
4. (if the device does not appears) "+" > Add device...
5. The entry "Developer" should appears in Settings of the device

Note: don't forget to disable it after test done

## Battery status

1. On macOS computer, open Console.app
2. select your target device (your device must be allowed on the computer you use)
3. connect the device to a power source (or wait a little)
4. find `BatteryHealth`, enter
5. similar log messages `com.apple.BatteryCenter` shoud appears:

		Found power source: {
			"Battery Provides Time Remaining" = 1;
			BatteryHealth = Good;
			"Current Capacity" = 10;
			"Is Charging" = 1;
			"Is Finishing Charge" = 0;
			"Is Present" = 1;
			"Max Capacity" = 100;
			Name = "InternalBattery-0";
			"Power Source ID" = 2424931;
			"Power Source State" = "AC Power";
			"Raw External Connected" = 1;
			"Show Charging UI" = 1;
			"Time to Empty" = 0;
			"Time to Full Charge" = 0;
			"Transport Type" = Internal;
			Type = InternalBattery;
		}

The possible value could be `Perfect`, `Good` and `Poor`

From diagnostic tool:

Open the URI `diags://`or `diagnostics://` in Safari

Beta only?:

> hold down Home+VolUp at cold boot to boot iOS 10.3 into CheckerBoard
> [...]
> I did. Plug in (to computer), shutdown, power on, quickly press home and volume up and kept holding down
> [...]
> hardware wise, volume down replaces the home button in functions like this, DFU, etc
– [Steve Troughton-Smith sur Twitter : "Fun fact: hold down Home+VolUp at cold boot to boot iOS 10.3 into CheckerBoard, a new diagnostics &amp; logs system for Apple Retail stores https://t.co/Ft9eys1Dc3"](https://mobile.twitter.com/stroughtonsmith/status/836544547614248960)

Capture diagnostic requets and change the response (works with iOS 9, but not with iOS 11 due to certificate pinning):

	from libmproxy.models import HTTPResponse
	from netlib.http.headers import Headers
	import cgi
	import re
	from gzip import GzipFile
	import StringIO
	import time
	
	XML_OK_RESPONSE = '''<?xml version="1.0" encoding="UTF-8"?>
	  <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
	  <plist version="1.0">
	   <dict>
		 <key>iPhone5,1</key><array><string>powerDiagnostics</string></array><key>iPhone5,2</key><array><string>powerDiagnostics</string></array><key>iPhone5,3</key><array><string>powerDiagnostics</string></array><key>iPhone5,4</key><array><string>powerDiagnostics</string></array><key>iPhone6,1</key><array><string>powerDiagnostics</string></array><key>iPhone6,2</key><array><string>powerDiagnostics</string></array><key>iPhone7,1</key><array><string>powerDiagnostics</string></array><key>iPhone7,2</key><array><string>powerDiagnostics</string></array><key>iPhone8,2</key><array><string>powerDiagnostics</string></array><key>iPhone8,1</key><array><string>powerDiagnostics</string></array>
	   </dict>
	</plist>'''
	
	
	def request(context, flow):
		path = flow.request.path
		context.log('Path is %s' % path, 'error')
		#if path == '/ios/TestConfiguration/1.2':
			# context.log('sending OK', 'error')
			# respond(flow, XML_OK_RESPONSE)
		if path == '/MR3Server/ValidateTicket?ticket_number=123456':
			context.log('sending OK', 'error')
			respond(flow, XML_OK_RESPONSE)
		elif path == '/MR3Server/MR3Post':
			context.log('sending OK', 'error')
			saveContent(flow, 'general')
			respond(flow, XML_OK_RESPONSE)
		elif path == '/ios/log/extendedUpload':
			context.log('sending OK', 'error')
			saveContent(flow, 'power')
			respond(flow, XML_OK_RESPONSE)
	
	
	def saveContent(flow, prefix):
		decodedData = StringIO.StringIO()
		decodedData.write(flow.request.get_decoded_content())
	
		contentType = flow.request.headers["Content-Type"]
		multipart_boundary_re = re.compile('^multipart/form-data; boundary=(.*)$')
		matches = multipart_boundary_re.match(contentType)
	
		decodedData.seek(0)
	
		query = cgi.parse_multipart( decodedData, {"boundary" : matches.group(1)})
	
		with open("%s-%s.tar.gz" % (prefix, time.strftime("%Y%m%d-%H%M%S")), "wb") as logs:
			logs.write(query['log_archive'][0])
	
	def respond(flow, content):
		resp = HTTPResponse([1,1], 200, "OK", Headers(Content_Type="text/xml"), content)
		flow.reply(resp)

- [How to Check Your iPhone’s Battery Health](https://www.howtogeek.com/254739/how-to-check-your-iphones-battery-health/)
- [iOS Diagnostics - Christopher Lyon Anderson](http://www.lyonanderson.org/blog/2014/02/06/ios-power-diagnostics/)
- [iphone - Battery diagnostic tool at Apple Genius Bars - Ask Different](https://apple.stackexchange.com/questions/111027/battery-diagnostic-tool-at-apple-genius-bars)
- [iOS Diagnostics (Part 2) - Christopher Lyon Anderson](http://www.lyonanderson.org/blog/2014/11/05/ios-diagnostics-part-2/) - [lyonanderson/iOS-Diagnostics: A simple iOS Diagnostics client](https://github.com/lyonanderson/iOS-Diagnostics)
- [iOS Diagnostics (Part 3) - Christopher Lyon Anderson](http://www.lyonanderson.org/blog/2014/11/13/ios-diagnostics-part-3/)
- [How to: Check iPhone battery health, DIY replace, and speed up performance | 9to5Mac](https://9to5mac.com/2017/12/20/how-to-replace-iphone-battery-speed-up-performance/)
- [coconutBattery 3.6.5 - by coconut-flavour.com](http://www.coconut-flavour.com/coconutbattery/)
- [How to Check iPhone Battery Health in 4 Easy Ways](http://www.iphonehacks.com/2017/12/how-check-iphone-battery-health.html)

## Simulator

Start the simulator with a specific SDK

	# Xcode changes these paths frequently, so doublecheck them
	SDK_DIR="/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs"
	SIM_APP="/Applications/Xcode.app/Contents/Developer/Applications/Simulator.app/Contents/MacOS/Simulator"
	$SIM_APP -SimulateApplication $SDK_DIR/iPhoneSimulator8.4.sdk/Applications/MobileSafari.app/MobileSafari

- [simctl: Control iOS Simulators from Command Line – XCBlog – Medium](https://medium.com/xcblog/simctl-control-ios-simulators-from-command-line-78b9006a20dc)
- [terminal - How to launch an iOS Simulator with Safari open using a single command? - Ask Different](https://apple.stackexchange.com/questions/170743/how-to-launch-an-ios-simulator-with-safari-open-using-a-single-command)

### Start old runtimes

> $ xcrun simctl list
> [...] The iOS 7.1 simulator runtime is not supported after 10.10.5.

To test old runtimes, you need older version of XCode (and Simulator app) (just change the name of `XCode.app`)

- [Why can't I see the iOS 7.0 simulator in Xcode on Yosemite? - Stack Overflow](https://stackoverflow.com/questions/26364239/why-cant-i-see-the-ios-7-0-simulator-in-xcode-on-yosemite)
- [More Downloads for Apple Developers](https://developer.apple.com/download/more/?name=Xcode)

### Import via Drag & Drop

For images (JPEGs)

1. Drag & Drop image onto simulator
	→ this will open a browser with your image
2. Click & hold image
	→ this will open options
3. Save image
	→ this will copy image onto simulator

Since Xcode 6+, drag & drop immediatly import images (with thumbnails) and open Photo app

For videos

1. Drag & Drop video onto simulator
	→ this will open a browser with your video (autoplay)
2. Click on Done
	→ this will close video (in Safari)
3. Click on Share & Action button (U+4067 of Apple Symbols)
	→ this will open options
4. Click on Save Video
	→ this will copy video onto simulator

### Import via files and folders

1. Add files (`.jpg`, `.m4v`, `.mov`?, `.png`?) in `~/Library/$DATA_PATH/Media/DCIM/100APPLE/`.
2. And delete these files

		~/Library/$DATA_PATH/Media/PhotoData/Photos.sqlite-shm
		~/Library/Application Support/$DATA_PATH/Media/PhotoData/Photos.sqlite-wal

	Maybe the folder `PhotoData` can be delete too.

	Where `$IPHONE_SIMULATOR_PATH` is `Application Support/iPhone Simulator/5.1` (`$VERSION` is `5.1`, `8.3`) or `~/Library/Developer/CoreSimulator/Devices/$DEVICE_UUID/data`
4. Relaunch Simulator

You can also (only for pictures) use `xcrun simctl addphoto`

### Clear devices data

`~/Library/Developer/CoreSimulator/Devices/`

```sh
xcrun simctl delete unavailable
```

### Test application

- [Install App On iOS Simulator | Anexinet](https://www.anexinet.com/blog/install-app-ios-simulator/)

### Create link to iOS Simulator app

Require Xcode installed.

Create a symbolic link :

	cd /Applications/Utilities/
	ln -s ../Xcode.app/Contents/Developer/Applications/Simulator.app

- `../Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Applications/iPhone\ Simulator.app iPhone\ Simulator.app`
- http://developer.apple.com/library/ios/DOCUMENTATION/Xcode/Conceptual/ios_development_workflow/25-Using_iOS_Simulator/ios_simulator_application.html

### Add to iOS simulator older SDK

Download older version of Xcode: https://developer.apple.com/downloads/ see also [Xcode - Support - Apple Developer](https://developer.apple.com/support/xcode/)

Since Xcode 5:

Copy

	/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Library/CoreSimulator/Profiles/Runtimes/iOS 7.1.simruntime
	→ /Library/Developer/CoreSimulator/Profiles/Runtimes/iOS 7.1.simruntime

Then, copy 

	Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator7.1.sdk
	→ /Library/Developer/CoreSimulator/Profiles/Runtimes/iOS 7.1.simruntime/Contents/Resources/RuntimeRoot

But could require to fix simulator runtime:

	sudo mv "/Library/Developer/CoreSimulator/Profiles/Runtimes/iOS 7.1.simruntime/Contents/Resources/RuntimeRoot/usr/lib/system/host/liblaunch_sim.dylib"{,.bak}
	sudo ln -sf "/Applications/Xcode-beta.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk/usr/lib/system/host/liblaunch_sim.dylib" "/Library/Developer/CoreSimulator/Profiles/Runtimes/iOS 7.1.simruntime/Contents/Resources/RuntimeRoot/usr/lib/system/host/liblaunch_sim.dylib"

See `~/Library/Logs/CoreSimulator.log`

For older version (but require copy other files):

	/Library/Developer/CoreSimulator/Profiles/Runtimes/iOS 7.1.simruntime/Contents/Resources/RuntimeRoot <=> Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator.sdk

- [iOS 8: Building custom simulators — Erica Sadun](http://ericasadun.com/2014/06/18/ios-8-building-custom-simulators/)

## iOS manager

- iTunes / Finder (10.15+) - iPhone manager
- [Use Quick Start to transfer data from your previous iOS device to your new iPhone, iPad, or iPod touch - Apple Support](https://support.apple.com/en-us/HT210216#migration) - iPhone Migration Utility
- [iMazing | iPhone, iPad & iPod Manager for Mac & PC](https://imazing.com/)
- [\[Official\] iMobie AnyTrans®, PhoneRescue®, PhoneClean®, MacClean](https://www.imobie.com/) - AnyTrans
- [iPhone Transfer Software · Macroplant](https://macroplant.com/) - iExplorer
- [\[Official\]dr.fone - Mobile Solutions for All iOS & Android Users](https://drfone.wondershare.com/)

### Relocate iOS backup directory

```sh
# Require to give "Full Disk Access" for Terminal (system preferences > security & privacy > privacy > full disk access > unlock lock to make changes > add terminal app)
# else it will give an error "Operation not permitted"
ln -s /Volumes/Backups/MobileSync ~/Library/Application\ Support/MobileSync/Backup
```

- [How to change the location of your iPhone backup and iTunes MobileSync Backup folder - Scott Hanselman](https://www.hanselman.com/blog/HowToChangeTheLocationOfYourIPhoneBackupAndITunesMobileSyncBackupFolder.aspx)
- [How to change the iTunes backup location](https://reincubate.com/support/how-to/change-itunes-backup-location/)

Remove that backup from TimeMachine:

```sh
cd "/Volumes/mytimemachinedrive/Backups.backupdb/<machinename>/"
sudo /System/Library/Extensions/TMSafetyNet.kext/Contents/Helpers/bypass rm -rf *"/<drivename>/Users/<username>/Library/Application Support/MobileSync/Backup/"*
```

See [Remove specific file from Time Machine backup](../macOS/macOS.md#remove-specific-file-from-time-machine-backup)
