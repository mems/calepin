## Coding conventions

- [PHP Standards Recommendations - PHP-FIG](http://www.php-fig.org/psr/)
- http://git.php.net/?p=php-src.git;a=blob_plain;f=CODING_STANDARDS;hb=HEAD
- http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
- http://pear.php.net/manual/en/standards.php
- http://www.horde.org/horde/docs/?f=CODING_STANDARDS.html
- http://codex.wordpress.org/WordPress_Coding_Standards
- [Coding Standards (Contributing to Symfony)](http://symfony.com/doc/current/contributing/code/standards.html)
- [Popular Coding Convention on Github](http://sideeffect.kr/popularconvention/#php)
- [PHP - The Wrong Way](https://phpthewrongway.com/)

> remember most important thing is being consistent in your naming conventions and coding style. 

## Change `composer.json`

Genre ajouter : `"facebook/php-sdk" : "@stable",`, faire en local

	php composer.phar update "facebook/php-sdk"

pour n'updater que la libraire concernée. 
Le `composer.lock` sera mis à jour. Lors d'un pull, avec `php composer.phar install` n'updatera que la nouvelle librairie (par le nouveau `composer.lock`)

## Update doctrine

`php app/console doctrine:schema:update --force` is the same as `app/console doc:sc:up --force`

## Base path

	<?php
	$base_path = dirname($_SERVER['PHP_SELF']) . '/';
	if($base_path === '//') $base_path = '/';
	
	$https = isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] == 'on';
	$port = $_SERVER['SERVER_PORT'];
	$base = ($https ? 'https' : 'http') . '://' . $_SERVER['SERVER_NAME'] . (!$https && $port == 80 || $https && $port == 443 ? '' : ':' . $port) . $base_path;
	
	list($request_path) = explode('?', $_SERVER['REQUEST_URI'], 2);// to get the query use $_SERVER['QUERY_STRING'] or use $_GET instead
	$request_path = rawurldecode($request_path);// REQUEST_URI is encoded, PHP_SELF not
	$relative_path = substr($request_path, strlen($base_path));
	
	$route = preg_split('/\/+/', $relative_path);// split to slashes (group or not). See also Apache AllowEncodedSlashes for %2F

## Get browser language

	$str_browser_language = !empty($_SERVER['HTTP_ACCEPT_LANGUAGE']) ? strtok(strip_tags($_SERVER['HTTP_ACCEPT_LANGUAGE']), ',') : '';
	$str_browser_language = !empty($_GET['language']) ? $_GET['language'] : $str_browser_language;
	switch (substr($str_browser_language, 0,2))
	{
		case 'de':
			$str_language = 'de';
			break;
		case 'en':
			$str_language = 'en';
			break;
		default:
			$str_language = 'en';
	}

## Get client's headers

	var_dump(apache_request_headers());

	function getHeaders()
	{
	    $headers = array();
	    foreach ($_SERVER as $k => $v)
	    {
	        if (substr($k, 0, 5) == "HTTP_")
	        {
	            $k = str_replace('_', ' ', substr($k, 5));
	            $k = str_replace(' ', '-', ucwords(strtolower($k)));
	            $headers[$k] = $v;
	        }
	    }
	    return $headers;
	}

## Send mutliple attachement in mail

	<?php
	// array with filenames to be sent as attachment
	$files = array("file_1.ext","file_2.ext","file_3.ext",......);
	
	// email fields: to, from, subject, and so on
	$to = "mail@mail.com";
	$from = "mail@mail.com";
	$subject ="My subject";
	$message = "My message";
	$headers = "From: $from";
	
	// boundary
	$semi_rand = md5(time());
	$mime_boundary = "==Multipart_Boundary_x{$semi_rand}x";
	
	// headers for attachment
	$headers .= "\nMIME-Version: 1.0\n" . "Content-Type: multipart/mixed;\n" . " boundary=\"{$mime_boundary}\"";
	
	// multipart boundary
	$message = "This is a multi-part message in MIME format.\n\n" . "--{$mime_boundary}\n" . "Content-Type: text/plain; charset=\"iso-8859-1\"\n" . "Content-Transfer-Encoding: 7bit\n\n" . $message . "\n\n";
	$message .= "--{$mime_boundary}\n";
	
	// preparing attachments
	for($x=0;$x<count($files);$x++){
	    $file = fopen($files[$x],"rb");
	    $data = fread($file,filesize($files[$x]));
	    fclose($file);
	    $data = chunk_split(base64_encode($data));
	    $message .= "Content-Type: {\"application/octet-stream\"};\n" . " name=\"$files[$x]\"\n" .
	    "Content-Disposition: attachment;\n" . " filename=\"$files[$x]\"\n" .
	    "Content-Transfer-Encoding: base64\n\n" . $data . "\n\n";
	    $message .= "--{$mime_boundary}\n";
	}
	
	// send
	
	$ok = @mail($to, $subject, $message, $headers);
	if ($ok) {
	    echo "<p>mail sent to $to!</p>";
	} else {
	    echo "<p>mail could not be sent!</p>";
	}
	
	?>

## Array are copied not referenced (default)

	$a = array(1,2);
	$b = $a; // $b will be a different array
	$c = &$a; // $c will be a reference to $a

- [Is there a function to make a copy of a PHP array to another? - Stack Overflow](https://stackoverflow.com/questions/1532618/is-there-a-function-to-make-a-copy-of-a-php-array-to-another/1532632#1532632)

## PHP proxy

	<?php
	// PHP Proxy example for Yahoo! Web services. 
	// Responds to both HTTP GET and POST requests
	//
	// Author: Jason Levitt
	// December 7th, 2005
	//
	
	// Allowed hostname (api.local and api.travel are also possible here)
	define ('HOSTNAME', 'http://search.yahooapis.com/');
	
	// Get the REST call path from the AJAX application
	// Is it a POST or a GET?
	$path = ($_POST['yws_path']) ? $_POST['yws_path'] : $_GET['yws_path'];
	$url = HOSTNAME.$path;
	
	// Open the Curl session
	$session = curl_init($url);
	
	// If it's a POST, put the POST data in the body
	if ($_POST['yws_path']) {
		$postvars = '';
		while ($element = current($_POST)) {
			$postvars .= key($_POST).'='.$element.'&';
			next($_POST);
		}
		curl_setopt ($session, CURLOPT_POST, true);
		curl_setopt ($session, CURLOPT_POSTFIELDS, $postvars);
	}
	
	// Don't return HTTP headers. Do return the contents of the call
	curl_setopt($session, CURLOPT_HEADER, false);
	curl_setopt($session, CURLOPT_RETURNTRANSFER, true);
	
	// Make the call
	$xml = curl_exec($session);
	
	// The web service returns XML. Set the Content-Type appropriately
	header("Content-Type: text/xml");
	
	echo $xml;
	curl_close($session);
	
	?>

## WebSocket

http://antoine.goutenoir.com/blog/2013/07/02/test-driven-websockets-and-symfony2-using-ratchet/

## DOMDocument and UTF-8

	// Create a DOMDocument instance 
	$doc = new DOMDocument();
	
	// The fix: mb_convert_encoding conversion
	$doc->loadHTML(mb_convert_encoding($content, 'HTML-ENTITIES', 'UTF-8'));

## Overwriting PHP file handler

I find today that the default "file" stream wrapper in PHP is overwritable. You only need to call stream_wrapper_unregister and then stream_wrapper_register with your wrapper.

Imagine that you want to integrate your system A with another system B and you need to "catch" some of the files the B system includes and modify them or replace with another file.

Implementing this by patching the files of the system B comes to mind first but making the same with a custom "file" stream wrapper may be more interesting.

File: test.php5

	<?php echo "I'm " . basename(__FILE__);

File: sample.php

	<?php
	
	class CustomFileStreamWrapper
	{
	  private $_handler;
	  function stream_open($path, $mode, $options, &$opened_path) {
	    stream_wrapper_restore('file');
	    $this->_handler = fopen($path . '5', $mode);
	    stream_wrapper_unregister('file');
	    stream_wrapper_register('file', 'CustomFileStreamWrapper');
	    return true;
	  }
	  function stream_read($count) {
	    return fread($this->_handler, $count);
	  }
	  function stream_write($data) {
	    return fwrite($this->_handler, $data);
	  }
	  function stream_tell() {
	    return ftell($this->_handler);
	  }
	  function stream_eof() {
	    return feof($this->_handler);
	  }
	  function stream_seek($offset, $whence) {
	    return fseek($this->_handler, $offset, $whence);
	  }
	}
	
	stream_wrapper_unregister('file');
	stream_wrapper_register('file', 'CustomFileStreamWrapper');
	
	// Includes test.php, not test.php5!
	require 'test.php';

Output:

	I'm test.php

## Handle HTML with DOM

HTML5 doc:

- https://bugs.php.net/bug.php?id=60021
- https://github.com/glenscott/dom-document-charset
- http://engineeredweb.com/blog/2013/html5-php-released/
- https://github.com/html5lib
- https://github.com/Masterminds/html5-php/wiki
- http://php.net/manual/fr/domdocument.savehtml.php

## Class Autoload

	define('PROJECT_ROOT', dirname(__FILE__));
	set_include_path(implode(PATH_SEPARATOR, array(
		get_include_path(),
		PROJECT_ROOT . DIRECTORY_SEPARATOR . 'source',
		PROJECT_ROOT . DIRECTORY_SEPARATOR . 'library'
	)));
	spl_autoload_register();

## Security

### Output / input safety

**Never echo `$_GET[index]` or `$_SERVER[PHP_SELF]` or `$_SERVER['QUERY_STRING']` etc. Always use `htmlspecialchars($var)` to escape it!**

`htmlspecialchars()` to output a string

for files, use `scandir()`

- `strip_tags()`
- `filter_input(INPUT_SERVER, 'REQUEST_URI', FILTER_SANITIZE_ENCODED)`
- `rawurlencode()`
- `htmlspecialchars()`
- [Encode URI](#encode-uri)
- `htmlspecialchars($value, ENT_COMPAT | ENT_HTML5)` for HTML tag attribute value `if(!defined('ENT_HTML5')) define('ENT_HTML5', 16|32);`

### `Host:` poisoning

Don't use host autodetection (or more generally base url autodetection), it relies first on `$_SERVER['HTTP_HOST']` or `$_SERVER['SERVER_NAME']`

See [15KB Of Fame: HTTP Cache Poisoning via Host Header Injection](http://carlos.bueno.org/2008/06/host-header-injection.html)

See [core - Apache HTTP Server Version 2.4](http://httpd.apache.org/docs/2.4/mod/core.html#usecanonicalname)

## UTF-8

- [What Every Programmer Absolutely, Positively Needs to Know About Encodings and Character Sets to Work With Text](http://kunststube.net/encoding/)

## Encode URI

Encore URL

	// https://stackoverflow.com/a/6059053/470117 + RFC3986 (IPV6 brackets)
	// http://php.net/manual/en/function.rawurlencode.php
	// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURI
	// It basically rawurlencodes everything, and then decodes a few things back
	function encode_uri($url) {
		$unescaped = array(
			'%2D'=>'-','%5F'=>'_','%2E'=>'.','%21'=>'!', '%7E'=>'~',
			'%2A'=>'*', '%27'=>"'", '%28'=>'(', '%29'=>')'
		);
		$reserved = array(
			'%3B'=>';','%2C'=>',','%2F'=>'/','%3F'=>'?','%3A'=>':',
			'%40'=>'@','%26'=>'&','%3D'=>'=','%2B'=>'+','%24'=>'$', '%5B'=>'[', '%5D'=>']'
		);
		$score = array(
			'%23'=>'#'
		);
		return strtr(rawurlencode($url), array_merge($reserved,$unescaped,$score));
	}

## JSON error

	$data = json_decode(file_get_contents($filename));

	if(json_last_error() !== JSON_ERROR_NONE){
		// PHP < 5.5
		if (!function_exists('json_last_error_msg')) {
			function json_last_error_msg() {
				static $errors = array(
					JSON_ERROR_NONE             => null,
					JSON_ERROR_DEPTH            => 'Maximum stack depth exceeded',
					JSON_ERROR_STATE_MISMATCH   => 'Underflow or the modes mismatch',
					JSON_ERROR_CTRL_CHAR        => 'Unexpected control character found',
					JSON_ERROR_SYNTAX           => 'Syntax error, malformed JSON',
					JSON_ERROR_UTF8             => 'Malformed UTF-8 characters, possibly incorrectly encoded'
				);
				$error = json_last_error();
				return array_key_exists($error, $errors) ? $errors[$error] : "Unknown error ({$error})";
			}
		}
		
		header($_SERVER['SERVER_PROTOCOL'] . ' 500 Internal Server Error', true, 500);// or if supported, use http_response_code(500)
		// TODO display JSON error https://github.com/Seldaek/jsonlint
		die(sprintf("Failed to parse json string '%s', error: '%s'", $filename, json_last_error_msg()));
	}

## Print object to JS

	// From https://gist.github.com/muhqu/863757
	function json_encode_unicode($data, $flags) {
		if (defined('JSON_UNESCAPED_UNICODE')) {
			return json_encode($data, $flags | JSON_UNESCAPED_UNICODE);
		}
		return preg_replace_callback('/(?<!\\\\)\\\\u([0-9a-f]{4})/i',
			function ($m) {
				$d = pack("H*", $m[1]);
				$r = mb_convert_encoding($d, "UTF8", "UTF-16BE");
				return $r!=="?" && $r!=="" ? $r : $m[0];
			}, json_encode($data, $flags)
		);
	}
	
	<!-- As raw JSON -->
	<script type="application/json" id="data"><?php echo json_encode_unicode($results, JSON_HEX_TAG | JSON_HEX_AMP | JSON_UNESCAPED_SLASHES | JSON_PARTIAL_OUTPUT_ON_ERROR) ?></script>
	
	<!-- As value of JS variable -->
	<script>var data = <?php echo json_encode_unicode($results, JSON_HEX_TAG | JSON_HEX_AMP | JSON_UNESCAPED_SLASHES | JSON_PARTIAL_OUTPUT_ON_ERROR) ?></script>

- [Data input implication](Security#data-input-implication)

## Detect XHR

	$from_xhr = !empty($_SERVER['HTTP_X_REQUESTED_WITH']) && strtolower($_SERVER['HTTP_X_REQUESTED_WITH']) === 'xmlhttprequest';
	header('Vary: X-Requested-With');

## Merge URL or query string

	parse_url();
	parse_str();
	http_build_query();

	// http_build_url($url1, $url2);// If PECL pecl_http installed (or use https://github.com/ivantcholakov/http_build_url)
	if (!function_exists('http_build_str') || !function_exists('http_build_url')) {
		require dirname(__FILE__).'/http_build_url.php';
	}
	$query = $_GET;
	unset($query['var1']);
	http_build_url('http://example.com/path/script.php?var1=1', array('query' => http_build_query($query), HTTP_URL_JOIN_QUERY));
	
	$_SERVER['QUERY_STRING'];
	$_GET;

## Build URL

`http_build_url()` see [Merge URL or query string](#merge-url-or-query-string)

## Remove empty values from arrays

	// removes all NULL, FALSE and Empty Strings and 0 (zero) values
	$result = array_filter( $array );

	// removes all NULL, FALSE and Empty Strings but leaves 0 (zero) values
	$result = array_filter( $array, 'strlen' );

## Default value

	$name = $_GET['name'] ?? 'john doe';//PHP7
	$name = isset($_GET['name']) ? $_GET['name'] : 'john doe';

- [PHP: New features - Manual](http://php.net/manual/en/migration70.new-features.php#migration70.new-features.null-coalesce-op)

## Chunked transfert encoding

	// PHP encode transfer automatically if you use flush() and output_buffering is activated (don't need to use special header nor chunk metadata)
	// http://php.net/manual/en/outcontrol.configuration.php#ini.output-buffering
	
	header('Transfer-Encoding: chunked');
	header('Content-Encoding: none');
	
	// Media type
	header('Content-Type: audio/mp3');
	
	$file = 'audio.mp3';
	$handle = fopen($file, 'rb');
	
	// Send your content in chunks
	while (!feof($handle)) {
		$chunk = fread($handle, 5000);
		echo dechex(strlen($chunk)) . "\r\n";
		echo $chunk;
		echo "\r\n";
		flush();// Note: some browsers have a buffer of 4096 bytes
		usleep(200000);
	}
	// 5KB/200ms -> 25KB/s
	
	fclose($handle);
	
	// last chunk
	echo "0\r\n\r\n";
	flush();

See [Transfert encoding](Web#transfert-encoding)
