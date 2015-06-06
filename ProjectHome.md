<p><b>This plugin is a number formatting and parsing plugin for jQuery.</b></p>

<p>
<b>Current Release: 1.2.4</b> [2013-10-22] Requires jQuery (1.x) and jshashtable (2.x or 3.0)<br>
</p>

<p>
<i>Thanks to all the contributions for defects and enhancements, I have more time these days to address them.</i><br />My time now will be focussed more on defects here and a rewrite hosted on github that supports more features and works with plain javascript as well as jQuery (<a href='https://github.com/andrewgp/jsNumberFormatter'>https://github.com/andrewgp/jsNumberFormatter</a>) _<br>
</p>_

<p>
Number formatting is likely familiar to anyone who's worked with server-side code like Java or PHP and who has worked with internationalization. People who aren't stuck in the US-centric frame of mind can quickly point out that people in other parts of the world don't format their numbers in the same way as Americans. For example, a number that we would write in the US as "1,250,500.75" would be written differently in different countries: "1.250.500,75" in Germany, "1 250 500,75" in France, and "1'250'500.75" in Switzerland, and "125,0500.75" in Japan. The number is exactly the same, but it's just written using a different format when presented to users of the web application.<br>
</p>

<p>
I've been working during the 1.2 rewrite to separate the parsing and formatting more. So your now required to parse the text first into a js number, before formatting it back into text. This should hopefully give more control over the process and allow more flexibility of use.<br>
</p>

<p>
<b>Example #1</b><br />
Here's a typical use case for what I'm describing. You have an input field in your web application that asks a person for their salary. In the US, the user can type in a varied forms of input - "$65000", "65,000", "65000", "65,000.00". All these numbers are exactly the same, but we want to control how these numbers look on the screen.<br>
<br>
<p>Here's an example of how you'd use this plugin.<br>
<pre><code>$("#salary").blur(function(){<br>
   $(this).parseNumber({format:"#,###.00", locale:"us"});<br>
   $(this).formatNumber({format:"#,###.00", locale:"us"});<br>
});<br>
</code></pre>
This code will ensure that any text in the "salary" textfield will be formatted properly when the user tabs out of it.  For example, the user can enter "65000", "65,000", "65000.00" and when they leave the field, the field will automatically format the number to be "65,000.00".<br>
</p>

<p>
<b>Example #2</b><br />
Say we have 2 text input fields, one accepts US format numbers, the other unformatted numbers only. When the user loses focus on the formatted input it parses the data and puts the number into the second input, when the user loses focus on the second input it formats the number back to the first input box. This is just to demonstrate how to parse and format values.<br>
<br />
<pre><code>$("#salaryUS").blur(function(){<br>
   // take US format text into std number format<br>
   var number = $(this).parseNumber({format:"#,###.00", locale:"us"}, false);<br>
   // write the number out<br>
   $("#salaryUnformatted").val(number);<br>
		<br>
   // OR<br>
		<br>
   number = $(this).val();<br>
   number = $.parseNumber(number, {format:"#,###.00", locale:"us"});<br>
   $("#salaryUnformatted").val(number);<br>
});<br>
	<br>
$("#salaryUnformatted").blur(function(){<br>
   // take the unformatted text and format into US number format<br>
   $("#salaryUS").val($(this).val());<br>
   $("#salaryUS").formatNumber({format:"#,###.00", locale:"us"});<br>
		<br>
   // OR<br>
		<br>
   var number = $(this).val();<br>
   number = $.formatNumber(number, {format:"#,###.00", locale:"us"});<br>
   $("#salaryUS").val(number);<br>
});<br>
</code></pre>
</p>

<p>
Right now there are dozens of countries supported.  The syntax for the formatting follows that in the Java DecimalFormatter, so that you can provide a reliable format string on the server and client.<br>
</p>

<h2>Syntax</h2>
The syntax for the formatting is:<br>
<ul><li>0 = Digit<br>
</li><li># = Digit, zero shows as absent<br>
</li><li>. = Decimal separator<br>
</li><li>- = Negative sign<br>
</li><li>, = Grouping Separator<br>
</li><li>% = Percent (multiplies number by 100)</li></ul>

<h2>Supported Locales</h2>
Here are the supported Locales.  They were chosen because a) they are offered by the Java DecimalFormatter or b) I just felt that they were interesting and wanted to include them.<br>
<ul><li>United States -> "us"<br>
</li><li>Arab Emirates -> "ae"<br>
</li><li>Egypt -> "eg"<br>
</li><li>Israel -> "il"<br>
</li><li>Japan -> "jp"<br>
</li><li>South Korea -> "kr"<br>
</li><li>Thailand -> "th"<br>
</li><li>China -> "cn"<br>
</li><li>Hong Kong -> "hk"<br>
</li><li>Taiwan -> "tw"<br>
</li><li>Australia -> "au"<br>
</li><li>Canada -> "ca"<br>
</li><li>Great Britain -> "gb"<br>
</li><li>India -> "in"<br>
</li><li>Germany -> "de"<br>
</li><li>Vietnam -> "vn"<br>
</li><li>Spain -> "es"<br>
</li><li>Denmark -> "dk"<br>
</li><li>Austria -> "at"<br>
</li><li>Greece -> "gr"<br>
</li><li>Brazil -> "br"<br>
</li><li>Czech -> "cz"<br>
</li><li>France  -> "fr"<br>
</li><li>Finland -> "fi"<br>
</li><li>Russia -> "ru"<br>
</li><li>Sweden -> "se"<br>
</li><li>Switzerland -> "ch"</li></ul>

<h2>Mentions</h2>

Thanks to the excellent <a href='http://www.timdown.co.uk/jshashtable/'>jshashtable</a> project, which is currently a requirement of the script, I may decide to support a standalone version too at some point.<br>
<br>
<h2>SNAPSHOTS</h2>
Available from the svn repo (<a href='https://jquery-numberformatter.googlecode.com/svn/trunk'>https://jquery-numberformatter.googlecode.com/svn/trunk</a>), please take care to read the notes in the main js file, may be unstable or incomplete.<br>
<br>
<h2>1.2.4</h2>
<ul><li>Issues Fixed:<br>
<ul><li>56 - Fixed NaN check slightly<br>
</li><li>66 - Fixed percentage parsing for no decimal points<br>
</li><li>69 - Fixed decimal parsing for long format masks<br>
</li><li>75 - Fixed variable declaration/scope in init()</li></ul></li></ul>

<ul><li>Enhancements<br>
<ul><li>51 - Added options to stop auto detection of percentages (parsing and formatting) to give more control<br>
</li><li>55 - Added override options for group, decimal and negative signs (to reduce need to add custom locales)<br>
</li><li>61 - Added strict option to allow parsing to reject really funny strings<br>
</li><li>71 - Added Bulgarian locale<br>
</li><li>72 - Added Norwegian locale<br>
</li><li>73 - Added support for parsing with prefixes that include 'allowed' chars, should give greater flexibility</li></ul></li></ul>

<h2>1.2.3</h2>
<ul><li>Issues Fixed:<br>
<ul><li>43 - Removed usage of $ inside plugin<br>
</li><li>44 - Fixed left padding for formatting<br>
</li><li>47 - Fixed percentage rounding for parsing method<br>
</li><li>50 - Added 'isPercentage' option to parsing, to force percentage handling<br>
</li><li>53 - Made locale a bit more strict and allowed it to extract country code from a java like locale string (en_NL etc.)</li></ul></li></ul>

<h2>1.2.2</h2>
<ul><li>All outstanding verified bugs resolved</li></ul>

<h2>1.2.1</h2>
<ul><li>All outstanding verified issues resolved</li></ul>

<h2>1.2</h2>
New/Fixes<br>
<ul><li>Fixed a number of issues left over from 1.1.x<br>
</li><li>Rewritten the bulk of the code<br>
</li><li>Separated out parsing and formatting<br>
</li><li>Rounding options when formatting<br>
Known issues<br>
</li><li>Parsing rounding not supported<br>
</li><li>Parsing decimal place precision not working currently</li></ul>

<h2>New in Version 1.1.2</h2>
1 major bug fixes, 1 minor fix, and 1 new feature included in this release.<br>
The bug fixes are<br>
<ul><li>Numbers that have more than one group separator in the pre-formatted number (e.g. 1,233,400) weren't formatted correctly, and threw an error (NaN) when they were formatted.<br>
</li><li>Numbers with many decimals (e.g. 12.2345) when formatted with a format like this "#.##" were formatted into "12.2".  Now, they will be formatted into "12.23".  The proper way to do this would be to use the format "#.00", but now this alternative will also be supported<br>
</li><li>There is a new option called "decimalSeparatorAlwaysShown" (defaults to 'false'), which you can use to override whether a decimal separator is always shown in numbers like 233, whether it should be formatted to "233" or "233.".<br>
<i>many thanks to advweb.nanasi.jp and scdietrich for their bug fixes</i></li></ul>

<h2>New in Version 1.1</h2>

I recommend everyone to move to the 1.1 version of the plugin, as it is more stable and contains more features.<br>
<br>
<ul><li>Added support for using the "%" character in formats.  This will convert all numbers into their percent equivalent by multiplying them by 100.  For example, if a user enters "0.125" and you specify a format of "#.0%", the text will be formatted to "12.5%"<br>
</li><li>Added support for prefixes and suffixes that aren't part of the syntax.  This is especially beneficial for currencies.  For example, if a user enters "12.34" and you specify a format of "$#.##", the text will be formatted to "$12.34".  Also, if you specify something like "#.## JPY", the same text will be formatted to "12.34 JPY".<br>
</li><li>Added special exceptions for negative numbers to appear <i>before</i> any prefixes.  So, for example, you can specify a format of "-$#.##" to display a formatted text of "-$12.34", or "$-#.##" to display a formatted text of "$-12.34", depending on your needs.<br>
</li><li>The parse() function has been updated with all the above fixes as well.<br>
</li><li>Various bug fixes that popped up from expanded testing