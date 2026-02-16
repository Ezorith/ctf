Today's task is "Hidden Deep Into my Heart" from the CTF "Love at First Breach" by TryHackMe. Thought I'd start with something easy today.

Let's get started!

Once the machine loads, visit the link and you'll be greeted with a secret valentine message board.

<img width="1920" height="1080" alt="01" src="https://github.com/user-attachments/assets/d1f6a4df-4605-4e8a-8662-321f2ed6bdc1" />

First thing I checked was the source HTML for any hidden data.

<img width="714" height="731" alt="02" src="https://github.com/user-attachments/assets/c6380dc3-8d53-4b11-9108-058a8acb9e82" />

I did not find anything there, so my next move was to check `robots.txt`. This is a simple text file located in the root directory that tells search engine crawlers which pages or sections of the site they are allowed or not allowed to visit.

And to my surprise, we found our first clue.

<img width="1428" height="1462" alt="03" src="https://github.com/user-attachments/assets/d73dd544-96ce-4c25-a00a-19ab6d8f63ea" />

We can see there's a disallow for one directory, and a comment which could be something useful. Type the address and you'll be greeted with this page:

<img width="1428" height="1462" alt="04" src="https://github.com/user-attachments/assets/d7bee0a2-2d02-43cb-af48-ad7445b8f3bc" />

Again, I checked the HTML source page, but found none. The wording on this page "but there's more to discover..." suggests that there's more, usually other directories on the site that's hidden to the user. For this, we can use a tool called `gobuster` (or dirbuster, whichever you fancy). It's a tool that uses a wordlist that appends words at the end of the target URL. It doesn't actually know what to look for, instead it uses the wordlist to brute-force the server for hidden directories.

<img width="1428" height="1462" alt="05" src="https://github.com/user-attachments/assets/c9e07188-4413-4ed4-ab0d-974b576ce3a3" />

Command used:
```
gobuster dir -u http://MACHINEIP:5000/cupids_secret_vault -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
```

`gobuster dir` tells the tool to run in directory or file enumeration mode.
`-u http://MACHINEIP:5000/cupids_secret_vault` is the target URL.
`-w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt` is our wordlist.

As you can see, it's already found another subdirectory called `/administrator` as it scans. We can then visit this page, and be greeted with a login page:

<img width="1428" height="1462" alt="06" src="https://github.com/user-attachments/assets/29029322-5352-47db-af1c-5402b49373cd" />

Using common login credentials, we can assume the username to be `administrator` (or just `admin` in this case) and the clue we found in the `robots.txt` file as the password.

<img width="1428" height="1462" alt="07" src="https://github.com/user-attachments/assets/d0cc913f-ca4e-40c8-b589-780933c58913" />

And voila!

<img width="1428" height="1462" alt="08" src="https://github.com/user-attachments/assets/3749ddd2-cfdf-4512-8ebe-ba2789145220" />

**Things I considered:**
- **Nmap** - This was the first thing I ran prior to running `gobuster`, but it did not work.
- **robots.txt** - This is located in the root and is easily accessible by typing it in the link. Though I think I was just lucky the CTF was this easy.
- **Web Vulnerabilities** - There were no input fields, or something for me to interact with, so vulnerabilities like SQL Injection and Cross-Site Scripting did not apply here.
