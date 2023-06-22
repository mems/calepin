AppleDouble: `._filename` (resource fork, Finder information and extended attributes) and `filename` (data fork)
AppleSingle:
- AFPS store it as extended attribute `com.apple.ResourceFork`

```
$; echo "data fork" > test.txt
$; echo "resource fork" > test.txt/..namedfork/rsrc
$; cat test.txt
data fork
$; cat test.txt/..namedfork/rsrc
resource fork
$; echo "resource fork" > test.txt/..namedfork/other
-bash: test.txt/..namedfork/other: Not a directory
$;
```

Convert AppleDouble to AppleSingle with `FixupResourceForks`

- [Macintosh resource fork data format spec for Kaitai Struct](https://web.archive.org/web/20230524012222/http://formats.kaitai.io/resource_fork/)
- [resource fork](https://en.wikipedia.org/wiki/Resource_fork)
- [AppleDouble file](https://en.wikipedia.org/wiki/AppleSingle_and_AppleDouble_formats)
- [Fork (file system) - Wikipedia](https://en.wikipedia.org/wiki/Fork_%28file_system%29#Apple)
- [xattr: com.apple.ResourceFork, a classic Mac resource fork – The Eclectic Light Company](https://web.archive.org/web/20201129065247/https://eclecticlight.co/2017/12/12/xattr-com-apple-resourcefork-a-classic-mac-resource-fork/)
- [AppleSingle and AppleDouble formats - Wikipedia](https://en.wikipedia.org/wiki/AppleSingle_and_AppleDouble_formats)
- [packagesdev/goldout: Command line tool to unsplit forks](https://github.com/packagesdev/goldout)
- [packagesdev/goldin: Command line tool to split forks](https://github.com/packagesdev/goldin)
- [macos - Does APFS actually support Named Forks or just Resource Forks and Extended Attributes? - Stack Overflow](https://stackoverflow.com/questions/66620681/does-apfs-actually-support-named-forks-or-just-resource-forks-and-extended-attri)
- [macos - How Do I Create a Named Fork and Store Data In It? - Ask Different](https://apple.stackexchange.com/questions/228444/how-do-i-create-a-named-fork-and-store-data-in-it/450382#450382)

See also:

- [Extended attribute](../../Operating%20Systems/macOS/macOS.md#extended-attribute)
