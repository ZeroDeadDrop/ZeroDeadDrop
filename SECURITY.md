# ZeroDeadDrop Security Policy

**Last updated:** February 08, 2026

ZeroDeadDrop is a single-file, fully client-side, offline encryption tool.  
**No data ever leaves your device.** There are no servers, no telemetry, no accounts, no analytics, and no persistent storage.

## Supported Versions

Only the **latest tagged release** on GitHub is supported for security fixes.

**Recommendation:** Always use the file directly from  
https://github.com/ZeroDeadDrop/ZeroDeadDrop/raw/main/ZeroDeadDrop.html  

## Reporting a Vulnerability

The developer takes security seriously and welcome responsible disclosure.

**Please report privately at my email if possible.**

Email: **ZeroDeadDrop@gmail.com**

**What to include (the more detail, the faster we can respond):**

- Clear description of the vulnerability
- Affected version(s) and how to reproduce
- Steps to exploit (PoC encouraged, but please do **not** include real user data)
- Impact (what an attacker could achieve)
- Your name/handle (if you want credit in the fix announcement)
- Preferred contact method if follow-up is needed

We will:

- Acknowledge receipt within **14 business days**
- Provide regular status updates
- Work with you to validate and fix the issue
- Coordinate public disclosure only **after** a patch is available (usually 30–90 days depending on severity)

We follow **Coordinated Vulnerability Disclosure** principles and will credit reporters unless you prefer anonymity.

## Supported Browsers & Environments

| Browser              | Minimum Version | Notes / Security Level                     |
|----------------------|-----------------|--------------------------------------------|
| Chrome / Edge        | ≥ 88            | Full support (best performance)            |
| Firefox              | ≥ 85            | Full support (video decoys may fall back to GIF) 
| Safari               | ≥ 14            | Good support (some video decoy limitations) |  
| Tor Browser          | Latest          | Works in **Standard** and **Safer** modes (JavaScript required) |
| Mobile (Android/iOS) | Latest Chrome/Safari | Reduced decoy quality due to memory & codec limits |

I have tested mostly with Chrome and Firefox.

**Not supported / known issues:**

- Browsers without Web Crypto API (very old versions)
- “Safest” mode in Tor Browser (disables JavaScript → app does not run)
- Environments that block local file access (some corporate-managed browsers)

## Threat Model & Security Guarantees

**What ZeroDeadDrop protects against:**

- Network interception (nothing is sent over the network)
- Server compromise (there are no servers)
- Developer backdoors (single self-contained file, strict CSP)
- RAM scraping after purge (5-pass overwrite + memory pressure)
- Weak or reused passphrases (if you choose a strong one)
- Forward secrecy breaks in asymmetric mode (ephemeral keys)

**What ZeroDeadDrop does NOT protect against:**

- Compromised device / browser (keylogger, memory dump before purge)
- Weak or leaked private key / passphrase
- Social engineering (someone tricks you into revealing your key/pass)
- Physical access after files are decrypted & saved
- Side-channel attacks not mitigated by browser (timing in JS is hard)
- Future breaks in AES-256-GCM or P-384 (unlikely but possible)

**Important:** The biggest risk is almost always **user error** — weak credentials, storing decrypted files insecurely, sending manifest + bundle + passphrase over the same channel, or losing your private key.

## Cryptographic Primitives

| Primitive          | Usage                              | Notes                                      |
|--------------------|------------------------------------|--------------------------------------------|
| AES-256-GCM        | All data encryption                | Authenticated encryption, 96-bit tags      |
| PBKDF2             | Symmetric key derivation           | SHA-256 or SHA-512, 300k–10M iterations    |
| ECDH               | Asymmetric shared secret           | NIST P-384 curve, forward secrecy          |
| HKDF               | Session key derivation (asym)      | SHA-384, empty salt & info (standard)      |
| Web Crypto API     | All crypto operations              | Native browser implementation              |

No custom crypto implementations — everything uses the browser’s hardened primitives. Maybe in the future I want to try hybrid or my own but a different version.

## Data Retention & Compliance

ZeroDeadDrop **never stores, logs, collects, or transmits** any user data, keys, or content.

- There are **no servers**.
- There are **no analytics**.
- There are **no databases**.
- There is **no way** for the developer to access your encrypted material.

If we ever receive a subpoena, court order, or national security letter:  
**We have nothing to hand over** because nothing is ever sent to us.

Users are **solely responsible** for:

- Secure handling of decrypted files
- Safe storage of private keys & passphrases
- Compliance with local laws regarding encryption

## Responsible Disclosure Hall of Fame

We publicly thank security researchers who responsibly report issues (with permission):

- (none yet — be the first!)

Thank you for helping keep ZeroDeadDrop secure.

Questions or responsible disclosures → **ZeroDeadDrop@gmail.com**
