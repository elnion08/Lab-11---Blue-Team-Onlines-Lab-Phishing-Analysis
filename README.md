# Lab-11---Blue-Team-Onlines-Lab-Phishing-Analysis

# 🛡️ Blue Team Lab: Phishing Analysis Walkthrough

> **Platform:** Blue Team Labs Online (BTLO)  
> **Category:** Phishing Analysis / Email Forensics  
> **Difficulty:** Easy / Beginner  
> **Goal:** Perform static analysis on a suspicious `.eml` file to extract Indicators of Compromise (IOCs) without executing malicious content.

---

## 📌 Lab Scenario

> *"A user has received a phishing email and forwarded it to the SOC. Can you investigate the email and attachment to collect useful artifacts?"*

As a SOC Analyst, your task is to analyze a suspected phishing email, extract metadata, trace the origin IP, identify malicious URLs, and safely visualize the phishing page — all without clicking on malicious links.

---

## 🧰 Tools Used

| Tool | Purpose |
|------|---------|
| **VSCode / Sublime Text** | View raw email headers and MIME encoding |
| **Mozilla Thunderbird** | Safely render the email for visual context |
| **DomainTools / `nslookup`** | Perform reverse DNS lookups |
| **URL2PNG** | Take safe screenshots of malicious URLs |

---

## 📁 Evidence File

- `Document.pdf` (converted from or containing the original `.eml` file)

---

## 🔍 Investigation Methodology & Answers

### 1️⃣ Email Metadata Extraction

| Question | Answer |
|----------|--------|
| **Q1: Who is the primary recipient of this email?** | `kinnar1975@yahoo.co.uk` |
| **Q2: What is the subject of this email?** | `Undeliverable: Website contact form submission` |
| **Q3: What is the date and time the email was sent?** | `18 March 2021 04:14` |

**Analysis:**  
Opened the `.eml` file in a text editor and located the `To:`, `Subject:`, and `Date:` header fields.

---

### 2️⃣ Network Forensics (Tracing the Origin)

| Question | Answer |
|----------|--------|
| **Q4: What is the Originating IP?** | `103.9.171.10` |
| **Q5: Reverse DNS resolved hostname?** | `c5s2-1e-syd.hosting-services.net.au` |

**Analysis:**  
I opened the raw `.eml` file in **Visual Studio Code (VSCode)** and used the search function (`Ctrl+F`) to look for `X-Originating-IP`. This header field is commonly added by email servers to track the original sender's IP address. I also examined the last `Received` header (the one closest to the sender) as a secondary verification method. The originating IP found was `103.9.171.10`. I then used **DomainTools** to perform a reverse DNS lookup on this IP address, which resolved to `c5s2-1e-syd.hosting-services.net.au` — revealing the attacker's hosting provider infrastructure.

---

### 3️⃣ Attachment and URL Analysis

| Question | Answer |
|----------|--------|
| **Q6: What is the name of the attached file?** | `Website contact form submission.eml` |
| **Q7: What is the URL found inside the attachment?** | `https://35000usdperwwekpodf.blogspot.sg?p=9swghttps://35000usdperwwekpodf.blogspot.co.il?o=0hnd` |
| **Q8: What service is this webpage hosted on?** | `blogspot` |

**Analysis:**  
Opened the attachment in Thunderbird and extracted the embedded URL. The domain `blogspot` indicates the phishing page was hosted on Google's free blogging platform — a common technique to bypass URL filters.

---

### 4️⃣ Safe Visualization (URL2PNG)

| Question | Answer |
|----------|--------|
| **Q9: Using URL2PNG, what is the heading text on this page?** | `Blog has been removed` |

**Analysis:**  
Submitted the extracted URL to URL2PNG instead of visiting it directly. The screenshot showed that the phishing page had already been taken down.

---

## 📊 Indicators of Compromise (IOCs)

| Type | Value |
|------|-------|
| 📧 Recipient Email | `kinnar1975@yahoo.co.uk` |
| 📝 Subject Line | `Undeliverable: Website contact form submission` |
| 🌐 Originating IP | `103.9.171.10` |
| 🖥️ Reverse DNS Hostname | `c5s2-1e-syd.hosting-services.net.au` |
| 🔗 Malicious URL | `https://35000usdperwwekpodf.blogspot.sg?p=9swg` |
| 📎 Attachment Name | `Website contact form submission.eml` |
| 🧩 Hosting Platform | `blogspot.com` |

---

## ✅ Lessons Learned

- Always examine **email headers** first — they contain critical routing and authentication data.
- Use `X-Originating-IP` and `Received` headers to trace the **true source** of an email.
- Attackers exploit **trusted domains** (like `blogspot.com`) to host phishing kits and evade filters.
- **Never click suspicious links** — use tools like URL2PNG, Wget, or sandboxed browsers.
- Even "taken down" pages can reveal useful artifacts via screenshot services.

---

## 📚 References

- [Blue Team Labs Online](https://blueteamlabs.online)
- [DomainTools Reverse DNS](https://reversedns.domaintools.com)
- [URL2PNG](https://www.url2png.com)

---

## 🏁 Conclusion

This lab demonstrates the core skills of **email forensics** and **phishing analysis** — critical competencies for any SOC Analyst or Blue Team member. By safely extracting and analyzing artifacts, we can block malicious infrastructure and protect users without exposing ourselves to risk.

---
<img width="575" height="324" alt="image" src="https://github.com/user-attachments/assets/f2125771-a55f-4b4f-b769-f58839dd1726" />

