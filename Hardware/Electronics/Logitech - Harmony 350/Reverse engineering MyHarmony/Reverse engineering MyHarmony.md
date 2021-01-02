- [Téléchargement Harmony](https://setup.myharmony.com/) https://support.myharmony.com/en-us/download https://app.myharmony.com/prod/mac/1.0/MyHarmony-App.dmg (32 bits) https://app.myharmony.com/prod/mac/HarmonyDesktop.dmg (64 bits)
- [Logitech Harmony](https://www.reddit.com/r/logitechharmony/)
- MyHarmony (required + an account) app is a Chromium including Sliverlight (Windows and macOS) that load http://web-dev03.myharmony.com/Account/harmonyconfig webpage include Sliverlight Application (XAP) See http://myharmony-app.s3.amazonaws.com/test/serviceConfig.xml (WebURL)
	Get 
	`{SUSAddress}/softwareupdatesplatform/softwareupdates/product/{productId}/unit/{unitId}/image/latest`
	with query string:
	`types` (only if type is not "None"): `FirmwareImageType` (Config = "0", SysBuild = "1", AppBuild = "2", None = "4")
	`trigger`: always "usb"
	`channel`: `SUSChannel` (ex: "production")
	`guid`: random Guid (anti cache?)
	`streams` (optional): `SpecialSUSStream` (ex: "preview")
	`criticalOnly` (only if type is SysBuild): "false"
	`sysBuild` (only if type is SysBuild): firmwareVersion, always "1.0.0"
	where:
	`SUSAddress` is `https://sus.dhg.myharmony.com` (from https://setup.myharmony.com/remoterecoverytool/recover.aspx)
	`productId` is Skin (Harmony 350 = "104", etc.)
	`unitId` is unit Guid
	add header: `Logitech-SUS-Key: UV6nr6k8ZqlLYksPWMOlv5qwNU2lo1j8Q57WgwE5`
	
	Search for `HttpWebRequest`
	
	The JS in the webpage use property harmonyWebSocket (in C#: `HtmlPage.RegisterScriptableObject`) to communicate with Silverlight
- [How to hack a Harmony remote to control more devices - CNET](https://www.cnet.com/how-to/how-to-hack-a-harmony-remote-to-control-more-devices/)
- [congruity download | SourceForge.net](https://sourceforge.net/projects/congruity/)
- [Setting Up a Logitech Harmony Remote on Linux](https://gist.github.com/amhendley/89965125556b219f84fd)
- [Concordance](https://www.phildev.net/concordance/) and [jaymzh/concordance: Program Harmony remote controls from Linux, Windows, or Mac!](https://github.com/jaymzh/concordance)
- [How to set up a Harmony remote using Linux. – Open attitude](http://openattitude.com/2011/01/27/how-to-set-up-a-harmony-remote-using-linux/)
- http://members.harmonyremote.com/EasyZapper/UserHome.asp
- [Configuring a Logitech Harmony Remote From Linux (Sort Of)](https://williamfriesen.com/2017/07/09/logitech-harmony-linux.html) - Don't give any tips, it's just about
- [Téléchargements Harmony](https://setup.myharmony.com/)
- [telecommande_logitech_harmony - Documentation Ubuntu Francophone](https://doc.ubuntu-fr.org/telecommande_logitech_harmony)
- [Developer crafts Linux support for Logitech Harmony remote controls | Linux.com | The source for Linux information](https://www.linux.com/news/developer-crafts-linux-support-logitech-harmony-remote-controls) - About Concordance, how it's works and how to use
- [Failure Reveals Character: Programming the Logitech Harmony 555 remote with Linux](http://failurerevealscharacter.blogspot.fr/2015/10/programming-logitech-harmony-555-remote.html)