- [Stickies (Apple) — Wikipedia](https://en.wikipedia.org/wiki/Stickies_%28Apple%29)

`/Applications/Stickies.app`

Document fields:

- `mRTFData`
- `mWindowFlags`
- `mWindowFrame`
- `mWindowColor`
- `mCreationDate`
- `mModificationDate`

See also:

- Inside StYNCies
	- [MacDevCenter.com](https://web.archive.org/web/20160823123634/http://www.macdevcenter.com:80/pub/a/mac/2005/03/11/cocoa.html)
	- [MacDevCenter.com](https://web.archive.org/web/20160813065859/http://www.macdevcenter.com/pub/a/mac/2005/03/11/cocoa.html?page=2)
	- [MacDevCenter.com](https://web.archive.org/web/20160823130712/http://www.macdevcenter.com:80/pub/a/mac/2005/03/18/cocoa.html)
	- [MacDevCenter.com](https://web.archive.org/web/20160813130502/http://www.macdevcenter.com/pub/a/mac/2005/03/18/cocoa.html?page=2)
- [class-dump - Steve Nygard](http://stevenygard.com/projects/class-dump/)
- [Notational Velocity](http://notational.net/) - [nv/StickiesDocument.m at master · scrod/nv](https://github.com/scrod/nv/blob/master/StickiesDocument.m)
- [calacoles/Document.m at master · kazu/calacoles](https://github.com/kazu/calacoles/blob/master/stickies-local/bundle/Document.m)
- [Reverse Engineering Stickies.app - Low Level Bits](https://lowlevelbits.org/reverse-engineering-stickies.app/)
- [cocoadev.github.io/index.md at master · cocoadev/cocoadev.github.io](https://github.com/cocoadev/cocoadev.github.io/blob/master/StickiesDatabase/index.md)
- http://www.cocoabuilder.com/archive/cocoa/125605-nsunarchiver-and-stickiesdatabase.html
- NSUnarchiver and StickiesDatabase
	- [Apple - Lists.apple.com](https://lists.apple.com/archives/cocoa-dev/2005/Jan/msg00736.html)
	- [Apple - Lists.apple.com](https://lists.apple.com/archives/Cocoa-dev/2005/Jan/msg00761.html)
	
Specificity with Apple implementation RTF don't embed images:

You can create RTF with inlined images (hex-encoded data) via `jpegblip` or `pngblip` (for PNG, GIF, BMP, TIFF)

- [ios - trouble saving NSAttributedString, with image, to an RTF file - Stack Overflow](https://stackoverflow.com/questions/23370275/trouble-saving-nsattributedstring-with-image-to-an-rtf-file/29181130#29181130)
- [HUB/NSAttributedString-EncodeRTFwithPictures.m at master · kinph/HUB](https://github.com/kinph/HUB/blob/master/Beans/NSAttributedString-EncodeRTFwithPictures.m)
- [objective c - Creating RTFD Programmatically - Stack Overflow](https://stackoverflow.com/questions/23637194/creating-rtfd-programmatically/35684977#35684977) — Create RTFD Bundle (with NSFileWrapper)
- [cocoadev.github.io/index.md at master · cocoadev/cocoadev.github.io](https://github.com/cocoadev/cocoadev.github.io/blob/master/RTFOrWordDocsWithImages/index.md)

## Stickies to RTFD

Export old stickies (from `~/Library/StickiesDatabase`) data to RTFD files readable by TextEdit.
Works at least on macOS 10.14.

```sh
clang stickies2rtfd.m StickiesDocument.m -fmodules -mmacosx-version-min=10.6 -o stickies2rtfd && ./stickies2rtfd
```

- `-fobjc-arc`: enables ARC
- `-fmodules`: enables modules so you can import with `@import AppKit;`
- `-mmacosx-version-min=10.6`: support older OS X versions, this might increase the binary size

`stickies2rtfd.m` code:

```objc
#import <Foundation/Foundation.h>
#import "StickiesDocument.h"

int main() {
	NSMutableArray *stickyNotes = nil;
	NSData *stickyData = [NSData dataWithContentsOfFile:@"StickiesDatabase"];// usally at ~/Library/StickiesDatabase
	// NSUnarchiver is deprecated in macOS 10.13, could be replaced by https://github.com/berkus/cocotron/ NSUnarchiver or https://github.com/depth42/MEUnarchiver
	NSUnarchiver *unarchiver = [[NSUnarchiver alloc] initForReadingWithData:stickyData];
	// Use https://github.com/scrod/nv/blob/master/StickiesDocument.m
	[unarchiver decodeClassName:@"Document" asClassName:@"StickiesDocument"];
	stickyNotes = [[unarchiver decodeObject] retain];
	//NSLog(@"Decoded object: %@", stickyNotes);
	[unarchiver release];
	
	if (stickyNotes && [stickyNotes isKindOfClass:[NSMutableArray class]]) {
		NSMutableArray *notes = [NSMutableArray arrayWithCapacity:[stickyNotes count]];
	
		// Stickies default colors
		// https://github.com/AlexDenisov/ModernStickies/blob/master/main.c
		// https://lowlevelbits.org/reverse-engineering-stickies.app/
		NSArray *colors = @[
			// Yello
			[NSColor colorWithDeviceRed:0.996078f green:0.956862f blue:0.611764f alpha:1.0f],
			// Blue
			[NSColor colorWithDeviceRed:0.678431f green:0.956863f blue:1.0f alpha:1.0f],
			// Green
			[NSColor colorWithDeviceRed:0.698039f green:1.0f blue:0.631373f alpha:1.0f],
			// Pink
			[NSColor colorWithDeviceRed:1.0f green:0.780392f blue:0.780392f alpha:1.0f],
			// Purple
			[NSColor colorWithDeviceRed:0.713725f green:0.792157f blue:1.0f alpha:1.0f],
			// Gray
			[NSColor colorWithDeviceRed:0.933333f green:0.933333f blue:0.933333f alpha:1.0f]
		];
		
		NSFileManager *fileManager = [NSFileManager defaultManager];
		
		unsigned int i;
		for (i=0; i<[stickyNotes count]; i++) {
			StickiesDocument *doc = [stickyNotes objectAtIndex:i];
			if ([doc isKindOfClass:[StickiesDocument class]]) {
				NSString *filename = [NSString stringWithFormat:@"stickynote-%d.rtfd", i + 1];
			
				// RTFDData can't be written directly (it's not RTFD bundle / disk format / com.apple.rtfd but Flat RTFD / pasteboard format / com.apple.flat-rtfd), TextEdit can't read it
				//[[doc RTFDData] writeToFile:filename atomically:NO];
				// We need to encode the data to an other format, RTF Apple implementation does not embedded images natively (see https://stackoverflow.com/a/29181130/470117)
				// Or we can use an other format that support images attachment like NSWebArchiveTextDocumentType (which use NSKeyedArchiver) https://developer.apple.com/documentation/uikit/nsattributedstringdocumenttype?language=objc
				// Here, instead we use the NSFileWrapper to create RTFD bundle (a folder with name *.rtfd that contains TXT.rtf and all includes images as file)
				int colorIndex = [doc windowColor];
				id color = colorIndex < (int)[colors count] ? colors[colorIndex] : colors[0];
				NSAttributedString *str = 
					[[NSAttributedString alloc] 
						initWithRTFD:[doc RTFDData] 
							documentAttributes:nil];
				NSDictionary *docAttrs = @{
					NSDocumentTypeDocumentAttribute: NSRTFDTextDocumentType,//NSWebArchiveTextDocumentType,
					//NSCharacterEncodingDocumentAttribute: [NSNumber numberWithInteger:NSASCIIStringEncoding],
					// Update the background color to use the same color as stikies
					NSBackgroundColorDocumentAttribute: color
				};
				NSFileWrapper* fileWrapper = [str fileWrapperFromRange:NSMakeRange(0, str.length) documentAttributes:docAttrs error:nil];
				// Remove the file or bundle first
				[NSFileManager.defaultManager removeItemAtPath:filename error:nil];
				[fileWrapper writeToURL:[NSURL fileURLWithPath:filename] options:NSFileWrapperWritingAtomic originalContentsURL:nil error:nil];
			
				// Update creation and modification dates
				[NSFileManager.defaultManager setAttributes: @{
					NSFileCreationDate: [doc creationDate],
					NSFileModificationDate: [doc modificationDate]
					}
					ofItemAtPath:filename
						error:nil];
			} else {
				NSLog(@"Sticky document is wrong: %@", [doc description]);
			}
		}
		
		[stickyNotes release];
	} else {
		NSLog(@"Sticky notes array is wrong: %@", [stickyNotes description]);
	}
	
	return 0;
}
```

## Dashboard widget

```sh
plutil -convert json -r -o - ~/Library/Preferences/widget-com.apple.widget.stickies.plist |
    awk '$1 ~ /-data/ { start=index($0, ":")+3
                        end=length($0)-2
                        sticky=substr($0, start, end-start+1)
                        gsub(/<.?.?div>/, "", sticky)
                        gsub(/<br>/, "\n", sticky)
                        print sticky
                        print "---" }' > ~/all-my-stickies.txt
```

- [mountain lion - Export all stickies at once on OS X 10.8? - Ask Different](https://apple.stackexchange.com/questions/59525/export-all-stickies-at-once-on-os-x-10-8/59531#59531)