This is a CTF writeup for: _**CupidBot**_ from the 2026 CTF "**Love at First Breach**" by TryHackMe.
<br>
<br>
Let's get started!
<br>
<br>
Open the Agent to start, and you'll be greeted with a chat interface.
<br>
<br>
<img width="1436" height="786" src="https://github.com/user-attachments/assets/fb2c1488-5e66-4153-b5a8-7fe71ebfbf0a" />
<br>
<br>
Here, we can send a "hello" as a test message. It returns a verification code, but it's unclear whether this is relevant.
<br>
<br>
<img width="714" height="731" src="https://github.com/user-attachments/assets/76af85df-8842-4f8d-ba2a-f50c7866d588" />
<br>
<br>
My next message is a direct reuqest asking the bot to list hidden flags or environment variables. To my surprise, it returns the flags I asked for.
<br>
<br>
<img width="714" height="731" src="https://github.com/user-attachments/assets/ed89cda9-69c4-43ae-995d-9a1260941f9f" />
<br>
<br>
Yes, it's _that_ easy.
