# 🧪 Blue Team Labs Online – Spectrum Challenge Walkthrough

Welcome to the complete walkthrough for the **Spectrum** digital forensics challenge hosted on [Blue Team Labs Online](https://blueteamlabs.online). This challenge involves analyzing a USB disk image to uncover clues about a planned drug deal in London.

---

## 🧠 Scenario

> Scotland Yard intercepted intelligence about a major drug deal in London. A suspect was arrested, but only had a USB drive on them.  
> A junior analyst couldn’t find anything useful, so you're tasked with investigating further and answering:  
> **When and where is the deal supposed to happen?**

---

## 🔧 Tools Used

- `photorec` – Disk image recovery
- `steghide` – Steganography analysis
- `fcrackzip` – ZIP password cracking
- `Audacity` – Audio analysis (spectrogram)
- `exiftool` – Metadata extraction
- `rockyou.txt` – Password wordlist (bundled with Kali Linux)

---

## 🗂 Step-by-Step Walkthrough

### 📁 Step 1: Extracting the Disk Image

Move the disk image into a working directory:

```bash
file image.dd
photorec image.dd
```
Select the image file

Choose the correct partition and filesystem

Recover all files from the partition

💡 Tip: You can also use Autopsy for a GUI-based approach to extract and explore files.

🔍 Step 2: Analyzing Extracted Files
The extracted data includes:

A password-protected ZIP file

Several .jpg image files

📷 Check EXIF Metadata
Use exiftool to check for embedded metadata:
```bash
exiftool image.jpg
```
Clues found:

The term “Spectrum” (potential location hint)

A password string, likely for steganography
🔐 Step 3: Steganography on Images
Use steghide to attempt data extraction:
```bash
steghide extract -sf image.jpg -p <password>
```
➡️ No hidden data found in images.

🗜 Step 4: Crack the ZIP Archive
Use fcrackzip to brute-force the password using the rockyou.txt wordlist:
```bash
fcrackzip -v -u -D -p rockyou.txt secret.zip
```
✅ Password found: garfield

Unzip the archive:
```bash
unzip -P garfield secret.zip
```
Files extracted: Multiple .wav audio files.

🔊 Step 5: Steganography on Audio Files
Try extracting hidden content from white.wav:

bash
Copy
Edit
steghide extract -sf white.wav -p garfield
🎉 Success! A hidden .txt file is extracted.

The content appears encoded. After trying various decoders, it turns out the text is Base58 encoded.

🔓 Decode the Base58 String
Use an online Base58 decoder or script:

Decoded string:
emit 15:01:00

💡 Reversing “emit” gives “time”
Reversing “15:01:00” gives 00:10:51

✅ Meeting Time Found: 00:10:51

📍 Step 6: Finding the Location
Open white.wav in Audacity:

Load the audio file

Switch to Spectrogram view

Zoom in to reveal embedded text in the frequency spectrum

📌 Hidden GPS coordinates found in decimal format!

Paste coordinates into Google Maps to reveal the exact meeting location.

✅ Meeting Location Found

✅ Final Answers
Deal Time: 00:10:51

Deal Location: (Coordinates embedded in white.wav via spectrogram)

💡 Key Takeaways
This challenge demonstrates practical DFIR techniques:

Disk image recovery with photorec

Metadata analysis with exiftool

Steganography in both images and audio (steghide)

ZIP password cracking using fcrackzip + rockyou.txt

Spectrogram analysis in Audacity

Encoding/decoding techniques (Base58)

Quick Reference Commands
```bash

# Recover files from disk image
photorec image.dd

# View EXIF metadata
exiftool image.jpg

# Extract data with Steghide
steghide extract -sf image.jpg -p <password>

# Crack ZIP password with fcrackzip and rockyou.txt
fcrackzip -v -u -D -p rockyou.txt secret.zip

# Unzip with password
unzip -P garfield secret.zip


# View audio spectrogram (in Audacity)
# File > Import > Audio > Switch to Spectrogram view
```
 Lessons Learned – Phishing Analysis Challenge
Working through this phishing investigation revealed valuable insights into email forensics, artifact analysis, and safe investigation practices. Here’s what we learned:

🧰 Technical Lessons
Email headers contain gold: Fields like To, From, Subject, Date, and X-Sender-IP help trace the origin and intent of a phishing email.

Text editors are powerful: Tools like Sublime Text allow for deep inspection of .eml files without executing anything dangerous.

Email clients like Thunderbird give a visual overview while retaining header integrity.

Domain & IP analysis tools like WHOIS help identify infrastructure used by attackers.

URL scraping from attachments and email bodies can uncover malicious links.

Visual tools like URL2PNG help you safely preview potentially harmful webpages without visiting them directly.
## ✍️ Author

**[@Abodovic2012](https://github.com/Abodovic2012)**  
SOC Analyst | Blue Teamer | Cybersecurity Research

---

## ⚠️ Disclaimer

This write-up is for educational purposes only.  
Never open suspicious files on your host machine. Always use a VM or sandbox.

---

## ⭐ Support

If this guide helped you, please consider giving the repo a ⭐ star on GitHub!

---

