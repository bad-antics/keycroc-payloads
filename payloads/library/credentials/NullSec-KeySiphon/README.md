# NullSec-KeySiphon — Key Croc Intelligent Keystroke Harvester

**Author:** bad-antics (NullSec)  
**Category:** Recon / Credential Harvesting  
**Target:** Windows / macOS / Linux  
**Version:** 1.0  

## Description

Intelligent keystroke logging payload for the Hak5 Key Croc. Uses pattern-matching MATCH rules to trigger enhanced logging when credential-related input is detected. Captures passwords, API keys, WiFi credentials, SSH sessions, database logins, and cloud authentication attempts.

## Features

- **Smart MATCH Rules** — 25+ patterns for credential detection
- **Categorized Logging** — Credentials separated from general keystrokes
- **Protocol Coverage:**
  - SSH / sudo / su authentication
  - Database logins (MySQL, PostgreSQL, SMB)
  - WiFi passwords (wpa_passphrase, nmcli, netsh)
  - Cloud credentials (AWS, Azure, GCloud)
  - API keys and tokens
  - Web login forms
- **Silent Operation** — No visible indicators to the user
- **Optional Active Recon** — Idle-triggered WiFi credential extraction

## MATCH Patterns

| Category | Patterns |
|----------|----------|
| System Auth | `sudo`, `su -`, `passwd`, `runas /user` |
| Remote Access | `ssh`, `smbclient`, `net use` |
| Databases | `mysql -u`, `psql -U` |
| Web Login | `password`, `login`, `username` |
| WiFi | `wifi`, `wpa_passphrase`, `nmcli.*password`, `netsh.*wlan` |
| Cloud/API | `aws configure`, `az login`, `gcloud auth`, `*TOKEN`, `*KEY`, `*SECRET`, `Bearer` |

## LED States

| LED          | Meaning                      |
|--------------|------------------------------|
| Green Solid  | Armed and listening          |
| Blue Blink   | Credential pattern detected  |
| Magenta      | Saving loot                  |
| Green Blink  | Loot saved successfully      |

## Output

Loot saved to `/root/loot/keysiphon/`:

```
keysiphon/
├── credentials.txt   # Matched credential patterns
├── keylog.txt        # Full keystroke log
├── summary.txt       # Session summary
├── wifi_keys.txt     # Extracted WiFi passwords
└── urls.txt          # Captured URLs
```

## Installation

1. Connect Key Croc to computer via USB
2. Access Key Croc storage (arming mode)
3. Copy `payload.txt` to `/root/payloads/`
4. Safely eject and reconnect inline (between keyboard and computer)

## Configuration

Edit MATCH rules in `payload.txt` to add custom patterns:

```bash
# Add your own triggers
MATCH my_custom_pattern
MATCH secret_project_name
```

## Requirements

- Hak5 Key Croc
- Target must be using a USB keyboard through the Key Croc

## Legal

For authorized security testing only. Keystroke logging without consent is illegal in most jurisdictions.
