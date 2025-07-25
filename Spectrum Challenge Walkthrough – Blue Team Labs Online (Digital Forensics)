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
