# Number Formatter jQuery Plugin

**This plugin is a number formatting and parsing plugin for jQuery.**

**Current Release: 1.2.4** [2013-10-22] Requires jQuery (1.x) and jshashtable (2.x or 3.0)

**Thanks to all the contributions for defects and enhancements, I have more time these days to address them.**

My time now will be focussed more on defects here and a rewrite hosted on github that supports more features and works with plain javascript as well as jQuery (https://github.com/andrewgp/jsNumberFormatter).


Number formatting is likely familiar to anyone who's worked with server-side code like Java or PHP and who has worked with internationalization. People who aren't stuck in the US-centric frame of mind can quickly point out that people in other parts of the world don't format their numbers in the same way as Americans. For example, a number that we would write in the US as "1,250,500.75" would be written differently in different countries: "1.250.500,75" in Germany, "1 250 500,75" in France, and "1'250'500.75" in Switzerland, and "125,0500.75" in Japan. The number is exactly the same, but it's just written using a different format when presented to users of the web application.

I've been working during the 1.2 rewrite to separate the parsing and formatting more. So your now required to parse the text first into a js number, before formatting it back into text. This should hopefully give more control over the process and allow more flexibility of use.


## Example #1

Here's a typical use case for what I'm describing. You have an input field in your web application that asks a person for their salary. In the US, the user can type in a varied forms of input - "$65000", "65,000", "65000", "65,000.00". All these numbers are exactly the same, but we want to control how these numbers look on the screen.

Here's an example of how you'd use this plugin.

```
#!javascript
$("#salary").blur(function(){

   $(this).parseNumber({format:"#,###.00", locale:"us"});

   $(this).formatNumber({format:"#,###.00", locale:"us"});

});
```

This code will ensure that any text in the "salary" textfield will be formatted properly when the user tabs out of it. For example, the user can enter "65000", "65,000", "65000.00" and when they leave the field, the field will automatically format the number to be "65,000.00".


## Example #2

Say we have 2 text input fields, one accepts US format numbers, the other unformatted numbers only. When the user loses focus on the formatted input it parses the data and puts the number into the second input, when the user loses focus on the second input it formats the number back to the first input box. This is just to demonstrate how to parse and format values.

```
#!javascript
$("#salaryUS").blur(function(){

   // take US format text into std number format

   var number = $(this).parseNumber({format:"#,###.00", locale:"us"}, false);

   // write the number out

   $("#salaryUnformatted").val(number);

   // OR

   number = $(this).val();

   number = $.parseNumber(number, {format:"#,###.00", locale:"us"});

   $("#salaryUnformatted").val(number);

});


$("#salaryUnformatted").blur(function(){

   // take the unformatted text and format into US number format

   $("#salaryUS").val($(this).val());

   $("#salaryUS").formatNumber({format:"#,###.00", locale:"us"});

   // OR

   var number = $(this).val();

   number = $.formatNumber(number, {format:"#,###.00", locale:"us"});

   $("#salaryUS").val(number);

});
```


Right now there are dozens of countries supported. The syntax for the formatting follows that in the Java DecimalFormatter, so that you can provide a reliable format string on the server and client.

## Syntax

The syntax for the formatting is:

- 0 = Digit
- # = Digit, zero shows as absent
- . = Decimal separator
- - = Negative sign
- , = Grouping Separator
- % = Percent (multiplies number by 100)


## Supported Locales

Here are the supported Locales. They were chosen because a) they are offered by the Java DecimalFormatter or b) I just felt that they were interesting and wanted to include them.

- United States -> "us"
- Arab Emirates -> "ae"
- Egypt -> "eg"
- Israel -> "il"
- Japan -> "jp"
- South Korea -> "kr"
- Thailand -> "th"
- China -> "cn"
- Hong Kong -> "hk"
- Taiwan -> "tw"
- Australia -> "au"
- Canada -> "ca"
- Great Britain -> "gb"
- India -> "in"
- Germany -> "de"
- Vietnam -> "vn"
- Spain -> "es"
- Denmark -> "dk"
- Austria -> "at"
- Greece -> "gr"
- Brazil -> "br"
- Czech -> "cz"
- France -> "fr"
- Finland -> "fi"
- Russia -> "ru"
- Sweden -> "se"
- Switzerland -> "ch"


## Mentions

Thanks to the excellent [jshashtable project](http://www.timdown.co.uk/jshashtable/), which is currently a requirement of the script, I may decide to support a standalone version too at some point.


## SNAPSHOTS

Available from the svn repo https://jquery-numberformatter.googlecode.com/svn/trunk, please take care to read the notes in the main js file, may be unstable or incomplete.


## 1.2.4

- Issues Fixed:
    - 56 - Fixed NaN check slightly
    - 66 - Fixed percentage parsing for no decimal points
    - 69 - Fixed decimal parsing for long format masks
    - 75 - Fixed variable declaration/scope in init()
- Enhancements
    - 51 - Added options to stop auto detection of percentages (parsing and formatting) to give more control
    - 55 - Added override options for group, decimal and negative signs (to reduce need to add custom locales)
    - 61 - Added strict option to allow parsing to reject really funny strings
    - 71 - Added Bulgarian locale
    - 72 - Added Norwegian locale
    - 73 - Added support for parsing with prefixes that include 'allowed' chars, should give greater flexibility


## 1.2.3

- Issues Fixed:
    - 43 - Removed usage of $ inside plugin
    - 44 - Fixed left padding for formatting
    - 47 - Fixed percentage rounding for parsing method
    - 50 - Added 'isPercentage' option to parsing, to force percentage handling
    - 53 - Made locale a bit more strict and allowed it to extract country code from a java like locale string (en_NL etc.)


## 1.2.2

- All outstanding verified bugs resolved


## 1.2.1

- All outstanding verified issues resolved


## 1.2

New/Fixes

- Fixed a number of issues left over from 1.1.x
- Rewritten the bulk of the code
- Separated out parsing and formatting
- Rounding options when formatting
- Known issues
- Parsing rounding not supported
- Parsing decimal place precision not working currently


## New in Version 1.1.2

1 major bug fixes, 1 minor fix, and 1 new feature included in this release.

The bug fixes are

- Numbers that have more than one group separator in the pre-formatted number (e.g. 1,233,400) weren't formatted correctly, and threw an error (NaN) when they were formatted.
- Numbers with many decimals (e.g. 12.2345) when formatted with a format like this "#.##" were formatted into "12.2". Now, they will be formatted into "12.23". The proper way to do this would be to use the format "#.00", but now this alternative will also be supported
- There is a new option called "decimalSeparatorAlwaysShown" (defaults to 'false'), which you can use to override whether a decimal separator is always shown in numbers like 233, whether it should be formatted to "233" or "233.".
- many thanks to advweb.nanasi.jp and scdietrich for their bug fixes


## New in Version 1.1

I recommend everyone to move to the 1.1 version of the plugin, as it is more stable and contains more features.

- Added support for using the "%" character in formats. This will convert all numbers into their percent equivalent by multiplying them by 100. For example, if a user enters "0.125" and you specify a format of "#.0%", the text will be formatted to "12.5%"
- Added support for prefixes and suffixes that aren't part of the syntax. This is especially beneficial for currencies. For example, if a user enters "12.34" and you specify a format of "$#.##", the text will be formatted to "$12.34". Also, if you specify something like "#.## JPY", the same text will be formatted to "12.34 JPY".
- Added special exceptions for negative numbers to appear before any prefixes. So, for example, you can specify a format of "-$#.##" to display a formatted text of "-$12.34", or "$-#.##" to display a formatted text of "$-12.34", depending on your needs.
- The parse() function has been updated with all the above fixes as well.
- Various bug fixes that popped up from expanded testing
