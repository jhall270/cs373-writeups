

### Agony Lab

I ran used cuckoo and fakenet to analyze the Agony malware.  After analyzing the resulting logs, some of the key points that I noticed were that

1. The malware is generating files in the SYSTEM32 directory with names such wship6.dll, wshqos.dll,

![alt text](./snip1.png "Snip1")

2. It also appears to be altering TCP/IP settings in the \Tcpip\Parameters\Winsock file.
3. It creates a file in a system device folder NifsPvd
4. There are lots of changes made to registry files.

5. Fakenet shows that it makes two network requests.  One involves a gmail-helper installer, the other seems to be a windows update file request.

![alt text](./snip2.png "Snip2")


The class lab debrief showed some elements that I had missed.  The Tuluka tool shows a suspicious wininit.sys file that was created in the directory where cuckoo was running.

![alt text](./snip3.png "Snip3")

This rootkit has hooked several system calls that deal with querying the file directory.  This has allowed the malware to hide the wininit.sys file from normal viewing and from anti-virus.


### 
