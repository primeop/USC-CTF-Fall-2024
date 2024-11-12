# USC-CTF-Fall-2024

This year’s event featured a classic Jeopardy-style format, offering challenges across a variety of categories, including Cryptography, Forensics, OSINT, Reverse Engineering, Pwn, Web, and Miscellaneous, with difficulties ranging from beginner to expert levels. 

![image](https://github.com/user-attachments/assets/4376c0b1-0e67-40c0-b854-98cec2d68a58)
 
Event Details:

Dates:
Start: Friday, November 1, 8:00 PM PDT
End: Sunday, November 3, 8:00 PM PST

My Results: Proud to have achieved 2nd place among USC students in this fiercely competitive CTF!


![image](https://github.com/user-attachments/assets/b90a26a3-4d16-47d8-9ea1-3bf7bf2e5173)

This challenge provides an overview of the CTF details and includes a flag.txt file, which contains the flag in plain text.

**CYBORG{lets_go}**
 Wow, sounds like you had a productive weekend with the USC Fall CTF! It’s fantastic to see such detailed write-ups for each challenge. Here's a refined version of your work that might help you share your experience more clearly:

---

## USC Fall CTF Write-up

This weekend, I competed in the USC Fall CTF. Although I couldn’t spend as much time on it as I’d have liked, I pushed through as many challenges as I could, securing 101st place out of 797 participants! 😎

### Challenges I Solved (Jump to Solutions):
- **Forensics**: weirdtraffic, think_twice, pineapple, Computer Has Virus
- **OSINT**: beer sales, TommyCam, Buildings, television
- **Cryptography**: colors, decipherium
- **Web**: iRobots
- **Reversing**: concoction
- **Miscellaneous**: Redwoods

Let’s dive into the solutions for each challenge!

---

### Forensics

#### **weirdtraffic**
- **Description**: Given a `.pcapng` file.
- **Solution**: Running `strings` on the file revealed the flag embedded within the output.

#### **think_twice**
- **Description**: The hint was "Think twice before you drive to the EXIT(F)!"
- **Solution**: I was given an image file. Using `exiftool`, I noticed a suspicious field in the metadata labeled as `Software`, which was Base64 encoded. Decoding it twice, I found the flag: `Cyb0rg{McCarthy}`.

#### **pineapple**
- **Description**: Another `.pcapng` file.
- **Solution**: Using Wireshark, I noticed HTTP requests. I then scripted in Python with Scapy to filter HTTP traffic and analyze DNS, TLS, and HTTP packets. I found a GET request for a zip file at an internal URL `/plans`. I reassembled the zip using the script below and retrieved a password-protected 7zip file.

```python
from scapy.all import TCP, IP, Raw, rdpcap
import re

def extract_7zip_from_pcapng(pcapng_file, output_file):
    packets = rdpcap(pcapng_file)
    tcp_streams = {}
    
    # Analyze packets
    for packet in packets:
        if TCP in packet and Raw in packet:
            tcp_segment = packet[TCP]
            stream_id = (packet[IP].src, packet[IP].dst, tcp_segment.sport, tcp_segment.dport)
            if stream_id not in tcp_streams:
                tcp_streams[stream_id] = b''
            tcp_streams[stream_id] += bytes(tcp_segment.payload)
            
    # Extract 7zip data
    for stream_id, stream_data in tcp_streams.items():
        match = re.search(b'Content-Type: application/x-7z-compressed\\r\\n\\r\\n(7z\\xBC\\xAF\\x27\\x1C.*)', stream_data, re.DOTALL)
        if match:
            with open(output_file, 'wb') as f:
                f.write(match.group(1).split(b'-----------------------------')[0])
            return

extract_7zip_from_pcapng("pineapple.pcapng", "output.7z")
```

After extracting the zip, I searched the HTTP POST requests and found the password `conjoined_TRIANGLES`. Once unlocked, I extracted the flag from an image within.

---

### OSINT

#### **beer sales**
- **Challenge**: "In August 2024, a lot of beer was sold in Orlando, Florida."
- **Solution**: A quick Google search led me to a PDF with the answer.

#### **TommyCam**
- **Challenge**: Find the specifications of the PC that ran the TommyCam in 1996.
- **Solution**: Using archive.org’s Wayback Machine, I accessed the 1996 USC website, locating the specs for the TommyCam’s Toshiba 5200 80386 PC.

#### **Buildings**
- **Challenge**: Match building images and acronyms to numbers.
- **Solution**: After researching each image and acronym, I reconstructed the flag by correlating each building acronym with its respective number.

---

### Cryptography

#### **colors**
- **Challenge**: Decode a sequence of numbers.
- **Solution**: The sequence looked like color codes or hex values. By translating the numbers through repeated transformations, I found the final message and flag.

---

This was a fun, challenging experience, and I learned a lot from working on each puzzle. Looking forward to the next competition! 

---

Feel free to adjust the specific code blocks, descriptions, or flags for a polished, professional presentation. Great job on the effort and problem-solving!
