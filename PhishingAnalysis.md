# 📧 Phishing Analysis Challenge Walkthrough – Blue Team Labs Online

This is a detailed walkthrough of the **Phishing Analysis** challenge from [Blue Team Labs Online](https://blueteamlabs.online). The task simulates a real-world SOC scenario where an analyst must extract and analyze artifacts from a reported phishing email.

---

## 🧠 Scenario

> A user has forwarded a **suspicious email** to the Security Operations Center (SOC).  
>  
> Your role as an analyst is to investigate the email and its attachment to identify indicators of compromise (IOCs), potential URLs, sender details, and hidden threats.

---

## 🧰 Tools Used

| Tool              | Purpose                                 |
|-------------------|------------------------------------------|
| Mozilla Thunderbird | Visual analysis of `.eml` email file     |
| Sublime Text      | Manual inspection of raw email headers   |
| WHOIS Lookup      | Domain and IP reputation analysis        |
| URL2PNG           | Preview phishing URLs safely             |
| Virtual Machine   | Safe file execution & inspection         |

---

## 📂 Step-by-Step Walkthrough

> ⚠️ **Note:** Always open suspicious email files in a **VM or sandbox** environment.

---

### 1️⃣ Who is the primary recipient of this email?

- Open the `.eml` file in **Sublime Text**
- Use `CTRL+F` to search for the `"To:"` field

**✅ Answer**: `kinnar1975@yahoo.co.uk`

---

### 2️⃣ What is the subject of this email?

- Look for the `"Subject:"` field

**✅ Answer**: `Undeliverable: Website contact form submission`

---

### 3️⃣ What is the date and time the email was sent?

- Locate the `"Date:"` field

**✅ Answer**: `18 March 2021 04:14`

---

### 4️⃣ What is the originating IP?

- Search for `"X-Sender-IP"` or look in the `"Received"` headers

**✅ Answer**: `103.9.171.10`

---

### 5️⃣ Perform reverse DNS on the IP. What is the resolved host?

- Use [DomainTools WHOIS](https://whois.domaintools.com)
- Enter `103.9.171.10`

**✅ Answer**: `c5s2–1e-syd.hosting-services.net.au`

---

### 6️⃣ What is the name of the attached file?

- Open the email in **Thunderbird**
- Scroll to the bottom where attachments are shown

**✅ Answer**: `Website contact form submission.eml`

---

### 7️⃣ What URL is found inside the attachment?

You can extract this in two ways:

**A. In Thunderbird:**  
Scroll through the message content  
**B. In Sublime Text:**  
Search for `http` or `https`

**✅ Answer**:  
https://35000usdperwwekpodf.blogspot.sg?p=9swg
https://35000usdperwwekpodf.blogspot.co.il?o=0hnd
---

### 8️⃣ What service is this webpage hosted on?

- Analyze the domain in the URLs above

**✅ Answer**: `Blogspot`

---

### 9️⃣ What is the heading text on this page using URL2PNG?

- Go to [URL2PNG](https://www.url2png.com/)
- Paste in the phishing URL

**✅ Answer**: `Blog has been removed`

---

## 🏁 Summary

| Question                                | Answer                                              |
|-----------------------------------------|-----------------------------------------------------|
| Primary Recipient                       | `kinnar1975@yahoo.co.uk`                           |
| Subject                                 | `Undeliverable: Website contact form submission`   |
| Date Sent                               | `18 March 2021 04:14`                              |
| Originating IP                          | `103.9.171.10`                                     |
| Resolved Host                           | `c5s2–1e-syd.hosting-services.net.au`              |
| Attachment Name                         | `Website contact form submission.eml`              |
| URL in Attachment                       | See above (Blogspot-hosted links)                  |
| Hosting Service                         | `Blogspot`                                         |
| Page Title (via URL2PNG)                | `Blog has been removed`                            |

---

## 🧠 Lessons Learned

- Always examine full **email headers** for sender info and originating IPs.
- Use **VMs or isolated environments** when analyzing suspicious attachments.
- **Stepping through raw `.eml` files** is often more revealing than GUI tools alone.
- Use tools like **WHOIS**, **URL2PNG**, and **text editors** to investigate safely and thoroughly.

---
## ✍️ Author

**[@Abodovic2012](https://github.com/Abodovic2012)**  
SOC Analyst | Blue Teamer |  Cybersecurity

---

## ⚠️ Disclaimer

This write-up is for educational purposes only.  
Never open suspicious files on your host machine. Always use a VM or sandbox.

---

## ⭐ Support

If this guide helped you, please consider giving the repo a ⭐ star on GitHub!

---
