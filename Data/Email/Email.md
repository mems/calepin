Signature in text email: use `--` as separator

# Email address

Can contain + or . (Gmail allow multiple dots inside username: u.s.e.r.n.a.m.e@gmail.com) => point to the same user

## Format

Max length: 230

- [RFC 5321 - Simple Mail Transfer Protocol - 4.5.3.1.  Size Limits and Minimums](https://tools.ietf.org/html/rfc5321#section-4.5.3.1)

## Email validation

format validation vs test (send an verification email)

> The specified e-mail address 'myemail@address,com' is invalid. Did you mean 'myemail@address.com'?

> If I ask you to validate a@uz and a@qz, a regex based on the RFC can't tell whether they are valid or not without reference to things outside the RFC, i.e. a DNS lookupn and that's not part of the validation!

> distinguish "well-formed" from "deliverable"

- [The 100% correct way to validate email addresses](https://hackernoon.com/the-100-correct-way-to-validate-email-addresses-7c4818f24643)
- [RFC Errata Report » RFC Editor](http://www.rfc-editor.org/errata_search.php?rfc=3696)
- [php - Using a regular expression to validate an email address - Stack Overflow](https://stackoverflow.com/questions/201323/using-a-regular-expression-to-validate-an-email-address/532972#532972)
- https://github.com/dominicsayers/isemail/ and JS port https://github.com/hapijs/isemail
- [How to reduce incorrect email addresses](https://medium.com/@david.gilbertson/how-to-reduce-incorrect-email-addresses-df3b70cb15a9#)
- [Email address — Wikipedia](https://en.wikipedia.org/wiki/Email_address#RFC_Specification)
- [Mail::RFC822::Address](http://www.ex-parrot.com/~pdw/Mail-RFC822-Address.html)
- [How to Verify if an Email Address Is Real or Fake](http://www.labnol.org/software/verify-email-address/18220/)

### Simple validation

	function isValidEmail($email) {
	    $email_regexp = "";
	    // Avant le @
	    $email_regexp .= "/^[-+_.A-Za-z0-9]+";
	    $email_regexp .= "@";
	    // Nom de domaine
	    $email_regexp .= "((([A-Za-z0-9]|[A-Za-z0-9][-A-Za-z0-9]*[A-Za-z0-9])\.)+";
	    // Extension du nom de domaine
	    $email_regexp .= "(ad|ae|aero|af|ag|ai|al|am|an|ao|aq|ar|arpa|as|at|au|aw|az|ba|bb|bd|be|bf|bg|bh|bi|biz|bj|bm|bn|bo|br|bs|bt|bv|bw|by|bz|ca|cc|cd|cf|cg|ch|ci|ck|cl|cm|cn|co|com|coop|cr|cs|cu|cv|cx|cy|cz|de|dj|dk|dm|do|dz|ec|edu|ee|eg|eh|er|es|et|eu|fi|fj|fk|fm|fo|fr|ga|gb|gd|ge|gf|gh|gi|gl|gm|gn|gov|gp|gq|gr|gs|gt|gu|gw|gy|hk|hm|hn|hr|ht|hu|id|ie|il|in|info|int|io|iq|ir|is|it|jm|jo|jp|ke|kg|kh|ki|km|kn|kp|kr|kw|ky|kz|la|lb|lc|li|lk|lr|ls|lt|lu|lv|ly|ma|mc|md|mg|mh|mil|mk|ml|mm|mn|mo|mp|mq|mr|ms|mt|mu|museum|mv|mw|mx|my|mz|na|name|nc|ne|net|nf|ng|ni|nl|no|np|nr|nt|nu|nz|om|org|pa|pe|pf|pg|ph|pk|pl|pm|pn|pr|pro|ps|pt|pw|py|qa|re|ro|ru|rw|sa|sb|sc|sd|se|sg|sh|si|sj|sk|sl|sm|sn|so|sr|st|su|sv|sy|sz|tc|td|tf|tg|th|tj|tk|tm|tn|to|tp|tr|tt|tv|tw|tz|ua|ug|uk|um|us|uy|uz|va|vc|ve|vg|vi|vn|vu|wf|ws|ye|yt|yu|za|zm|zw)$";
	    $email_regexp .= "|";
	    // ou adresse IP...
	    $email_regexp .= "(([0-9][0-9]?|[0-1][0-9][0-9]|[2][0-4][0-9]|[2][5][0-5])\.){3}([0-9][0-9]?|[0-1][0-9][0-9]|[2][0-4][0-9]|[2][5][0-5]))$/";
		
	    if (! preg_match($email_regexp, $email)) return false;
	    return true;
	}

### Ping an Email Adress to validate it

**This not always works, because server often disallow it.**

	$ nslookup –type=mx gmail.com
	gmail.com MX preference=30, exchanger = alt3.gmail-smtp-in.l.google.com
	gmail.com MX preference=20, exchanger = alt2.gmail-smtp-in.l.google.com
	gmail.com MX preference=5,  exchanger = gmail-smtp-in.l.google.com
	gmail.com MX preference=10, exchanger = alt1.gmail-smtp-in.l.google.com
	gmail.com MX preference=40, exchanger = alt4.gmail-smtp-in.l.google.com

Use the MX with the lowest preference, here: gmail-smtp-in.l.google.com

	telnet gmail-smtp-in.l.google.com 25
	< 220 mx.google.com ESMTP bo10si2114398wjb.163 - gsmtp
	> HELO
	< 250 mx.google.com at your service
	> MAIL FROM:<my@email.address>
	< 250 2.1.0 OK bo10si2114398wjb.163 - gsmtp
	> RCPT TO:<email-to-test@gmail.com>
	< 550-5.1.1 The email account that you tried to reach does not exist. Please try...

	printf 'HELO\r\nMAIL from:<my@email.address>\r\nRCPT to:<email-to-test@gmail.com>\r\nQUIT' | nc gmail-smtp-in.l.google.com 25 -i 1

Result:
-> abc@gmail.com - The email account that you tried to reach does not exist.
-> support@gmail.com - The email account that you tried to reach is disabled.

Trace roote or GeoIP last IP address (between bracets) of "Received: from" field of (location of the sender).

### Send a confirmation email

A test.