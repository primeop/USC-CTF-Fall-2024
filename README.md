# USC-CTF-Fall-2024
Writeups for USC CTF
This year’s event will feature a classic Jeopardy-style format, offering challenges across a variety of categories, including Cryptography, Forensics, OSINT, Reverse Engineering, Pwn, Web, and Miscellaneous, with difficulties ranging from beginner to expert levels. Open to participants of all skill levels, the competition welcomes everyone from first-time players to seasoned CTF veterans. Competitors can join either online or in person, making the event accessible to all.

![image](https://github.com/user-attachments/assets/4376c0b1-0e67-40c0-b854-98cec2d68a58)
 
Event Details:

Dates:
Start: Friday, November 1, 8:00 PM PDT
End: Sunday, November 3, 8:00 PM PST
Location:
Online: USC CTF Platform
In-Person: USC Campus
For more details and updates, visit the CTFTime event page and join the community on Discord.

My Results: Proud to have achieved 2nd place among USC students in a fiercely competitive field!


![image](https://github.com/user-attachments/assets/b90a26a3-4d16-47d8-9ea1-3bf7bf2e5173)

This challenge provides an overview of the CTF details and includes a flag.txt file, which contains the flag in plain text.

**CYBORG{lets_go}**

Beginner Category
Colors (Crypto)
![image](https://github.com/user-attachments/assets/4e265c9c-68c1-4a60-bc48-d241a9c7983d)

In this challenge, we received a message.txt file containing the following encoded string:
MzAgMzEgMzAgMzAgMzAgMzAgMzEgMzEgMjAgMzAgMzEgMzAgMzEgMzEgMzAgMzAgMzEgMjAgMzAgMzEgMzAgMzAgMzAgMzAgMzEgMzAgMjAgMzAgMzEgMzAgMzAgMzEgMzEgMzEgMzEgMjAgMzAgMzEgMzAgMzEgMzAgMzAgMzEgMzAgMjAgMzAgMzEgMzAgMzAgMzAgMzEgMzEgMzEgMjAgMzAgMzEgMzEgMzEgMzEgMzAgMzEgMzEgMjAgMzAgMzEgMzEgMzEgMzAgMzEgMzAgMzAgMjAgMzAgMzEgMzAgMzEgMzAgMzAgMzEgMzAgMjAgMzAgMzAgMzEgMzEgMzAgMzAgMzAgMzAgMjAgMzAgMzEgMzEgMzAgMzEgMzAgMzEgMzAgMjAgMzAgMzEgMzEgMzAgMzAgMzAgMzAgMzEgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzEgMzAgMjAgMzAgMzEgMzEgMzEgMzAgMzAgMzEgMzEgMjAgMzAgMzEgMzAgMzEgMzEgMzEgMzEgMzEgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzAgMzAgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzEgMzEgMjAgMzAgMzEgMzEgMzEgMzAgMzEgMzEgMzAgMjAgMzAgMzEgMzEgMzAgMzAgMzEgMzAgMzEgMjAgMzAgMzEgMzAgMzEgMzEgMzEgMzEgMzEgMjAgMzAgMzEgMzAgMzAgMzAgMzAgMzEgMzEgMjAgMzAgMzAgMzEgMzEgMzAgMzEgMzAgMzAgMjAgMzAgMzEgMzEgMzEgMzAgMzAgMzEgMzAgMjAgMzAgMzEgMzEgMzAgMzAgMzEgMzAgMzAgMjAgMzAgMzEgMzEgMzAgMzEgMzAgMzAgMzEgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzEgMzAgMjAgMzAgMzEgMzEgMzAgMzAgMzAgMzAgMzEgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzAgMzAgMjAgMzAgMzEgMzAgMzEgMzEgMzEgMzEgMzEgMjAgMzAgMzEgMzAgMzAgMzAgMzAgMzAgMzAgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzEgMzAgMjAgMzAgMzEgMzEgMzAgMzAgMzEgMzAgMzAgMjAgMzAgMzEgMzAgMzEgMzEgMzEgMzEgMzEgMjAgMzAgMzEgMzAgMzAgMzAgMzEgMzEgMzEgMjAgMzAgMzAgMzEgMzEgMzAgMzAgMzAgMzAgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzAgMzAgMjAgMzAgMzEgMzEgMzAgMzAgMzEgMzAgMzAgMjAgMzAgMzEgMzEgMzEgMzEgMzEgMzAgMzE=

Multi-layered Encoding Solution
To decode the provided text, I used CyberChef. I started by pasting in the encoded text, where the first layer was Base64. After decoding from Base64, the output appeared in Hex format. Decoding the Hex revealed a final layer in Binary, which CyberChef then converted to plaintext, unveiling the hidden message.

Tools and Approach:
Tool Used: CyberChef
Decoding Steps: Base64 -> Hex -> Binary -> Plaintext
