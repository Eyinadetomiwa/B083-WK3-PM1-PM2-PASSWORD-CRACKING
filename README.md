# Networkwalks Cybersecurity & Ethical Hacking: Week 3 Practical Lab Documentation

This repository documents Week 3 (Project Modules 1 & 2) of the Networkwalks Cybersecurity & Ethical Hacking internship: auditing password-protected PDF files using both web-based security utilities and terminal-based tools (John the Ripper) on Kali Linux.

---

# 📌 Project Module 1: Web-Based PDF Hash Extraction & Dictionary Attack

### 🎯 Objective
Extract the cryptographic hash from the encrypted document `My-Locked-PDF2.pdf` and recover its passphrase using Networkwalks' web-based utilities to understand client-side hash extraction, candidate matching, and flag verification[cite: 2, 3].

### 🛠️ Tools Used
| Tool | Purpose |
| :--- | :--- |
| **Networkwalks Hash Calculator** | Extracts a crackable `$pdf$...` hash directly from the PDF file in-browser. |
| **Networkwalks Password Cracker** | Runs an in-browser dictionary attack against the extracted hash. |

### 🖥️ Environment
* **Platform:** Web Browser (Client-Side JavaScript)
* **Target File:** `My-Locked-PDF2.pdf`

### 📋 Steps Performed

#### Step 1: Extract Hash Signature
* Opened the Hash Calculator utility in the browser[cite: 2].
* Uploaded `My-Locked-PDF2.pdf` to parse the encryption metadata and extract the `$pdf$` format hash[cite: 2].

#### Step 2: Run the Dictionary Attack
* Copied the extracted hash into the web-based Password Cracker[cite: 2].
* Initiated the attack against candidate passwords[cite: 2].
* The tool matched candidate passphrase `good-luck`[cite: 2].

```text
[-] Trying: 369 X
[-] Trying: Abcdef X
[-] Trying: Asdfgh X
[-] Trying: Changeme X
[-] Trying: NCC1701 X
[-] Trying: Zxcvbnm X
[-] Trying: demo X
[-] Trying: doom2 X
[-] Trying: e X
[+] MATCH good-luck ✓
[cite: 2]

📸 Screenshot 1 – Password recovered successfully via web utility (good-luck)

[cite: 2]

Step 3: Unlock Document & Capture Flag
Opened the protected PDF document using the cracked password good-luck[cite: 2].

Validated file access and recorded the challenge flag.   
JPG

📸 Screenshot 2 – Captured Flag: nw{cybersecurity_flag_captured_2608}

   
JPG

✅ Module 1 Result
File	Recovered Password	Captured Flag
My-Locked-PDF2.pdf	
good-luck

[cite: 2]

nw{cybersecurity_flag_captured_2608}

 
JPG

📌 Project Module 2: Linux CLI Password Auditing with John the Ripper
🎯 Objective
Extract the encryption hash from My-Locked-PDF2.pdf in Kali Linux and audit it against standard wordlists using John the Ripper CLI (john) to evaluate weak password susceptibility in local environments.   
PNG
+ 1

🛠️ Tools Used
Tool	Purpose
pdf2john	
Parses the encrypted PDF file into a standard JTR-compatible hash signature. 
PNG

john (John the Ripper CLI)	
Audits the extracted hash using default rule-sets and wordlists (password.lst). 
PNG

🖥️ Environment
OS: Kali Linux   
PNG
+ 1

Target File: My-Locked-PDF2.pdf

   
PNG

📋 Steps Performed
Step 1: File Location & Environment Prep
Encountered a File not found error initially because the target file was located on the Desktop rather than the home directory (~).   
JPG

Relocated the file to the working directory using mv ~/Desktop/My-Locked-PDF2.pdf ~.   
PNG

📸 Screenshot 3 – File path troubleshooting and directory verification

   
JPG

Step 2: Extract the Password Hash
Ran pdf2john to parse the document encryption parameters into JTR_default_password.txt:   
PNG

Bash
pdf2john My-Locked-PDF2.pdf > JTR_default_password.txt
cat JTR_default_password.txt
   
PNG

Extracted Signature:

Plaintext
My-Locked-PDF2.pdf:$pdf$4*4*128*-1028*1*16*0853f2cde0ef15b1c0f93ed229d3b1ad*32*8f13ce5aa39ad974364d36a057da76790021446990b9e4114071a4d9104984c1*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1
   
PNG

📸 Screenshot 4 – Cryptographic hash extracted via pdf2john

   
PNG

Step 3: Audit Hash with John the Ripper CLI
Executed John the Ripper against the extracted hash file:   
PNG

Bash
john JTR_default_password.txt
   
PNG

Terminal Output:

Plaintext
Loaded 1 password hash (PDF [MD5 SHA2 RC4/AES 32/64])
Cost 1 (revision) is 4 for all loaded hashes
Will run 2 OpenMP threads
Proceeding with single, rules:Single
Proceeding with wordlist:/usr/share/john/password.lst
password1        (My-Locked-PDF2.pdf)
1g 0:00:00:03 DONE 2/3 (2026-10-01 10:07) 0.2739g/s 11302p/s 11302c/s 11302C/s 123456..green
Session completed.
   
PNG

Verified the recovered password using the --show parameter:   
PNG

Bash
john --show --format=PDF JTR_default_password.txt
   
PNG

Output:

Plaintext
My-Locked-PDF2.pdf:password1
1 password hash cracked, 0 left
   
PNG

📸 Screenshot 5 – Password successfully recovered via John the Ripper CLI (password1)

   
PNG

✅ Module 2 Result
File	Recovered Password	Audit Status
My-Locked-PDF2.pdf	
password1

 
PNG

Successfully matched against password.lst

 
PNG

🧠 Key Takeaways & Security Insights
Local Parsing vs. Server Upload: Both browser tools and CLI scripts like pdf2john extract only document security headers locally without exposing raw file content over the network.   
JPG
+ 1

Impact of Password Entropy: Dictionary words with basic increments (password1) or common phrases (good-luck) provide virtually no protection against offline verification algorithms[cite: 2, 6].

Defensive Recommendations: Ensure sensitive PDF documents employ AES-256 (Revision 6) encryption standards and passphrases with high character entropy (or certificate-based public keys) to mitigate brute-force and dictionary matching.

⚠️ Disclaimer
This lab documentation is conducted strictly for educational and auditing purposes as part of the Networkwalks Cybersecurity & Ethical Hacking training program. All activities were performed on authorized virtual machines and test files.
