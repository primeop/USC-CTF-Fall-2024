USC CTF Fall 2024 Write-Up (Forensics Category)
This repository contains detailed write-ups for the Forensics challenges solved during the USC CTF Fall 2024. Each solution includes a description of the approach, the steps taken, and the tools used.

Forensics Category
WeirdTraffic
Challenge Description: I was provided with a .pcapng file.

Solution:

Step 1: Running strings on the .pcapng file helped quickly identify the flag embedded in the output, as it was not obscured by any encryption or obfuscation.
Flag:

CYBORG{flag_example}
Think Twice
Description: “Think twice before you drive to the EXIT(F)!!!”

Solution:

Step 1: The provided file was an image, and the description hinted at examining its metadata.
Metadata Extraction: Using exiftool, I reviewed the image's metadata.
Analyzing Software Field: The Software field contained a suspicious string in Base64. Decoding it revealed a second Base64 string: Q3liMHJne01jQ2FydGh5fSA=.
Decoding the Flag: Decoding the second Base64 string yielded the flag.
Flag:

Cyb0rg{McCarthy}
Pineapple
Challenge Description: A .pcapng file with suspected HTTP traffic was provided.

Solution:

Traffic Analysis: I used Wireshark to analyze the file and noted a high volume of HTTP requests.

Python Script with Scapy: I wrote a script to filter DNS, TLS, TCP, and HTTP packets for easier inspection. Below is the Python code used to extract and analyze the relevant traffic:

from scapy.all import TCP, IP, Raw, rdpcap

pcap_file = "pineapple.pcapng" 
packets = rdpcap(pcap_file)

for packet in packets:
    if packet.haslayer('DNS') and packet.getlayer('DNS').qr == 0:
        dns_request = packet.getlayer('DNS').qd.qname.decode()
        print(f"DNS Request: {dns_request}")
    elif packet.haslayer('TCP') and packet.haslayer('Raw'):
        raw_data = bytes(packet['Raw'].load)
        if b'\x16\x03' in raw_data[:2]:
            # TLS Record analysis here
            pass
        else:
            print(f"HTTP Request: {raw_data}")
File Extraction: I observed an HTTP GET request to /plans which retrieved a zip file. Using another Python script, I reassembled the zip file.

def extract_7zip_from_pcapng(pcapng_file, output_file):
    # Extracts zip file from pcap
Password Search: After extracting the zip, I searched through POST requests for any password hints. The script found conjoined_TRIANGLES as the password, which unlocked the zip file and revealed an image containing the flag.

Flag:

CYBORG{extracted_flag_here}
Computer Has Virus
Challenge Description: I was provided with an .eml email file.

Solution:

Inspecting the Email: Opening the .eml file in a text editor revealed an attached Base64-encoded executable.

Decoding the Executable: I converted the Base64 string into an .exe file and used strings on the executable to review its contents.

Decompressing Data: I found a compressed Base64 variable (compressed) within the file. Using the following Python script, I decoded and decompressed the data, which yielded the flag:

import base64
import gzip
from io import BytesIO

compressed = "H4sIAAAAAAAA/1TNQWvyQBDG8Xs+xRg..."
decoded_data = base64.b64decode(compressed)
with gzip.GzipFile(fileobj=BytesIO(decoded_data)) as f:
    decompressed_data = f.read()

print(decompressed_data.decode('utf-8'))
Flag:

CYBORG{decompressed_flag_here}
Each solution in this repository demonstrates methodical problem-solving and a combination of network analysis, scripting, and forensic tools to uncover hidden information and retrieve flags.






