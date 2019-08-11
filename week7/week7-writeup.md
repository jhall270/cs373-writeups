## Week 7

This week covered web security. The majority of malware is delivered over the web.  Historically, web security has changed rapidly.  There have been certain types of attacks which were commonly used at certain points in time and the browsers or plug-ins would eventually develop security measures to block these types of attacks.  On the other hand, browsers are continually adding new technologies such as html5 and AJAX requests, and when new technologies are added to the browser, these provide new means for attacks to be developed.

#### User Level Attacks

* social engineering - examples of this include fake websites designed to steal logins, fake antivirus popups, obscured urls.  These social engineering attacks are designed to get the user to click on something they should not click on or enter information they should not be entering.

* phishing - examples of phishing include a fake version of a bank website or some other site designed to harvest logins.

* SEO Poisoning - Malicious actors are able to trick search engines to display malicious files based on the trends people are searching for

* Fake AV - by simulating an update or a av website, the attacker can trick the user into clicking on a link which installs malware

* homographic attack -- crafting urls which resemble valid urls using similar looking characters tricks users into clicking bad links

* Social Media attack - fake social media actors can join groups and retrieve compromising information

* Malvertising - using targeted advertising paltforms, attackers can target specific groups of users with malware included in ads

#### Defenses against user level attacks

* url domain reputation -- can indicate suspicious urls

* site certification - web certificiations should show who is the owner who registered the site.

* Education - users can be trained to prevent themselves from becoming victims



### Browser Level Attacks

There's a number of attack surfaces within the browser.

* Browser Exploits - these are malicious files which are often exploiting zero day vulnerabilities in the browser or targeting unupdated browsers with older vulnerabilities

* Script obfuscation/Script Attacks - The Javascript language provides a number of means to obscure malware, such as encoding and packing.  Malware authors will exploit these tools to make the javascript files difficult to understand and conceal their actions.

* Man-in-the-middle - These attacks intecept and modify traffic

* Clickjacking - by overlaying elements in the browser you can fool the user into clicking onto something malicious

* SQL Injection
    * SQL Injection is a common attack technique for websites.  Most websites are storing data in databases and usually these are sql databases.  These webpages often have means to enter input such as a form text or the url which then is run against the database.  If the developer does not clean the input properly the attacker can craft input in a manner to run queries that the developer did not intend.  This could allow the user to retrieve data from tables, use errors to gather intelligence on the system, or alter data in the database.

* XSS Cross-Site Scripting -- These are way to inject client-side script into other user's browsers.  This could be non-persistent such as an XSS attack which reflects a query string, or a persistent if it stores the script.


### Web Goat

With the web goat lab I was able to try out some XSS attacks.



### URL Classification

The second portion of Week 7 discussed attributes which could be used to predict the trustworthiness of urls.

* Alexa - this is a website which tracks the prevalence of domains.  The most popular domains are usually safe.  The malicious domains are often somewhere in the middle because attackers create new domains and then attempt to increase their prevalence.

* Archive.org  - this is useful for researching previous versions of pages

* IPVOID - this provides a manner to check IP blacklists.  Attackers will often create new urls, but these will point to the same malicious IP addresses.  Additional information about IPs can provide other clues.  For example, having only a single IP for a site or not having a mail server would be suspicious.

* URL shorteners - there's many url shortening services.  These can provide information such as a url being shortened to remove a parameter, which might be suspicious.

* Site Dossier - general site information such as what the site links to and what links to the site can be useful.

* Reputation Clearinghouses - there are community generated ratings available through many tools

* Web Inspector - these tools do additional scanning of a webpage such as analyzing scripts

* Virus Total - this is particularly useful if there is a file involved.  You can check the file hash for virus information.

* JWHOIS - just looking at the domain registration can be a simple way to see if there is a known malicious person involved or provide other information.


### Research Tools

* Burp Suite and Web Scarab are two examples of tools which provide proxies for analysis of web traffic.
    * Burp Suite can do spidering, this provides a way to jump from domain to domain
    * Both tools can do fuzzing - automated testing to find vulnerabilities

* PhantomJS - this is a webkit which can be used to interact with websites in a automated way.
    * Tools like PhantomJS are used in malware detection to automatically search through links and websites to find malware

* jsunpack - this unpacks javascript. It is useful for doing static analysis of javascript








