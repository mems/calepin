Signature in text email: use `--` as separator

## Email address

Can contain `+` or `.` (Gmail allow multiple dots inside username: u.s.e.r.n.a.m.e@gmail.com) are often an alias that point to the same user

### Format

Max length: 230

- [RFC 5321 - Simple Mail Transfer Protocol - 4.5.3.1.  Size Limits and Minimums](https://tools.ietf.org/html/rfc5321#section-4.5.3.1)

### Validate email address format

format validation vs test (send an verification email)

> ✔️ DO use a small regular expression to check for the valid structure of an email.
> ✔️ DO send a test email to the address provided by a user of your app.
> ❌ DON'T use a regular expression as the only way you validate an email.
>
> — [How to verify that strings are in valid email format | Microsoft Learn](https://web.archive.org/web/20230129040505/https://learn.microsoft.com/en-us/dotnet/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format)

> The specified e-mail address 'myemail@address,com' is invalid. Did you mean 'myemail@address.com'?

> If I ask you to validate a@uz and a@qz, a regex based on the RFC can't tell whether they are valid or not without reference to things outside the RFC, i.e. a DNS lookupn and that's not part of the validation!

> distinguish "well-formed" from "deliverable"

- [Email address - Wikipedia](https://en.wikipedia.org/wiki/Email_address#Local-part)
- [The 100% correct way to validate email addresses | by David Gilbertson | Medium](https://web.archive.org/web/20230519221313/https://david-gilbertson.medium.com/the-100-correct-way-to-validate-email-addresses-7c4818f24643)
- [How to reduce incorrect email addresses | by David Gilbertson | Medium](https://web.archive.org/web/20230614154145/https://david-gilbertson.medium.com/how-to-reduce-incorrect-email-addresses-df3b70cb15a9)
- [How to verify that strings are in valid email format | Microsoft Learn](https://web.archive.org/web/20230129040505/https://learn.microsoft.com/en-us/dotnet/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format)
- [RFC Errata Report » RFC Editor](http://www.rfc-editor.org/errata_search.php?rfc=3696)
- [php - Using a regular expression to validate an email address - Stack Overflow](https://stackoverflow.com/questions/201323/using-a-regular-expression-to-validate-an-email-address/532972#532972)
- https://github.com/dominicsayers/isemail/ and JS port https://github.com/hapijs/isemail
- [Email address — Wikipedia](https://en.wikipedia.org/wiki/Email_address#RFC_Specification)
- [Mail::RFC822::Address](http://www.ex-parrot.com/~pdw/Mail-RFC822-Address.html)
- [How to Verify if an Email Address Is Real or Fake](http://www.labnol.org/software/verify-email-address/18220/)
- https://github.com/twitter/twitter-text/blob/9537bdf/js/src/regexp/extractUrl.js - Lib Twitter use to find URL in text
- [In search of the perfect URL validation regex](https://web.archive.org/web/20220508030856/https://mathiasbynens.be/demo/url-regex)

```php
function isValidEmail($email) {
	$email_regexp = "";
	// Before `@`
	$email_regexp .= "/^[-+_.A-Za-z0-9]+";
	$email_regexp .= "@";
	// Domain
	$email_regexp .= "((([A-Za-z0-9]|[A-Za-z0-9][-A-Za-z0-9]*[A-Za-z0-9])\.)+";
	// TLD
	$email_regexp .= "(ad|ae|aero|af|ag|ai|al|am|an|ao|aq|ar|arpa|as|at|au|aw|az|ba|bb|bd|be|bf|bg|bh|bi|biz|bj|bm|bn|bo|br|bs|bt|bv|bw|by|bz|ca|cc|cd|cf|cg|ch|ci|ck|cl|cm|cn|co|com|coop|cr|cs|cu|cv|cx|cy|cz|de|dj|dk|dm|do|dz|ec|edu|ee|eg|eh|er|es|et|eu|fi|fj|fk|fm|fo|fr|ga|gb|gd|ge|gf|gh|gi|gl|gm|gn|gov|gp|gq|gr|gs|gt|gu|gw|gy|hk|hm|hn|hr|ht|hu|id|ie|il|in|info|int|io|iq|ir|is|it|jm|jo|jp|ke|kg|kh|ki|km|kn|kp|kr|kw|ky|kz|la|lb|lc|li|lk|lr|ls|lt|lu|lv|ly|ma|mc|md|mg|mh|mil|mk|ml|mm|mn|mo|mp|mq|mr|ms|mt|mu|museum|mv|mw|mx|my|mz|na|name|nc|ne|net|nf|ng|ni|nl|no|np|nr|nt|nu|nz|om|org|pa|pe|pf|pg|ph|pk|pl|pm|pn|pr|pro|ps|pt|pw|py|qa|re|ro|ru|rw|sa|sb|sc|sd|se|sg|sh|si|sj|sk|sl|sm|sn|so|sr|st|su|sv|sy|sz|tc|td|tf|tg|th|tj|tk|tm|tn|to|tp|tr|tt|tv|tw|tz|ua|ug|uk|um|us|uy|uz|va|vc|ve|vg|vi|vn|vu|wf|ws|ye|yt|yu|za|zm|zw)$";
	$email_regexp .= "|";
	// or IP address...
	$email_regexp .= "(([0-9][0-9]?|[0-1][0-9][0-9]|[2][0-4][0-9]|[2][5][0-5])\.){3}([0-9][0-9]?|[0-1][0-9][0-9]|[2][0-4][0-9]|[2][5][0-5]))$/";

	if (! preg_match($email_regexp, $email)) return false;
	return true;
}
```

### Ping an email address to validate it

**This not always works, because server often disallow it.**

```
$ nslookup –type=mx gmail.com
gmail.com MX preference=30, exchanger = alt3.gmail-smtp-in.l.google.com
gmail.com MX preference=20, exchanger = alt2.gmail-smtp-in.l.google.com
gmail.com MX preference=5,  exchanger = gmail-smtp-in.l.google.com
gmail.com MX preference=10, exchanger = alt1.gmail-smtp-in.l.google.com
gmail.com MX preference=40, exchanger = alt4.gmail-smtp-in.l.google.com
```

Use the MX with the lowest preference, here: gmail-smtp-in.l.google.com

```
telnet gmail-smtp-in.l.google.com 25
< 220 mx.google.com ESMTP bo10si2114398wjb.163 - gsmtp
> HELO
< 250 mx.google.com at your service
> MAIL FROM:<test@test.com>
< 250 2.1.0 OK bo10si2114398wjb.163 - gsmtp
> RCPT TO:<email-to-test@gmail.com>
< 550-5.1.1 The email account that you tried to reach does not exist. Please try...
```

```
printf 'HELO\r\nMAIL from:<test@test.com>\r\nRCPT to:<email-to-test@gmail.com>\r\nQUIT' | nc gmail-smtp-in.l.google.com 25 -i 1
```

Result:
-> abc@gmail.com - The email account that you tried to reach does not exist.
-> support@gmail.com - The email account that you tried to reach is disabled.

Trace roote or GeoIP last IP address (between bracets) of "Received: from" field of (location of the sender).

## Copy emails from account to another

```sh
# require php imap and php mbstring
php ./src/cli/imapcopy.php config.json -test
php ./src/cli/imapcopy.php config.json
```

```json
{
    "src": {
        "hostname": "imap.example.com",
        "port": 993,
        "username": "test@example.com",
        "password": "password1",
        "ssl": true,
        "sslNovalidateCert": false,
        "readOnly": true,
        "flags": true
    },
    "dst": {
        "hostname": "imap.example.com",
        "port": 993,
        "username": "test2@example.com",
        "password": "password2",
        "ssl": true,
        "sslNovalidateCert": false,
        "readOnly": false,
        "flags": true
    }
}
```

- [Official imapsync migration tool ( release 2.264 )](https://imapsync.lamiral.info/)
- [wrzlbrmft/imapcopy: Recursively copy all e-mail messages and folders from one IMAP account to another.](https://github.com/wrzlbrmft/imapcopy)

## Subaddressing

`<local-part>+<tag>@<domain>`

- [Subaddressing - Email address - Wikipedia](https://en.wikipedia.org/wiki/Email_address#Subaddressing)
- [Plus Addressing in Exchange Online | Microsoft Learn](https://learn.microsoft.com/en-us/exchange/recipients-in-exchange-online/plus-addressing-in-exchange-online)
- [Official Gmail Blog: 2 hidden ways to get more from your Gmail address](https://gmail.googleblog.com/2008/03/2-hidden-ways-to-get-more-from-your.html?m=1)
- [Plus addressing and subdomain addressing – Fastmail](https://web.archive.org/web/20221207144956/https://www.fastmail.help/hc/en-us/articles/360060591053-Plus-addressing-and-subdomain-addressing)
- [The IAB loves tracking users. But it hates users tracking them | Hacker News](https://news.ycombinator.com/item?id=34400024)
- [Plus Addressing - Migadu Email](https://www.migadu.com/guides/plus_addressing/)

## Normalization

Usally used for track users: remove parts that could be used for [subaddressing](#subaddressing), remove dots (`.`) in local-part, change case, etc. This could be destructive.

- [uid2docs/api at main · IABTechLab/uid2docs · GitHub](https://web.archive.org/web/20230116231810/https://github.com/IABTechLab/uid2docs/tree/main/api#email-address-normalization)
- [Passing Partner Data to ID5](https://web.archive.org/web/20230116221038/https://support.id5.io/portal/en/kb/articles/passing-partner-data-to-id5#Cleansing_Emails_Prior_to_Hashing)
- [Local-part normalization - Email address - Wikipedia](https://en.wikipedia.org/wiki/Email_address#Local-part_normalization)
