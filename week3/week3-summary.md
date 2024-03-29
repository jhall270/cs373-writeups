
## Attack Graph

1. First Contact
    * This is the method by which malware makes contact with a user.  For example, a wordpress vulnerability could provide a means to maliciously alter a website.

2. Local Execution
    * After making contact, there is some method by which the malware is executed.  This may be some way the user is tricked into executing the file, or some autorun method.

3. Establish Presence
    * At this stage the malware spreads within the system, and possibly develops some methods for persistence and some ways to conceal itself.

4. Malicious Activity
     * This is the ultimate purpose behind the attack.  Often, it will involve collecting some type of information for financial reasons

From the perspective of Malware defense, defenses can be built in each of these stages of the attack graph and for common methods within each stage.  For example, a trusted site list can be helpful to prevent the first contact via a malicious site.  None of these are 100% effective.  Building a layered approach which targets different stages of the thread model and specific threat vectors is recommended.

### Yara

Yara is a pattern matching language which is popular with malware researchers

#### Lab 1

For the first Yara lab, I opened each sample file in fileinsight and used the strings tool to dump the strings.  Then I examined the string output and tried to identify anything that seemed common and not a system call.  I first noticed calls to \Borland\Delphi, presumably because the program is written in delphi.  I also noticed various celebrity names.  There appeared to be a 'Jenna Jam' substring in most files.  I continued searching to see if I could find anything else.  It seemed like those two items might not be great search criteria because it might flag any Delphi program or any file with 'Jenna Jam' string and there could be safe files with these.
I found that many of the files seemed to have a string 'bFQ'.  This seemed like a good search criteria, so I built my first attempt using this string.  I found that this matched all but one of the sample files, so I then added a second criteria based on a string I found in this one file.

```
rule rule1
{
    strings:
        $a = "bFQ"
        $b = "TErrorRec"

    condition:
        $a or $b

}

```

I then tested this on the Win32 folder and found that it was finding false positives.  This would not be a good rule for detecting the malware because of the false positives.

I then compared my attempt to the suggestions in the lab debrief.  The suggested example did use the 'Jenna Jam' string that I had initially identified, but ended up not using.  The example paired this string with another string and required matching on both.

Reflecting on this a bit, I was originally confused about whether I should use something like a person's name since it could theoretically cause false positives for safe files, but I think it works better if you include that type of criteria with a logical AND to another criteria.  I was looking for a single string that could identify the files, but it's probably easier to use some logical AND grouping.


#### Lab 2

The second lab's sample files all appeared to be html files, as opposed to the packed executables in the first lab.  Since they were html files, my first instinct was to scan for any executable code within the html and ignore most of the plain html.  I found that several of the files had individual javascript calls, but there didn't seem to be a common javascript for all files.  I saw that each file also appeared to have a script tag at the bottom with a "DownloaderActiveX1" string in it.  This seemed suspicious so I built my first attempt at a yara signature using this string.


```
rule lab2
{
    strings:
        $a = "DownloaderActiveX1"
    
    condition:
        $a

}


```

I found that this rule matched all but one of the samples, so I modified it with extra conditions to catch the sample I was missing


```
rule lab2v2
{
    strings:
        $a = "DownloaderActiveX1"
        $b = "DownloaderActiveX.cab"
        $c = "mwaextraedit"
    
    condition:
        $a or ($b and $c)

}


```

This detected all the samples, and had no false positives in the system32 folder

After reviewing the lab2 debrief, I realized that my yara signature, while seeming to work fine on my VM, would not be a good real-world sample.  The ActiveX strings would be common in the real-world, so it would cause false positives.  The lab solutions rely on knowing that ActiveX controls are identified by unique control numbers and doing a wildcard search for the exploited control number.  This seems to have required specific knowledge of how ActiveX works, so overall I think I had gotten as close as possible given that I knew nothing about ActiveX.



## Final Lab

I started by examining the file strings for all four files in FileInsight.  

File 068D5 appears to try to display a fake form with a number of error messages to the user and includes multiple suspicious urls.  

File 00670F, similarly appears to try to download suspicious files from the internet, and tries to run suspicious executable files.

The file starting with 4844FD appears to be a valid file. It contains a detailed description of what the file is intended to be along with copyright information.  When run, the file appears to take the actions described in the program description.

File A1874F is more highly packed and so the information available from examining the strings is limited.  Further dynamic analysis showed that this file was malware.

In summary, files 068D5, 00670F, and A1874F are malware.  File 4844FD is valid.



### Blog Post: Malware A1874F


The malware was packed and this limited static analysis.  I analyzed it by running with Cuckoo.

Cuckoo logs showed that it created a Deleteme.bat file in the \Appdata\Local\Temp directory.
![blog1](blog1.PNG)

I examined the files in this directory and found the malware had created an image file.  The image file appears to be a login form with Chinese text
![blog2](blog2.PNG)

There was also a ntshruis2.dll file created in the temp directory.  Examining this file in fileinsight showed that it was attempting to make a number of calls over the internet and many of the urls had words like ‘pay’ in them.
![blog3](blog3.png)

Based on the evidence collected, I believe that this malware may be designed to steal login information usign the fake login form and then possibly conduct some nefarious payment activity over the internet.

#### Yara Signature

The following yara signature will dectect the A1874F malware without System32 false positives

```
rule blogrule
{
    strings:
        $a = "BT2Attributes"
        $b = "cgi-bin"
    
    condition:
        $a and $b

}


```


