## Headers 


Instead of user any text editor, I'll use commands of Linux.

Acouple of thigs take my atenttion, I see a lot of Irregular paramenters 


[!Screenshot of parameters](screenshots/suspicius_parameters.png)

1. SPF: False | microapple.com | IP 93.99.104.210

This means there's no a match between this IP and microapple.com in SPF list 

2. Reply-To: negeja3921@pashter.com 

This got me curious, why is there a discrepancy between the senders and who it supose to recive the enswer

3. Content-Type: multipart/mixed; boundary=BOUND_600FB98E0DCEE8.49207210

This in is not suspicious, BUT, after that, we got a boundary sed for it, this is used to tell the server
when to start and stop rendering the content using a specific format

4.There is a first boundary coded in base64

--BOUND_600FB98E0DCEE8.49207210
Content-Type: text/plain; charset=utf-8
Content-Transfer-Encoding: base64

In my case I'll bash commands to decoded:

[! What I got](screenshots/base64_decoded.png)

