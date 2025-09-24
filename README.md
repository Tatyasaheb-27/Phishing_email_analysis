# Phishing_email_analysis
This repository contains a detailed report on identifying phishing characteristics such as spoofed domains, header anomalies, suspicious links, and social engineering techniques..

⸻

# 📧 Phishing Email Dataset

This repository contains a small, curated dataset of **phishing vs. benign email examples**.  
Each entry includes metadata (subject, sender, headers, body), a label, and a set ofME.md tailored fdescribing why an email is considered suspicious.

The dataset is meant for:
- Security research
- Machine learning model training
- Awareness & education (identifying phishing characteristics)

---

## 🏷 Schema Overview
Each email entry has the following fields:

- id: unique identifier  
- label:Here’s a REAorre’s a REA 
-e’s a README. email subject line  
- from_display: display name shown in client  
- from_addr: actual sender email address  
- reply_to: reply-to field (if different)  
- received_date: ISO 8601 timestamp  
- body_plain: plaintext body  
- attachments: list of attachment filenames/types  
- headers: relevant header info (SPF/DKIM/DMARC)  
- indicators: list of phishing characteristics (tags)  
- severity: integer 1–5  
- recommended_action: e.g., a READMEHere’s a READM delete  

---

## 🔎 Example Entry (from this repo)

### Suspicious email (`e009`)
```json
{
  "id": "e009",
  "label": "phishing",
  "subject": "Microsoft account unusual sign-in activity",
  "from_display": "Microsoft account team",
  "from_addr": "account-security-noreply@accountprotection.microsoft.c",
  "reply_to": "",
  "received_date": "2025-09-24T10:36:00Z",
  "body_plain": "Microsoft account\nVerify your account...\nReview recent activity\nThanks,\nThe Microsoft account team",
  "attachments": [],
  "headers": {
    "From": "account-security-noreply@accountprotection.microsoft.c",
    "SPF": "unknown",
    "DKIM": "unknown",
    "DMARC": "unknown"
  },
  "indicators": [
    "suspicious_domain",
    "urgent_language",
    "link_mismatch",
    "generic_salutation"
  ],
  "severity": 5,
  "recommended_action": "quarantine"
}

Indicators flagged
 • suspicious_domain → sender’s domain may not be legitimate Microsoft
 • urgent_language → uses fear/urgency (“unusual sign-in”, “blocked access”)
 • link_mismatch → “Review recent activity” button likely points to non-Microsoft domain
 • generic_salutation → does not address recipient personally

⸻

🚨 Phishing Indicators Taxonomy
 • display_name_mismatch — display name claims trusted brand but address does not match
 • suspicious_domain — typo/typosquatted or unusual TLD domain
 • link_mismatch — visible text ≠ actual hyperlink
 • urgent_language — scare tactics, urgency, “verify now”
 • attachment_exe — disguised executable
 • suspicious_attachment_zip — malicious ZIP archive
 • spoofed_brand — brand impersonation
 • replyto_mismatch — Reply-To differs from From
 • generic_salutation — “Dear user”, not personalized
 • spf_fail, dkim_fail, dmarc_fail — authentication failures

⸻

⚡ Usage
 1. Run:

python scripts/generate_dataset.py

→ generates data/examples.json and data/examples.csv.

 2. Use scripts/features.py to extract simple features (urgent words, suspicious links, domain lookalikes).
 3. Extend dataset with more samples (sanitized) while keeping the same schema.

⸻

⚠️ Disclaimer
 • No real malicious attachments or payloads are included.
 • Examples are sanitized and safe for research/educational use.
 • Always verify phishing reports in a secure environment.

⸻
