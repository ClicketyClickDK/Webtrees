# Supplement for Webtrees installations

This refers to my personal experience and installation of Webtrees.

## One.com

The good people at `One.com` have some odd ideas about disrupting standard - and following their own obscure rules.

One of these is to let SSL / HTTPS use port 80 for communication - same as unencryptet HTTP. 
This breaks any application that - by default - whould use port 443 for HTTPS

> HTTPS URLs begin with "https://" and use port 443 by default,
<br>[Wikipedia](https://en.wikipedia.org/wiki/HTTPS)

### HTTPS / SSL

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
 

## Variations - in danish

Webtrees handles english months - but not local names - while creating dates. 

The Hacks for converting month names are version specific but is inserted into `includes/Webtree.js`

### 1.7.9:

Appended to function `function valid_date(v)`:

<!--
```valid_date():s=s.replace(/(JANUAR)/,"JAN");s=s.replace(/(FEBRUAR)/,"FEB");s=s.replace(/(MARTS)/,"MAR");/*s=s.replace(/(APRIL)/,"APR");*/s=s.replace(/(MAJ)/,"MAY");s=s.replace(/(JUNI)/,"JUN");s=s.replace(/(JULI)/,"JUL");/*s=s.replace(/(AUGUST)/,"AUG");s=s.replace(/(SEPTEMBER)/,"SEP");*/s=s.replace(/(OKTOBER)/,"OCT");/*s=s.replace(/(NOVEMBER)/,"NOV");s=s.replace(/(DECEMBER)/,"DEC");*/s=s.replace(/(OKT)/,"OCT");```
-->
```
s=s.replace(/(JANUAR)/,"JAN");
s=s.replace(/(FEBRUAR)/,"FEB");
s=s.replace(/(MARTS)/,"MAR");
/*s=s.replace(/(APRIL)/,"APR");     // Same as in English */
s=s.replace(/(MAJ)/,"MAY");
s=s.replace(/(JUNI)/,"JUN");
s=s.replace(/(JULI)/,"JUL");
/*s=s.replace(/(AUGUST)/,"AUG");
s=s.replace(/(SEPTEMBER)/,"SEP");   // Same as in English */
s=s.replace(/(OKTOBER)/,"OCT");
/*s=s.replace(/(NOVEMBER)/,"NOV");  // Same as in English 
s=s.replace(/(DECEMBER)/,"DEC");    // Same as in English  */
s=s.replace(/(OKT)/,"OCT");
```
### 1.7.11

```
/*2018-10-14/EBP: Danish months >>> */
datestr=datestr.replace(/(JANUAR)/,"JAN");
datestr=datestr.replace(/(FEBRUAR)/,"FEB");
datestr=datestr.replace(/(MARTS)/,"MAR");

datestr=datestr.replace(/(MAJ)/,"MAY");
datestr=datestr.replace(/(JUNI)/,"JUN");
datestr=datestr.replace(/(JULI)/,"JUL");
datestr=datestr.replace(/(OKTOBER)/,"OCT");
datestr=datestr.replace(/(OKT)/,"OCT");
/*<<< 2018-10-14/EBP: Danish months  */

/* Remove . after month */
datestr=datestr.replace(/(JAN|FEB|MAR|APR|MAY|JUN|JUL|AUG|SEP|OCT|NOV|DEC)\.?/,"$1");
``` 
