# ZeroDeadDrop
**Most Recent Version:** v8  
**Last Updated:** April 12, 2026

This is **not** a messaging app.  
It is a **Digital DeadDrop Preparation Tool**. You encrypt your files locally and receive encrypted outputs that you can send through any channel you choose (USB, email, mail, anonymous upload, etc.).

A stateless, client-side, privacy-first application.  
**Zero Servers • Zero Dependencies • Zero Data Collection • Zero Knowledge of Your Data**

- Symmetric Encryption (AES-256-GCM)  
- Asymmetric Encryption (ECDH P-384)  
- Built-in Plausible Deniability  
- Realistic Decoy File Generator  
- Fully Offline

AES-256-GCM + ECDH P-384 asymmetric encryption that runs entirely in your browser using the Web Crypto API.

No accounts. No uploads. No telemetry. No trust required.  
Just open the HTML file and it works offline.

https://github.com/ZeroDeadDrop/ZeroDeadDrop.git

---

## Why You Should Actually Use It
- Per-message forward secrecy in asymmetric mode without needing Signal, PGP, or any app installation
- Give someone your public key once — they can encrypt files for you indefinitely without ever sharing a passphrase
- Strong plausible deniability (symmetric mode): the decoy password reveals innocent files; the real password reveals your actual data
- Aggressive memory sanitization — everything is wiped from RAM after 5 minutes of inactivity or when the page closes (adaptive pressure + 5-pass overwrite)
- Single HTML file (~1.15 MB) — save it, air-gap it, burn it to USB, email it, or run it from anywhere
- Works best in Chrome and Firefox (limited mobile support, with improvements planned)

---

## Core Features

| Feature                        | Symmetric (passphrase) | Asymmetric (public key) | Notes                                      |
|--------------------------------|------------------------|--------------------------|--------------------------------------------|
| AES-256-GCM                    | Yes                    | Yes                      | Per-chunk unique IV + salt                 |
| PBKDF2 key derivation          | Yes                    | No                       | 4M–20M iterations, SHA-256/SHA-512         |
| ECDH P-384                     | No                     | Yes                      | Ephemeral keys destroyed after encryption  |
| Multiple recipients            | No                     | Yes                      | Encrypt once, many can decrypt             |
| Compression (gzip)             | Yes                    | Yes                      | Applied before encryption                  |
| Chunked processing             | Yes                    | Yes                      | Large-file friendly (4 MB max per chunk)   |
| Manifest + bundle system       | Yes                    | Yes                      | Auto-split for very large payloads         |
| Plausible deniability / decoys | Yes                    | No                       | Hidden volume + realistic fake files       |
| Memory sanitization            | Yes                    | Yes                      | 8–32 MB adaptive pressure + 5-pass wipe    |
| Auto-purge after inactivity    | Yes                    | Yes                      | 5 minutes default                          |
| CSP                            | Partial                | Partial                  | `unsafe-inline` required (single-file)     |
| Offline                        | Yes                    | Yes                      | No network calls ever                      |

---

## A Note on Plausible Deniability
In Hidden Volume mode, the app produces a single binary container with two independently encrypted volumes. These volumes are placed at password-derived positions inside a 4 MB noise header. Each volume uses its own password-derived key and a unique random salt.

Entering the **decoy password** reveals only the innocent decoy files.  
Entering the **real password** reveals only your actual sensitive files.  

Neither password can derive the other volume’s key. A forensic examiner can recognize the file as a ZeroDeadDrop container by its structure, but cannot access either volume without the correct password.

---

## Quick Start (2 minutes)

### As Receiver (people will send you encrypted files)
1. Open `ZeroDeadDrop.html`
2. Click **Generate Asymmetric Keypair**
3. Save your **private key** somewhere very secure (offline storage or password manager)
4. Share your **public key** with anyone who should be able to send you files

You only need to do this once.

### As Sender
**Asymmetric mode (recommended — no passphrase sharing)**
1. Paste the receiver’s public key
2. Enable Asymmetric Mode
3. Optionally add more recipients
4. Add your files or text and click **Start Encryption**
5. Send the resulting manifest and bundle(s) via any channel (even insecure ones)

**Symmetric mode (classic passphrase)**
1. Enter a strong passphrase (16+ characters recommended)
2. Add your files or text and click **Start Encryption**
3. Send the manifest, bundle(s), and passphrase via **separate channels**

### Decrypt (for receiver)
1. Open the same HTML file
2. Import the manifest and bundle(s)
3. Paste your private key (asymmetric) or passphrase (symmetric)
4. Click Decrypt and download your files

---

## Security Posture (April 2026)
✅ Strong primitives (Web Crypto AES-GCM + ECDH P-384)  
✅ Per-message forward secrecy in asymmetric mode via ephemeral keys  
✅ Aggressive memory sanitization and auto-purge  
✅ No external dependencies or network calls ever  
✅ Hidden volume offsets derived from password + per-container random salt  

⚠️ CSP allows `unsafe-inline` (unavoidable in a single-file app; no external script or style exfiltration possible)  
⚠️ Not formally audited yet  
⚠️ Decoy generator can be fingerprinted on mobile, Firefox, and Safari (often falls back to simpler formats)  

**Use for non-state-level-threat data until an independent audit is completed.**

---

## License
Licensed under the **ZeroDeadDrop Software License v1.0**  
(see [LICENSE.md](./LICENSE.md) for full terms)

Free for personal and non-commercial use. Attribution required. No warranty.  
Commercial use, redistribution, or derivative works: contact ZeroDeadDrop@gmail.com

© 2025–2026 ZeroDeadDrop (a project by Tuyen Evans). All rights reserved.

---

## Feedback & Contact
🐦 X / Twitter: [@TheRedDressNeo](https://x.com/TheRedDressNeo) (main announcements)  
📧 Email: ZeroDeadDrop@gmail.com

Love it? Hate it? Found a bug? Want to sponsor an audit? Just say hi.

---

*Kerckhoffs's principle: A system should remain secure even if everything about it is known except the key.*
