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

- [HTTP Archive Viewer 2.0.17](http://www.softwareishard.com/har/viewer/)
- [HAR Analyzer](https://toolbox.googleapps.com/apps/har_analyzer/)
- [ahmadnassri/node-har-validator: Extremely fast HTTP Archive (HAR) validator using JSON Schema](https://github.com/ahmadnassri/node-har-validator)
- [request/request: 🏊🏾 Simplified HTTP request client.](https://github.com/request/request#support-for-har-12)
- [Archive::Har - Provides an interface to HTTP Archive (HAR) files - metacpan.org](https://metacpan.org/pod/Archive::Har)
- https://github.com/ahmadnassri/har
- [HTTP Archive (HAR) format](https://w3c.github.io/web-performance/specs/HAR/Overview.html)
- [benchlab - Browse /Archives/HarLib at SourceForge.net](http://sourceforge.net/projects/benchlab/files/Archives/HarLib/)
- [Generating HAR files and Analyzing Web Requests - Atlassian Documentation](https://confluence.atlassian.com/kb/generating-har-files-and-analysing-web-requests-720420612.html)
- [andrewf/pcap2har: A convertor from .pcap network capture files to HTTP Archive files.](https://github.com/andrewf/pcap2har)
- [Generating HAR files and Analyzing Web Requests - Atlassian Documentation](https://confluence.atlassian.com/kb/generating-har-files-and-analysing-web-requests-720420612.html)
