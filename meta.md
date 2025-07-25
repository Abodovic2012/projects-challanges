 🕵️‍♂️ Image Metadata Challenge – Blue Team Labs Online

## 🧩 Scenario

> The attached images were posted online by a criminal on the run with the caption:  
>  
> **"I’m roaming free. You will never catch me."**  
>  
> Authorities need your help to analyze these images and track the suspect’s location. Your task is to extract metadata and use open-source intelligence techniques to answer a set of questions and ultimately pinpoint the criminal's location.

---

## 🧰 Tools Used

| Tool       | Purpose                              |
|------------|---------------------------------------|
| `exiftool` | Extract EXIF metadata from images     |
| `Yandex`   | Reverse image search for geolocation  |

---

## 📝 Challenge Questions & Answers

### 📷 1. What is the camera model? (2 points)

Using `exiftool`, we inspect the image metadata:

```bash
exiftool image1.jpg
```
✅ Answer: Canon EOS 550D

🕒 2. When was the picture taken? (2 points)
Still using exiftool, we locate the original Date/Time Original field:

✅ Answer: 2021:11:02 13:20:23

💬 3. What does the comment on the first image say? (3 points)
Scrolling through the metadata, we find a comment embedded in the image:

✅ Answer: relying on altered metadata to catch me?

📍 4. Where could the criminal be? (3 points)
This step involves reverse image searching the photos using Yandex. The first image yielded too many results, so we searched the second image instead, which returned an exact location.

✅ Answer: Kathmandu

🔚 Conclusion
This was a relatively straightforward digital forensics challenge focused on image metadata analysis and open-source geolocation. It provided a glimpse into:

How attackers may leave behind subtle traces in media files.

The power of tools like exiftool and Yandex for digital investigations.

🧠 Key Takeaway:
Steganography and metadata manipulation are increasingly common in adversarial tradecraft. Knowing how to analyze and trace hidden or embedded data is a vital skill for any blue teamer or digital investigator.

🎓 Lessons Learned
📸 Image metadata can expose device details like camera model and timestamps.

🧠 Attackers may leave misleading metadata, either to taunt defenders or mislead them.

🔍 Reverse image search is an effective OSINT technique, especially when GPS metadata is missing or stripped.

🛡️ Steganography is challenging to defend against, but awareness of such techniques improves detection chances.
## ✍️ Author

**[@Abodovic2012](https://github.com/Abodovic2012)**  
SOC Analyst | Blue Teamer | DFIR | Cybersecurity Research

---

## ⚠️ Disclaimer

This write-up is for educational purposes only.  
Never open suspicious files on your host machine. Always use a VM or sandbox.

---

## ⭐ Support

If this guide helped you, please consider giving the repo a ⭐ star on GitHub!

---
