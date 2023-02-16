> 	// A HAR timing record includes the duration of several events.
> 	// ssl overlaps connect.  Otherwise, all events happen one at a time in
> 	// order:
> 	//
> 	// |<-blocked->|<-dns->|<-connect->|<-send->|<-wait->|<-receive->|
> 	//                         |<-ssl->|
> 	// A duration of -1 or omitting an event means the event did not happen.
> 	// For example, fetching from a URL whose host is an IP address would
> 	// not have a DNS event.
> 	[...]
> 	//   $entryTime
> 	//       |
> 	//      \|/
> 	//
> 	// HAR:  |<-blocked->|<-dns->|<-connect->|<-send->|<-wait->|<-receive->|
> 	//                               |<-ssl->|
> 	//
> 	// WPT:             /|\     /|\ /|\     /|\               /|\         /|\
> 	//                   |       |   |       |                 |           |
> 	//                dns start  |   |       |<-- ttfb ------->|           |
> 	//                           | conn end  |<-- load ------------------->|
> 	//                           |           |                 |
> 	//                        dns end      start          receive_start
> 	//                       conn start
— https://github.com/WPO-Foundation/webpagetest/blob/c14ec7fce8c709e94d12b2441d962566c2360a7d/www/harTiming.inc#L53-L61
See also https://github.com/WPO-Foundation/webpagetest/blob/4234baa351eb1cb9d6b00dc513133c24f1d5a990/www/devtools.inc.php

- [HAR 1.2 Spec | Software is hard](http://www.softwareishard.com/blog/har-12-spec/)
- [.har - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/.har)

- https://github.com/Stuk/server-replay
- Charles


- [HAR Analyzer](https://web.archive.org/web/20230214070052/https://toolbox.googleapps.com/apps/har_analyzer/)
- [Network Analysis Reference  |  Tools for Web Developers  |  Google Developers](https://developers.google.com/web/tools/chrome-devtools/network-performance/reference#save-as-har)
- [Chrome HAR Viewer](http://ericduran.github.io/chromeHAR/)
- [HTTP Archive Viewer master](http://gitgrimbo.github.io/harviewer/master/) - new/up to date version of [HTTP Archive Viewer 2.0.17](http://www.softwareishard.com/har/viewer/)
- [What's New In DevTools (Chrome 62)  |  Web  |  Google Developers](https://developers.google.com/web/updates/2017/08/devtools-release-notes#har-imports) - HAR imports in the Network panel
- [pcapperf](https://web.archive.org/web/20200506001340/http://pcapperf.appspot.com:80/) - PCAP Web Performance Analyzer
- [.har - Wikipedia](https://en.wikipedia.org/wiki/.har)
- [HAR Adopters | Software is hard](https://web.archive.org/web/20230211155350/http://www.softwareishard.com/blog/har-adopters/)
- [HTTP Archive Viewer 2.0.17](http://www.softwareishard.com/har/viewer/)
- [HAR Diff | GTmetrix](https://web.archive.org/web/20221001090222/https://gtmetrix.com/blog/har-diff/)
- [ahmadnassri/node-har-validator: Extremely fast HTTP Archive (HAR) validator using JSON Schema](https://github.com/ahmadnassri/node-har-validator)
- [request/request: 🏊🏾 Simplified HTTP request client.](https://github.com/request/request#support-for-har-12)
- [Archive::Har - Provides an interface to HTTP Archive (HAR) files - metacpan.org](https://metacpan.org/pod/Archive::Har)
- [ahmadnassri/node-har: HTTP Archive (HAR) Dynamic Object](https://github.com/ahmadnassri/node-har)
- [HTTP Archive (HAR) format](https://w3c.github.io/web-performance/specs/HAR/Overview.html)
- [benchlab - Browse /Archives/HarLib at SourceForge.net](http://sourceforge.net/projects/benchlab/files/Archives/HarLib/)
- [Generating HAR files and analyzing web requests | Atlassian Support | Atlassian Documentation](https://web.archive.org/web/20221001105159/https://confluence.atlassian.com/kb/generating-har-files-and-analyzing-web-requests-720420612.html)
- [andrewf/pcap2har: A convertor from .pcap network capture files to HTTP Archive files.](https://github.com/andrewf/pcap2har)
- [Save all network requests to a HAR file - Network features reference - Chrome Developers](https://developer.chrome.com/docs/devtools/network/reference/#save-as-har)
