Today's task is "Hidden Deep Into my Heart" from the CTF "Love at First Breach" by TryHackMe. Thought I'd start with something easy today.

Let's get started!

Once the machine loads, visit the link and you'll be greeted with a secret valentine message board.

![[01.png]]

First thing I checked was the source HTML for any hidden data.

![[02.png]]

I did not find anything there, so my next move was to check `robots.txt`. This is a simple text file located in the root directory that tells search engine crawlers which pages or sections of the site they are allowed or not allowed to visit.

And to my surprise, we found our first clue.

![[03.png]]

We can see there's a disallow for one directory, and a comment which could be something useful. Type the address and you'll be greeted with this page:

![[04.png]]

Again, I checked the HTML source page, but found none. The wording on this page "but there's more to discover..." suggests that there's more, usually other directories on the site that's hidden to the user. For this, we can use a tool called `gobuster` (or dirbuster, whichever you fancy). It's a tool that uses a wordlist that appends words at the end of the target URL. It doesn't actually know what to look for, instead it uses the wordlist to brute-force the server for hidden directories.

![[05.png]]

Command used:
```
gobuster dir -u http://MACHINEIP:5000/cupids_secret_vault -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
```

`gobuster dir` tells the tool to run in directory or file enumeration mode.
`-u http://MACHINEIP:5000/cupids_secret_vault` is the target URL.
`-w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt` is our wordlist.

As you can see, it's already found another subdirectory called `/administrator` as it scans. We can then visit this page, and be greeted with a login page:

![[06.png]]

Using common login credentials, we can assume the username to be `administrator` (or just `admin` in this case) and the clue we found in the `robots.txt` file as the password.

![[07.png]]

And voila!

![[08.png]]

**Things I considered:**
- **Nmap** - This was the first thing I ran prior to running `gobuster`, but it did not work.
- **robots.txt** - This is located in the root and is easily accessible by typing it in the link. Though I think I was just lucky the CTF was this easy.
- **Web Vulnerabilities** - There were no input fields, or something for me to interact with, so vulnerabilities like SQL Injection and Cross-Site Scripting did not apply here.