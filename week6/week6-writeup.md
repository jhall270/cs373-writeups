## Week 6, Network Security







##### Wireshark Lab

For the wireshark lab, I needed to use wireshark to analyze network traffic and try to find a message establishing a secret meeting.

At first, I started examining TCP conversations to see if anything looked suspicious.  I viewed some of the conversations in more detail which had a large amount of bytes transfered, but when I viewed the details they seemed to be mostly data from someone surfing the web, rather than two people transferring data.

![alt text](./snip1.png "Snip1")

Since this wasn't working, I went back to read the details of the challenge and it mentioned the name 'Betty'.  So, I next searched packets for the string 'Betty'.  When I eventually got the search parameters in Wireshark set up correctly, it found a match in one packet.  I then used the tool to export the http of this conversation and it was a back and forth message of a conversation between the two people.

![alt text](./snip2.png "Snip2")

This was what I was looking for, however some of the messages were encoded.  I saved the message to a file and then used the decode utility that was provided to decode this message.

![alt text](./snip3.png "Snip3")

The results showed a decoded message and showed the meeting is Wednesday at 2pm.

