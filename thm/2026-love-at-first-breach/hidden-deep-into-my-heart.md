This is a CTF writeup for: _**Hidden Deep Into my Heart**_ from the 2026 CTF "**Love at First Breach**" by TryHackMe.
<br>
<br>
Let's get started!
<br>
<br>
Once the machine loads, visit the provided link and you’ll be greeted with a secret Valentine message board.
<br>
<br>
<img width="3811" height="1792" src="https://github.com/user-attachments/assets/a6a7e040-116a-448e-990f-638d8c795a4f" />
<br>
<br>
The first thing I check is the HTML source code for any hidden data.
<br>
<br>
<img width="701" height="668" src="https://github.com/user-attachments/assets/da3af9de-3499-42dd-87dc-3a6a488aef87" />
<br>
<br>
I don’t find anything there, so my next move is to check `robots.txt`. This is a simple text file located in the website’s root directory that tells search engine crawlers which pages or sections of the site they are allowed or not allowed to visit.
<br>
<br>
Here, we find our first clue.
<br>
<br>
<img width="697" height="218" src="https://github.com/user-attachments/assets/37e0699c-eebf-4f76-859b-cdfa2aa6f4d8" />
<br>
<br>
We can see there is a disallowed directory and a comment that could be useful. If we type the address into the browser, we are greeted with this page:
<br>
<br>
<img width="700" height="669" src="https://github.com/user-attachments/assets/d3508b8f-516e-4b6d-a2fc-ec792751e606" />
<br>
<br>
Again, I check the HTML source code but find nothing. The wording on this page “_but there's more to discover..._” suggests there is more content hidden elsewhere, usually in other directories on the site that are not directly accessible to users.
<br>
<br>
I initially run an `nmap` scan, but it doesn’t work on my machine. Since we don’t need to perform a full network scan, we can use `gobuster` instead to scan for other directories.
<br>
<br>
<img width="573" height="388" src="https://github.com/user-attachments/assets/23b1a3df-67f6-425a-bde1-2f311fa3795f" />
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
<img width="699" height="666" src="https://github.com/user-attachments/assets/1fce02e0-17c4-42f6-b6dc-736d45f798ba" />
<br>
<br>
Using common login conventions, we can assume the username is `administrator` (or simply `admin` in this case), and use the clue found in the `robots.txt` file as the password.
<br>
<br>
<img width="700" height="669" src="https://github.com/user-attachments/assets/ebcce5ce-0e47-489f-9b6c-1251d7cd9600" />
<br>
<br>
And voilà! With the administrator credentials in hand, we successfully broke into "Cupid’s Secret Vault" and captured the flag. It turns out that even in the world of cybersecurity, a little bit of curiosity and the right wordlist can lead to a "perfect match."
<br>
<br>
<img width="702" height="437" src="https://github.com/user-attachments/assets/d87e9ebe-b257-448d-b851-f8fec142db2c" />
<br>
<br>
To recap the attack path:
<br>
<br>
**Recon:** Found the hidden directory clue in `robots.txt`.\
**Enumeration:** Used `gobuster` to uncover the `/administrator` login portal.\
**Exploitation:** Logged in using the credentials gathered from the initial recon phase.
<br>
<br>
Thanks to TryHackMe and the creators of the 2026 CTF for this creative Valentine-themed challenge. See you in the next one!
