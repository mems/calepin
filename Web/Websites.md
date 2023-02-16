# Websites informations and tips

Logos: https://github.com/larsenwork/social.svg.min

- [Web scrapping](Web scrapping)
- [site-deaths - IndieWeb](https://indieweb.org/site-deaths)

- [anticontainer/plugins at master · downthemall/anticontainer](https://github.com/downthemall/anticontainer/tree/master/plugins)
- [jdownloader/src/jd/plugins/hoster at master · mirror/jdownloader](https://github.com/mirror/jdownloader/tree/master/src/jd/plugins/hoster) - see [jDownloadder](Applications#jdownloader)
- [tinyMediaManager](https://github.com/tinyMediaManager)

- [Bit rate - Wikipedia, the free encyclopedia](https://en.wikipedia.org/wiki/Bit_rate#MP3)

Creative networks:

- https://cargocollective.com
- https://thedisplay.me
- https://deviantart.com
- https://behance.net

## Access

Services not available in China: [GreatFire.org - Expanding Online Freedom of Speech in China and Beyond](https://en.greatfire.org/)
Twitter, Github, Microsoft's OneDrive, Dropbox, Google Drive, Youtube, Instragram can be blocked in Turkey
LinkedIn is blocked in Russia

Social network are not the same everywhere. Ex.: in China Facebook and Twitter are banned, Chinese use WeChat and Weibo instead.

This can also impact dependencies like styles, fonts, images, video, scripts (libs, API scripts), etc.

- [The Essential Meta Tags for Social Media | CSS-Tricks](https://css-tricks.com/essential-meta-tags-social-media/)
- [File:Most popular social networking sites by country.svg — Wikipedia](https://en.wikipedia.org/wiki/File:Most_popular_social_networking_sites_by_country.svg)
- [List of virtual communities with more than 100 million active users — Wikipedia](https://en.wikipedia.org/wiki/List_of_virtual_communities_with_more_than_100_million_active_users)
- [List of social networking websites — Wikipedia](https://en.wikipedia.org/wiki/List_of_social_networking_websites)
- [Russia starts blocking LinkedIn website after court ruling | Reuters](http://www.reuters.com/article/us-russia-linkedin-idUSKBN13C0RN)
- [How Google’s CDN prevents your site from loading in China](https://edjiang.com/how-googles-cdn-prevents-your-site-from-loading-in-china-67504845cd04)
- [Dropbox, Google Drive and Microsoft OneDrive cloud services blocked in Turkey following leaks - Turkey Blocks](https://turkeyblocks.org/2016/10/08/google-drive-dropbox-blocked-in-turkey/)

## Social media dimensions

- https://docs.google.com/spreadsheets/d/1IpTYTTMJLcSXcPDtW9zSbPBHQyRdrLfKERohGIIkE_Q/edit#gid=1990145635
- [Social media image size cheat sheet and tips: 2015 edition - The American Genius](http://theamericangenius.com/social-media/social-media-image-size-cheat-sheet-tips-2015-edition/)
- [The Ridiculously Exhaustive Social Media Dimensions Blueprintjeffberezny.com](http://jeffberezny.com/2013/02/12/the-ridiculously-exhaustive-social-media-dimensions-blueprint-infographic/)
- [Raidious Support Your Owned Media Strategy by Creating Graphics - Raidious](http://www.raidious.com/support-your-owned-media-strategy-by-creating-graphics/)
- [The Complete Social Media Image Size Guide: With Awesome Design Tips [Infographic] – Design School](https://designschool.canva.com/blog/social-media-image-size/)

## Avatar

Aka [identicon](https://en.wikipedia.org/wiki/Identicon)

- [Gravatar - Globally Recognized Avatars](https://en.gravatar.com/site/implement/images/)
- [Libravatar :: federated avatar hosting service](https://www.libravatar.org/)
- [Jdenticon - Open source identicon generator](https://jdenticon.com/)
- [Creating Sigils - Urbit](https://web.archive.org/web/20210419224026/https://urbit.org/blog/creating-sigils/)
	- [urbit-ob/co.js at master · urbit/urbit-ob](https://github.com/urbit/urbit-ob/blob/master/src/internal/co.js)
	- [urbit/sigil-js: ~4.2 billion default profile pics](https://github.com/urbit/sigil-js)
- [Volosh1n/github-avatar-generator: Simple script, which generates GitHub's avatar-style images.](https://github.com/Volosh1n/github-avatar-generator)
- [How is the default user avatar generated? - Meta Stack Exchange](https://meta.stackexchange.com/questions/17443/how-is-the-default-user-avatar-generated/17444#17444)
- [WP_MonsterID – WordPress plugin | WordPress.org](https://wordpress.org/plugins/wp-monsterid/)
- [Avatars, identicons, and hash visualization](https://web.archive.org/web/20210123140238/https://barro.github.io/2018/02/avatars-identicons-and-hash-visualization/)
- [Representing SHA-256 Hashes As Avatars | François Best](https://web.archive.org/web/20210419115426if_/https://francoisbest.com/posts/2021/hashvatars)
- [drhus/awesome-identicons: A curated list of "Visual Hashs" (Identicon, Avatar, Fractal, RandomArt and general Hash Visualization)](https://github.com/drhus/awesome-identicons)
- [Moji - The advent of large identifiers and howto conquer them as human. by Michael Luggen](https://web.archive.org/web/20210419224030/https://exascale.info/assets/pdf/students/MSc_Thesis_-_Michael_Luggen__14_09_2012.pdf)

## Intent URLs

See also [Web Intents](http://www.webintents.org/) and [WebActivities](https://wiki.mozilla.org/WebAPI/WebActivities)

See also [`navigator.share()` API](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/share) and [`navigator.canShare()` API](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/canShare)

Some social network have a direct access to share an URL, text or to prefill a message

Test with [URI template online tester](https://codepen.io/mmems/pen/oNxxRvN)

- [bradvin/social-share-urls: Social Share URLs](https://github.com/bradvin/social-share-urls)

### Twitter

URL template: `https://twitter.com/intent/tweet{?url,text,via,related,hashtags}`

Parameters (optional):

- `text`: the tweet text
- `url`: the URL or title `:` URL (ex: `Some title:http://example.com`)
- `via`: Twitter handle
- `hashtags`: comma-separated list of hashtags, ex: `hashtag1,hashtag2,hashtag3`
- `original_referer`: URL
- `in_reply_to`: tweet ID

Examples:

```json
{
  "url": "https://twitter.com/Interior/status/463440424141459456",
  "via": "Interior",
  "hashtags": ["nature", "sunset"]
}
```

```json
{
  "text": "Stunning!",
  "in_reply_to": "Interior"
}
```

- [Overview | Docs | Twitter Developer](https://developer.twitter.com/en/docs/twitter-for-websites/web-intents/overview#tweet-or-reply)

URL template: `https://twitter.com/intent/retweet{?tweet_id}`

Parameter (required) `tweet_id`: Tweet ID

- [Overview | Docs | Twitter Developer](https://developer.twitter.com/en/docs/twitter-for-websites/web-intents/overview#retweet-a-tweet)

### Facebook

URL templates:

- `https://www.facebook.com/sharer/sharer.php?u={url}`
- `https://www.facebook.com/sharer.php?s=100&p[url]={url}`
- `https://www.facebook.com/dialog/share?display=popup{&app_id,href,quote,hashtag}`

Parameters:

- `app_id`: the (controled) Facebook App ID
- `href`: the URL
- `quote` (optional): description
- `hashtag` (optional): (only one)hashtag including the hash symbol

Examples:

```json
{
  "app_id": "249377268519431",
  "href": "http://example.com",
  "hashtag": "#facebook",
  "quote": "Some example"
}
```

- [Share Dialog - Sharing](https://developers.facebook.com/docs/sharing/reference/share-dialog)

URL template: `https://www.facebook.com/dialog/send?display=popup{&app_id,link}`

Parameters:

- `app_id`: the (controled) Facebook App ID
- `link`: the URL
- `locale` (optional): the locale (with an underscore separator)
- `redirect_uri` (optional): redirect URL
- `to` (optional): app-scoped other user ID (the recipient)

Examples:

```json
{
  "app_id": "249377268519431",
  "link": "http://example.com",
  "locale": "en_US",
  "redirect_uri": "http://thefinaldestination.com"
}
```

- [Send Dialog - Sharing](https://developers.facebook.com/docs/sharing/reference/send-dialog)

### Linkedin

URL template: `https://www.linkedin.com/shareArticle?mini=true{&url,title,summary,source}`

Parameters:

- `url`: the URL
- `title`: a title
- `summary`: a description
- `source`: the source URL

### Pinterest

URL template: `https://www.pinterest.com/pin/create/button/{?url,description,media}`

Parameters:

- `url`: the URL
- `description`: a description
- `media`: a source image source

URL template: `https://www.pinterest.com/pin/create/link/{?url,description,media}`

Parameters:

- `url`: the URL
- `description`: a description
- `media`: a source image source

URL template: `https://www.pinterest.com/pin/find/{?url}`

### Others

+-----------------------+---------------------------------------------------------------+-----------------------------------------------------------
| Network				| [URL templates](https://en.wikipedia.org/wiki/URL_Template)	| Parameters
+=======================+===============================================================+===========================================================
| AddThis				| https://api.addthis.com/oexchange/0.8/offer					| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Diaspora				| https://share.diasporafoundation.org/							| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Flattr				| https://flattr.com/submit/auto								| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `description`: `{DESCRIPTION}`
| 						| 																| - `user_id`: `{FLATTR_USER_ID}`
| 						| 																| - `hidden`: `0` or `1`
| 						| 																| - `category`: `text` or other?
| 						| 																| - `tags`: ?
| 						| 																|
| 						| 																| - [HowTo: Flattr in WordPress.com](https://blog.flattr.com/2011/06/flattr-in-wordpress-com/)
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Reddit				| https://www.reddit.com/submit/								| - `url`: `{URL}`
| 						| 																| - `title` (optional): `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Hacker News			| https://news.ycombinator.com/submitlink						| - `u`: `{URL}`
| 						| 																| - `t`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Viadeo				| https://www.viadeo.com/shareit/share/							| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Tumblr				| https://www.tumblr.com/share									| - `v`: `3`
| 						| 																| - `u`: `{URL}`
| 						| 																| - `t`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Tumblr				| https://tumblr.com/widgets/share/tool							| - `canonicalUrl`: `{URL}`
| 						| 																| - `posttype` (optional): `link`
| 						| 																| - `title` (optional): `{TITLE}`
| 						| 																| - `caption` (optional): `{TITLE}`
| 						| 																| - `content` (optional): `{URL}`
| 						| 																| - `shareSource` (optional): `tumblr_share_button`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Digg					| https://digg.com/submit										| - `url`: `{URL}`
| 						| 																| - `title={TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Skype					| https://web.skype.com/share									| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Delicious				| https://delicious.com/save_url								| - `v`: `5`
| 						| 																| - `provider`: `getsocial`
| 						| 																| - `noui`: no value
| 						| 																| - `jump`: `close`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `pic`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| StumbleUpon			| https://www.stumbleupon.com/badge/							| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Stumbleupon			| https://www.stumbleupon.com/submit							| - `url`: `{URL}`
| 						| 																| - `title` (optional): `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Odnoklassniki			| https://www.ok.ru/dk											| - `st.cmd`: `addShare`
| 						| 																| - `st.s`: `1`
| 						| 																| - `st._surl`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Buffer				| https://buffer.com/add										| - `url`: `{URL}`
| 						| 																| - `text`: `{TITLE}`
| 						| 																| - `picture`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Yummly				| https://www.yummly.com/urb/verify								| - `url`: `{URL}`
| 						| 																| - `imageurl`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Draugiem.lv			| https://www.draugiem.lv/say/ext/add.php						| - `title`: `{TITLE}`
| 						| 																| - `link`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Slack					| https://slack.com/oauth/authorize								| - `scope`: `incoming-webhook,chat:write:user`
| 						| 																| - `client_id`: `{SLACK_CLIENT_ID}`, ex: `11072499345.25274635444`
| 						| 																| - `redirect_uri`: `{REDIRECT_URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Evernote				| https://www.evernote.com/clip.action							| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Flipboard				| https://share.flipboard.com/bookmarklet/popout				| - `v`: `2`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Pocket				| https://getpocket.com/save									| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| VKontakte				| https://vk.com/share.php										| - `url`: `{URL}`
| 						| 																| - `title` (optional): `{TITLE}`
| 						| 																| - `description` (optional): `{DESCRIPTION}`
| 						| 																| - `image` (optional): `{IMAGE_SRC}`
| 						| 																| - `noparse` (optional): `true`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Xing					| https://www.xing-share.com/app/user							| - `op`: `share`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `sc_p` (optional): `xing-share`
| 						| 																|
| 						| 																| Note: use `;` as pairs separator
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Xing					| https://www.xing.com/app/user									| - `op`: `share`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																|
| 						| 																| Note: use `;` as pairs separator
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Xing					| https://www.xing.com/social_plugins/share						| - `h` (optional): `1`
| 						| 																| - `url`: `{URL}`
| 						| 																|
| 						| 																| Note: use `;` as pairs separator
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Xing					| https://www.xing.com/spi/shares/new							| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| RenRen				| https://share.renren.com/share/buttonshare					| - `link`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| RenRen				| https://share.renren.com/share/buttonshare.do					| - `link`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| YoudaoNote			| https://note.youdao.com/memory/								| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `sumary`: ``
| 						| 																| - `pic`: `{IMAGE_SRC}`
| 						| 																| - `product`: ``
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Facenama				| https://facenama.com/links/									| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Cloob					| https://www.cloob.com/share/link/add							| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Telegram				| https://t.me/share/url										| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Telegram				| https://telegram.me/share/url									| - `text`: `{TEXT}`
| 						| 																| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Telegram				| https://telegram.me/share/									| - `text`: `{TITLE}`
| 						| 																| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Yahoo App				| ymsgr:sendim													| - `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Afsaran				| http://www.afsaran.ir/link/share								| - `from`: `out`
| 						| 																| - `id`: `0`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `url`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Baidu					| https://like.baidu.com/set									| - `url`: `{URL}`
| 						| 																| - `buttontype` (optional): `small`
| 						| 																| - `cb` (optional): `{JS_CALLBACK_NAME}`, ex: `bdShare.ajax._callbacks.bd4bb141b`
| 						| 																| - `index` (optional): `0`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Baidu					| https://hi.baidu.com/pub/show/share							| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Baidu					| https://s.share.baidu.com/									| - `click`: `1`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `to`: `bdhome`
| 						| 																| - `type`: `text`
| 						| 																| - `pic`: `{IMAGE_SRC}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `sign`: `on`
| 						| 																| - `l`: ?, ex: `1auq178vh1auq17a0t1auq18luh`
| 						| 																| - `linkid`: ?, ex: `iu5kdble07c`
| 						| 																| - `sloc`: ?, ex: `570.1.1.95.17.75.16.97.31.1.1404.836.1043.1440.803`
| 						| 																| - `apiType`: `0`
| 						| 																| - `buttonType`: `0`
| 						| 																| - `firstime`: ?, ex: `1476184008114`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Weibo					| https://service.weibo.com/share/share.php						| - `url`: `{URL}`
| 						| 																| - `title` (optional): `{TITLE}`
| 						| 																| - `pic` (optional): `{IMAGE_SRC}`
| 						| 																| - `appkey` (optional): `SINA_AKEY` or empty value
| 						| 																| - `ralateUid` (optional): `{SINA_USER}` or empty value, ex: `SinaWeibo`; RelatedID http://open.weibo.com/sharebutton
| 						| 																| - `language` (optional): `{LANG}`, ex: `zh_cn`
| 						| 																| - `searchPic` (optional): `false`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| QZone					| https://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey	| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `desc`: empty value
| 						| 																| - `summary`: empty value
| 						| 																| - `site`: empty value
| 						| 																| - `pics`: `{IMAGE_SRC}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Tencent Weibo			| https://v.t.qq.com/share/share.php							| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Qzone					| https://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey	| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| QQWeibo				| https://share.v.t.qq.com/index.php							| - `c`: `share`
| 						| 																| - `a`: `index`
| 						| 																| - `url`: `{URL}`
| 						| 																| - `title`: `{TITLE}`
| 						| 																| - `pic`: `{IMAGE_SRC}`
| 						| 																| - `appkey`: `QQT_APPKEY`, ex: `QQWeibo`; AppKey http://open.t.qq.com/apps/share/explain.php
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| QQEmail Me			| https://mail.qq.com/cgi-bin/qm_share							| - `t`: `qm_mailme`
| 						| 																| - `email`: `{QQ_EMAIL_ID}`, ex: `QQEmail`; Code http://open.mail.qq.com/
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| QQChat Me 			| https://wpa.qq.com/msgrd										| - `v`: `3`
| 						| 																| - `uin`: `{QQ_TALK_ID}`, ex: http://wpa.qq.com/msgrd?v=3&uin={NUM}&site=XiaoMac&menu=yes
| 						| 																| - `site`: `{URL}`
| 						| 																| - `menu`: `yes`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Threema App			| threema://compose												| - `text`: `{TEXT} {URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| WeChat				| 																| WeChat require JS API or display a QRCode to be scanned with WeChat
| 						| 																|
| 						| 																| - http://dev.wechat.com/
| 						| 																| - http://admin.wechat.com/wiki/index.php?title=JS_SDK_DOCUMENT
| 						| 																| - https://github.com/weui/weui/wiki/%E5%BE%AE%E4%BF%A1JSAPI
| 						| 																| - https://stackoverflow.com/questions/22636071/wechat-sharing-how-to-change-re-share-description-and-thumbail
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Twitter App			| twitter://post												| - `message`: `{URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| WhatsApp App			| whatsapp://send												| - `text`: `{URL}` or `{TEXT} {URL}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| WhatsApp App			| https://api.whatsapp.com/send									| - `phone`: phone number (international format, without spaces, etc.)
| 						| 																| - `text`: `{TEXT}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| WhatsApp App			| https://wa.me/{PHONE}											| - [WhatsApp FAQ - Using Click to Chat](https://faq.whatsapp.com/en/android/26000030/)
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Line App				| line://msg/text/{URL}											|
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------
| Mail					| mailto:														| - `to`: `{RECIPIENT_EMAIL}`
| 						|																| - `subject`: `{TITLE}`
| 						|																| - `body`: `{URL}` or `{DESCRIPTION}`
+-----------------------+---------------------------------------------------------------+----------------------------------------------------------

Others activities:

|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| Activity					| URI															| Parameters
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| Print						| javascript:window.print()										|
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| Add to Google Calendar	| https://www.google.com/calendar/event							| - `text`: `{TITLE}`
| 							| https://calendar.google.com/calendar/r/eventedit				| - `action` (optional): `TEMPLATE`
| 							|																| - `pprop` (optional): `HowCreated:QUICKADD`
| 							|																| - `sprop` (optional): ex: `website:www.justgiving.com`
| 							|																| - `sprop` (optional): ex: `name:Justgiving`
| 							|																| - `sf` (optional): `true`
| 							|																| - `dates`: `{START_DATE}/{END_DATE}` (format for each dates: `YYYYMMDD` or `YYYYMMDDTHHmmSS`)
| 							|																| - `details`: `{DESCRIPTION}` (multilines)
| 							|																| - `location`: `{LOCATION}` (could be an address, only one line, parts separated by comma `,`)
| 							|																| - `output` (optional): `xml`
| 							| 																|
| 							| 																| - [Add a Google calendar to your website - Calendar Help](https://support.google.com/calendar/answer/41207?hl=en&visit_id=1-636677701437823955-3736175218&rd=2)
|---------------------------|---------------------------------------------------------------|------------------------------------------------------------------------------------------------
| Add to Yahoo Calendar		| https://calendar.yahoo.com/									| - `text`: `{TITLE}`
| 							|																| - `v`: `60`
| 							|																| - `DUR` (optional): `{DURATION}` (format `HHmm`) For all-day event, dont use this field
| 							|																| - `TITLE`: `{TITLE}`
| 							|																| - `ST`: `{START_DATE}` (format: YYYYMMDD for all-day event or YYYYMMDDTHHmmSS)
| 							|																| - `in_loc`: `{LOCATION}`
| 							|																| - `DESC`: `{DESCRIPTION}`
| 							|																| - `URL`: `{URL}` page to link back to from the calendar
| 							|																| - `REND`: `{END_DATE}` format: total seconds since 1/1/1970 12:00:00 AM
| 							|																| - `RPAT`: `{REPEAT_DELAY}` format:
| 							|																| 	- Day: `01Dy`
| 							|																| 	- Week: `01Wk`
| 							|																| 	- Month: `01Mh`
| 							|																| 	- Year: `01Yr`
| 							|																| 	- Mon Wedn Fri: `01MoWeFr`
| 							|																| 	- Tues Thurs: `01TuTh`
| 							|																| 	- Mon - Fri: `01MoTuWeThFr`
| 							|																| 	- Sat - Sun: `01SuSa`
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| Add to Windows Live		| https://calendar.live.com/calendar/calendar.aspx				| - `rru`: `addevent`
| 							|																| - `summary`: `{TITLE}`
| 							|																| - `location`: `{LOCATION}`
| 							|																| - `dtstart`: `{START_DATE}` (format: `YYYYMMDDTHHmmSS` or `YYYYMMDD` for all-day event)
| 							|																| - `dtend`: `{END_DATE}` (format: same as `dtstart`)
| 							|																| - `description`: `{DESCRIPTION}`
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| QRCode (WeChat, etc.)		| https://chart.googleapis.com/chart							| - `chs`: `{WIDTH}x{HEIGHT}`, ex: `400×400`
| 							| 																| - `cht`: `qr`
| 							| 																| - `chld`: `{QRCODE_ECL}|{MARGIN}`, ex: `L|5`
| 							| 																| - `chl`: `{URL}`
| 							| 																|
| 							| 																| - [QR Codes  |  Infographics  |  Google Developers](https://developers.google.com/chart/infographics/docs/qr_codes)
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------
| iCalendar file			| data:text/calendar,											| URL encoded content of iCalendar
| 							| 																|
| 							| 																| [iCalendar - Wikipedia](https://en.wikipedia.org/wiki/ICalendar)
|---------------------------|---------------------------------------------------------------|----------------------------------------------------------

More networks and informations:

- [bradvin/social-share-urls: Social Share URLs](https://github.com/bradvin/social-share-urls)
- [cferdinandi/social-sharing: Add social sharing links and buttons without the bloat.](https://github.com/cferdinandi/social-sharing#2-add-the-markup-to-your-html)
- [The Simplest (and Most Performant) Way to Offer Sharing Links for Social Media | CSS-Tricks](https://css-tricks.com/simple-social-sharing-links/)
- [url - Renren, Weibo, and Baidu Like buttons using only HTML (No Javascript) - Stack Overflow](https://stackoverflow.com/questions/10490443/renren-weibo-and-baidu-like-buttons-using-only-html-no-javascript)
- [How To Add Chinese Social Media Sharing Links in WordPress Jetpack Sharing | Duncan's Blog](https://blog.duncanworthy.me/misc/how-to-add-chinese-social-media-sharing-links-on-wordpress/)
- [How do I setup custom sharing? – Ideas and Knowledge Base for Netvibes](http://faq.netvibes.com/knowledgebase/articles/370909-how-do-i-setup-custom-sharing)
- [WP Open Social – WordPress plugin | WordPress.org](https://wordpress.org/plugins/open-social/#developers)

Plugins and libs:

- [2 Click Social Media Buttons – WordPress plugin | WordPress.org](https://wordpress.org/plugins/2-click-socialmedia-buttons/)

### Interactions count

- [BuzzSumo - Chrome Web Store](https://chrome.google.com/webstore/detail/buzzsumo/gedpbnanjmblcmlfhgfficjnglidndfo)
- [Get number of shares from social platforms](https://gist.github.com/ihorvorotnov/9132596)
- [Get the share counts from various APIs](https://gist.github.com/jonathanmoore/2640302)

### Open Intent URL

Use `target="_blank"` (adviced) and `rel="nofollow"` (required).

```js
// Note: chrome doesn't support "noopener", that break other features
const width = 600;
const height = 600;
const left = (window.screen.width - width) / 2 - 10;
const top = (window.screen.height - height) / 2 - 50;

// top and left not work when the opener window is at secondary screen.
const intentWindow = window.open("about:blank", "Share on Twitter", `resizable,scrollbars,noopener,status,width=${width},height=${height},left=${left},top=${top}`);

// Or:
//const intentWindow = window.open("about:blank", "Share on Twitter", `resizable,scrollbars,noopener,status`);
//intentWindow.resizeBy(width - shareWindow.innerHeight, height - shareWindow.innerWidth);// resize to match requested size for the content (innerWidth and innerHeight)
//intentWindow.moveTo(top, left);// don't support toolbars, scrollbars, and other UI element size. But let the browser to choose where the popup should be

// Clear opener (for security purpose)
intentWindow.document.write(`<script>window.opener=null;location.replace("${url}");setTimeout(function(){window.close();}, 2000)</script>`);// on iOS, when an Universal Link is registered by an app (ex: Twitter catch all URLs https://www.twitter.com/*), it could handle the URL, leaving the about:blank page opened. Else wait few second let the time to the next page to load and discard the setTimeout.
// doc.write is a navigation and require doc.close()
// data URI can't be used here because of IE. You can use blob URI, but it's not pratical because we need to revoke the object URL once the popup is loaded
```

Note: if the intent document load start can't be made direclty after the user interaction (set the final `window.open` href in click listener), open a blank document the intent window first, and later (after a asynchronous task, update the content of popup) set the final URL

- Facebook: 600×300 or 555×320
- Twitter: 550×420 or 500×310
- LinkedIn:
	- login: content: 974×622, window.open(): 974×688 (Chrome macOS)
	- share: content: 550×475 (content call automatically `window.resizeBy(offsetX, offsetY)`)

- [Tabnabbing: Link and `target="_blank"` or `window.open()`](Security#tabnabbing-link-and-target_blank-or-windowopen)
- [Overview — Twitter Developers](https://developer.twitter.com/en/docs/twitter-for-websites/web-intents/overview)
- [Window.open() - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window/open)
- [javascript - Use window.open but block use of window.opener - Stack Overflow](https://stackoverflow.com/questions/40593632/use-window-open-but-block-use-of-window-opener)

## Share buttons

Is it really usefull?

> ils ne sont utilisé que moins d’une fois sur 5
– [De l'intérêt des boutons de partage - MediasSociaux.fr](http://www.mediassociaux.fr/2012/11/15/de-linteret-des-boutons-de-partage/)

- [Social media unbuttoned | Roxane](http://www.roxane-company.com/blog/2012/11/27/social-media-unbuttoned/)
- [How important are all those ugly Tweet Buttons to news sites? » Nieman Journalism Lab](http://www.niemanlab.org/2012/05/how-important-are-all-those-ugly-tweet-buttons-to-news-sites/)
- [Social Media Sharing Buttons. No JavaScript. No tracking. Super fast and easy.](http://sharingbuttons.io/)

## Map engine API

- [Category:Internet censorship by country — Wikipedia](https://en.wikipedia.org/wiki/Category:Internet_censorship_by_country)
- [All disruptions – Traffic – Google Transparency Report](https://www.google.com/transparencyreport/traffic/disruptions/#group=REGION)

HTTPS not supported by Google Apps for Crimea, Cuba, Iran, North Korea, Sudan, and Syria. That means accounts not working.

- [Countries or regions with restricted access - Google Apps Administrator Help](https://support.google.com/a/answer/2891389?hl=en)

Borders and labels are differents based where your request maps. Examples: Arunachal Pradesh and Kashmir (google.cn/maps, google.co.in/maps, google.com/maps)

- [Category:Territorial disputes by country — Wikipedia](https://en.wikipedia.org/wiki/Category:Territorial_disputes_by_country)
- [List of territorial disputes — Wikipedia](https://en.wikipedia.org/wiki/List_of_territorial_disputes)
- [Google Maps in China — Wikipedia](https://en.wikipedia.org/wiki/Google_Maps#Google_Maps_in_China)

In China?

- https://maps.googleapis.com with http://maps.google.cn
- [百度地图API-首页](http://lbsyun.baidu.com/) http://developer.baidu.com/map/jsdemo.htm#a5_1
	http://lbsyun.baidu.com/index.php?title=webapi/guide/webservice-geocoding
	http://lbsyun.baidu.com/index.php?title=jspopular
- [搜狗地图API - Sogou Maps JavaScript API](http://map.sogou.com/api/documentation/javascript/api2.5/basics.html)
- http://api.map.baidu.com/staticimage?center={longitude},{latitude}&width={width}&height={height}&zoom=15&markers={longitude},{latitude}
	http://api.map.baidu.com/staticimage?center=121,31&width=300&height=300&zoom=15

- [android - Using Google Maps and Baidu Maps in same app - Stack Overflow](https://stackoverflow.com/questions/18910361/using-google-maps-and-baidu-maps-in-same-app/29468356#29468356)

- [Websites blocked in mainland China — Wikipedia](https://en.wikipedia.org/wiki/Websites_blocked_in_mainland_China)

## Google Search Console

- [Malicious Google Search Console Verifications](https://blog.sucuri.net/2015/09/malicious-google-search-console-verifications.html)

## Online document previewer

Only files under 25 MB can be previewed with the Google Drive viewer.

Google Drive viewer:

- Image files (.JPEG, .PNG, .GIF, .TIFF, .BMP)
- Video files (WebM, .MPEG4, .3GPP, .MOV, .AVI, .MPEGPS, .WMV, .FLV)
- Text files (.TXT)
- Markup/Code (.CSS, .HTML, .PHP, .C, .CPP, .H, .HPP, .JS)
- Microsoft Word (.DOC and .DOCX)
- Microsoft Excel (.XLS and .XLSX)
- Microsoft PowerPoint (.PPT and .PPTX)
- Adobe Portable Document Format (.PDF)
- Apple Pages (.PAGES)
- Adobe Illustrator (.AI)
- Adobe Photoshop (.PSD)
- Tagged Image File Format (.TIFF)
- Autodesk AutoCad (.DXF)
- Scalable Vector Graphics (.SVG)
- PostScript (.EPS, .PS)
- TrueType (.TTF)
- XML Paper Specification (.XPS)
- Archive file types (.ZIP and .RAR)

```html
<iframe src="https://docs.google.com/viewer?embedded=true&url=URL_OF_DOCUMENT"><a href="URL_OF_DOCUMENT">DOCUMENT_TITLE</a></iframe>
<!-- https://drive.google.com/viewerng/viewer?embedded=true&url=URL_OF_DOCUMENT -->
```

Office Web Apps Viewer:

- ppt
- pptx
- doc
- docx
- xls
- xlsx

```html
<iframe src="https://view.officeapps.live.com/op/embed.aspx?src=URL_OF_DOCUMENT"></iframe>
<iframe src="http://docs.google.com/fileview?id=GOOGLE_DOC_ID&hl=en&pid=explorer&efh=false&a=v&chrome=false&embedded=true"></iframe>
```

- [Embedded File Viewer: Google Drive, OneDrive](https://gist.github.com/tzmartin/1cf85dc3d975f94cfddc04bc0dd399be)
- https://docs.google.com/spreadsheets/d/SHEET_ID/pubhtml?widget=true&amp;headers=true
- [oEmbed]
- [Google Docs oEmbed — WordPress Plugins](https://wordpress.org/plugins/google-docs-oembed/#developers)

## URL shorteners

- http://bit.ly/
- http://goo.gl/
- http://t.co/
- http://ow.ly/
- http://adf.ly/
- http://tinyurl.com/
- http://wp.me/

- http://amzn.to/
- http://youtu.be/

- http://bit.do/
- http://lnkd.in/
- http://db.tt/
- http://qr.ae/
- http://cur.lv/
- http://ht.ly/
- http://ity.im/
- http://q.gs/
- http://is.gd/
- http://po.st/
- http://bc.vc/
- http://u.to/
- http://j.mp/
- http://buzurl.com/
- http://cutt.us/
- http://u.bb/
- http://x.co/
- http://scrnch.me/
- http://vzturl.com/
- http://qr.net/
- http://1url.com/
- http://tweez.me/
- http://v.gd/
- http://tr.im/
- http://trib.al/
- http://zip.net/
- http://➡.ws/
- http://✩.ws/
- http://0.mk/
- http://888.hn/
- http://b54.in/
- http://bit.ly/
- http://budurl.com/
- http://doiop.com/
- http://korta.nu/
- http://lxcurl.com/
- http://s.coop/
- http://snipurl.com/
- http://tiny.cc/
- http://tinyurl.com/
- http://gg.gg/
- http://urlcut.org/
- http://qr.net/
- http://7.ly/
- http://clicky.me/
- http://bigly.us/
- http://minu.me/
- http://tinyarro.ws/
- http://urlrace.com/
- http://qoiob.com/
- http://sh.st/

Branded bitly

- [http://lemde.fr/](https://bitly.com/pages/landing/branded-short-domains-powered-by-bitly?bsd=lemde.fr)

- [List of URL Shorteners](http://bit.do/list-of-url-shorteners.php)
- [Sites about Url shortener](http://dig.do/about/url-shortener)
- [URL shortening — Wikipedia](https://en.wikipedia.org/wiki/URL_shortening)
- [List of URL Shorteners](http://l-lists.com/en/lists/gvaoif.html)
- [URL Toolbox: 90+ URL Shortening Services](http://mashable.com/2008/01/08/url-shortening-services/#XL2l1FTKhPq4)
- https://gist.github.com/MrSherlockHolmes/b3fc2b21b94040921c69
- https://www.techmaish.com/list-of-230-free-url-shorteners-services/

Unshorten:

- `https://unshorten.me/s/{short}`
- `http://www.linkexpander.com/?url={short}`

```js
function unshorten_url($url) {
	// Don't use this in production: need to limit API access, need a resolved URL cache, have security issues (SSRF), etc.
	// Filter in Location localhost domains. See http://php.net/manual/en/function.curl-setopt.php#116223
	$ch = curl_init($url);
	curl_setopt_array($ch, array(

		CURLOPT_RETURNTRANSFER => true,     // don't output response
		CURLOPT_HEADER         => false,    // do not return headers
		CURLOPT_FOLLOWLOCATION => true,     // follow redirects. Note: CURLOPT_FOLLOWLOCATION cannot be activated when safe_mode is enabled or an open_basedir is set in. See http://php.net/manual/en/function.curl-setopt.php#113682
		CURLOPT_USERAGENT      => $_SERVER['HTTP_USER_AGENT'],
		CURLOPT_AUTOREFERER    => true,     // set referer on redirect
		CURLOPT_CONNECTTIMEOUT => 120,      // timeout on connect
		CURLOPT_TIMEOUT        => 120,      // timeout on response
		CURLOPT_MAXREDIRS      => 10,       // stop after 10 redirects
		CURLOPT_PROTOCOLS      =>  CURLPROTO_HTTP || CURLPROTO_HTTPS // limit to HTTP and HTTPS protocols
	));
	curl_exec($ch);
	$url = curl_getinfo($ch, CURLINFO_EFFECTIVE_URL);
	curl_close($ch);
	return $url;
}
```

## Youtube

Link at time: `http://www.youtube.com/watch?v=cOde0332432&t=1m5s`

Embed with start time and stop (in seconds) `https://www.youtube.com/embed/7qkmGjWtG0w?start=840&end=1240&aut‌​oplay=1` or `https://www.youtube.com/v/7qkmGjWtG0w?start=840&end=1240&aut‌​oplay=1`
See [YouTube Embedded Players and Player Parameters  |  YouTube IFrame Player API  |  Google Developers](https://developers.google.com/youtube/player_parameters?#end) or [How to share a YouTube video with a specific start and end time? - Web Applications Stack Exchange](https://webapps.stackexchange.com/questions/61397/how-to-share-a-youtube-video-with-a-specific-start-and-end-time/61398)
But it's looklike the end parameter doesn't works (2018)

### Youtube video data

Video thumbnail:

```
https://i.ytimg.com/vi/{video-id}/{0,1,2,3,default,maxresdefault,hqdefault,mqdefault,sddefault}.jpg
https://img.youtube.com/vi/{video-id}/{0,1,2,3,default,maxresdefault,hqdefault,mqdefault,sddefault}.jpg
https://i.ytimg.com/vi_webp/{video-id}/{0,1,2,3,default,maxresdefault,hqdefault,mqdefault,sddefault}.webp
```

Require an API key:

```
https://www.googleapis.com/youtube/v3/videos?part={properties}&id={video_ids}&key={api_key}
```

- view count `json.videos[0].statistics.viewCount` (see also `.likeCount`)
- title `items.snippet.title`
- `items.contentDetails.duration`

- `https://www.youtube.com/get_video_info?video_id={video_id}` - `application/x-www-form-urlencoded` (for Flash player?)
- `https://www.youtube.com/oembed?url={video-url}&format=json` - [oEmbed](https://oembed.com/) JSON (no CORS)
- `https://noembed.com/embed?url={video-url}&format=json` - [Noembed - oEmbed everything.](https://noembed.com/), [leedo/noembed: oEmbed gateway service with additional non-oEmbed sources](https://github.com/leedo/noembed) and [noembed/noembed: oEmbed gateway service with additional non-oEmbed sources](https://github.com/noembed/noembed)
- [itteco/iframely: oEmbed proxy. Supports over 1800 domains via custom parsers, oEmbed, Twitter Cards and Open Graph](https://github.com/itteco/iframely)
- [YouTube Data API Overview  |  YouTube Data API  |  Google Developers](https://developers.google.com/youtube/v3/getting-started)

### API

Require embed src with param `enablejsapi=1`

Add it in with wordpress:

```php
/* add post message api mode for youtube embeds */
add_filter('oembed_result' , function($html){
	return preg_replace_callback( '/(?<=")(https?:\/\/www.youtube.com\/embed\/[^"]+)/', function($matches){return add_query_arg('enablejsapi', '1', $matches[1]);}, $html);
});
```

- [YouTube Player API Reference for iframe Embeds  |  YouTube IFrame Player API  |  Google Developers](https://developers.google.com/youtube/iframe_api_reference?hl=en)
- [YouTube Embedded Players and Player Parameters  |  YouTube IFrame Player API  |  Google Developers](https://developers.google.com/youtube/player_parameters?hl=en#Parameters)
- [javascript - YouTube iframe API: how do I control a iframe player that's already in the HTML? - Stack Overflow](https://stackoverflow.com/questions/7443578/youtube-iframe-api-how-do-i-control-a-iframe-player-thats-already-in-the-html)

#### Stop video

```js
iframe.contentWindow.postMessage("{"\"event/":\"command\",\"func\":\"stopVideo\",\"args\":\"\"}", "*");
```

#### Listen events

`event.data` is a serialized JSON object

```js
window.addEventListener("message", function(event){JSON.parse(event.data).event});
iframe.contentWindow.postMessage("{\"event\":\"listening\"}", "*");
```

### Watch video in full HD

```
http://www.youtube.com/watch_popup?v=VIDEO_ID&vq=hd1080
```

### Video formats

- taille standard : 320×180@330Kbps en H263 (Sorenson)
- taille "HD" : 480×270@570Kbps en H263

## Dailymotion

### API

Require embed src with param `api=postMessage`.

Add it in with wordpress:

```php
/* add post message api mode for dailymotion embeds */
add_filter('oembed_result' , function($html){
	return preg_replace_callback( '/(?<=")(https?:\/\/www.dailymotion.com\/embed\/[^"]+)/', function($matches){return add_query_arg('api', 'postMessage', $matches[1]);}, $html);
});
```

- [Video Player Documentation - Dailymotion Developer Area](https://developer.dailymotion.com/player)

#### Pause video

```js
iframe.contentWindow.postMessage("{\"command\":\"pause\",\"parameters\":[]}", "*");
```

Previously?:

```js
iframe.contentWindow.postMessage("pause", "*");
```

- [javascript - Dailymotion stop video from iframe - Stack Overflow](https://stackoverflow.com/questions/26174793/dailymotion-stop-video-from-iframe)

#### Listen events

`event.data` is a query string

```js
window.addEventListener("message", function(event){new URLSearchParams(event.data).get("event")});
```

## Google Maps

- `https://www.google.com/maps/@{latitude},{longitude},{zoom}z`
- `https://maps.google.com/maps?daddr={latitude},{longitude}{&saddr}` `saddr` is optional: start point, `daddr` is optional: destination point (add `+to:` for steps "via")
- `https://www.google.com/maps/dir/{startpoint}/{destpoint}` (`startpoint` is optional, can be blank, `startpoint` can be `current+location`). For steps "via" (multidestination / waypoints) add `/{point}` between start and dest. Encode space with `+` (`%20` is also supported). For multiline/multipart addresses (ex: street name, city, zipcode, country), replace line break with `,`
- `https://www.google.com/maps/place/?q=place_id:{placeid}` `placeid` start with `ChIJ...`
- `https://www.google.com/maps/place/{placename}/@{latitude},{longitude},{zoom}z/`

Bracket syntax (add a label for start or dest) doesn't work any more.

- [javascript - Google Maps Directions API Equivalent URL - Stack Overflow](https://stackoverflow.com/questions/16326143/google-maps-directions-api-equivalent-url/24065211#24065211)
- [Everything You Never Wanted to Know About Google Maps' Parameters - YouMoz - Moz](https://moz.com/ugc/everything-you-never-wanted-to-know-about-google-maps-parameters)
- [Google maps query parameter clarification - Stack Overflow](https://stackoverflow.com/questions/11354211/google-maps-query-parameter-clarification/11354743#11354743)
- [android - Can I add titles to locations for the directions url for maps.google.com? - Stack Overflow](https://stackoverflow.com/questions/12716152/can-i-add-titles-to-locations-for-the-directions-url-for-maps-google-com/12716995#12716995)
- [Google Maps URL Scheme | Google Maps SDK for iOS | Google Developers](https://developers.google.com/maps/documentation/ios-sdk/urlscheme)
- [Google Map Parameters - Google Mapki](http://web.archive.org/web/20110903160743/http://mapki.com/wiki/Google_Map_Parameters)

### Google Maps My Maps

Use it as data source and editor (can output KML)

Import Google Drive Sheet in My Map : New Layer > Import > Google Drive. Must contains at least columns: Title, Latitude, Longitude

Original Google Drive Share Url: `https://drive.google.com/file/d/{kml_file_id}`
Hosted KML file to use in your application: `https://googledrive.com/host/{kml_file_id}`

- [Visualize your data on a custom map using Google My Maps – Google Earth Outreach](https://www.google.com/earth/outreach/learn/visualize-your-data-on-a-custom-map-using-google-my-maps/)
- [Mapping from a Google Spreadsheet – Google Earth Outreach](https://www.google.com/earth/outreach/learn/mapping-from-a-google-spreadsheet/)

### Google Maps styles

Only for embeded maps

- [Snazzy Maps - Free Styles for Google Maps](https://snazzymaps.com/) `window.map.setMapTypeId(google.maps.MapTypeId.HYBRID)` or `window.editor.map.setMapTypeId(google.maps.MapTypeId.HYBRID)` for https://snazzymaps.com/editor/customize/XXXXX
- [Styling Wizard: Google Maps APIs](https://mapstyle.withgoogle.com/)
- [Start Styling your Map | Google Maps JavaScript API | Google Developers](https://developers.google.com/maps/documentation/javascript/styling)

```json
[
	{
		"elementType": "labels",
		"stylers": [
			{
				"visibility": "off"
			}
		]
	},
	{
		"featureType": "administrative.land_parcel",
		"stylers": [
			{
				"visibility": "off"
			}
		]
	},
	{
		"featureType": "administrative.neighborhood",
		"stylers": [
			{
				"visibility": "off"
			}
		]
	}
]
```

### API

```html
<!DOCTYPE html>
<html>
	<head>
		<title>PlaceID finder</title>
		<meta name="viewport" content="initial-scale=1.0, user-scalable=no">
		<meta charset="utf-8">
		<style>
			html, body {
				height: 100%;
				margin: 0;
				padding: 0;
			}
			#map {
				height: 100%;
			}
			.controls {
				background-color: #fff;
				border-radius: 2px;
				border: 1px solid transparent;
				box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
				box-sizing: border-box;
				font-family: Roboto;
				font-size: 15px;
				font-weight: 300;
				height: 29px;
				margin-left: 17px;
				margin-top: 10px;
				outline: none;
				padding: 0 11px 0 13px;
				text-overflow: ellipsis;
				width: 400px;
			}

			.controls:focus {
				border-color: #4d90fe;
			}

		</style>
	</head>
	<body>
		<input id="pac-input" class="controls" type="text"
				placeholder="Enter a location">
		<div id="map"></div>

		<script>
// This sample uses the Place Autocomplete widget to allow the user to search
// for and select a place. The sample then displays an info window containing
// the place ID and other information about the place that the user has
// selected.

function initMap() {
	var map = new google.maps.Map(document.getElementById('map'), {
		center: {lat: -33.8688, lng: 151.2195},
		zoom: 13
	});

	var input = document.getElementById('pac-input');

	var autocomplete = new google.maps.places.Autocomplete(input);
	autocomplete.bindTo('bounds', map);

	map.controls[google.maps.ControlPosition.TOP_LEFT].push(input);

	var infowindow = new google.maps.InfoWindow();
	var marker = new google.maps.Marker({
		map: map
	});
	marker.addListener('click', function() {
		infowindow.open(map, marker);
	});

	autocomplete.addListener('place_changed', function() {
		infowindow.close();
		var place = autocomplete.getPlace();
		if (!place.geometry) {
			return;
		}

		if (place.geometry.viewport) {
			map.fitBounds(place.geometry.viewport);
		} else {
			map.setCenter(place.geometry.location);
			map.setZoom(17);
		}

		// Set the position of the marker using the place ID and location.
		marker.setPlace({
			placeId: place.place_id,
			location: place.geometry.location
		});
		marker.setVisible(true);

		infowindow.setContent('<div><strong>' + place.name + '</strong><br>' +
				'Place ID: ' + place.place_id + '<br>' +
				'Place loc: ' + place.geometry.location.lat() + "," + place.geometry.location.lng() + '<br>' +
				place.formatted_address);
		infowindow.open(map, marker);
	});

	// Get the placeID of point of interest ("poi", always visible on the map)
	var placesService = new google.maps.places.PlacesService(map);
	map.addListener('click', function(event){
		if (event.placeId) {
			// Calling e.stop() on the event prevents the default info window from
			// showing.
			// If you call stop here when there is no placeId you will prevent some
			// other map click event handlers from receiving the event.
			event.stop();

			placesService.getDetails({placeId: event.placeId}, function(place, status) {
				if (status === 'OK') {
					infowindow.close();
					infowindow.setPosition(place.geometry.location);
					// place.icon;
					infowindow.setContent('<div><strong>' + place.name + '</strong><br>' +
							'Place ID: ' + place.place_id + '<br>' +
							'Place loc: ' + place.geometry.location.lat() + "," + place.geometry.location.lng() + '<br>' +
							place.formatted_address);
					infowindow.open(map);
				}
			});
		}

	});
}

		</script>
		<script src="https://maps.googleapis.com/maps/api/js?key=YOUR_API_KEY&libraries=places&callback=initMap" async defer></script>
	</body>
</html>
```

- `https://maps.googleapis.com/maps/api/place/details/json?key=YOURAPIKEY&placeid=THEPLACEID` -> `json["result"]["url"]` `PLACE_ID` start with `ChIJ...`
- [google maps - How do I remove default markers? - Stack Overflow](https://stackoverflow.com/questions/7538444/how-do-i-remove-default-markers) - How to remove Points of Interest (colored marker for commercial places, monuments, etc.), use [style feature type `poi`](https://developers.google.com/maps/documentation/javascript/style-reference)
- [API Manager](https://console.developers.google.com/apis/api/maps_backend/overview)
- [PlaceID Finder | Google Maps JavaScript API | Google Developers](https://developers.google.com/maps/documentation/javascript/examples/places-placeid-finder)
- [POI Click Event | Google Maps JavaScript API | Google Developers](https://developers.google.com/maps/documentation/javascript/examples/event-poi)

Center to all markers

```js
var markers = [];//some array
var bounds = new google.maps.LatLngBounds();
for (var i = 0; i < markers.length; i++) {
	bounds.extend(markers[i].place.location);
}

map.fitBounds(bounds);
```

- [javascript - Center/Set Zoom of Map to cover all visible Markers? - Stack Overflow](https://stackoverflow.com/questions/19304574/center-set-zoom-of-map-to-cover-all-visible-markers)

### Icons

```
https://mt.google.com/vt/icon/... = https://mt0.google.com/vt/icon/... = https://mt.google.com/vt/icon?... = https://www.google.com/maps/vt/icon/....
```

`https://www.google.com/maps/vt/icon/name=...&scale=...` or `https://www.google.com/maps/vt/icon?...=...&...=...` or `https://www.google.com/maps/vt/icon/...=...&...=...?...=...&...=...`

- `name=...` path (1,n) required. List of graphic resources to use. The last element is the first in front
- `highlight=...` color (1,n). Replace a color (ex. `assets/icons/poi/quantum/container_shadow-1-small.png`: none, `assets/icons/poi/quantum/container-1-small.png`: 0×00FF00, icon: 0xFF00FF) by the given color
- `scale=...` number 1 (default), 2 (retina, 2x), 3, 4. Scale of the result image
- `text=...` string. Text
- `psize=...` text size
- `font=...` font path eq. `fonts/Roboto-Bold.ttf`
- `color=...` color. text color
- `ax=...` number. Text x position
- `ay=...` number. Text y position

- `color`: hexadecimal: 0, ARGB, RRGGBB or AARRGGBB
- quantity `1, n`: could be 1 value or multiple values separated by `,`
- `...-3-large`, `...-2-medium`, `...-1-small`, `...-0-tiny`. All sizes are not supported by each icons. All support at least medium and small sizes. Width and height are related to size, resolution and icon

List of available resources (protocol buffer encoded data): https://www.gstatic.com/maps/res/CompactLegend-Roadmap-cbc3edfa467314789e34bc25eaddcfe2 (to get the last version, `view-source:https://www.google.com/maps/search/` and search `gstatic.com/maps/res/CompactLegend`)

```
9 {
	1: "bank_dollar-1-small"// name without full path and extension .png
	2: 4//
	5: 0// type/collection 0 poi assets/icons/poi/quantum/*, 9 assets/icons/poi/quantum/container*, 12 London related, 17 Sydney related see "transit/localizations/.../..."
	6: 0×00ffffff// color. See highlight
}
```

0×6d7be3, 0×8d6e63, 0xf57f17

- `name=icons/spotlight/restaurant_search_L_8x.png&scale=1`
- `name=icons/spotlight/lodging_search_L_8x.png&scale=1`
- `name=icons/spotlight/star_L_8x.png&scale=1`
- `name=icons/spotlight/generic_search_L_8x.png&scale=1`
- `name=icons/spotlight/spotlight-poi.png&scale=2`
- `name=assets/icons/poi/tactile/measle-2-medium.png&color=ff000000?scale=1`
- `name=assets/icons/road/transparent-2-medium.png&color=ff000000?scale=1`
- `name=assets/icons/spotlight/spotlight_poi-1-small.png&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container-19px-2-medium.png,assets/icons/poi/quantum/container-19px-2-medium.png,assets/icons/poi/quantum/branded/...`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/restaurant-1-small.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/lodging-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/cemetery-1-small.png&highlight=ff000000,ffffff,7cb342&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/golf-1-small.png&highlight=ff000000,ffffff,7cb342&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/historic-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/hospital_H-1-small.png&highlight=ff000000,ffffff,db4437&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/museum-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/note-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/paw-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/school-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/shoppingbag-1-small.png&highlight=ff000000,ffffff,6b79c5&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/stadium-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/worship_temple-1-small.png&highlight=ff000000,ffffff,8d6e63&color=ff000000?scale=1`
- `name=assets/icons/transit/localizations/ru/moscow-metro_ring-0-tiny.png,assets/icons/transit/localizations/ru/moscow-metro_circle-0-tiny.png,assets/icons/transit/localizations/ru/moscow-metro_m-0-tiny.png&highlight=143c9a,ffffff,e6362e&color=ff000000?scale=1`
- `name=assets/icons/transit/localizations/ru/moscow-metro_ring-1-small.png,assets/icons/transit/localizations/ru/moscow-metro_circle-1-small.png,assets/icons/transit/localizations/ru/moscow-metro_m-1-small.png&highlight=143c9a,ffffff,e6362e&color=ff000000?scale=1`
- `name=assets/icons/transit/quantum/container_shadow-0-tiny.png,assets/icons/transit/quantum/container-0-tiny.png,assets/icons/transit/quantum/train-0-tiny.png&highlight=0,b0ff,ffffff&color=ff000000?scale=1`
- `name=assets/icons/transit/quantum/container_shadow-1-small.png,assets/icons/transit/quantum/container-1-small.png,assets/icons/transit/quantum/train-1-small.png&highlight=0,b0ff,ffffff&color=ff000000?scale=1`
- `text=A&psize=16&font=fonts/arialuni_t.ttf&color=ff330000&name=icons/spotlight/spotlight-waypoint-b.png&ax=44&ay=48&scale=1`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/home-1-small.png&highlight=ff000000,78909c,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/restaurant-1-small.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/star_shadow-1-small.png,assets/icons/poi/quantum/star_container-1-small.png,assets/icons/poi/quantum/star-1-small.png&highlight=ff000000,cd814b,ffed47&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/library-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/civic_bldg-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/shoppingcart-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/movie-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/shoppingbag-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/quantum/container_shadow-1-small.png,assets/icons/transit/quantum/container-1-small.png,assets/icons/transit/quantum/train-1-small.png&highlight=0,b0ff,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/stadium-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/worship_islam-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/localizations/fr/paris-rail-1-small.png,assets/icons/transit/localizations/fr/paris-rail_inside-1-small.png&highlight=111b8a,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/localizations/fr/paris-metro-1-small.png,assets/icons/transit/localizations/fr/paris-metro_inside-1-small.png&highlight=111b8a,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/museum-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/hospital_H-1-small.png&highlight=ff000000,db4437,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/camera-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/road/arrow-1-small.png&highlight=19286a&color=ff000000?scale=2`
- `name=assets/icons/transit/quantum/container_shadow-0-tiny.png,assets/icons/transit/quantum/container-0-tiny.png,assets/icons/transit/quantum/tram-0-tiny.png&highlight=0,b0ff,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/school-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/cemetery-1-small.png&highlight=ff000000,7cb342,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/lodging-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/theater-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/bar-1-small.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/monument-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/paw-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/localizations/fr/paris-rail-0-tiny.png,assets/icons/transit/localizations/fr/paris-rail_inside-0-tiny.png&highlight=111b8a,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/quantum/container_shadow-0-tiny.png,assets/icons/transit/quantum/container-0-tiny.png,assets/icons/transit/quantum/train-0-tiny.png&highlight=0,b0ff,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/bridge-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/historic-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/event_venue-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/worship_temple-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/tree-1-small.png&highlight=ff000000,7cb342,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/note-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/generic-1-small.png&highlight=ff000000,7cb342,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/bank_euro-1-small.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/police-1-small.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-1-small.png,assets/icons/poi/quantum/container-1-small.png,assets/icons/poi/quantum/cafe-1-small.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-2-medium.png,assets/icons/poi/quantum/container-2-medium.png,assets/icons/poi/quantum/ferriswheel-2-medium.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-2-medium.png,assets/icons/poi/quantum/container-2-medium.png,assets/icons/poi/quantum/parking-2-medium.png&highlight=ff000000,8d6e63,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-2-medium.png,assets/icons/poi/quantum/container-2-medium.png,assets/icons/poi/quantum/atm-2-medium.png&highlight=ff000000,6d7be3,ffffff&color=ff000000?scale=2`
- `name=assets/icons/poi/quantum/container_shadow-2-medium.png,assets/icons/poi/quantum/container-2-medium.png,assets/icons/poi/quantum/cafe-2-medium.png&highlight=ff000000,f57f17,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/quantum/container_shadow-1-small.png,assets/icons/transit/quantum/container-1-small.png,assets/icons/transit/quantum/bus-1-small.png&highlight=0,b0ff,ffffff&color=ff000000?scale=2`
- `name=assets/icons/transit/localizations/fr/paris-rail-3-large.png,assets/icons/transit/localizations/fr/paris-rail_inside-3-large.png&highlight=111b8a,ffffff&color=ff000000?scale=2`

- `https://maps.gstatic.com/mapfiles/api-3/images/spotlight-poi-dotless_hdpi.png`
- `https://maps.gstatic.com/mapfiles/api-3/images/spotlight-poi_hdpi.png`
- `https://maps.gstatic.com/mapfiles/api-3/images/icon_error.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/restaurant-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/generic_business-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/lodging-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/cafe-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/generic_recreational-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/bar-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/bus-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/civic_building-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/worship_general-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/museum-71.png`
- `https://maps.gstatic.com/mapfiles/place_api/icons/shopping-71.png`

- [Google Map icons with VisualRefresh - Stack Overflow](https://stackoverflow.com/questions/17746740/google-map-icons-with-visualrefresh)
- [image - What are the filenames of new colored Google maps markers? - Stack Overflow](https://stackoverflow.com/questions/19142242/what-are-the-filenames-of-new-colored-google-maps-markers)
- [javascript - Changing Color of New Google Markers (Google JS API v3) - Stack Overflow](https://stackoverflow.com/questions/22154188/changing-color-of-new-google-markers-google-js-api-v3)

### Static image with hdpi resolution

```
http://maps.googleapis.com/maps/api/staticmap?center=41.015408,28.970194&scale=2&zoom=15&size=470×250&sensor=false
```

See `scale=2` parameter, `scale=4` only available with key for "Google Maps API for Work"
Sizes are limited too.

https://developers.google.com/maps/documentation/staticmaps/

Grayscale : `...&style=feature:all|element:all|saturation:-100`

### Streetview 3D depth

Google maps provide a depth image in a base64 encoded + zlib compressed format (inside XML) for streetview

```
http://maps.google.com/cbk?output=xml&cb_client=maps_sv&v=4&dm=1&hl=en&panoid=4WGyVODT4of8gbmA48XKmw
```

- https://github.com/proog128/GSVPanoDepth.js/tree/master

## Google Search

Ignore country, go to http://www.google.com/ncr (No Country Redirect), to disable it, remove cookies

Search for specific country: http://www.google.com/search?hl=en&q=sample+query&gl=uk use `hl` for language and `gl` (for Geographic Location)

```js
/*
Get Google search result as text
But give not exacly the same as Google Search Page
*/
var urls = [], start = 0, rsz = 8;
var site = "example.com";
function xhrLoadHandler(event){
	var xhr = event.currentTarget;
	xhr.removeEventListener("load", xhrLoadHandler);
	xhr.removeEventListener("error", xhrErrorHandler);
	// should be a json
	var results;
	try {
		results = xhr.response["responseData"]["results"];
	}catch(error){
		console.log("Error at page " + start / rsz + ": " + error.message);
		console.log(urls.join("\n"));
		return;
	}

	for(var i = 0, l = results.length; i < l; i++){
		urls.push(results[i].url);
	}

	start += rsz;
	getNextPage();
}
function xhrErrorHandler(event){
	var xhr = event.currentTarget;
	xhr.removeEventListener("load", xhrLoadHandler);
	xhr.removeEventListener("error", xhrErrorHandler);
	console.log("Error at page " + start / rsz);
	console.log(urls.join("\n"));
}
function getNextPage(){
	var xhr = new XMLHttpRequest();
	xhr.addEventListener("load", xhrLoadHandler);
	xhr.addEventListener("error", xhrErrorHandler);
	xhr.open("GET", "https://ajax.googleapis.com/ajax/services/search/web?v=1.0&q=site:" + site + "&rsz=" + rsz + "&start=" + start);
	xhr.responseType = "json";
	xhr.send();
}
getNextPage();
```

## Chrome Web Store

### Download Google Chrome extension without installing it

1. Find the ID of the extension you’re interested in. When on the details page of the extension, it will be something like `bfbmjmiodbnnpllbbbfblcplfjjepjdn` after `https://chrome.google.com/extensions/detail/` in the page URL
2. Paste this URL into your browser: `https://clients2.google.com/service/update2/crx?response=redirect&prodversion=38.0&x=id%3D{EXT_ID}%26installsource%3Dondemand%26uc` replacing `{EXT_ID}` with the extension ID.
3. You’ll be prompted to save a CRX file. Drag this file to a Chrome window and proceed with installation

 ```
product_version = 91.0.4442.4 | 32.0
os = mac | win | android | cros | openbsd | linux
product_channel = unknown
product_id = chromium
nacl_arch =  arm | x86-64 | x86-32
arch = x64
os_arch = x86_64
language = en-US
accept_format = crx2,crx3
https://clients2.google.com/service/update2/crx?response=redirect&os={os}&arch={arch}&os_arch={os_arch}&nacl_arch={nacl_arch}&prod={product_id}&prodchannel={product_channel}&prodversion={product_version}&lang={language}&acceptformat={accept_format}&x=id%3D{EXT_ID}%26installsource%3Dondemand%26uc
https://clients2.google.com/service/update2/crx?response=redirect&os=linux&arch=x64&os_arch=x86_64&nacl_arch=x86-64&prod=chromium&prodchannel=unknown&prodversion=91.0.4442.4&lang=en-US&acceptformat=crx2,crx3&x=id%3Daedmpdookgbneegaeajpoldpnpfbpmlb%26installsource%3Dondemand%26uc
https://clients2.google.com/service/update2/crx?response=redirect&prodversion={product_version}&x=id%3D{EXT_ID}%26installsource%3Dondemand%26uc
```

Or:

- https://addons.opera.com/en/extensions/details/download-chrome-extension-9/

See [CRX / NEX (Opera)](#crx--nex-opera)

### CRX / NEX (Opera)

Find "PK" and remove all bytes before

```c
typedef struct {
	SetBackColor(0xd8e5ed);
	char magicNumber[4];
	SetBackColor(0xd8edd8);
	uint32 version;
	SetBackColor(0xd8e5ed);
	uint32 pkLength;
	SetBackColor(0xd8edd8);
	uint32 sigLength;
	SetBackColor(0xf7d6c3);
	byte pubKey[pkLength];
	SetBackColor(0xd8edd8);
	byte sig[sigLength];
	byte zipData[];
} CRX;
```

- [CRX Package Format - Google Chrome](https://developer.chrome.com/extensions/crx)

## Open Street Map

- [OpenStreetMap](https://www.openstreetmap.org/) `#map=12/49.2272/2.5303` (zoom/lat/lng)
- [Open styles, map gallery, catography](https://openmaptiles.org/styles/)
- [Maputnik](http://editor.openmaptiles.org/) `#11.6/47.3720/8.5420` (zoom/lat/lng)

## Vimeo

Link at time: `https://vimeo.com/1111111111#t=1m5s`

- taille standard : 504×404@440Kbps en On2 VP6
- taille "HD" : 1280×720@1500Kbps en On2 VP6

### API

- [Player JavaScript API sur Vimeo sur l'API Vimeo Developer](https://developer.vimeo.com/player/js-api)

Require embed src with param `api=1` (only for listening messages, not required to send commands)

Add it in with wordpress:

```php
/* add post message api mode for vimeo embeds */
add_filter('oembed_result' , function($html){
	return preg_replace_callback( '/(?<=")(https?:\/\/player.vimeo.com\/video/\/[^"]+)/', function($matches){return add_query_arg('api', '1', $matches[1]);}, $html);
});
```

#### Pause video

```js
iframe.contentWindow.postMessage("{\"method\":\"pause\"}", "*");
```

#### Seek video

```js
iframe.contentWindow.postMessage("{\"method\":\"seekTo\", \"value\":0}", "*");// in seconds
```

#### Listen events

`event.data` is a serialized JSON object

```js
// register all event subscriptions you want: `pause`, `play`, `finish` or `playProgress`. `ready` don't need subscription, it's dispatched automatically
iframe.contentWindow.postMessage("{\"method\":\"addEventListener\",\"value\":\"pause\"}", "*");
window.addEventListener("message", function(event){JSON.parse(event.data).event});
```

## Digital Distribution Platforms

### Apple Store

Badge:

- [App Store Marketing Guidelines - Apple Developer](https://developer.apple.com/app-store/marketing/guidelines/#downloadOnAppstore)

- http://www.apple.com/itunes/affiliates/resources/documentation/itunes-store-web-service-search-api.html
- https://linkmaker.itunes.apple.com/
- [Scrape ratings from iTunes store with PHP](https://gist.github.com/sgmurphy/1878352)

See also [Data/iTunes tips]()

App infos

```
http://itunes.apple.com/lookup?id=%%&country=%REGION%&lang=%LANG%
// Where %REGION% language ID like "us", "fr", "ca" (optional)
// Where %LANG% language ID like "en", "fr", "es" (optional)
// Return JSON with array (zero, one or more items, see `json.resultCount` field)
```

Artist or developper URL

```
https://itunes.apple.com/artist/id%ARTIST_ID%

https://itunes.apple.com/%REGION%/artist/id%ARTIST_ID%?l=%LANG%
// Where %REGION% language ID like "us", "uk", "fr", "ca". But there are redirections like "us" → "en", "uk" → "gb"
// Where %LANG% language ID like "en", "fr", "es"
```

App URL

```
https://itunes.apple.com/app/id%APP_ID%

https://itunes.apple.com/%REGION%/app/id%APP_ID%?l=%LANG%
// Where %REGION% language ID like "us", "uk", "fr", "ca". But there are redirections like "us" → "en", "uk" → "gb"
// Where %LANG% language ID like "en", "fr", "es"
```

### Google Play

Badge:

- [Google Play Badge Generator | Android Developers](http://developer.android.com/distribute/tools/promote/badges.html)
- https://developer.android.com/downloads/brand/en_generic_rgb_wo.ai or https://android.googlesource.com/platform/frameworks/base/+/refs/heads/master/docs/downloads/brand/en_generic_rgb_wo.ai

App info

```
https://play.google.com/store/xhr/getdoc
// POST ids=%APP_ID%&hl=%LANG% (application/x-www-form-urlencoded)
// Where %LANG% language ID like "en-us", "en_us" or "en"
// Remove first 6 chars (JSONP XSS protection)
// Replace "[," to "[null,", ",," to ",null," and ",]" to ",null]". You should use lookbehind and lookahead regexp
// Parse it as JSON
// `json[0][2][0]`: APP_ID is [0], APP_NAME is [8], user average rate is [16], user num reviews is [17], URL is [6]
```

- https://stackoverflow.com/questions/22134494/formatting-json-data-using-php

Or scrapper like http://code.google.com/p/google-playstore-api

- [PHP scrapper for Amazon App Store, Google Play Store and Windows Phone Store](https://github.com/pastfuture/MarketBot)
- [PHP scrapper for Google Play Store](https://github.com/thetutlage/Google-Play-Store-API)
- [JavaScript code to get reviews](http://android.stackexchange.com/questions/30185/how-to-display-comments-from-devices-that-i-dont-own/30668#30668)

Or use an unofficial API

- https://github.com/splitfeed/android-market-api-php (require a Google account)
- https://42matters.com/api/lookup
- http://playstore-api.herokuapp.com/playstore/apps/com.toj.gasnow

Developper URL

```
https://play.google.com/store/apps/developer?id=%DEV_ID%
```

```
https://play.google.com/store/apps/developer?id=%DEV_ID%&hl=%LANG%
// Where %LANG% language ID like "en-us", "en_us" or "en"
```

App URL

```
https://play.google.com/store/apps/details?id=%APP_ID%
```

```
https://play.google.com/store/apps/details?id=%APP_ID%&hl=%LANG%
// Where %LANG% language ID like "en-us", "en_us" or "en"
```

Other

Open an app

```html
<a href="intent://<anything>/#Intent;scheme=<scheme_name>;package=<must.open.this.p‌​ackage>;end">Force open by package_name app</a>
```

### Windows Phone

App infos

```
http://marketplaceedgeservice.windowsphone.com/v3.2/%LANG%/apps/%APP_ID%/
// Where %LANG% language ID like "en-us"
// Parse it as XML
```

Developper URL

```
https://www.windowsphone.com/%LANG%/store/publishers?publisherId=%DEV_ID%
// Where %LANG% language ID like "en-us"
```

App URL

```
https://www.windowsphone.com/%LANG%/apps/%APP_ID%
// Where %LANG% language ID like "en-us"
```

```
http://windowsphone.com/s?appId=%APP_ID%
```

- `http://catalog.zune.net/v3.2/en-US/apps/APP_ID/?version=latest&clientType=CLIENT_TYPE&store=Zest`, where `APP_ID`, `CLIENT_TYPE` (optional) is `Zune+3.0` (Zune HD applications) or `WinMobile+7.1` (Windows Phone applications)
- [Windows Store app marketing guidelines - UWP app developer | Microsoft Docs](https://docs.microsoft.com/en-us/windows/uwp/publish/app-marketing-guidelines)
- [Publish Windows apps - Windows app development](https://developer.microsoft.com/en-us/store/publish-apps)
- [Coding4Fun ZuneDataViewer - Home](http://zunedata.codeplex.com/wikipage?title=Application%20Information)
- [How to get Windows app store dev center data - Stack Overflow](https://stackoverflow.com/questions/13912624/how-to-get-windows-app-store-dev-center-data/13912746#13912746)

### Amazon

https://developer.amazon.com/appsandservices/resources/marketing-tools/using-badges
https://developer.amazon.com/announcements/tradebrand-guidelines.html

```
http://www.amazon.com/gp/product/%ASIN%/

http://www.amazon.com/gp/product/%ASIN%/ref=mas_pm_%APP_NAME%
```

## Facebook

Fakes likes, it's harmful: [Facebook Fraud - YouTube](https://www.youtube.com/watch?v=oVfHeWTKjag)

How stories are ranked: see [Rank content](Algorithms/Rank content)

```html
<html prefix="og: http://ogp.me/ns# fb: http://ogp.me/ns/fb#">
<!-- … -->
<meta property="og:title" content="…">
<meta property="og:image" content="…">
<meta property="og:site_name" content="…">
<meta property="og:description" content="…">
<meta property="og:url" content="…">
<meta property="og:type" content="…">
<meta property="fb:app_id" content="00000000000">
```

Supported locales: https://www.facebook.com/translations/FacebookLocales.xml

`https://www.facebook.com/photo.php?fbid={photo_id}` and `https://www.facebook.com/{user}/photos/{timeline_id}/{photo_id}/` where `00000000_{photo_id}_0000000000000000000_o.jpg` `photo_id` `00000000000000000` `timeline_id` `a.000000000000.000000.00000000000`

Default profile picture
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c29.0.100.100/p100×100/10354686_10150004552801856_220367501106153455_n.jpg?oh=e8ca515e48d1bc743308966715634bee&oe=58C66077
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c59.0.200.200/p200×200/10354686_10150004552801856_220367501106153455_n.jpg?oh=da4eafdad0da0d0958352977771c3fd7&oe=58BE4325
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c94.0.320.320/p320×320/10354686_10150004552801856_220367501106153455_n.jpg?oh=bc3e9e2ccfd2f54a246e4bfb77b63001&oe=58D3F5DE
https://scontent-cdg2-1.xx.fbcdn.net/t31.0-1/c379.0.1290.1290/10506738_10150004552801856_220367501106153455_o.jpg
https://scontent-cdg2-1.xx.fbcdn.net/t31.0-1/c379.0.1290.1290/10506738_10150004552801856_220367501106153455_o.png

Default page picture (flag)
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c9.0.32.32/p32×32/399548_10149999285987789_1102888142_n.png?oh=c46263750a4e4abc38892ff8b5ba1547&oe=58C587AD
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c19.0.64.64/p64×64/399548_10149999285987789_1102888142_n.png?oh=1ad605f9d9d0e204554e71ce8637135e&oe=58C38AF9
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c81.0.275.275/399548_10149999285987789_1102888142_n.png?oh=3b9a562b00802fed00b571fc7d1342bb&oe=58C907A0

Default xxx picture (student)
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c81.0.275.275/580846_10149999285985791_1565762244_n.png?oh=c46928fcbaf3660bd5834a2a48397fdf&oe=58B5F7C8

Default xxx picture (TV)
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c81.0.275.275/404798_10150000700901954_63461675_n.png?oh=d8d8add1bae05a606338c65cb9a4369e&oe=58CC165C

Default xxx picture (music note)
https://scontent-cdg2-1.xx.fbcdn.net/v/t1.0-1/c81.0.275.275/417197_10149999285992991_711134825_n.png?oh=ac147d4d487b0ead68b4c695d61b6cf1&oe=58D0AEFF

Default app picture (atomic box)
https://scontent-cdg2-1.xx.fbcdn.net/t39.2081-0/p128×128/851578_455087414601994_1601110696_n.png
https://scontent-cdg2-1.xx.fbcdn.net/t39.2081-0/851578_455087414601994_1601110696_n.png

- [Sharing Debugger - Facebook for Developers](https://developers.facebook.com/tools/debug/sharing/)
- [Facebook Crawler - Sharing](https://developers.facebook.com/docs/sharing/webmasters/crawler)
- [Open Graph Stories - Sharing](https://developers.facebook.com/docs/sharing/opengraph)
- [The Open Graph protocol](http://ogp.me/)
- [Webmasters - Sharing](https://developers.facebook.com/docs/sharing/webmasters/#markup)
f
### Setup Facebook Website Application

**Note: the SDK is not available (loaded) in Firefox private mode by the Tracking Protection**

**The following examples will use Facebook Application ID `00000000000`**

Simply `<script src="https://connect.facebook.net/en_US/sdk.js#appId=00000000000&amp;version=v3.2" async></script>` then `window.fbAsyncInit = function(){console.log("FB SDK is ready")}`. Additional parameters can be provided, will auto init. So if you do it manually you will get [`FB.init has already been called - this could indicate a problem`](https://stackoverflow.com/questions/10415884/fb-init-has-already-been-called), see also [javascript - FB init function gives wrong version error - Stack Overflow](https://stackoverflow.com/questions/24019877/fb-init-function-gives-wrong-version-error).
Or use `document.createElement("script"); ... window.fbAsyncInit = function(){FB.init({appId: 00000000000, version: "v2.8"}); FB.getLoginStatus(...)}`

- `https://connect.facebook.net/en_US/sdk/debug.js`
- [Initialization - Web SDKs](https://developers.facebook.com/docs/javascript/reference/FB.init/v3.2)
- [Login Status - Web SDKs](https://developers.facebook.com/docs/reference/javascript/FB.getLoginStatus/)
- HTTPS is required, but `localhost` is allowed (but not `0.0.0.0`) [Requiring HTTPS for Facebook Login - Facebook for Developers](https://developers.facebook.com/blog/post/2018/06/08/enforce-https-facebook-login/) [Login Security - Facebook Login](https://developers.facebook.com/docs/facebook-login/security/#https)

 ```js
FB.login(..., {scope: "..."});
```

- [Reference - Facebook Login](https://developers.facebook.com/docs/facebook-login/permissions/v3.2)

For App ID, check it with `http://graph.facebook.com/00000000000`. For pages (TL;DR: you have to create an App ID):

- https://stackoverflow.com/questions/6997368/facebook-how-to-receive-app-id-for-official-page
- https://stackoverflow.com/questions/10339192/how-to-get-app-id-for-an-existing-facebook-page
- multiple domains is allowed, but must reflect Website URL (else you will get an error "App domains must match the domain of the Secure Canvas URL, Mobile Site URL, Unity Binary URL, Site URL or Secure Page Tab URL. Please correct these domains: foobaz.com"). Ex.: Website/Site URL = http://www.example.com App Domains = example.fr example.es example.de example.co.uk

### Facebook login

```js
function doSomethingWithFBLoginStatus(response, state){
	// The user doesn't allow the app, even after rerequest
	// The user cancel relogin
	// Other reason...
	if(state !== "getstatus" && response.status !== "connected"){
		// Should display something to the user
		console.assert(false, "Something wrong with get FB login status", state);
		return;
	}

	switch(response.status){
		case "connected":
			doSomethingWithFB(response.authResponse.accessToken);
			break;
		case "not_authorized":
			// Request FB user to authorize the FBApp
			// https://developers.facebook.com/docs/reference/javascript/FB.login/v2.12 auth_type
			FB.login(response => doSomethingWithFBLoginStatus(response, "rerequest"), {scope: "permission1,permission2,permission3", auth_type: "rerequest"});
			break;
		case "unknown":
			// Request FB user to (re)login
			FB.login(response => doSomethingWithFBLoginStatus(response, "relogin"));
			break;
		default:
			console.assert(false, "Facebook status invalid", response.status);
	}
}

// https://developers.facebook.com/docs/facebook-login/web#checklogin
FB.getLoginStatus(response => doSomethingWithFBLoginStatus(response, "getstatus"));
```

### Facebook shares and likes count

Without access token:

`http://graph.facebook.com/?id=URL&fields=og_object%7Blikes.summary(total_count).limit(0)%7D,share` returns JSON `json.share.share_count`

With access token:

https://developers.facebook.com/tools/explorer/?method=GET&path=%3Fid%3DURL%26fields%3Dengagement&version=v2.9

- [Getting the Facebook like/share count for a given URL - Stack Overflow](https://stackoverflow.com/questions/9728279/getting-the-facebook-like-share-count-for-a-given-url)

### Facebook share and like

Simple URL. See [Share URLs](#share-urls)

Following methods require an Facebook App ID:

- [Facebook Share button](https://stackoverflow.com/questions/6145489/is-the-facebook-share-button-being-deprecated/) (still works, but depreciated)
- Feed Dialog or Share Dialog URL:

	```
	https://www.facebook.com/dialog/share?
	  app_id=145634995501895
	  &display=popup
	  &quote=An%20example%20quote
	  &href=https%3A%2F%2Fdevelopers.facebook.com%2Fdocs%2F
	```

	Note: share popup with `quote` text and URL of animated gif file as `href` will not displayed exactly the same as shared animated gif URL (as `href`). The playback (play/pause) of the gif is not available (Facebook bug): click open URL. If the gif is not autoplayed (see "Auto-Play Videos" https://www.facebook.com/settings?tab=videos). On mobile the gif is display as standard link.

	```
	https://www.facebook.com/dialog/feed?
	  app_id=145634995501895
	  &display=popup
	  &caption=An%20example%20caption
	  &link=https%3A%2F%2Fdevelopers.facebook.com%2Fdocs%2F
	```
- Feed Dialog or Share Dialog from SDK. SDK need to be included, see [Setup Facebook Website Application](#setup-facebook-website-application).

	```js
	var dialog = FB.ui({
		method: "share",
		href: url,
		quote: message
	});
	// FB.UIServer._triggerDefault(dialog.id);// if need to close the dialog
	```

> Share dialog, which gives people the most flexibility. They can choose where they want to share, including in groups and private messages on Messenger
> If you want to let someone post a plain text status update without a link attachment, you should use the Feed dialog. If you're sharing photos or videos rather than links, you will need to create a custom interface that lets people post to their own timeline, which requires implementing [Facebook Login](https://developers.facebook.com/docs/facebook-login/login-flow-for-web/) and requesting the [`publish_actions` permission](https://developers.facebook.com/docs/facebook-login/permissions/#reference-publish_actions)

- [Share Dialog - Sharing](https://developers.facebook.com/docs/sharing/reference/share-dialog)
- [Feed Dialog - Sharing](https://developers.facebook.com/docs/sharing/reference/feed-dialog/v2.1)

Note: undocumented parameters: `locale=en_US`

Metadata:

- [The Open Graph protocol](http://ogp.me/#structured)
- [opengraph - How does Facebook Sharer select Images? - Stack Overflow](https://stackoverflow.com/questions/1138460/how-does-facebook-sharer-select-images)
- [Facebook Content Sharing Best Practices](https://developers.facebook.com/docs/sharing/best-practices#images)
- [Creating Custom Stories](https://developers.facebook.com/docs/opengraph/creating-custom-stories#objecttypes-properties)
- https://developers.facebook.com/tools/debug/
- [Object Debugger](https://developers.facebook.com/tools/debug/og/object?q=%s)
- [Platform Update: Facebook Removes Pre-Filled Stream Stories, Like Box Configurator Gets Border Color | SocialTimes](http://www.adweek.com/socialtimes/pre-filled-stream-stories-like-box-border-color/263479?red=if)
- [Platform Policy 2.3](https://developers.facebook.com/docs/apps/review/prefill)

 ```html
<iframe src="https://www.facebook.com/plugins/like.php?href=YOUR_URL" scrolling="no" style="border:none; width:450px; height:80px"></iframe>
```

```
https://www.facebook.com/plugins/like.php?
	href			URL
	layout			button_count
	width			75
	show_faces		true
	action			like
	colorscheme		light
	font			arial or lucida%20grande
	height			30
	app_id			120295828008556
	channel			...url
	container_width	0
	locale			en_US
	sdk				joey
	send			true
	share			false
```

- [Like Button - Social Plugins](https://developers.facebook.com/docs/plugins/like-button)
- [Social Plugins](https://developers.facebook.com/docs/plugins)

### Stream

See [Facebook Graph API](#facebook-graph-api)

- (obselete) http://liljosh.com/facebook-page-json-rss-feed/
- (obselete) `https://www.facebook.com/feeds/page.php?id=163276271689&format=json` (`format=rss20`)

### Facebook Graph API

**User ID are app scoped/specific**: [Graph API User](https://developers.facebook.com/docs/graph-api/reference/user/#Reading)

The field `username` is no more available. It's possible to get it by `https://www.facebook.com/app_scoped_user_id/APP_SCOPED_USER_ID/` (get with Graph API `/me?fields=link`) or `https://www.facebook.com/USER_ID/` (logged only) redirect to `https://www.facebook.com/USERNAME`

- Check validity of access token: https://graph.facebook.com/me?access_token=ACCESS_TOKEN (return `{"error": ...}` if it's invalid)
- [Expiration and Extension - Facebook Login](https://developers.facebook.com/docs/facebook-login/access-tokens/expiration-and-extension)
- [Access Token Tool - Facebook for Developers](https://developers.facebook.com/tools/access_tokens)
- [Access Token Debugger - Facebook for Developers](https://developers.facebook.com/tools/debug/accesstoken/)
- [Access Tokens - Facebook Login](https://developers.facebook.com/docs/facebook-login/access-tokens/)
- [Best practice for Facebook login flow with the JavaScript SDK and PHP SDK v4.1 :: Sammy Kaye Powers](https://www.sammyk.me/best-practice-for-facebook-login-with-the-javascript-sdk-and-php-sdk-v4-1)
- [How to create never expires Access Token for Facebook Page](https://medium.com/@Jenananthan/how-to-create-non-expiry-facebook-page-token-6505c642d0b1)
- Extends the validity of the access token (for be used by the server APP): https://graph.facebook.com/oauth/access_token?client_id=YOUR_APP_ID&client_secret=YOUR_APP_SECRET&grant_type=fb_exchange_token&fb_exchange_token=YOUR_ACCESS_TOKEN

Test with Demo application [Graph API Explorer](https://developers.facebook.com/tools/explorer/), "Access Token" > (button) "Get User Access Token" to select required permissions to test.
You can test JS code with https://developers.facebook.com/tools/javascript-console/

Common parameters:

- `summary=true` is available on `{user-id}/likes`, `{user-id}/friends` (where `summary` is always true) to return `{"data":[], summary: {"total_count": 131}}`
- `locale` set locale like `de_DE`
- `access_token` to set use you access token. Get it via an application
	https://graph.facebook.com/oauth/access_token?grant_type=client_credentials&client_id={app-id}&client_secret={app-secret}
	To get a user access token use param `user_id` and `user_secret` instead.
	See https://developers.facebook.com/docs/facebook-login/access-tokens/
	Ex. of invalid access token: `AAACZBLSe4fcoBAFcGMJZAUS9OthIr5o6ZCUySgXYj0nfWX7u08×7h0VZAFFuJJs9LmeWgud2u5ZCEZCeUHZCVIq1Y2j4gjKAjJ0gx5OY9PBihlABJn64njm`
- `limit=xx` is not fixed. Never rely to it for a fixed limit between pages. Ex: `limit=500`, but return `487` items for page 1 and `492` items for page 2.

	- [Maximum limit fetching facebook pages with Graph API - Stack Overflow](https://stackoverflow.com/questions/29730526/maximum-limit-fetching-facebook-pages-with-graph-api)
	- [The limit of Facebook's graph api "limit" parameter - Stack Overflow](https://stackoverflow.com/questions/14876105/the-limit-of-facebooks-graph-api-limit-parameter)
- `fields` to filder fields. Ex.: `me/albums?fields=count,name`: will get only `id`, photo `count` and `name` per album
- `order=reverse_chronological` works only for comments

- `/me/picture?type=large` but also `?width=1000` or `?height=1000` (preserve aspect ratio). If both width and height are defined, image will be cropped
- `{page-id}/feed?fields=id,shares,likes.limit(0).summary(true),comments.limit(0).summary(true)`
- `{post-id}?fields=id,shares,likes.limit(0).summary(true),comments.limit(0).summary(true)`

Error codes: [Using the Graph API](https://developers.facebook.com/docs/graph-api/using-graph-api/#errors)

```json
{
	"error": {
		"message": "Error validating access token: The user is enrolled in a blocking, logged-in checkpoint",
		"type": "OAuthException",
		"code": 190,
		"error_subcode": 490,
		"error_data": "{\"checkpoint_flow_id\":\"207799259245384\",\"checkpoint_content_id\":\"0\",\"show_native_checkpoints\":\"\"}",
		"fbtrace_id": "Dmruy525PeA"
	}
}
```

```json
{
	"error": {
		"message": "Invalid OAuth access token.",
		"type": "OAuthException",
		"code": 190,
		"fbtrace_id": "F32VcO27MO3"
	}
}
```

Get infos about a page:

- likes/fan count https://stackoverflow.com/questions/29702192/request-to-get-total-count-of-facebook-page-likes-in-v2-3-api
- likes `/{object-id}/likes?summary=true` `response.summary.total_count`
- feed https://stackoverflow.com/questions/28204978/facebook-rss-feeds-have-stopped-working/28291957#28291957

To get page categories (paged):

```
/search?type=placetopic&topic_filter=all&limit=5000&locale=fr_FR
```

- https://gist.github.com/bloudermilk/2173940
- [Facebook Pages — Authoritative List of Categories - Stack Overflow](https://stackoverflow.com/questions/4216648/facebook-pages-authoritative-list-of-categories/)

Get count of posts, friends, likes and uploaded medias. Use jQuery Deferred (es2016 `Promise` like):

```html
<!DOCTYPE html PUBLIC>
<html>
	<head>
		<title>Facebook stats</title>
		<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
		<script src="//connect.facebook.net/fr_FR/sdk.js#appId=1509340019322396&version=v2.8&status=1" async></script>
	</head>
	<body>

		<button id="fb_start">Get my Facebook stats</button>
		<pre id="output"></pre>

		<script>
		var fbSDKInit = $.Deferred();
		// Facebook SDK init listener
		window.fbAsyncInit = () => fbSDKInit.resolve("FBSDKInit");

		function mergeObjects(obj1, obj2){
			// Both are arrays
			if(Array.isArray(obj1) && Array.isArray(obj2)){
				return obj1.concat(obj2);
			}

			return Object.assign({}, obj1, obj2);
		}

		// Doesn't support Multiple Requests https://developers.facebook.com/docs/graph-api/using-graph-api#multirequests nor batch requests https://developers.facebook.com/docs/graph-api/making-multiple-requests
		function getFBGraphAllData(graphURL){
			return getFBGraphResponse(graphURL).pipe(response => {
				// Paging https://developers.facebook.com/docs/graph-api/using-graph-api#paging
				// paging.next is available if next page exist (but could be empty)
				if(response.paging && response.paging.next){
					return getFBGraphAllData(response.paging.next).pipe(data => mergeObjects(response.data, data));
				}

				return response.data || response;// some edges return the field data as object  (`{}`, ex. `/user/picture/`) and no `paging` field
			});
		}

		// Get Facebook Graph API data as promise
		function getFBGraphResponse(relativeURL){
			var d = $.Deferred();
			FB.api(relativeURL, (response) => d[response && !response.error ? "resolve" : "reject"](response));
			return d.promise();
		}

		function loginFB(permissions, rerequest = false){
			var options = {
				scope: permissions.join(","),
				return_scopes: true
			};
			if(rerequest){
				options.auth_type = "rerequest";
			}

			var d = $.Deferred();
			// reject: The user user cancelled login or did not fully authorize.
			FB.login((response) => d[response.authResponse ? "resolve" : "reject"](response), options);

			return d.promise();
		}

		function checkFBStatus(){
			var d = $.Deferred();
			FB.getLoginStatus(response => d.resolve(response));
			return d.promise();
		}

		// Check if all values in array are in sourceArray
		function arrayMatchAll(array, sourceArray){
			return array.every(value => sourceArray.indexOf(value) >= 0)
		}

		// Log the user if not and check permissions
		// permissions called also scope/scopes
		// https://developers.facebook.com/docs/facebook-login/permissions
		function loginAndGrantPermissionsFB(requiredPermissions){
			return checkFBStatus().pipe(function(response){
				return checkFBStatus().pipe(function(response){
					var status = response.status;
					var promise;
					if(status === "connected"){
						promise = getFBGraphAllData("/me/permissions")
							.pipe(data => data.filter(permission => permission.status == "granted").map(permission => permission.permission))
							.pipe(grantedPermissions => {
								if(arrayMatchAll(requiredPermissions, grantedPermissions)){
									return grantedPermissions;
								}

								// Special case: add an oportunity to the user to grant permissions again
								return loginFB(requiredPermissions, true)
									.pipe(response => response.authResponse.grantedScopes.split(","));
							});
					}else{
						promise = loginFB(requiredPermissions, status === "not_authorized")
							.pipe(response => response.authResponse.grantedScopes.split(","));
					}

					return promise.pipe(grantedPermissions => {
						// If all requested permissions are granted
						if(arrayMatchAll(requiredPermissions, grantedPermissions)){
							return $.Deferred().resolve(grantedPermissions);
						}

						return $.Deferred().reject({error: {message: "All required permissions are not granted."}});
					});
				});
			});
		}

		function addCount(target, field, count){
			target[field] += count;
			return target;
		}
		function getLength(items){
			return items.length;
		}
		function getSummaryCount(result){
			return result.summary.total_count;
		}

		function getFBData(){
			var result = {
				name: null,
				picture: null,
				posts: 0,
				friends: 0,
				likes: 0,
				medias: 0
			};

			var addLikesCount = addCount.bind(null, result, "likes");
			var addMediaCount = addCount.bind(null, result, "medias");
			var lastYear = Math.floor(Date.now() / 1000 - 365*24*60*60);//timestamp in seconds

			return fbSDKInit

				.pipe(loginAndGrantPermissionsFB.bind(null, [
					// https://developers.facebook.com/docs/facebook-login/permissions
					// This permissions are approved by default
					"email", "public_profile", "user_friends",
					// Additional permissions
					"user_posts", "user_likes", "user_photos", "user_videos"
				]))
				.pipe(function(){
					return $.when(
						// Indentity
						getFBGraphResponse("/me?fields=name,picture.type(large)").pipe(response => {
							result.name = response.name;
							result.picture = response.picture.data.is_silhouette ? null : response.picture.data.url;
							return result;
						}),

						// Posts
						//getFBGraphAllData("/me/posts?fields=id&limit=500").pipe(getLength).pipe(addCount.bind(null, result, "posts")),
						getFBGraphAllData(`/me/posts?since=${lastYear}&fields=id&limit=500`).pipe(getLength).pipe(addCount.bind(null, result, "posts")),// posts over one year

						// Friends
						getFBGraphResponse("/me/friends?limit=0").pipe(getSummaryCount).pipe(addCount.bind(null, result, "friends")),

						// Likes
						getFBGraphResponse("/me/likes?limit=0&summary=true").pipe(getSummaryCount).pipe(addLikesCount),
						getFBGraphAllData("/me/games?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
						getFBGraphAllData("/me/books?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
						getFBGraphAllData("/me/movies?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
						getFBGraphAllData("/me/music?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
						getFBGraphAllData("/me/television?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),
						getFBGraphAllData("/me/og.likes?fields=id&limit=500", true).pipe(getLength).pipe(addLikesCount),

						// Medias
						getFBGraphAllData("/me/albums?fields=count&limit=100", true).pipe(function(data){
							return data.reduce((total, album) => total + album.count, 0);
						}).pipe(addMediaCount),
						getFBGraphAllData("/me/videos?type=uploaded&fields=id", true).pipe(getLength).pipe(addMediaCount)
					);
				}).pipe(() => result);
		}

		document.getElementById("fb_start").addEventListener("click", function(){
			var start = Date.now();
			document.getElementById("output").textContent = "Getting Facebook stats...";
			getFBData().always(data => document.getElementById("output").textContent = `Facebook stats (duration: ${Date.now() - start}ms):\n\n${JSON.stringify(data, null, '\t')}`);
			// response.error.type == "OAuthException");// response.error.code https://developers.facebook.com/docs/graph-api/using-graph-api#errors
		});
		</script>
	</body>
</html>
```

About getting the registration date:

No API provide this information. Previously, before app-scoped user-ids, an [estimation date could be done based on user ID](http://metadatascience.com/2013/03/11/inferring-facebook-account-creation-date-from-facebook-user-id/)
Then you find the first posts, photos or profile picture: [Facebook API: Get all profile pictures - Stack Overflow](https://stackoverflow.com/questions/5058144/facebook-api-get-all-profile-pictures)
From 10 year ago, `length=1` over 6 month with `until` and `since` (Unix timestamps) then try 5 year after
Note: It's possible to back dating content with `backdated_time`: https://developers.facebook.com/docs/graph-api/common-scenarios#backdating

#### Get age from Facebook user's birthdate

```js
// facebook-user-age.js
/**
 * Get Facebook user age from given birthdate
 * Can be MM/DD/YYYY or MM/DD or YYYY
 * @param {String} birthdate
 * @returns {Number}
 * @see https://developers.facebook.com/docs/graph-api/reference/user/
 */
module.exports = birthdate => {
	const currentYear = new Date().getFullYear();
	// Convert to UTC ISO-8601 date

	// MM/DD/YYYY
	if(birthdate.length === 10){
		const [month, day, year] = birthdate.split("/");
		return currentYear - new Date(`${year}-${month}-${day}`).getFullYear() - 1;
	}

	// YYYY
	if(birthdate.length === 4){
		const year = birthdate;
		return currentYear - parseInt(year, 10) - 1;
	}

	// MM/DD

	return NaN;
};
```

### Share an external Animation

Post an url to create a card/push with the animation + a link

GIF: Only posted URL, not file uploaded (in Facebook album)

#### Video

**To get a custom HTML5 player (embeded in Facebook feed), you must be whitlisted.** Don't know how.

(need verification) Note: `og:video` can be defined multiple times (for types `text/html`, `application/x-shockwave-flash`, `video/mp4`, etc.). Even if it's not a video
Note: `og:video`, `og:video:type`, `og:video:width` and `og:video:width` should be explicited provided for each format
Note: `og:video:secure_url` is not required, but **`og:video`/`og:video:url` must use HTTPS**
Note: `fb:app_id` is not required
Note: `text/html` type it's seem to be **reserved to whitlisted domains**. No information is available about the process of whitlisting. Custom flash player is still possible (`application/x-shockwave-flash`) or use only `video/mp4`
Note: if the `og:video` as `text/html` is not valid, Facebook fallback to the first `og:video` url will be used as `src` for a `<video>` (directly in feed) and `og:video:type` as `type`
Note: a div with `me-cannotplay` class with a link "Download File" as child
Note: based on `og:image` file dimensions if width <= ~400 the image is squared and take 1/3 of the post width. Where the title and description take 2/3. If width > ~400 the image will take all the width and only the title and origin are visible (no description)
Note: does the size provided (`og:video:width` and `og:video:height`) have any impact?

```html
<meta property="og:type" content="video">
<meta property="og:image" content="poster.jpg">

<!-- direct asset ref: -->
<meta property="og:video" content="http://example.com/video.mp4">
<meta property="og:video:type" content="video/mp4">
<meta property="og:video:width" content="500">
<meta property="og:video:height" content="400">

<!-- Facebook iframe embed  -->
<meta property="og:video:url" content="http://example.com/video.html">
<meta property="og:video:type" content="text/html">
<meta property="og:video:width" content="500">
<meta property="og:video:height" content="400">

<!--  legacy swf embed:  -->
<meta property="og:video:url" content="http://example.com/animation.swf">
<meta property="og:video:type" content="application/x-shockwave-flash">
<meta property="og:video:height" content="500">
<meta property="og:video:width" content="400">
```

2016/12/09: only MP4 and SWF served via HTTPS works. In user feed (desktop), MP4 will be played in native HTML5 player and SWF will be placed in object inside an isolated iframe. On mobile (native app) it's a simple link (not interaction)

It's related with `https://www.facebook.com/ajax/flash/expand_inline.php?...` `response.dompos[0][3].__html`

> When you call the debugger to scrap changes on your og:tags of your page, all previous Facebook shares of that URL will still show the old image/video. There is no way to update all previous posts and it's this way by design for security reasons. Otherwise, someone would be able to pretend that a user shared something that he/she actually didn't.
— [opengraph - Facebook Open Graph not clearing cache - Stack Overflow](https://stackoverflow.com/questions/5776567/facebook-open-graph-not-clearing-cache)

- https://developers.facebook.com/docs/sharing/webmasters#video
- https://developers.facebook.com/docs/reference/opengraph/object-type/video.other
- https://stackoverflow.com/questions/30934400/embed-video-iframe-in-facebook-wall
- https://stackoverflow.com/questions/8708233/share-html5-player-on-facebook-wall
- https://blog.kaltura.com/facebook-now-require-html5-and-fallback-in-open-graph/
- http://player.kaltura.com/modules/KalturaSupport/components/share/Share.html
- [Facebook video share - Stack Overflow](https://stackoverflow.com/questions/27525006/facebook-video-share/28987920#28987920)
- [Setting Videos not Hosted on Brightcove to Play within Facebook | Brightcove Support](https://support.brightcove.com/en/video-cloud/docs/setting-videos-not-hosted-brightcove-play-within-facebook)
- [html5 - How to embed a iframe player in FB's wall? - Stack Overflow](https://stackoverflow.com/questions/33215828/how-to-embed-a-iframe-player-in-fbs-wall/33226663#33226663)
- [How to embed my own flash video player in Facebook? - Stack Overflow](https://stackoverflow.com/questions/26367646/how-to-embed-my-own-flash-video-player-in-facebook/26399297#26399297)
- [Embedding video player html5 iframe in facebook share like YouTube - Stack Overflow](https://stackoverflow.com/questions/28815838/embedding-video-player-html5-iframe-in-facebook-share-like-youtube#comment45907003_28815838)

Note: HTTPS is required to be played (and the field `og:video:secure_url`? else it's recognized as video, but not displayed as video player)

#### GIF

Working GIFs:

- 600 × 400 for 319kB
- 499 × 499 for 931kB

Interlaced could not work well

The GIF is not working properly if you add `quote` using dialog share.

Note: GIF will be cached and converted as MP4

- [How to Post an Animated Image (Like .gif) On my Wall? | Facebook Help Community](https://www.facebook.com/help/community/question/?id=383880968404336)

Works ? Else detect the crawler and output the gif instead:

```php
header('Content-Length: ' . filesize($gif));
header('Content-Type: ' . mime_content_type($gif));
readfile($gif);
exit();
```

```html
<meta property="og:site_name"   content="Site Name">
<meta property="og:url"         content="url to GIF on web">
<meta property="og:title"       content="Title of GIF page">
<meta property="og:description" content="Some description">
<meta property="og:type"        content="video.other">
<meta property="og:image"       content="Same as og:url above">
<meta property="og:image:width"  content="800">
<meta property="og:image:height" content="400">
```

- [opengraph - How does Giphy share gifs to facebook? (2015, NOT FLASH ANYMORE) - Stack Overflow](https://stackoverflow.com/questions/31216481/how-does-giphy-share-gifs-to-facebook-2015-not-flash-anymore/35999163#35999163)

For `http://giphy.com/gifs/hot-funny-cartoon-fBEDuhnVCiP16`:

```html
<meta property="og:url" content="https://media.giphy.com/media/fBEDuhnVCiP16/giphy.gif">
<meta property="og:title" content="The Simpsons GIF - Find &amp; Share on GIPHY">
<meta property="og:description" content="Discover &amp; Share this The Simpsons GIF with everyone you know. GIPHY is how you search, share, discover, and create GIFs.">
<meta property="og:type" content="video.other">
<meta property="og:image" content="https://media.giphy.com/media/fBEDuhnVCiP16/giphy.gif">
<meta property="og:image:width" content="500">
<meta property="og:image:height" content="376">
<meta property="og:type" content="video">
<meta property="og:image" content="https://media.giphy.com/media/fBEDuhnVCiP16/giphy-facebook_s.jpg">
<meta property="og:image:width" content="480">
<meta property="og:image:height" content="270">
<meta property="og:type" content="video">
<meta property="og:image" content="https://media.giphy.com/media/fBEDuhnVCiP16/giphy-facebook_s.jpg">
<meta property="og:image:width" content="480">
<meta property="og:image:height" content="270">
<meta property="og:video" content="https://giphygifs.s3.amazonaws.com/swiphy20141103.swf?api_hostname=&gif_url=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2FfBEDuhnVCiP16%2Fgiphy.gif&giphy_height=376&video_url=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2FfBEDuhnVCiP16%2Fgiphy.mp4&giphyWidth=500&path=%2Fgifs%2Fhot-funny-cartoon-fBEDuhnVCiP16&destination_url=http%3A%2F%2Fgiphy.com%2Fgifs%2Fhot-funny-cartoon-fBEDuhnVCiP16&giphyHeight=376&gif_id=fBEDuhnVCiP16&mode=embed&giphy_width=500">
<meta property="og:video:secure_url" content="https://giphygifs.s3.amazonaws.com/swiphy20141103.swf?api_hostname=&gif_url=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2FfBEDuhnVCiP16%2Fgiphy.gif&giphy_height=376&video_url=https%3A%2F%2Fmedia.giphy.com%2Fmedia%2FfBEDuhnVCiP16%2Fgiphy.mp4&giphyWidth=500&path=%2Fgifs%2Fhot-funny-cartoon-fBEDuhnVCiP16&destination_url=http%3A%2F%2Fgiphy.com%2Fgifs%2Fhot-funny-cartoon-fBEDuhnVCiP16&giphyHeight=376&gif_id=fBEDuhnVCiP16&mode=embed&giphy_width=500">
<meta property="og:video:type" content="application/x-shockwave-flash">
<meta property="og:video:width" content="470">
<meta property="og:video:height" content="353">
```

### Detect Facebook crawler

```php
if (
	strpos($_SERVER["HTTP_USER_AGENT"], 'facebookexternalhit/') !== false ||
	strpos($_SERVER["HTTP_USER_AGENT"], 'Facebot') !== false
) {
	// it is probably Facebook's bot
}
else {
	// probably not
}
```

- [Facebook Crawler - Sharing](https://developers.facebook.com/docs/sharing/webmasters/crawler)

## Twitter

- [Obfusc-a-tweet reloaded](http://xem.github.io/articles/#obfuscatweet_url_en)
- [API changelog](https://www.hitchhq.com/twitter/activities)
- [Big GIFs welcome: Twitter increases maximum GIF size to 15MB on web | Ars Technica](http://arstechnica.com/business/2016/07/big-gifs-welcome-twitter-increases-maximum-gif-size-to-15mb-on-web/)
- [Oisín Moran | How I Made a Self-Quoting Tweet](https://web.archive.org/web/20211010081904/https://oisinmoran.com/quinetweet)

### Fetch tweets

- [Twitter timeline in true chronological order include retweets](https://twitter.com/search?f=tweets&vertical=default&q=filter%3Afollows%20-filter%3Areplies%20include%3Anativeretweets) (click "Latest" on mobile)
- [Twitter timeline in true chronological order without retweets, liked tweets](https://twitter.com/search?f=tweets&q=filter%3Afollows%20-filter%3Areplies&src=typd)
- Exemple of complex search: https://twitter.com/search?f=tweets&vertical=default&q=to%3Awaxpancake%20-from%3Awaxpancake%20%28irony%20OR%20ironic%20OR%20%22else%27s%20retweet%22%20OR%20%22have%20found%22%20OR%20%22someone%20i%20follow%22%29%20since%3A2018-06-06%20-from%3Aadambanksdotcom&src=typd

URL: `https://twitter.com/i/profiles/show/{user}/timeline/tweets?include_available_features=1&include_entities=1&include_new_items_bar=true`

Optional: `max_position={last_tweet_id}`

Headers:

```http
Accept: application/json, text/javascript, */*; q=0.01
Referer: https://twitter.com/{user}
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/603.3.8 (KHTML, like Gecko) Version/10.1.2 Safari/603.3.8
X-Twitter-Active-User: yes
X-Requested-With: XMLHttpRequest
```

Response:

```
{"items_html": "..."}
```

- [bisguzar/twitter-scraper: Scrape the Twitter Frontend API without authentication.](https://github.com/bisguzar/twitter-scraper)

### Card

Note: Twitter use meta `twitter:image` and remove mention to `twitter:image:src`, but only the lastest works (or have the precedence). See https://twittercommunity.com/t/twitter-image-src-or-twitter-image/16085/7
Note: Use `twitter:image:alt` to provide alternative text content. Equivalent of `alt` attribute of an `img` element. See [Twitter Has Alt Text! (with some caveats) | Adrian Roselli](http://adrianroselli.com/2016/03/twitter-has-alt-text-with-some-caveats.html)
Note: For Summary card with large image, the aspect ratio is 2:1. See [Advertiser creative specifications](https://business.twitter.com/en/help/campaign-setup/advertiser-card-specifications.html)

**Note: [player card](https://dev.twitter.com/cards/types/player) require HTTPS and must be approved.** It's composed as an iframe playing a stream (video/audio). `twitter:player:stream` support only MP4 (H.264 and/or AAC)

- [Card Validator | Twitter Developers](https://cards-dev.twitter.com/validator)
- [Advertiser creative specifications](https://business.twitter.com/en/help/campaign-setup/advertiser-card-specifications.html)

### Profile image

Default profile picture: `https://abs.twimg.com/sticky/default_profile_images/default_profile_1_400×400.png` where `1` can be changed

### Download media

Aka image

- `https://pbs.twimg.com/media/MEDIA_ID?format=png&name=large`, `https://pbs.twimg.com/media/MEDIA_ID.png:large` (`.jpg`, without `:large`)

**Image at maximum resolution**, right-click -> View in new tab -> add `:orig` after the `.jpg` in the URL

Media video:

1. load:
	`https://api.twitter.com/2/timeline/conversation/{tweet_id}.json?include_profile_interstitial_type=1&include_blocking=1&include_blocked_by=1&include_followed_by=1&include_want_retweets=1&include_mute_edge=1&include_can_dm=1&include_can_media_tag=1&skip_status=1&cards_platform=Web-12&include_cards=1&include_ext_alt_text=true&include_reply_count=1&tweet_mode=extended&include_entities=true&include_user_entities=true&include_ext_media_color=true&send_error_codes=true&count=20&ext=mediaStats%2ChighlightedLabel`
	Require header `authorization: Bearer ....`
2. read the JSON, as `root[0].globalObjects.tweets[${TWEET_ID}].extended_entities.media[0].video_info.variants`

Or

1. load `https://api.twitter.com/1.1/videos/tweet/config/{tweet_id}.json`
	Require header `authorization: Bearer ....`
2. read the JSON as `root.track.playbackUrl`

Or use jDownloader with `https://twitter.com/{user}/status/{tweet_id}/video/1`

- [How I downloaded a video from Twitter using Curl | Zero One Labs](http://zeroonelabs.com/how-i-downloaded-a-video-from-twitter-using-curl/)
- [SAVEVIDEO.ME: Download Dailymotion Videos, Vimeo, Facebook, Twitter and more!](http://savevideo.me/)

### Direct message

https://twitter.com/messages/compose?
	recipient_id	user ID. Ex: 3309375033 for @AppleSupport

You can send to yourself a direct message.
Share this link on Twitter create a special twitter card with "Send a private message" link

### Share an animation

GIF or Video

Note: you need to request approval to allow your domain to be allowed to use twitter card player. See [twitter card validator](https://dev.twitter.com/cards/types/player)

```html
<!-- page URL: http://gifboom.com/x/771600be -->
<meta name="twitter:card"       content="player">
<meta name="twitter:player"     content="https://gifboom.com/p/771600be">
<meta name="twitter:player:width" content="480">
<meta name="twitter:player:height" content="270">
<meta name="twitter:player:stream" content="https://medias.gifboom.com/medias/0928a540746501330b2e723c91561e03.mp4">
<meta name="twitter:player:stream:content_type" content="video/mp4; codecs=&quot;avc1.42E01E, mp4a.40.2&quot;">

<meta name="twitter:account_id" content="1020383864" />
<meta name="twitter:card" content="player">
<meta name="twitter:title" content="The Simpsons GIF - Find &amp; Share on GIPHY">
<meta name="twitter:creator" content="@giphy">
<meta name="twitter:site" content="@giphy">
<meta name="twitter:description" content="Discover &amp; Share this The Simpsons GIF with everyone you know. GIPHY is how you search, share, discover, and create GIFs.">
<meta name="twitter:image:src" content="https://media3.giphy.com/media/fBEDuhnVCiP16/giphy-facebook_s.jpg?t=1">
<meta name="twitter:image" content="https://media3.giphy.com/media/fBEDuhnVCiP16/giphy-facebook_s.jpg?t=1">
<meta name="twitter:domain" content="giphy.com">
<meta name="twitter:player" content="https://giphy.com/embed/fBEDuhnVCiP16/twitter/iframe">
<meta name="twitter:player:width" content="435">
<meta name="twitter:player:height" content="327">
```

- https://github.com/twitterdev/cards-player-samples
- [Player Card validator — Twitter Developers](https://dev.twitter.com/cards/types/player)
- https://twittercommunity.com/t/animated-gifs-are-currently-supported-in-twitter-cards-via-the-player-card-but-how/16825/6

### Twitter shares

- http://opensharecount.com/count.json?source=bubble&url=URL
- http://public.newsharecounts.com/count.json?url=URL (detect new shares within 60 seconds)
- https://api.twitter.com/1.1/search/tweets.json?q=URL (with valid access token)
- https://counts.twitcount.com/button/?url=URL (html for share button + count)
- [OpenShareCount](http://opensharecount.com/)

### Twitter share and like

- [Share URLs](#share-urls)
- Twitter buttons [Twitter Publish](https://publish.twitter.com/)

### Stream

With `dnt=false` `lang=fr`, this return JSON:

```
https://syndication.twitter.com/timeline/likes?screen_name={username}&suppress_response_codes=true{&lang}{&dnt}
https://syndication.twitter.com/timeline/profile?screen_name={username}&suppress_response_codes=true{&lang}{&dnt}
https://syndication.twitter.com/timeline/list?list_slug={userlist_id}&screen_name={username}&suppress_response_codes=true{&lang}
https://twitter.com/settings/widgets/new/search?query={term}
https://cdn.syndication.twimg.com/widgets/timelines/{widget_id}?&suppress_response_codes=true{&lang}
https://twitter.com/i/profiles/popup?screen_name={username}&wants_hovercard=true{&lang}
https://twitter.com/i/profiles/popup?user_id={user_id}&wants_hovercard=true{&lang}
```

- [Reference Documentation — Twitter Developers](https://dev.twitter.com/rest/reference)
- (JS) https://github.com/jasonmayes/Twitter-Post-Fetcher
- (PHP) https://packagist.org/packages/j7mbo/twitter-api-php
- (JS) https://github.com/jublonet/codebird-js
- https://dev.twitter.com/resources/twitter-libraries
- https://mikerogers.io/2013/02/25/how-use-twitter-oauth-1-1-javascriptjquery.html
- https://umerpasha.wordpress.com/2013/06/13/c-code-to-get-latest-tweets-using-twitter-api-1-1/

```php
$username = isset($_GET['screen_name']) ? $_GET['screen_name'] : 'twitter';// 'privateaccount'
$page_content = @file_get_contents('https://twitter.com/' . urlencode($username) . '?lang=en');

if(preg_match('/<input type="hidden" id="init-data" class="json-data" value="([^"]+)/', $page_content, $matches)){
	$data = json_decode(html_entity_decode($matches[1]), true);
	$profile_data = json_encode($data['profile_user']);
	header('Content-Type: application/json');
	echo $profile_data;
}
```

```php
define('TWITTER_PROFILE_VALUES', 6);
$username = isset($_GET['screen_name']) ? $_GET['screen_name'] : 'twitter';
$page_content = file_get_contents('https://twitter.com/' . urlencode($username) . '?lang=en');
$profileKeys = array('tweets', 'following', 'followers', 'likes', 'lists', 'moments');
$profileValues = array();
$matchOffset = 80000;//skip first 80kB
while(preg_match('/<span class="ProfileNav-value"[^>]*>([^<]+)/', $page_content, $matches, PREG_OFFSET_CAPTURE, $matchOffset) && count($profileValues) < TWITTER_PROFILE_VALUES){
	$fullPatternMatch = $matches[0];
	$matchOffset = $fullPatternMatch[1] + strlen($fullPatternMatch[0]);
	$firstCapGroupMatch = $matches[1];
	$value = $firstCapGroupMatch[0];
	$value = str_replace(',', '', $value);
	$lastChar = strtoupper($value[strlen($value) - 1]);// abbreviation
	$value = floatval($value);
	switch($lastChar) {
		case 'T':// Trillion, Tera-
			$value *= 1000;
		case 'B':// Billion
		case 'G':// Giga-
			$value *= 1000;
		case 'M':// Million, Mega-
			$value *= 1000;
		case 'K':// Kilo-
			$value *= 1000;
	}
	array_push($profileValues, $value);
}

$data = array(
	'screenName' => '',
	'fullName' => ''
);
$data += array_combine($profileKeys, $profileValues);
echo '<pre>';
echo json_encode($data);
echo '</pre>';
```

### GIF

Twitter has a limit of max 15 MB

### Detect Twitter crawler

```php
if (
	strpos($_SERVER["HTTP_USER_AGENT"], 'Twitterbot/') !== false
) {
	// it is probably Twitter's bot
}
else {
	// probably not
}
```

- [Getting Started Guide | Twitter Developers](https://dev.twitter.com/cards/getting-started#crawling)

## Instagram

To add line breaks in post caption on iOS, copy the caption and past in Note app to add lines break or use a [text replacement](https://support.apple.com/en-us/HT207525)

To add a text replacement for add a line break you need macOS synchronized with the same iCloud account than the iOS device (on iOS you can't add text replacement with only spaces / line breaks). Copy a line return, then go at System Preferences > Keyboard > Text, add a shortcut.

**Note: You need to remove all space before the last line of previous paragraph (automatically added after each hashtags, user names or text replacements)**

## Pinterest

### Pinterest share count

`http://api.pinterest.com/v1/urls/count.json?url=$1`, returns `receiveCount({"url":"$1","count":0})` (optional: parameter `callback` eg. `console.log`)

### Pinterest share

- [Share URLs](#share-urls)
- http://business.pinterest.com/widget-builder/
- [Pinterest Developers](https://developers.pinterest.com/docs/widgets/pin-it/)

### Detect Pinterest crawler

```php
if (
	strpos($_SERVER["HTTP_USER_AGENT"], 'Pinterest/') !== false
) {
	// it is probably Twitter's bot
}
else {
	// probably not
}
```

## LinkedIn

### Linkedin share count

`http://www.linkedin.com/countserv/count/share?url=$1&format=json` returns `{"count":1304,"fCnt":"1,304","fCntPlusOne":"1,305","url":"$1"}`

### LinkedIn share

Parameter `mini` is required and must be `true`

- [Share on LinkedIn | LinkedIn Developer Network](https://developer.linkedin.com/docs/share-on-linkedin)

## Reddit

### Reddit share

- [reddit.com: boutons reddit](https://www.reddit.com/buttons/)

## Google Calendar

https://calendar.google.com/calendar/event?action=TEMPLATE&text=Title+part&details=Details+part&dates=20180524T190000/20180524T200000&location=Somewhere

- [Google Calendar render action Template parameter documentation - Stack Overflow](https://stackoverflow.com/questions/22757908/google-calendar-render-action-template-parameter-documentation)

## Google+

- [Share URLs](#share-urls)
- [Share  |  Google+ Platform for Web  |  Google Developers](https://developers.google.com/+/web/share/#sharelink)

### Google+ share and like

- https://developers.google.com/+/web/+1button/

### GIF

OK: 800 × 480 px (3.14 MB)

## Github

Get Markdown of Wiki:

For home page `https://github.com/msndevs/protocol-docs/wiki` go to `https://github.com/msndevs/protocol-docs/wiki/Home.md` (redirect to `https://raw.githubusercontent.com/wiki/msndevs/protocol-docs/Home.md`)
For other page `https://github.com/msndevs/protocol-docs/wiki/Authentication` go to `https://github.com/msndevs/protocol-docs/wiki/Authentication.md` (redirect to `https://raw.githubusercontent.com/wiki/msndevs/protocol-docs/Authentication.md`)

Found commit that delete file: `https://github.com/{username}/{repository}/commits/{branch}/{filepath}`. Branch could be `main` (or `master`)

- `https://api.github.com/repos/{username}/{repository}/commits/{branch}`
- `https://gist.github.com/{gist_id}{/revision_id}{/filename}` (`revision_id` and `filename` are optional)
- `https://gist.githubusercontent.com/{gist_id}/raw{/revision_id}{/filename}` (`revision_id` and `filename` are optional)
- `https://raw.github.com/{username}/{repository}/{reference}/{filepath}` and `https://raw.githubusercontent.com/{username}/{repository}/{reference}/{filepath}`
- `https://github.com/{username}/{repository}{/format}/{reference}/{filepath}` `format` could be `blob` or `raw` (shouldn't be `releases`)

- [if you have the dmca repo on your computer, you can checkout this PR via git fet... | Hacker News](https://news.ycombinator.com/item?id=24883933)

### Gist

- `https://gist.github.com/{user}/{id}`
- `https://gist.github.com/{user}/{id}.js` - Script to insert embedded gist
- `https://api.github.com/gists/{id}`
- `https://api.github.com/gists/{id}/{version}`

- [Customizing GitHub Gists / Coder's Block](http://codersblock.com/blog/customizing-github-gists/)

## Stackexchange

Aka Stackoverflow, etc.

Short URLs:

```
https://{subdomain}.stackexchange.com/q/{question_id}
https://{subdomain}.stackexchange.com/q/{anwser_id}
```

## Voyage SNCF

- [generates urls to voyages-sncf.com to book trains with prefilled form items](https://gist.github.com/mmuman/5ed425a130e65224b184)
- https://oui.sncf

## Gitweb

Download snapshot: `http://{gitweburl}/gitweb.cgi?p={repo};a=snapshot;h=HEAD` Use `h=HEAD` or `h=` (path hash, from `ls-tree`)
Or use "snapshot" link

Example:
`https://gitorious.org/microsoft-qt-interop/microsoft-qt-interop?p=microsoft-qt-interop:microsoft-qt-interop.git;a=summary`

- [git - gitweb snapshot of sub-directory - Stack Overflow](https://stackoverflow.com/questions/14444593/gitweb-snapshot-of-sub-directory)
- https://github.com/git/git/blob/master/gitweb/gitweb.perl

## Jira

- [How to create issues using direct HTML links in Jira Server | Jira | Atlassian Documentation](https://confluence.atlassian.com/jirakb/how-to-create-issues-using-direct-html-links-in-jira-server-159474.html)

## Scribd

```
?start_page=n
#page=n
#full
```

## Wikimedia

Aka Wikipedia

- `http://en.wikipedia.org/w/api.php?action=query&prop=revisions&rvprop=content&titles=%s&format=json&callback=%s`
- https://www.wikidata.org/wiki/Special:ApiSandbox#action=query&format=json
- [Wikidata Query Service](https://query.wikidata.org/)

Contribute:

- [Gerrit patch uploader - MediaWiki](https://www.mediawiki.org/wiki/Gerrit_patch_uploader) - Simple way to create a patch
- [Developer account - MediaWiki](https://www.mediawiki.org/wiki/Developer_account)
- [New Developers - MediaWiki](https://www.mediawiki.org/wiki/New_Developers)
- [wikimedia/mediawiki: 🌻 The collaborative editing software that runs Wikipedia. This is a mirror from gerrit.wikimedia.org. See https://www.mediawiki.org/wiki/Developer_access for contributing.](https://github.com/wikimedia/mediawiki/tree/master)
- [Gerrit/Tutorial - MediaWiki](https://www.mediawiki.org/wiki/Gerrit/Tutorial)

Exemple:

- List of countries
	- [Wikidata Query Service](https://query.wikidata.org/#%23List%20of%20present-day%20countries%20and%20capital%28s%29%0ASELECT%20DISTINCT%20%3Fcountry%20%3FcountryLabel%20%3Fcapital%20%3FcapitalLabel%0AWHERE%0A%7B%0A%20%20%3Fcountry%20wdt%3AP31%20wd%3AQ3624078%20.%0A%20%20%23not%20a%20former%20country%0A%20%20FILTER%20NOT%20EXISTS%20%7B%3Fcountry%20wdt%3AP31%20wd%3AQ3024240%7D%0A%20%20%23and%20no%20an%20ancient%20civilisation%20%28needed%20to%20exclude%20ancient%20Egypt%29%0A%20%20FILTER%20NOT%20EXISTS%20%7B%3Fcountry%20wdt%3AP31%20wd%3AQ28171280%7D%0A%20%20OPTIONAL%20%7B%20%3Fcountry%20wdt%3AP36%20%3Fcapital%20%7D%20.%0A%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20%7D%0A%7D%0AORDER%20BY%20%3FcountryLabel)
	- [Wikidata:SPARQL query service/queries/examples - Wikidata](https://www.wikidata.org/wiki/Wikidata:SPARQL_query_service/queries/examples#Countries) - List of present-day countries and capital(s)
	- [Research in programming Wikidata/Countries - Wikiversity](https://en.wikiversity.org/wiki/Research_in_programming_Wikidata/Countries)

## SlideShare

Permalink to a slide number: `http://www.slideshare.net/.../presentation-name` → `http://www.slideshare.net/.../presentation-name/10` for the slide 10

- [Friday Tip: create a permalink to a specific slide](https://blog.slideshare.net/2011/07/29/friday-tip-create-a-permalink-to-a-specific-slide)

## CONTENTdm

- [Download full size image from OLCL's CONTENTdm http:\/\/www.contentdm.org\/]https://gist.github.com/mems/4739515)

## Fashion Anthology bookmarlet

Show all fullres images (without watermark, + inaccessible ones) of a Fashion Anthology gallery in one page and without require any account

Filename pattern `%designer_name% %collection% %year% %image_number%.jpg`

```
javascript:var t=document.title.split(/\s+\|\s+/).slice(1).join(" ");$("head").append("<style>.pictures{margin:0px calc((100vw - 993px) / -2);padding:10px;display:flex;flex-wrap:wrap;}.picture-wrap{width:400px;flex-grow:1;box-sizing:border-box;padding:10px;}.picture{width: 100%;}</style>");var p=$(".bigphoto");var s=p.find("img").prop("src").replace(/\d{3}_m.jpg/, "");p.remove();var r=$("<div class='pictures'/>");var e=function(){$(this).parent().remove()};for(var i=1;i<=999;i++){var a=s+("000"+i).slice(-3)+".jpg";r.append($("<a class='picture-wrap'/>").attr("download", t+" "+i+".jpg").prop("href", a).append($("<img class='picture' src='#'>").error(e).prop("src", a)))};$(".allphotos").replaceWith(r);void(0);
```

- https://gist.github.com/mems/5a87941e00c8c15954ce

## Apple

### Apple live stream URL

Found the Apple live stream URL

1. Open `http://www.apple.com/live/` which redirect to something like `http://www.apple.com/live/2015-june-event/`
2. Find a loaded script like: `/live/2015-june-event/scripts/2015-june-event.built.js`
3. Open this script and search `p.events-delivery.apple.com.edgesuite.net`. You find something like `http://p.events-delivery.apple.com.edgesuite.net/15pijbnaefvpoijbaefvpihb06/js_files/event`
4. append to it `/url.json` (details: host + path + `url.json`)
5. Open the generated URL
6. Found an URL like `http://p.events-delivery.apple.com.edgesuite.net/15pijbnaefvpoijbaefvpihb06/m3u8/hls_mvp.m3u8`

Now you can watch it in VLC or any other videoplayer that support M3U and MP4(H.264+AAC)!

Previous Apple's website:

1. [...]
2. Find a loaded script like: `http://p.events-delivery.apple.com.edgesuite.net/15pijbnaefvpoijbaefvpihb06/js_files/event/url.js`
3. Grab the correct URL

- https://gist.github.com/mems/d54ad804d8d8d17d0011

## Online cursor editor

Add support of load an image in http://www.rw-designer.com/online-cursor-editor tool (Make CUR file)

```js
/*
Make CUR file using online editor, with basic support of load an image
http://www.rw-designer.com/online-cursor-editor

Require image file to base64 string convertion tool like:
http://www.motobit.com/util/base64-decoder-encoder.asp
*/

//------------

// Define draw position
var x = 0;
var y = 0;

// Define canvas size 32 × 32
var canvasWidth = 32;
var canvasHeight = 32;

var format = "image/png";
// Define image base64
var data = //"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAOeC3b8h2EGQmBU8ajioawYKLgJWQEevAmkWAGIvxJQCJJXgJleSUBxJbJTWIH4Gg6F14GYDd3tDkD8D00hiO+IKyQWoylegi/YxIH4PVQhiJYgFM5ZUMVZxEQKMxBPB9HocgARnh3leFIWmgAAAABJRU5ErkJggg=="
//"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAN6rVb/YZiBEBhVPKp4KCsGCm5CVoAHbwIpVgDirwQUguQVYKZXElBciewUViC+hkPhdSBmQ3e7AxD/Q1MI4jviConFaIqX4As2cSB+D1UIoiUIhXMWVHEWMZHCDMTTQTS6HABLqs2uDLgrlgAAAABJRU5ErkJggg=="
//"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAOv0zj+wzADITCqeFTxUFYMFNyErAAP3gRSrADEXwkoBMkrwEyvJKC4EtkprEB8DYfC60DMhu52ByD+h6YQxHfEFRKL0RQvwRds4kD8HqoQREsQCucsqOIsYiKFGYing2h0OQAUJ/3GEXDEHgAAAABJRU5ErkJggg=="
"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAP9Zi//wzADITCqeFTxUFYMFNyErAAP3gRSrADEXwkoBMkrwEyvJKC4EtkprEB8DYfC60DMhu52ByD+h6YQxHfEFRKL0RQvwRds4kD8HqoQREsQCucsqOIsYiKFGYing2h0OQA5PiOv+GamsAAAAABJRU5ErkJggg=="
//"iVBORw0KGgoAAAANSUhEUgAAAAsAAAAaCAYAAABhJqYYAAAAbUlEQVR42mNgQAOH12r/h2EGQmBU8ajioawYKLgJWQEevAmkWAGIvxJQCJJXgJleSUBxJbJTWIH4Gg6F14GYDd3tDkD8D00hiO+IKyQWoylegi/YxIH4PVQhiJYgFM5ZUMVZxEQKMxBPB9HocgBlExs5LfZeRAAAAABJRU5ErkJggg=="


//------------
//------------

var img = document.createElement("img");
img.src = "data:" + format + ";base64," + data;

var canvas = document.createElement("canvas");
canvas.width = canvasWidth;
canvas.height = canvasHeight;

var ctx = canvas.getContext("2d");

ctx.drawImage(img, x, y);

var imageData = ctx.getImageData(0, 0, canvasWidth, canvasHeight);
var imageWidth = imageData.width;
var imageHeight = imageData.height;
var rawPixels = imageData.data;
var numPixels = imageWidth * imageHeight;
var argb;
for(var i = 0; i < numPixels; i++){
	//32bits RGBA to ARGB
	argb = rawPixels[i * 4] << 16;//R
	argb |= rawPixels[i * 4 + 1] << 8;//G
	argb |= rawPixels[i * 4 + 2];//B
	argb |= rawPixels[i * 4 + 3] << 24;//A
	OCE_replacepixel(i, argb);
}
```

- https://gist.github.com/mems/5338017

## App animations

First exec this in WebDev console for each page, copy in clipboard the iframes src of each videos + title + keywords


```js
copy(JSON.stringify(Array.from(document.querySelectorAll("article")).map(article => [article.querySelector("iframe").src, /<a[^>]*>([^<]+)/.exec(article.querySelector("textarea").value)[1], article.querySelector(".cat").textContent])))
```

Go to https://videos.sproutvideo.com/embed/189bdbb01e1ce7c790/98b77e706be88310, open WebDev console and exec:

```js
var videos = [
	/*PAST HERE the content of all pages*/
];
var output = "";
// Decode function using XOR with key `t`
function d(e, t) {
	var i, n, s, r, o, a, l, u;
	for (o = [], i = '', n = 0, u = s = 1; 255 >= s; u = s += 1) o[String.fromCharCode(u)] = u;
	for (l = r = 0, a = e.length - 1; a >= r; l = r += 1) i += String.fromCharCode(o[e.substr(l, 1)] ^ o[t.substr(n, 1)]),
	n = n < t.length ? n + 1 : 0;
	return i.replace(/[^\x20-\x7E]+/g, '')
}
var count = 0;
var total = videos.length;
for(let i = 0; i < total; i++){
	let video = videos[i];
	let xhr = new XMLHttpRequest();
	xhr.addEventListener("load", event => {
		let data = event.target.response.querySelector("script").textContent.slice(11, -2)
		let config = JSON.parse(atob(data));
		let url = d(unescape(config.hdvu), config.host);
		output += `		<file name="${video[1]}">
			<resources>
				<url type="http">${url}</url>
			</resources>
		</file>`;

		if(++count >= total){
			copy(`<?xml version="1.0" encoding="UTF-8"?>
			<metalink version="3.0" xmlns="http://www.metalinker.org/">
				<files>
					${ouput}
				</files>
			</metalink>`);
			alert("You can now past clipboard content in a new file.")
		}
	})
	xhr.responseType = "document"
	xhr.open("GET", video[0])
	xhr.send()
}
```

- [Download all videos from http://www.appanimations.com/](https://gist.github.com/mems/7e00ba82012d668d0164)

## ccMixter

[ccMixter](http://ccmixter.org/)

```js
copy(Array.from(document.querySelectorAll(".upload_info[about]")).map(info => info.getAttribute("about").trim()).join("\n"))
```

## Wayback Machine

`robots.txt` is retroactive

`http://web.archive.org/cdx/search/cdx?url={domain}&matchType={matchType}&output=json&fl=timestamp,original&fastLatest=true&filter=statuscode:200&collapse=original` `&from={from}&to={to}`
`http://web.archive.org/web/{timestamp}id_/{originalurl}`

- [Wayback Machine APIs | Internet Archive](https://archive.org/help/wayback_api.php)
- [Retrieving Snapshots · Internet Archive](https://archive.readme.io/docs/website-snapshots)
- [Internet Archive Frequently Asked Questions](http://archive.org/about/faqs.php)
- [hartator/wayback-machine-downloader: Download an entire website from the Wayback Machine.](https://github.com/hartator/wayback-machine-downloader/) - [Recovering missing content from the Internet Archive](https://simonwillison.net/2017/Oct/8/missing-content/)
- [waybackmachine.sh](https://gist.github.com/lazanet/872f88c9874e4a7a78fd)
- [Heritrix - Heritrix - IA Webteam Confluence](https://webarchive.jira.com/wiki/display/Heritrix)
- [Stop Throwing Away Your Content | Adrian Roselli](http://adrianroselli.com/2016/07/stop-throwing-away-your-content.html)
- [Surprisingly, the default for the Internet Archive is Don’t Archive](http://cogdogblog.com/2016/06/dont-archive/)

## Blog export

Save the RSS / Atom

- [Migration Overblog vers Blogger ou Wordpress - Iv Oam Blog](https://iv-oam.blogspot.fr/2013/08/sauvegarde-overblog.html)
- [blogtowp download | SourceForge.net](https://sourceforge.net/projects/blogtowp/) - Ruby script `ruby dialog.rb`
	Support only the old version of blog-spot
	See [Importer les commentaires d'un blog sous Wordpress (4) - Reedition - nouvelles fonctionnalités + Haut et Fort - jrcourtois: le blog](http://blog.jrcourtois.net/post/2009/07/30/Importer-les-commentaires-d-un-blog-sous-Wordpress-4)
	See [Sauvegarde Erog et export vers Wordpress (voire vers Blogger) - Iv Oam Blog](https://iv-oam.blogspot.fr/2013/02/export-d-vers-wordpress-voire-vers.html)
	But get only posts have a category:

	- execute first the tool (will create `files/index.html` and empty file `TheBigFile.xml`)
	- edit files/index.html to add `categorie-0.html">Uncategorized</a>`
- [Back up, import, or delete your blog - Blogger Help](https://support.google.com/blogger/answer/41387?hl=en)
- `httrack myblog.com/faq "-admin.over-blog.com/*" "-www.over-blog.com/*" -O "My blog" -s0` - add `--update` to update only

## RFC

- https://datatracker.ietf.org/doc/search/?rfcs=on&name=%s (where `%s` is 2616 for RFC 2616)
- [IETF | RFCs](https://www.ietf.org/standards/rfcs/)
- [📄 HTTP Documentation](https://httpwg.org/specs/)

## Can I use

```js
const type = "custom";
const id = "mysite";
const source = "custom";
const uid = `${type}.${id}`;

localStorage.setItem("config-primary_usage", uid);
localStorage.setItem("usage-data-by-id", JSON.stringify({
	[uid]: {
		id,
		name: "My Custom Data Usage",
		type,
		source,
		/*meta: {
			"access_date": "2019-05-03",
			"month": "2019-04"
		},*/
		uid,
		// 100 based values
		dataByBrowser: {
			// see "data" field in https://caniuse.com/process/request_region_data.php?id=US
		},
	}
}));
```

[Simple Analytics](https://www.simpleanalytics.com/):

```json
{
	"hostname": "example.com",
	"agents": [
		{
			"count": 135755,
			"browser_name": "Chrome",
			"browser_version": "79",
			"os_name": "Windows",
			"os_version": "10",
			"type": "desktop"
		}

	]
}
```

Notes:
- `hostname` is used as default name of the dataset if none provided
- `browser_name` see an ex. list https://simpleanalytics.com/simpleanalytics.com.json?version=5&fields=browser_names
- `type`: `mobile` or `desktop`
- `os_name`: `(not set)`, `Windows`, `iOS`, `iPad`, `iPhone`, `iPod`, `Android`
- `browser_version` and `os_version` can be empty (`""`) or `null`

- `webpack:///src/components/ciu-sa-stats-import.ts` and `webpack:///src/utils/stats-import-utils.ts` `findBrowserVersion`
- [Import statistics exclude some versions of Safari · Issue #6605 · Fyrd/caniuse](https://github.com/Fyrd/caniuse/issues/6605)
- [Additional browser usage sources/functionality · Issue #1724 · Fyrd/caniuse](https://github.com/Fyrd/caniuse/issues/1724#issuecomment-497950671)
- [Be able to import usage data from csv or json · Issue #6410 · Fyrd/caniuse](https://github.com/Fyrd/caniuse/issues/6410)

## Outlook

Execute in a console of Outlook page:

```js
navigator.registerProtocolHandler("mailto", "https://outlook.office.com/mail/deeplink/compose?mailtouri=%s", "Outlook");
// Like navigator.registerProtocolHandler("mailto", "https://mail.google.com/mail/?extsrc=mailto&url=%s", "Gmail")
```

```cmd
@echo off
set address=%1
set address=%address:~7%
rundll32 URL.DLL,FileProtocolHandler "https://outlook.office.com/?path=/mail/action/compose&to=%address%"
```

- `https://outlook.office.com/mail/deeplink/compose?to={to}&subject={subject}&body={body}&cc={cc}`
- `https://outlook.office.com/owa/?rru=compose&to={to}&subject={subject}&body={body}&cc={cc}`
- [jonroig/MailtOWA: Chrome extension, opens mailto: links by default in by Microsoft Office 365 / Outlook Web Application (OWA)](https://github.com/jonroig/MailtOWA)
- [How to set the default Mailto to outlook.live.com - and have it actually WORK | Firefox Support Forum | Mozilla Support](https://support.mozilla.org/en-US/questions/1126241)
- [WesleyBranton/Outlook.com-mailto: Add Outlook.com as a default email provider for all mailto links in Firefox.](https://github.com/WesleyBranton/Outlook.com-mailto)
- [Set Office365 Outlook as mailto handler in Chrome - Spiceworks](https://web.archive.org/web/20190818054619/https://community.spiceworks.com/topic/1212102-set-office365-outlook-as-mailto-handler-in-chrome)

## Register protocol handler

- [Detecting if a URL scheme can be handled](https://web.archive.org/web/20221121231529/https://paul.kinlan.me/detecting-if-a-url-scheme-can-be-handled/)
- [Testing registerProtocolHandler and the web+ scheme prefix · lookout.net](https://web.archive.org/web/20161019081928/http://web.lookout.net:80/2012/01/testing-registerprotocolhandler-and-web.html)
- [Web-based protocol handlers - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/registerProtocolHandler/Web-based_protocol_handlers)
- [protocol_handlers - Web app manifests | MDN](https://developer.mozilla.org/en-US/docs/Web/Manifest/protocol_handlers)
