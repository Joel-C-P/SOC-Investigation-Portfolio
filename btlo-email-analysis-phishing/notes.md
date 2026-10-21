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

In my case I'll use bash commands to decoded:

[! What I got](screenshots/base64_decoded.png)

As I'm seeing the content I'll keep it in a txt file named email.txt

After that I note there another content 

68   │ --BOUND_600FB98E0DCEE8.49207210
69   │ Content-Type: application/pdf; name="PuzzleToCoCanDa.pdf"
70   │ Content-Transfer-Encoding: base64
71   │ Content-Disposition: attachment; filename="PuzzleToCoCanDa.pdf"

This another content appers to be in "pdf" format, after all previous evidence that I got, I not to see this in a ddeep way

Well, I take the magic number, and compare it with 

[!Magic numbers](/screenshots/magic_numbers.png)

[!Its a ZIP format](/screenshots/file_signature)

Now I only need to dacocode with base64, then keep it with de name coded.zip.

SO IMPORT, Whatever you analisys, You should use a virtual machine

After this I only need to unzip this file, and make sure there no hidden files inside this document

[!Unzip with 7z x file.zip](/screenshots/unzip.png)


