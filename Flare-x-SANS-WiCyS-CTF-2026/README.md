# Sisterhood of the Travelling Packets

> Flare x SANS WiCyS Capture the Flag 2026

## Challenge Overview

**Event:** FLARE x SANS WiCyS Capture the Flag 2026  
**Category:** Cybersecurity / CTF  
**Focus:** Reconnaissance, web investigation, threat intelligence, API enumeration and forensic analysis  
**Status:** Completed

> ⚠️ This write-up contains spoilers and challenge solutions.

---

## 1. Initial Reconnaissance

The challenge initially led to an AetherFlow-related environment containing information that appeared to have been exposed by the ransomware group **pantalones**.

The objective was not simply to download the AetherFlow leak. The exposed information provided clues that could be followed to investigate the group's infrastructure and eventually uncover the CTF flag.

The initial exposed files included:

```text
aetherflow/
├── .exfil.sh
├── api_keys_internal.yaml
├── customers.sql
└── route_algorithms_PROPRIETARY.sql
This challenge involved investigating the infrastructure of a
ransomware group known as `pantalones`.

The investigation began with a leak portal and ultimately required
following several pieces of exposed information across:

- A ransomware leak site
- AetherFlow's leaked files
- A hidden `.exfil.sh` script
- A Tor hidden service
- An exposed API
- Sequential conversation IDs
- Internal attacker communications
- Credential discovery
- An administrative panel

The final objective was to identify the flag associated with the
Sisterhood of the Travelling Packets target.

---
```
## Investigation Path

```
Pantalones Leak Site
        |
        v
AetherFlow Leak
        |
        v
AetherFlow ZIP
        |
        v
Hidden .exfil.sh
        |
        v
Panel URL + API Key
        |
        v
API Enumeration
        |
        v
Conversation Enumeration
        |
        v
Internal Crew Messages
        |
        v
Credential Discovery
        |
        v
Admin Panel
        |
        v
Sisterhood of the Travelling Packets
        |
        v
FLAG
