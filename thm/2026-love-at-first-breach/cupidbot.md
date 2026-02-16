Today's task is "CupidBot" from the CTF "Love at First Breach" by TryHackMe.
<br>
<br>
Let's get started!
<br>
<br>
Open the Agent to start, and you'll be greeted with a chat interface.
<br>
<br>
<img width="1436" height="786" alt="Screenshot 2026-02-16 at 22 04 09" src="https://github.com/user-attachments/assets/fb2c1488-5e66-4153-b5a8-7fe71ebfbf0a" />
<br>
<br>
I sent "hello" as test message, to see what the bot responds with. It returned a verification code, but unsure if this is relevant.
<br>
<br>
<img width="714" height="731" alt="Screenshot 2026-02-16 at 22 00 33" src="https://github.com/user-attachments/assets/76af85df-8842-4f8d-ba2a-f50c7866d588" />
<br>
<br>
My next message was outright ask the bot to list hidden flags or environment variables, and to my surprise, it returned the flags I asked for.
<br>
<br>
<img width="714" height="731" alt="Screenshot 2026-02-16 at 22 02 16" src="https://github.com/user-attachments/assets/ed89cda9-69c4-43ae-995d-9a1260941f9f" />
<br>
<br>
Yes, it was _that_ easy.
