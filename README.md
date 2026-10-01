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
