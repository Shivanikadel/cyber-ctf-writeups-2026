# Sisterhood of the Travelling Packets

> Flare x SANS WiCyS Capture the Flag 2026

## Overview

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

## Investigation Path

```text
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
