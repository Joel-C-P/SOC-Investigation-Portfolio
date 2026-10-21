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

Inside this document I found 3 files, one of those is in "xlsx" format, for sure, I'll look for there file signatures.

[!The content](/screenshots/files.png)
[!Correct Format Files](/screenshots/files_format.png)


There is no relevant contect inside of the 2 first files, now the file with the format "xlsx" is the last

I only found irrelevant information, but in another "empty" file I change the color and found the Key of the 
machine, clearly is in base64 Format

[!CTF flag](/screenshots/hidden_ctf.png)

At the end I need it to look for the metadata of these 3 files to find the name of the author, its one flag of the laboratory

```bash

exiftool PuzzleToCoCanDa/*

perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
	LANGUAGE = (unset),
	LC_ALL = (unset),
	LC_CTYPE = (unset),
	LC_NUMERIC = (unset),
	LC_COLLATE = (unset),
	LC_TIME = (unset),
	LC_MESSAGES = (unset),
	LC_MONETARY = (unset),
	LC_ADDRESS = (unset),
	LC_IDENTIFICATION = (unset),
	LC_MEASUREMENT = (unset),
	LC_PAPER = (unset),
	LC_TELEPHONE = (unset),
	LC_NAME = (unset),
	LANG = "es_ES.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").
======== PuzzleToCoCanDa/DaughtersCrown.jpg
ExifTool Version Number         : 12.57
File Name                       : DaughtersCrown.jpg
Directory                       : PuzzleToCoCanDa
File Size                       : 19 kB
File Modification Date/Time     : 2021:01:25 15:41:00-05:00
File Access Date/Time           : 2026:10:21 10:29:50-04:00
File Inode Change Date/Time     : 2026:10:21 10:22:42-04:00
File Permissions                : -rw-rw-r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 120
Y Resolution                    : 120
Image Width                     : 822
Image Height                    : 435
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 822x435
Megapixels                      : 0.358
======== PuzzleToCoCanDa/GoodJobMajor.pdf
ExifTool Version Number         : 12.57
File Name                       : GoodJobMajor.pdf
Directory                       : PuzzleToCoCanDa
File Size                       : 28 kB
File Modification Date/Time     : 2021:01:26 10:14:22-05:00
File Access Date/Time           : 2026:10:21 10:26:46-04:00
File Inode Change Date/Time     : 2026:10:21 10:23:37-04:00
File Permissions                : -rw-rw-r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.5
Linearized                      : No
Author                          : Pestero Negeja
Producer                        : Skia/PDF m90
Page Count                      : 1
======== PuzzleToCoCanDa/Money.xlsx
ExifTool Version Number         : 12.57
File Name                       : Money.xlsx
Directory                       : PuzzleToCoCanDa
File Size                       : 17 kB
File Modification Date/Time     : 2021:01:26 09:27:30-05:00
File Access Date/Time           : 2026:10:21 07:55:13-04:00
File Inode Change Date/Time     : 2026:10:21 07:33:28-04:00
File Permissions                : -rw-rw-r--
File Type                       : XLSX
File Type Extension             : xlsx
MIME Type                       : application/vnd.openxmlformats-officedocument.spreadsheetml.sheet
Zip Required Version            : 20
Zip Bit Flag                    : 0x0808
Zip Compression                 : Deflated
Zip Modify Date                 : 2021:01:25 20:57:24
Zip CRC                         : 0x83696207
Zip Compressed Size             : 261
Zip Uncompressed Size           : 775
Zip File Name                   : xl/drawings/drawing1.xml
    3 image files read

```

The name of the author is "Pestero Negeja"
