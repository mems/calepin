> `.DS_Store` files are only used by the Finder to hold custom view settings for that particular folder

> Finder view settings are stored in invisble `.DS_Store` files, in the **parent** of the folder being set. So the settings for `/Applications` are stored in `/.DS_Store`, and `/Applications/.DS_Store` holds the settings for subfolders of `/Applications`, such as `/Applications/Utilities`.

- `defaults write com.apple.desktopservices DSDontWriteNetworkStores true`
- [finder - Consequences of deleting .DS_Store - Ask Different](https://apple.stackexchange.com/questions/69467/consequences-of-deleting-ds-store)
- [DS Store Easy Way to Update - MozillaWiki](https://web.archive.org/web/20230320231248/https://wiki.mozilla.org/DS_Store_Easy_Way_to_Update)
- [DS Store File Format - MozillaWiki](https://web.archive.org/web/20230428231937/https://wiki.mozilla.org/DS_Store_File_Format)
- [DS Store Easy Way to Update - MozillaWiki](https://web.archive.org/web/20230320231248/https://wiki.mozilla.org/DS_Store_Easy_Way_to_Update)
- [dsstore: log](https://web.archive.org/web/20170602034746/http://www.hhhh.org/src/hg/dsstore)
- [DSStoreFormat - metacpan.org](https://web.archive.org/web/20230428231937/https://metacpan.org/dist/Mac-Finder-DSStore/view/DSStoreFormat.pod)
- [Reading Writing ".DS_Store" Files](https://web.archive.org/web/20211128175627/https://plt.cs.northwestern.edu/snapshots/current/doc/ds-store/index.html#%28part._aliases%29)
- [macOS '.DS_Store' format format spec for Kaitai Struct](https://web.archive.org/web/20230524001158/https://formats.kaitai.io/ds_store/)
- [ds-store · PyPI](https://pypi.org/project/ds-store/) - [dmgbuild/ds_store](https://github.com/dmgbuild/ds_store)
- [Identifying Deleted File References in the Trash (.DS_Store) Files - Part 1 | Ponder The Bits](https://web.archive.org/web/20230326094445/http://ponderthebits.com/2017/01/mac-dumpster-diving-identifying-deleted-file-references-in-the-trash-ds_store-files-part-1/)
