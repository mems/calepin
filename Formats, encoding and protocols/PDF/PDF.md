- https://github.com/HaxeFoundation/format/tree/master/format/pdf
- [Convert HTML to PDF using Webkit (QtWebKit)](https://github.com/wkhtmltopdf/wkhtmltopdf)
- [Convert (simple) SWF to PDF with swftools](https://gist.github.com/mems/5301297)
- [sephiroth74/purePDF- A complete actionscript PDF library](https://github.com/sephiroth74/purePDF) [purePDF | Alessandro Crugnola](http://blog.sephiroth.it/projects/purepdf/)
- [PDF Reader in JavaScript](https://github.com/mozilla/pdf.js)
- [An overview of PDF inaccessibility | The Paciello Group – Your Accessibility Partner (WCAG 2.0/508 audits, VPAT, usability and accessible user experience)](https://www.paciellogroup.com/blog/2017/02/pdf-inaccessibility/)
- [PDFMiner](http://www.unixuser.org/~euske/python/pdfminer/) - Python PDF parser and analyzer
- [pdftabextract - A set of tools for data mining (OCR-processed) PDFs](https://github.com/WZBSocialScienceCenter/pdftabextract)
- [pdfimages - Wikipedia](https://en.wikipedia.org/wiki/Pdfimages) - Export embedded bitmap images in PDF `pdfimages -all file.pdf file.pdf.image`
- [Use `pdflatex` to embed image in PDF without modification (byte-for-byte identical)](https://askubuntu.com/questions/776679/why-are-the-images-produced-by-pdfimages-different-when-using-the-all-flag#778395)
- [imagemagick - Convert PDF to image with high resolution - Stack Overflow](https://stackoverflow.com/questions/6605006/convert-pdf-to-image-with-high-resolution#6605085)
- [Apache PDFBox | A Java PDF Library](https://pdfbox.apache.org/)
- [XpdfReader Support](https://www.xpdfreader.com/support.html) - `pdftotext`, `pdfimages`, `pdftohtml`, etc.
- [pdfsandwich](http://www.tobias-elze.de/pdfsandwich/)
- [pdfimages — Wikipedia](https://en.wikipedia.org/wiki/Pdfimages) - `pdfimages`. [Install poppler on macOS with MacPorts](https://ports.macports.org/port/poppler/)
![PDF](PDF.png)

![PDF101 An Adobe Document Walkthrough](PDF101%20an%20Adobe%20document%20walkthrough.png)

- [Free PDF Reader - Sumatra PDF](https://www.sumatrapdfreader.org/free-pdf-reader) - [sumatrapdfreader/sumatrapdf: SumatraPDF reader](https://github.com/sumatrapdfreader/sumatrapdf)

## Optimization

- with Preview and Quartz filters (open the file in Preview, File -> Export, then selecting one of the Quartz filters)
	- [Compress a PDF in Preview on Mac - Apple Support](https://support.apple.com/guide/preview/compress-a-pdf-prvw1509/mac)
	- `/System/Library/Printers/Libraries/quartzfilter <inputfile> <filterpath.qfilter> <outputfile>`
	- [joshcarr/Apple-Quartz-Filters](https://github.com/joshcarr/Apple-Quartz-Filters)
	- [Shrink Preview files without ruining image quality | Macworld](https://web.archive.org/web/20240404094654/https://www.macworld.com/article/218979/shrink-preview-files-without-ruining-image-quality.html)
	- [How to create custom PDF compression filters in OS X - CNET](https://web.archive.org/web/20240614195748/https://www.cnet.com/tech/computing/how-to-create-custom-pdf-compression-filters-in-os-x/)
	- [macos - How to decrease .pdf size without losing quality - Ask Different](https://apple.stackexchange.com/questions/297417/how-to-decrease-pdf-size-without-losing-quality)
- [Lightweight PDF – A PDF compressor for Mac](https://lightweightpdf.com/)
- [mattdesl/gsx-pdf-optimize: Optimize PDFs with Ghostscript command](https://github.com/mattdesl/gsx-pdf-optimize)

## Signature

- [Fill out and sign PDF forms in Preview on Mac - Apple Support](https://support.apple.com/guide/preview/fill-out-and-sign-pdf-forms-prvw35725/mac)

Digital signature:

- [PortableSigner Mainpage](http://portablesigner.sourceforge.net/)
- `gpg --clearsign --output=signed.pdf input.pdf`
- signing existing PDF files in LibreOffice: File → Digital signatures → Sign Existing PDF
- [Sign PDFs in Adobe Acrobat Reader.](https://helpx.adobe.com/reader/using/sign-pdfs.html)
- [certificates - How do I digitally sign a PDF? - Ask Ubuntu](https://askubuntu.com/questions/147379/how-do-i-digitally-sign-a-pdf)
- pdf.js
	- [JohanOtto/digitalSignaturePDFJS: Digital Signatures feature for PDF JS](https://github.com/JohanOtto/digitalSignaturePDFJS)
	- [Digital signatures in pdf.js · Issue #1076 · mozilla/pdf.js](https://github.com/mozilla/pdf.js/issues/1076)
	- [E-signature not showing up in pdf.js viewer · Issue #4743 · mozilla/pdf.js](https://github.com/mozilla/pdf.js/issues/4743)
- [node-signpdf - npm](https://www.npmjs.com/package/node-signpdf)
- [eSignature standards](https://ec.europa.eu/cefdigital/wiki/display/CEFDIGITAL/eSignature+standards#eSignaturestandards-PAdES%28PDFAdvancedElectronicSignature%29BaselineProfile)
