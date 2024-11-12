# USC-CTF-Fall-2024

This year’s event featured a classic Jeopardy-style format, offering challenges across a variety of categories, including Cryptography, Forensics, OSINT, Reverse Engineering, Pwn, Web, and Miscellaneous, with difficulties ranging from beginner to expert levels. 

![image](https://github.com/user-attachments/assets/4376c0b1-0e67-40c0-b854-98cec2d68a58)

## Welcome challenge

![image](https://github.com/user-attachments/assets/b90a26a3-4d16-47d8-9ea1-3bf7bf2e5173)

This challenge provides an overview of the CTF details and includes a flag.txt file, which contains the flag in plain text.

**CYBORG{lets_go}**
 Wow, sounds like you had a productive weekend with the USC Fall CTF! It’s fantastic to see such detailed write-ups for each challenge. Here's a refined version of your work that might help you share your experience more clearly:

---

## USC Fall CTF Write-up

This weekend, I competed in the USC Fall CTF. Although I couldn’t spend as much time on it as I’d have liked, I pushed through as many challenges as I could, securing runner up amongst USC students ! 😎

### Challenges I Solved (Jump to Solutions):
- **Forensics**: weirdtraffic, think_twice, pineapple, Computer Has Virus
- **OSINT**: beer sales, TommyCam, Buildings, television
- **Cryptography**: colors, decipherium
- **Web**: iRobots
- **Reversing**: concoction
- **Miscellaneous**: Redwoods

---

Here's a refined write-up for your GitHub, formatted and explained step-by-step for each challenge in a beginner-friendly way.

---

# Beginner CTF Write-Up

This repository contains solutions to beginner-level challenges from the USC CTF Fall 2024 event. Each challenge involved different aspects of cybersecurity, including cryptography, forensics, web exploitation, and reverse engineering. Here's a breakdown of how each challenge was solved.

---

## 1. Colors (Crypto)

**Challenge Description**: We were provided with a `message.txt` file containing an encoded string.

### Solution Steps:
1. **Analyze Encoding**: The encoded string initially appeared as Base64. Using [CyberChef](https://gchq.github.io/CyberChef/), I decoded it, revealing a new encoding in Hex.
2. **Decode Hex**: The Hex output was further decoded, resulting in Binary.
3. **Decode Binary**: Finally, I converted the Binary string to reveal the plaintext message.

**Flag**: `CYBORG{tR0jans_love_C4rdinal_@nd_G0ld}`

---

## 2. Weird Traffic (Forensics)

**Challenge Description**: A `weirdtraffic.pcapng` file was given, capturing network traffic that seemed unusual. The goal was to analyze the file for hidden data.

### Solution Steps:
1. **Open in Wireshark**: I opened the `weirdtraffic.pcapng` file in Wireshark.
2. **Inspect ICMP Packets**: By carefully examining each ICMP packet, I discovered the flag embedded in the details of packet number 21.

**Flag**: `CYBORG{hping3-is-a-cool-tool}`

---

## 3. iRobots (Web)

**Challenge Description**: We were presented with a website requiring a password. The hint was in the challenge name, "iRobots."

### Solution Steps:
1. **Check /robots.txt**: Since the name hinted at "robots," I checked the `/robots.txt` file of the website. This file often contains hidden paths that are restricted or disallowed.
2. **Locate Flag**: Inside `/robots.txt`, I found a disallowed path: `/hidden/flag.txt`. Navigating to `https://usc-irobots.chals.io/hidden/flag.txt` revealed the flag in plain text.

**Flag**: `CYBORG{robots_txt_is_fun}`

---

## 4. Concoction (Reverse Engineering)

**Challenge Description**: We were given a binary file named `concoction`. The goal was to reverse-engineer it and find the flag.

### Solution Steps:
1. **Analyze in Ghidra**: I loaded the binary into [Ghidra](https://ghidra-sre.org/), a reverse engineering tool, to inspect its contents.
2. **Identify the Flag Format**: In the `main` function, I found the start of the flag (`CYBORG{RECIPE=`) in the strings section.
3. **Decode Values**: By scrolling through the main function, I found values being compared to construct the rest of the flag. Converting these values manually and entering them revealed the complete flag.

**Flag**: `CYBORG{RECIPE=7914-111100-2310-51337-42154142-9111-decompiler}`

---

### Summary

These challenges covered a variety of basic cybersecurity techniques, from decoding layered ciphers to analyzing network traffic and reverse engineering executables. This write-up details the tools and steps taken for each solution, serving as a practical guide for similar CTF challenges.

--- 

**Tools Used**:
- [CyberChef](https://gchq.github.io/CyberChef/) for decoding multiple layers.
- [Wireshark](https://www.wireshark.org/) for network traffic analysis.
- [Ghidra](https://ghidra-sre.org/) for binary analysis.
  
Each tool was invaluable in decoding, dissecting, and analyzing the challenges, offering insights into basic yet fundamental cybersecurity skills. Happy hacking!

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
