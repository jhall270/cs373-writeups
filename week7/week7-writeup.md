## Week 7

This week covered web security. The majority of malware is delivered over the web.  Historically, web security has changed rapidly.  There have been certain types of attacks which were commonly used at certain points in time and the browsers or plug-ins would eventually develop security measures to block these types of attacks.  On the other hand, browsers are continually adding new technologies such as html5 and AJAX requests, and when new technologies are added to the browser, these provide new means for attacks to be developed.

#### User Level Attacks

These attacks often involve social engineering.  Examples of this include fake websites designed to steal logins, fake antivirus popups, obscured urls.
These social engineering attacks are designed to get the user to click on something they should not click on or enter information they should not be entering.

The Javascript language provides a number of means to obscure malware, such as encoding and packing.  Malware authors will exploit these tools to make the javascript files difficult to understand and conceal their actions.


#### SQL Injection

SQL Injection is a common attack technique for websites.  Most websites are storing data in databases and usually these are sql databases.  These webpages often have means to enter input such as a form text or the url which then is run against the database.  If the developer does not clean the input properly the attacker can craft input in a manner to run queries that the developer did not intend.  This could allow the user to retrieve data from tables, use errors to gather intelligence on the system, or alter data in the database.