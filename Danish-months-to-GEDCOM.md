# Handling Danish months convertion to GEDCOM

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
