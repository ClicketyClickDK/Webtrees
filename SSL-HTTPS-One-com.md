# HTTPS / SSL on One.com

Please refere to: 
https://www.webtrees.net/index.php/en/forum/help-for-ver-1-7-9/31893-solved-switching-from-http-to-https-port-80-issue

I've cleared the SERVER_URL in `wt_site_setting` and the Login-url in the control panel.

And I've hardcoded the port in `include/session.php`:
```
	$port = Filter::server('SERVER_PORT', null, '80');
	$port = Filter::server('SERVER_PORT', null, '443');
```

If you are allowed to use .htaccess files, the following lines might help
```
  SetEnv HTTPS On
	SetEnv SERVER_PORT 443
```

Made at brute force in include/session.php aprox line 185 after:
```
// Ignore the default port.
	if ($protocol === 'http' && $port === '80' || $protocol === 'https' && $port === '443') {
		$port = '';
	} else {
		$port = ':' . $port;
	}
```
Inserted:
```
  $port = '';		Hardcoded
```
