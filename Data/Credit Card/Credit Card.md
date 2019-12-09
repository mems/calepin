See [Luhn algorithm](Algorithms#luhn), China UnionPay is use non luhn cards number

MasterCard BIN 2-Series (222100-272099)
Sample Master Card: 2221 0012 3412 3456, Expiry : 12/18

Credit card sample

```
American Express: 378282246310005
American Express: 371449635398431
American Express: 340353278080900
American Express Corporate: 378734493671000
BankCard (Australia): 5610591081018250
Diner's Club test number: 36438936438936
Discover test numbers: 6011016011016011
Discover Diners: 36110361103612
Discover: 6011111111111117
Discover: 6011000990139424
Discover: 6011003179988686
Diners Club: 30569309025904
Diners Club: 38520000023237
JCB: 3530111333300000
JCB: 3566003566003566
JCB: 3566002020360505
MasterCard: 5500005555555559
MasterCard: 5555555555554444
MasterCard (debit): 5200828282828210
MasterCard (prepaid): 5105105105105100
MasterCard: 5500005555555559
MasterCard Diners: 36111111111111
MasterCard II: 5115915115915118
MasterCard III: 4061724061724061
Visa: 4005520201264821 (without card art)
Visa: 4242424242424242 (with card art)
Visa: 4012888888881881
Visa: 4111111111111111
Visa: 4222222222222
Visa (debit): 4000056655665556
Visa Credit Card: 4444444444444448
Visa Commercial Card: 4110144110144115
Visa Corporate Card II: 4114360123456785
Visa Purchasing Card III: 4061724061724061
Visa: 4916 6293 0528 7782 (CVV 933)

Visa Brand : 4111 1111 1111 1111
Visa 3D Brand : 4000 0000 0000 0002
American Express Brand : 3741 1111 1111 111
MasterCard Brand : 5399 9999 9999 9999
Diners Brand : 3625 5695 5800 17
Bancontact/Mister Cash Brand : 67030000000000003
Visa Purchasing Brand : 4484 1200 0000 0029
American Express Purchasing Brand : 3742 9101 9071 995
Any expiry date in a near future may be used and any 3 digit CVC code. (4 digits for American Express and no CVC code for purchasing cards)
```

- American Express: starts with 34|37
- VISA: starts with 4
- Diners Club: starts with 300-305|309...
- MasterCard: starts with 51-55|22-27
- JCB: starts with 2131|1800|35
- Discover: starts with 6011|65|644-649
 
 ```
1800			JCB
2014			Diner's Club / enRoute
2131			JCB
2149			Diner's Club / enRoute
300 to 305		Diner's Club / Carte Blanche
34				American Express
36				Diner's Club / International
37				American Express
38				Diner's Club / Carte Blanche
3 (all others)	JCB
4				Visa
51 to 55		MasterCard
6011			Discover
```

```js
var
cards = {
	amex: {
		pattern: /^3[47]/,
		length: [15]
	},
	visa: {
		pattern: /^4/,
		length: [16]
	},
	mastercard: {
		pattern: /^5[1-5]/,
		length: [16]
	},
	discover: {
		pattern: /^(6011|622(12[6-9]|1[3-9][0-9]|[2-8][0-9]{2}|9[0-1][0-9]|92[0-5]|64[4-9])|65)/,
		length: [16]
	},
	unionPay: {
		pattern: /^(62|88)/,
		length: [16, 17, 18, 19]
	},
	dinersClub: {
		pattern: /^30[0-5]/,
		length: [14]
	},
	dinersClubInternational: {
		pattern: /^36/,
		length: [14]
	},
	jcb: {
		pattern: /^35(2[89]|[3-8][0-9])/,
		length: [16]
	},
	laser: {
		pattern: /^(6304|670[69]|6771)/,
		length: [16, 17, 18, 19]
	},
	visaElectron: {
		pattern: /^(4026|417500|4508|4844|491(3|7))/,
		length: [16]
	},
	maestro: {
		pattern: /^(5018|5020|5038|6304|6759|676[1-3])/,
		length: [12, 13, 14, 15, 16, 17, 18, 19]
	}
};


var invalid = "*** INVALID ***";
var undetermined = "enter more digits";

var mc = "MasterCard";
var visa = "Visa";
var amex = "American Express";
var diners = "Diners Club / Carte Blanche";
var dinersint = "Diners Club / International";
var discover = "Discover"
var er = "Diners Club / enRoute";
var jcb = "JCB";

function GetBank(numb) {

  // 51-55 mc
  // 4     visa
  // 34, 37amex
  // 300-305     diners carte blanche
  // 36, 38diners int
  // 6011  discover
  // 2014, 2149  er
  // 3     jcb
  // 2131, 1800  jcb

  var bank = "???";
  var prefix;
  if (numb.length == 0) { // nothing entered yet
    bank = "";
  } else if (numb.charAt(0) > 6) { // 1st digit is 7, 8, or 9
    bank = invalid;
  } else if (numb.charAt(0) == "4") { // 1st digit is 4
    bank = visa;
  } else if (numb.length == 1) { // one digit entered
    bank = undetermined;
  } else if (numb.length >= 2) { // two or more digits entered
    if (numb.substr(0,2) >= "51" && numb.substr(0,2) <= "55") { // 1st 2 digits are 51-55
      bank = mc;
    } else if (numb.charAt(0) == "3") { // first digit is 3
      if (numb.charAt(1) == "4" || numb.charAt(1) == "7") { // 1st 2 digits are 34 or 37
	bank = amex;
      } else if (numb.charAt(1) == "6") { // 1st 2 digits are 36 or 36
	bank = dinersint;
      } else if (numb.charAt(1) == "6") { // 1st 2 digits are 36 or 38
	bank = diners;
      } else if (numb.length == 2) { // exactly two digits entered starting with a 3
	if (numb.charAt(1) == "0") { // 1st 2 digits are 30
	  bank = undetermined;
	} else {
	  bank = jcb;
	}
      } else if (numb.substr(1,2) >= "00" &&
		 numb.substr(1,2) <= "05") { // 1st 3 digits are 300-305
	bank = diners;
      } else { // 1st digit is 3 and none of the special cases for 3 apply
	bank = jcb;
      }
    } else if (numb.length == 2) { // exactly 2 digits
      prefix = numb.substr(0,2);
      if (prefix != "30" && prefix != "60" && // 30 is for diners, 60 is for discover
	  prefix != "20" && // for enRoute
	  prefix != "21" && prefix != "18") {
	 // doesn't start with any remaining allowable sequence
	bank = invalid;
      } else { // need more than 2 digits to determine the bank
	bank = undetermined;
      }
    } else if (numb.length == 3) { // exactly 3 digits
      prefix = numb.substr(0,3);
      if (prefix != "601" &&
	  prefix != "201" && prefix != "214" && // for enRoute 
	  prefix != "213" && prefix != "180") {
	// doesn't start with any remaining allowable sequence
	bank = invalid;
      } else { // need more than 3 digits to determine the bank
	bank = undetermined;
      }
    } else if (numb.length >= 4) { // 4 or more digits
      prefix = numb.substr(0,4);
      if (prefix == "6011") { // first 4 digits are 6011
	bank = discover;
      } else if (prefix == "2131" || prefix == "1800") { // first 4 digits are 2131 or 1800
	bank = jcb;
      } else if (prefix == "2014" || prefix == "2149") { // first 4 digits are 2014 or 2149
	bank = er;
      } else { // nothing left, it's invalid
	bank = invalid;
      }
    }
  }
  return bank;
}

function GetLength(numb, bank) {
  if (bank == mc) return 16;
  if (bank == visa) return 16; // could also be 13 ??? -- obsolete
  if (bank == amex) return 15;
  if (bank == diners) return 14;
  if (bank == dinersint) return 14;
  if (bank == discover) return 16
  if (bank == er) return 15;
  if (bank == jcb) {
    if (numb.charAt(0) == "3") return 16; else return 15;
  }
  return 0;
}
```

Test payment cards:

- [drmonkeyninja/test-payment-cards: Cheatsheet of test payment cards for various payment gateways](https://github.com/drmonkeyninja/test-payment-cards)
- [Testing](https://stripe.com/docs/testing)
- [How can I test payment methods? – HiPay Support Center](https://support.hipay.com/hc/en-us/articles/213882649-How-can-I-test-payment-methods-)
- [Test Payflow Transactions - PayPal Developer](https://developer.paypal.com/docs/classic/payflow/payflow-pro/payflow-pro-testing/#credit-card-numbers-for-testing)
- [Números de tarjeta de crédito de pruebas | Módulos y pasarelas de pago](https://modulosdepago.es/blog/numeros-de-tarjeta-de-credito-de-pruebas/)
- [Credit Card Numbers Generator | Get Fake Credit Card Numbers for Testing Purposes](http://www.getcreditcardnumbers.com/)
- [Credit Card Numbers Generator | Get Fake Credit Card Numbers for Testing Purposes](http://www.getcreditcardnumbers.com/cvv-numbers-credit-card)
- [Credit Card Numbers Generator | Get Fake Credit Card Numbers for Testing Purposes](http://www.getcreditcardnumbers.com/credit-card-generator)
- [Graham King » Credit card generator](https://www.darkcoding.net/credit-card-generator/) - [grahamking/darkcoding-credit-card: Credit card generators from darkcoding.net](https://github.com/grahamking/darkcoding-credit-card)
- [Credit Card Numbers Generator | Get Fake Credit Card Numbers for Testing Purposes](http://www.getcreditcardnumbers.com/)
- [Online Credit Card Generator](https://names.igopaygo.com/credit-card)

Validation:

- [Credit Card Number Generator & Validator - FreeFormatter.com](http://www.freeformatter.com/credit-card-number-generator-validator.html)
- [Check Credit Card Numbers | Validate your credit card number with our free online checker](http://www.validcreditcardnumber.com/)
- [Check Credit Card Numbers | Validate your credit card number with our free online checker](http://www.validcreditcardnumber.com/)
- [Graham King » CVV numbers](https://www.darkcoding.net/credit-card/cvv-numbers/)
- [Graham King » Luhn formula](https://www.darkcoding.net/credit-card/luhn-formula/)
- [ISO/IEC 7812 — Wikipedia](https://en.wikipedia.org/wiki/ISO/IEC_7812)
- [Everything you ever wanted to know about CC's](http://euro.ecom.cmu.edu/resources/elibrary/everycc.htm)
- [Mastercard 2-Series BIN/IIN Number | New BIN Range for Mastercard Cards](https://www.mastercard.us/en-us/issuers/get-support/2-series-bin-expansion.html)
- [Credit Card Validation, Step 1: Confirming the pattern | Ascad Networks](http://web.archive.org/web/20151012122918/http://www.ascadnetworks.com/Guides-and-Tips/Credit-Card-Validation,-Step-1:-Confirming-the-pattern)
- [Credit Card Validation, Step 2: The Luhn Algorithm | Ascad Networks](http://web.archive.org/web/20151021075528/http://www.ascadnetworks.com/Guides-and-Tips/Credit-Card-Validation,-Step-2:-The-Luhn-Algorithm)
- [Anatomy of Credit Card Numbers](http://web.archive.org/web/20120614072656/http://www.merriampark.com/anatomycc.htm)
- [Cartes Bancaires | Intégrateur d'innovation - Groupement des Cartes Bancaires CB](https://www.cartes-bancaires.com/)
- [List of Issuer Identification Numbers - Wikipedia, the free encyclopedia](https://web.archive.org/web/20130827121726/http://en.wikipedia.org/wiki/List_of_Bank_Identification_Numbers)
- [BIN Database - Search card issuing bank name and country](https://www.bindb.com/bin-database.html)
- [binlist/data: binlist.net data repo](https://github.com/binlist/data)
- [banks-db/banks at master · ramoona/banks-db](https://github.com/ramoona/banks-db/tree/master/banks)
- https://github.com/stripe/jquery.payment
- https://github.com/inacho/php-credit-card-validator

UI/UX:

- [The anatomy of a credit card form](https://uxdesign.cc/the-anatomy-of-a-credit-card-payment-form-32ec0e5708bb)
- [billing - Why do credit card forms ask for Visa, MasterCard, etc.? - User Experience Stack Exchange](http://ux.stackexchange.com/questions/51346/why-do-credit-card-forms-ask-for-visa-mastercard-etc) - [Why do credit card forms ask for Visa, Mastercard, etc.? | Hacker News](https://news.ycombinator.com/item?id=7158626)
