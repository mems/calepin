Write a plist file contains:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>URL</key>
    <string>http://apple.com</string>
</dict>
</plist>
```

- [safari - How to manually create a working .webloc file? - Ask Different](https://apple.stackexchange.com/questions/180922/how-to-manually-create-a-working-webloc-file)
- [objective c - Crafting .webloc file - Stack Overflow](https://stackoverflow.com/questions/146575/crafting-webloc-file)
- https://github.com/chromium/chromium/blob/72ceeed2ebcd505b8d8205ed7354e862b871995e/ui/base/clipboard/clipboard_util_mac.mm#L112-L149
- [chrome/browser/ui/cocoa/location_bar/autocomplete_text_field_cell.mm WriteURLToNewWebLocFileResourceFork](https://github.com/chromium/chromium/commit/e4ec3055dbc64a64eec023566493970ba010c57f#diff-df9100f6588e383cd73d1090599ff051fe3bc625603a8eae18dc9d63209f1409)

- [URL File Format - Fmtz File Formats Information and Specifications](https://web.archive.org/web/20160324231122/http://www.fmtz.com/formats/url-file-format/article) - Windows URL format (`*.url`)
- https://github.com/chromium/chromium/blob/72ceeed2ebcd505b8d8205ed7354e862b871995e/ui/base/clipboard/clipboard_util_win.cc#L68-L79
- https://github.com/chromium/chromium/blob/72ceeed2ebcd505b8d8205ed7354e862b871995e/ui/base/dragdrop/os_exchange_data_provider_win.cc#L334-L338
