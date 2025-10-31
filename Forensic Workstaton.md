# 🔍 Using SANS SIFT for Internal Incident Response & Forensics

When we must perform digital forensics internally after a security incident — prior to, or alongside, external DFIR support — we use the **SANS SIFT Workstation**.

> SIFT is a free, open-source DFIR environment built by SANS for incident responders and forensic analysts.  
> https://www.sans.org/tools/sift-workstation

This guide explains **when and how** we use SIFT, and provides links to training and cheat sheets for fast response.

---

## 🎯 When to Use SIFT

Use SIFT when:

- A host/system appears compromised.
- Evidence must be **captured, preserved, and analyzed**.
- We need repeatable forensic workflows (chain of custody, hashing, timelines, triage).
- We are conducting initial in-house IR before escalation to external DFIR resources.

Typical use cases:

- Disk image analysis (E01/raw)
- Memory forensics
- Timeline analysis (Plaso / log2timeline)
- Malware / persistence / IOCs triage
- Recover deleted or modified artifacts
- Deep inspection of logs, registry, browser artifacts, and more

---

## 🧠 Reference Material

### 📺 How-To Training Video  
Hands-on SIFT usage and workflow:  
https://www.youtube.com/watch?v=ai_7Fkv6igw&t=963s

### 📚 SANS DFIR Cheat Sheet Booklet  
Essential commands and workflows:  
https://www.sans.org/posters/sans-dfir-cheatsheet-booklet

---

## 🛠️ Getting & Installing SIFT

### ✅ Option A — Prebuilt VM (Recommended)
1. Download VM image: https://www.sans.org/tools/sift-workstation  
2. Import into VirtualBox / VMware  
3. Credentials are shown on the download page  
4. **Take a clean snapshot** before first forensic use

### ✅ Option B — Native Ubuntu Install
Install on Ubuntu 22.04+:

```bash
sudo apt-get update
sudo apt-get install -y curl
curl -s https://repo.saltproject.io/install.sh | sudo bash
sudo salt-call --local state.apply sift
