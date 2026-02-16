This is a CTF writeup for: _**Hidden Deep Into my Heart**_ from the 2026 CTF "**Love at First Breach**" by TryHackMe.
<br>
<br>
Let's get started!
<br>
<br>
Once the machine loads, visit the provided link and you’ll be greeted with a secret Valentine message board.
<br>
<br>
<img width="1920" height="1080" alt="01" src="https://github.com/user-attachments/assets/d1f6a4df-4605-4e8a-8662-321f2ed6bdc1" />
<br>
<br>
The first thing I check is the HTML source code for any hidden data.
<br>
<br>
<img width="714" height="731" alt="02" src="https://github.com/user-attachments/assets/c6380dc3-8d53-4b11-9108-058a8acb9e82" />
<br>
<br>
I don’t find anything there, so my next move is to check `robots.txt`. This is a simple text file located in the website’s root directory that tells search engine crawlers which pages or sections of the site they are allowed or not allowed to visit.
<br>
<br>
Here, we find our first clue.
<br>
<br>
<img width="1428" height="1462" alt="03" src="https://github.com/user-attachments/assets/d73dd544-96ce-4c25-a00a-19ab6d8f63ea" />
<br>
<br>
We can see there is a disallowed directory and a comment that could be useful. If we type the address into the browser, we are greeted with this page:
<br>
<br>
<img width="1428" height="1462" alt="04" src="https://github.com/user-attachments/assets/d7bee0a2-2d02-43cb-af48-ad7445b8f3bc" />
<br>
<br>
Again, I check the HTML source code but find nothing. The wording on this page “_but there's more to discover..._” suggests there is more content hidden elsewhere, usually in other directories on the site that are not directly accessible to users.
<br>
<br>
I initially run an `nmap` scan, but it doesn’t work on my machine. Since we don’t need to perform a full network scan, we can use `gobuster` instead to scan for other directories.
<br>
<br>
<img width="1428" height="1462" alt="05" src="https://github.com/user-attachments/assets/c9e07188-4413-4ed4-ab0d-974b576ce3a3" />
<br>
<br>
It doesn’t inherently know what to look for; it uses a wordlist to append words to the end of the target URL and brute-force the server for hidden directories. It then logs links that return valid HTTP responses.
<br>
<br>
Command used:
```
gobuster dir -u http://MACHINE_IP:5000/cupids_secret_vault -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
```

`gobuster dir` tells the tool to run in directory enumeration mode.\
`-u http://MACHINE_IP:5000/cupids_secret_vault` specifies the target URL.\
`-w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt` specifies the wordlist.
<br>
<br>
As you can see, it finds another subdirectory called `/administrator` during the scan. When we visit this page, we are greeted with a login form:
<br>
<br>
<img width="1428" height="1462" alt="06" src="https://github.com/user-attachments/assets/29029322-5352-47db-af1c-5402b49373cd" />
<br>
<br>
Using common login conventions, we can assume the username is `administrator` (or simply `admin` in this case), and use the clue found in the `robots.txt` file as the password.
<br>
<br>
<img width="1428" height="1462" alt="07" src="https://github.com/user-attachments/assets/d0cc913f-ca4e-40c8-b589-780933c58913" />
<br>
<br>
And voilà!
<br>
<br>
<img width="1428" height="1462" alt="08" src="https://github.com/user-attachments/assets/3749ddd2-cfdf-4512-8ebe-ba2789145220" />
