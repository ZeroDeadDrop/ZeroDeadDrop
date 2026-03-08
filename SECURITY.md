# ZeroDeadDrop Security Policy

**Last updated:** March 08, 2026
**Current version:** 4.1.0

ZeroDeadDrop is a single-file, fully client-side, offline encryption tool.

**No data ever leaves your device.** There are no servers, no telemetry, no accounts, no analytics, and no persistent storage.

---

## Supported Versions

Only the **latest tagged release** on GitHub is supported for security fixes.

**Recommendation:** Always use the file directly from
https://github.com/ZeroDeadDrop/ZeroDeadDrop.git

---

## Reporting a Vulnerability

The developer takes security seriously and welcomes responsible disclosure.

**Please report privately by email if possible.**

Email: **ZeroDeadDrop@gmail.com**

**What to include (the more detail, the faster I can respond):**

- Clear description of the vulnerability
- Affected version(s) and how to reproduce
- Steps to exploit (proof of concept encouraged, but please do **not** include real user data)
- Impact assessment (what an attacker could achieve)
- Your name or handle if you want credit in the fix announcement
- Preferred contact method if follow-up is needed

I will try to:

- Acknowledge receipt within **14 business days**
- Provide regular status updates
- Work with you to validate and fix the issue

---

## Supported Browsers and Environments

| Browser | Minimum Version | Notes |
|---|---|---|
| Chrome / Edge | 88 or later | Full support, best performance |
| Firefox | 85 or later | Full support, video decoys may fall back to GIF |
| Safari | 16.4 or later | Full support including compression |
| Safari (older) | 14 to 16.3 | Good support, no compression, some video decoy limits |
| Tor Browser | Latest | Works in Standard and Safer modes (JavaScript required) |
| Mobile Android / iOS | Latest Chrome or Safari | Reduced decoy quality due to memory and codec limits |

Testing has been done primarily in Chrome and Firefox.

**Not supported or known issues:**

- Browsers without Web Crypto API (very old versions)
- Safest mode in Tor Browser (disables JavaScript and the app will not run)
- Corporate managed browsers that block local file access

---

## Threat Model and Security Guarantees

**What ZeroDeadDrop protects against:**

- Network interception (nothing is sent over the network)
- Server compromise (there are no servers)
- Developer backdoors (single self-contained file with strict CSP)
- RAM scraping after purge (5-pass overwrite plus adaptive memory pressure)
- Weak or reused passphrases (if you choose a strong one)
- Forward secrecy breaks in asymmetric mode (ephemeral keys destroyed after each encryption)

**What ZeroDeadDrop does NOT protect against:**

- Compromised device or browser (keylogger, memory dump before purge completes)
- Weak or leaked private key or passphrase
- Social engineering (someone tricks you into revealing your key or passphrase)
- Physical access after files are decrypted and saved to disk
- Side-channel attacks not mitigated by the browser (timing precision in JavaScript is limited)
- Future cryptographic breaks in AES-256-GCM or P-384 (unlikely but possible)

**Important:** The biggest risk is almost always user error. Weak credentials, storing decrypted files insecurely, sending the manifest and bundle and passphrase over the same channel, or losing your private key are the most common failure points.

---

## Cryptographic Primitives

| Primitive | Usage | Notes |
|---|---|---|
| AES-256-GCM | All data encryption | Authenticated encryption, 96-bit IV per chunk |
| PBKDF2 | Symmetric key derivation | SHA-256 or SHA-512, 300k to 10M iterations, unique salt per chunk |
| ECDH P-384 | Asymmetric shared secret | NIST P-384 curve, forward secrecy via ephemeral keys |
| HKDF | Session key derivation (asymmetric) | SHA-384 |
| Web Crypto API | All crypto operations | Native browser implementation, no JavaScript crypto polyfills |

No custom cryptographic implementations. Everything uses the browser's hardened native primitives.

---

## Data Retention and Compliance

ZeroDeadDrop **never stores, logs, collects, or transmits** any user data, keys, or content.

- There are no servers
- There are no analytics
- There are no databases
- There is no way for the developer to access your encrypted material

If a subpoena, court order, or national security letter is ever received, **there is nothing to hand over** because nothing is ever sent to the developer.

Users are **solely responsible** for:

- Secure handling of decrypted files after download
- Safe storage of private keys and passphrases
- Compliance with local laws regarding encryption use and export

---

Thank you for helping keep ZeroDeadDrop secure.

Questions or responsible disclosures: **ZeroDeadDrop@gmail.com**
