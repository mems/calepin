`plutil -convert xml1 -o - /Library/Preferences/com.apple.Bluetooth.plist`
`plutil -convert xml1 -o - /private/var/root/Library/Preferences/com.apple.bluetoothd.plist`

Get system Bluetooth devices

`system_profiler -xml -detaillevel full SPBluetoothDataType`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
	<dict>
		<key>_SPCommandLineArguments</key>
		<array>
			<string>/usr/sbin/system_profiler</string>
			<string>-nospawn</string>
			<string>-xml</string>
			<string>SPBluetoothDataType</string>
			<string>-detailLevel</string>
			<string>full</string>
		</array>
		<key>_SPCompletionInterval</key>
		<real>0.056383967399597168</real>
		<key>_SPResponseTime</key>
		<real>0.084382891654968262</real>
		<key>_dataType</key>
		<string>SPBluetoothDataType</string>
		<key>_detailLevel</key>
		<integer>-1</integer>
		<key>_items</key>
		<array>
			<dict>
				<key>controller_properties</key>
				<dict>
					<key>controller_address</key>
					<string>F0:18:98:3E:E7:A8</string>
					<key>controller_chipset</key>
					<string>BCM_4364B0</string>
					<key>controller_discoverable</key>
					<string>attrib_off</string>
					<key>controller_firmwareVersion</key>
					<string>v117 c4433</string>
					<key>controller_productID</key>
					<string>0x0001</string>
					<key>controller_state</key>
					<string>attrib_on</string>
					<key>controller_supportedServices</key>
					<string>0x382039 &lt; HFP AVRCP A2DP HID Braille AACP GATT Serial &gt;</string>
					<key>controller_transport</key>
					<string>UART</string>
					<key>controller_vendorID</key>
					<string>0x004C (Apple)</string>
				</dict>
				<key>device_connected</key>
				<array>
					<dict>
						<key>Inflorescence</key>
						<dict>
							<key>device_address</key>
							<string>C4:14:11:03:70:9A</string>
							<key>device_firmwareVersion</key>
							<string>1.0.7</string>
							<key>device_minorType</key>
							<string>Keyboard</string>
							<key>device_productID</key>
							<string>0x026C</string>
							<key>device_services</key>
							<string>0x800020 &lt; HID ACL &gt;</string>
							<key>device_vendorID</key>
							<string>0x004C</string>
						</dict>
					</dict>
					<dict>
						<key>MX Master 3</key>
						<dict>
							<key>device_address</key>
							<string>F5:A0:1B:CA:1E:33</string>
							<key>device_batteryLevelMain</key>
							<string>100 %</string>
							<key>device_firmwareVersion</key>
							<string>MPM19.01_0015</string>
							<key>device_minorType</key>
							<string>Mouse</string>
							<key>device_productID</key>
							<string>0xB023</string>
							<key>device_services</key>
							<string>0x400000 &lt; BLE &gt;</string>
							<key>device_vendorID</key>
							<string>0x046D</string>
						</dict>
					</dict>
				</array>
				<key>device_not_connected</key>
				<array>
					<dict>
						<key>Echidna</key>
						<dict>
							<key>device_address</key>
							<string>50:DE:06:21:93:CB</string>
						</dict>
					</dict>
					<dict>
						<key>Grasshopper</key>
						<dict>
							<key>device_address</key>
							<string>94:B0:1F:76:D7:C8</string>
						</dict>
					</dict>
				</array>
			</dict>
		</array>
		<key>_name</key>
		<string>SPBluetoothDataType</string>
		<key>_parentDataType</key>
		<string>SPHardwareDataType</string>
		<key>_properties</key>
		<dict>
			<key>_name</key>
			<dict>
				<key>_detailLevel</key>
				<string>-1</string>
				<key>_isColumn</key>
				<string>YES</string>
				<key>_isOutlineColumn</key>
				<string>YES</string>
				<key>_order</key>
				<string>0</string>
			</dict>
			<key>controller_address</key>
			<dict>
				<key>_detailLevel</key>
				<string>0</string>
				<key>_order</key>
				<string>2</string>
			</dict>
			<key>controller_name</key>
			<dict>
				<key>_detailLevel</key>
				<string>1</string>
				<key>_order</key>
				<string>1</string>
			</dict>
			<key>controller_properties</key>
			<dict>
				<key>_detailLevel</key>
				<string>-1</string>
				<key>_order</key>
				<string>1</string>
			</dict>
			<key>controller_state</key>
			<dict>
				<key>_detailLevel</key>
				<string>-1</string>
				<key>_order</key>
				<string>3</string>
			</dict>
			<key>device_address</key>
			<dict>
				<key>_detailLevel</key>
				<string>0</string>
				<key>_order</key>
				<string>1</string>
			</dict>
			<key>device_connected</key>
			<dict>
				<key>_detailLevel</key>
				<string>-1</string>
				<key>_order</key>
				<string>2</string>
			</dict>
			<key>device_productID</key>
			<dict>
				<key>_detailLevel</key>
				<string>0</string>
				<key>_order</key>
				<string>4</string>
			</dict>
			<key>device_vendorID</key>
			<dict>
				<key>_detailLevel</key>
				<string>0</string>
				<key>_order</key>
				<string>3</string>
			</dict>
			<key>devices_list</key>
			<dict>
				<key>_detailLevel</key>
				<string>-1</string>
				<key>_order</key>
				<string>100</string>
			</dict>
			<key>volumes</key>
			<dict>
				<key>_detailLevel</key>
				<string>0</string>
			</dict>
		</dict>
		<key>_timeStamp</key>
		<date>2023-02-01T21:32:03Z</date>
		<key>_versionInfo</key>
		<dict>
			<key>com.apple.SystemProfiler.SPBluetoothReporter</key>
			<string>1</string>
		</dict>
	</dict>
</array>
</plist>
```

Public `device_address`: `security find-generic-password -a "Public {device_address}" -s BluetoothLE -w`
Random `device_address`: `security find-generic-password -a "Random {device_address}" -s BluetoothLE -w`

Inflorescence `C4:14:11:03:70:9A` (`c4141103709a`, not BLE/BTHLE):

```
# See also /private/var/root/Library/Preferences/com.apple.bluetoothd.plist

# security find-generic-password -a "Public C4:14:11:03:70:9A" -s BluetoothLE -w | xxd -r -p
security: SecKeychainSearchCopyNext: The specified item could not be found in the keychain.

# security find-generic-password -a "Random C4:14:11:03:70:9A" -s BluetoothLE -w | xxd -r -p
security: SecKeychainSearchCopyNext: The specified item could not be found in the keychain.

# security find-generic-password -a "C4:14:11:03:70:9A" -s MobileBluetooth -w | xxd -r -p
# Same as get the password in KeyChain app for "MobileBluetooth" "location" and "C4:14:11:03:70:9A" account
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>LinkKey</key>
	<string>BE-D3-24-C4-1B-6E-62-DD-3D-F9-C3-4E-42-60-8A-2E</string>
	<key>LinkKeyType</key>
	<string>Authenticated</string>
	<key>LocalAddress</key>
	<string>F0:18:98:3E:E7:A8</string>
</dict>
</plist>
```

MX Master 3 `F5:A0:1B:CA:1E:33` (`f5a01bca1e36` et `f5a01bca1e33` ? BLE/BTHLE):

```
# See also /private/var/root/Library/Preferences/com.apple.bluetoothd.plist

security find-generic-password -a "Public F5:A0:1B:CA:1E:33" -s BluetoothLE -w | xxd -r -p
security: SecKeychainSearchCopyNext: The specified item could not be found in the keychain.

# security find-generic-password -a "Random F5:A0:1B:CA:1E:33" -s BluetoothLE -w | xxd -r -p
# Same as get the password in KeyChain app for "BluetoothLE" "location" and "Random F5:A0:1B:CA:1E:33" account
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>Local Encryption</key>
	<dict>
		<key>Long-term Key</key>
		<data>
		ke/BOpl1khoz1kVqE4RtHQ==
		</data>
		<key>Long-term Key Length</key>
		<data>
		EA==
		</data>
		<key>Long-term Key Type</key>
		<data>
		Aw==
		</data>
	</dict>
	<key>Remote Encryption</key>
	<dict>
		<key>Long-term Key</key>
		<data>
		ke/BOpl1khoz1kVqE4RtHQ==
		</data>
		<key>Long-term Key Length</key>
		<data>
		EA==
		</data>
	</dict>
	<key>Remote IRK</key>
	<data>
	Yyy4W8H2JqinJBCtrin7hw==
	</data>
</dict>
</plist>
```

Example to install Inflorescence (Apple Magic Keyboard):

```reg
Windows Registry Editor Version 5.00

; On macOS, disconnect the device first to get that file from Hackintool
; Data from LinkKey (pairing key, changes after each new/re connection)
; On Windows, in PowerShell with administrator rights:
; .\PsExec64.exe -s -i regedit "$PWD\Inflorescence.reg"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys\f018983ee7a8]
;"c4141103709a"=hex:be,d3,24,c4,1b,6e,62,dd,3d,f9,c3,4e,42,60,8a,2e
"c4141103709a"=hex:54,bb,b0,b6,49,5d,1b,1c,24,c7,5f,0a,e3,b8,31,ac
```

Example of data you get with MX Master 3 (Logitech) and other BT LT devices:

```reg
Windows Registry Editor Version 5.00

; .\PsExec64.exe -s -i regedit /e "$PWD\MX Master 3.reg" "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys"

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys\f018983ee7a8]
"MasterIRK"=hex:97,cd,3a,69,fb,6f,54,79,29,83,86,ab,bb,bb,58,c8

; MX Master 3 - Channel 1
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys\f018983ee7a8\f5a01bca1e33]
"LTK"=hex:91,ef,c1,3a,99,75,92,1a,33,d6,45,6a,13,84,6d,1d
"KeyLength"=dword:00000010
"IRK"=hex:87,fb,29,ae,ad,10,24,a7,a8,26,f6,c1,5b,b8,2c,63
"Address"=hex(b):33,1e,ca,1b,a0,f5,00,00
"AddressType"=dword:00000001
"MasterIRKStatus"=dword:00000001
"AuthReq"=dword:0000002d

; MX Master 3 - Channel 2
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys\f018983ee7a8\f5a01bca1e36]
"LTK"=hex:e0,78,b1,f5,80,a3,a5,63,0c,30,71,d3,fe,5f,98,4e
"KeyLength"=dword:00000010
"ERand"=hex(b):00,00,00,00,00,00,00,00
"EDIV"=dword:00000000
"IRK"=hex:be,32,7e,de,cc,6a,8b,64,d6,d3,8a,ee,4f,25,44,53
"Address"=hex(b):36,1e,ca,1b,a0,f5,00,00
"AddressType"=dword:00000001
"MasterIRKStatus"=dword:00000000
"AuthReq"=dword:0000002d
```

Example to install MX Master 3 (Logitech):

```reg
Windows Registry Editor Version 5.00

; On macOS, see below
; On Windows, in PowerShell with administrator rights:
; .\PsExec64.exe -s -i regedit "$PWD\MX Master 3.reg"

; MX Master 3 - Channel 1
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys\f018983ee7a8\f5a01bca1e33]
"ERand"=hex(b):00,00,00,00,00,00,00,00
"EDIV"=dword:00000000
"MasterIRKStatus"=dword:00000000
```

> I think you'd better try using remote encryption values, including `LTK`, `EDIV`, `ERAND` and `IRK`. Make sure in Windows Registry the address of `...\Keys\Devices` and `...\Keys\hub's address\keyboard address` are the same. And don't forget to also check whether the address value of `...\Keys\hub's address\keyboard address\Address matches the keyboard address`.

The content of this tree is only visible for `SYSTEM` user (via `psexec`) `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys`

List of devices (see `Name`)
`Ordinateur\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Devices\{device_mac_address}` where `{device_mac_address}` could be `c4141103709a`

> One is LE legacy pairing, which may change `IRK`, `LTK`, `ERAND`, `EDVI` and `CSRK` values.
> The other is LE Secure Connections, which changes `IRK` and `CSRK`.

> `LTK`, `RAND`, `IRK`, `Address` and `EDIV` need to be changed. They're respectively `LTK`, `ERand`, `IRK`, `Address` and `EDIV` from the reg file, nothing needs to be endian swapped except for the `EDIV` (as an example, `"EDIV"=dword:000080b4` in the reg file means the macOS `EDIV` is `b480`) and the `Address` (as an example, `"Address"=hex(b):46,78,f9,ba,1a,db,00,00` in the reg file means the macOS `Address` is `db1abaf9 7846`).
> — https://github.com/digitalbirdo/BT-LinkkeySync/issues/12#issue-345657850

> to encode from plist base64 to reg format `REG_BINARY`: `echo -n "hex:"; echo -n 'ke/BOpl1khoz1kVqE4RtHQ==' | base64 -d | hexdump -e '/1 "%02x,"' | head -c-1`
> to encode from plist base64 to reg format `REG_DWORD`: `echo -n "dword:"; echo -n 'EA==' | base64 -d | hexdump -e '/1 "%08d"' -n 1`
> to encode from plist base64 to reg format `REG_BINARY` (reverse): `echo -n "hex:"; echo -n 'Yyy4W8H2JqinJBCtrin7hw==' | base64 -d | xxd -p -c1 | tac | xxd -p -r | hexdump -e '/1 "%02x,"' | head -c-1`
> see also `echo "obase=10; ibase=16; 07468FA698ABB40E" | bc` and `od`

- `controller_address`: Bluetooth adapter MAC address, hexdec (ex: `f018983ee7a8`)

- `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys\{controller_address}`
	- `MasterIRK`: ?? this can be ignored
	- `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\BTHPORT\Parameters\Keys\{controller_address}\{device_address}`
		- `LTK`: "Remote Encryption: Long-term Key", format: `REG_BINARY`, ex: `hex:e0,78,b1,f5,80,a3,a5,63,0c,30,71,d3,fe,5f,98,4e`
		- `KeyLength`: "Remote Encryption : Long-term Key Length", format: `REG_DWORD`, ex: `dword:00000010`
		- `ERand`: "Random Number" (`RAND`), format: `REG_QWORD`, ex: `hex(b):00,00,00,00,00,00,00,00`
		- `EDIV`: "Encrypted Diversifier", format: `REG_DWORD`, ex: `dword:00000000`
		- `IRK`: "Remote IRK" "Identity Resolving Key", format: `REG_BINARY` is reversed hex (vs macOS), ex: `hex:87,fb,29,ae,ad,10,24,a7,a8,26,f6,c1,5b,b8,2c,63`
		- `Address`: MAC address of the device, format: `REG_QWORD`, , ex: `hex(b):36,1e,ca,1b,a0,f5,00,00` (for `f5a01bca1e36` as `device_address`)
		- `AddressType`: ??, format: `REG_DWORD`, ex: `dword:00000001`
		- `MasterIRKStatus`: ??, format: `REG_DWORD`, ex: `dword:00000000` or `dword:00000001`, related with `MasterIRK`?
		- `AuthReq`: ??, format: `REG_DWORD`, ex: `dword:0000002d`
		- `SLTK`: "Slave Long Term Key"

If a device don't want to connect or not work a expect (ex. for a keyboard, no keys works) try to pair again (on one of the OS or others), then copy the keys again on the other OS.

- [Windows Registry - Wikipedia](https://en.wikipedia.org/wiki/Windows_Registry#.REG_files)
- https://www.reddit.com/r/hackintosh/comments/p5ost3/macos_monterey_and_windows_bluetooth_pairing/
- https://github.com/digitalbirdo/BT-LinkkeySync/issues/12#issuecomment-988789311
- https://github.com/digitalbirdo/BT-LinkkeySync/issues/12#issuecomment-989436271
- https://web.archive.org/web/20220809160033/https://averylarsen.com/posts/keeping-bluetooth-devices-paired-between-linux-and-windows/
- https://web.archive.org/web/20230201215559/https://bbs.pcbeta.com/viewthread-1800655-1-1.html
- https://github.com/spxak1/weywot/blob/9065341be5a8563ab6796388811cf2b063901afb/guides/bt_dualboot.md
- [fedora - Dual Boot Bluetooth LE (low energy) device pairing - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/402488/dual-boot-bluetooth-le-low-energy-device-pairing/413831#413831)
- https://github.com/x2es/bt-dualboot/
- [lietxia/BT-LinkkeySync: Scripts to synchronize bluetooth link keys from mac OSX to windows](https://github.com/lietxia/BT-LinkkeySync)
- [PowerShell script for dumping Bluetooth keys (e.g. for importing into Linux)](https://gist.github.com/h3x4d3c1m4l/884dba007da8d04caf5e8760e43560aa?permalink_comment_id=4045548)
