# ZeroDeadDrop

**A Stateless Client-based Privacy-first Application With Zero Servers, Zero Dependencies, Zero Data Collection, and Zero Knowledge of Your Data • Symmetric Encryption • Asymmetric Encryption • Plausible Deniability • Decoy File Generator • Offline**

Military-grade AES-256-GCM + ECDH-P-384 asymmetric encryption that runs **entirely in your browser**.

No accounts. No uploads. No telemetry. No trust required.

Just open the file and works offline.

https://github.com/ZeroDeadDrop/ZeroDeadDrop.git

## Why you should actually use it

- You get **true forward secrecy** (asymmetric mode) without needing Signal, PGP, or any app install  
- You can give someone your **public key once** — they can encrypt for you forever, no passphrase sharing ever again  
- **Plausible deniability built-in** (symmetric mode): decoy password shows innocent files, real password shows your actual data  
- **Everything wiped from RAM** after 5 min inactivity or page close (5-pass overwrite + memory pressure)  
- Single HTML file ≈ 1.4 MB — save it, air-gap it, burn it to USB, email it, whatever  
- Works in Chrome and Firefox with limited mobile with more coming. (Standard & Safer security levels)

## Core Features

| Feature                          | Symmetric (passphrase) | Asymmetric (public-key) | Notes / Status                              |
|----------------------------------|------------------------|--------------------------|---------------------------------------------|
| AES-256-GCM                      | Yes                    | Yes                      | per-chunk unique IV + salt                  |
| PBKDF2 key derivation            | Yes                    | —                        | 300k–10M iterations, SHA-256/512            |
| ECDH-P-384 + forward secrecy     | —                      | Yes                      | ephemeral keys, destroyed after encrypt     |
| Multiple recipients              | —                      | Yes                      | encrypt once, many can decrypt              |
| Compression (gzip)               | Yes                    | Yes                      | before encryption                           |
| Chunked processing (≤4 MB)       | Yes                    | Yes                      | large-file friendly                         |
| Manifest + bundle system         | Yes                    | Yes                      | auto-split for huge payloads                |
| Plausible deniability / decoys   | Yes                    | No                       | hidden volume + fake files                  |
| Memory sanitization              | Yes                    | Yes                      | 32 MB pressure + 5-pass wipe                |
| Auto-purge after inactivity      | Yes                    | Yes                      | 5 min default                               |
| CSP                              | Partial                | Partial                  | unsafe-inline required (single-file design) |
| Offline                          | Yes                    | Yes                      | no network at all                           |

As for plausible deniability mode, it generates:

One real set

One fake set

But:

A forensic analyst can see:

Two encrypted payload structures

They cannot distinguish which is real,
but they can detect that there are two.

So:

Plausible deniability works psychologically,
not cryptographically for right now until I fix how to make it seamless.

Short answer: yes — for normal use, you still have a seamless “one container” experience.
But in PD mode specifically, it’s not technically a single hidden container internally.

## Quick Start (2 minutes)

### As Receiver (you want people to send you encrypted stuff)

1. Open **ZeroDeadDrop.html**  
2. Click **Generate Asymmetric Keypair**  
3. Save your **private key** somewhere very safe (password manager / offline)  
4. Copy your **public key** and send it to anyone who should be able to encrypt files for you  
   → Done. You never need to do this step again.

### As Sender (you want to send something encrypted)

**Asymmetric (recommended – no passphrase hassle)**

1. Paste the receiver's **public key**  
2. Enable **Asymmetric Mode**  
3. (Optional) Add more recipients  
4. Add files/text → Start Encryption  
5. Send the **manifest** + **bundle(s)** (any channel, even insecure)

**Symmetric (classic passphrase mode)**

1. Enter strong passphrase (16+ chars recommended)  
2. Add files/text → Start Encryption  
3. Send **manifest** + **bundle(s)** + **passphrase** (use **different channels**!)

### Decrypt (for receiver)

1. Open the same HTML file  
2. Import manifest + bundle(s)  
3. Paste your **private key** (asymmetric) or passphrase (symmetric)  
4. Decrypt → download files immediately

## Security posture (Mar 2026)

✅ Strong primitives (Web Crypto AES-GCM + ECDH-P-384)  
✅ Forward secrecy in asymmetric mode  
✅ Memory sanitization + auto-purge  
✅ No external dependencies, no network calls ever  

⚠️ CSP allows unsafe-inline (unavoidable in a single-file app; no external script/style exfil possible)  
⚠️ Not formally audited (yet)  
⚠️ Decoy generator fingerprintable on mobile/Firefox/Safari (often falls back to GIF or random bytes)  
⚠️ Hidden volume offset currently deterministic from password only (should use per-file random salt)

Use for non-state-level-threat data until independent audit.

## License

ZeroDeadDrop Software License v1.0  
(see Modified LICENSE file in repo)

Basically: free for personal/non-commercial use, attribution required, no warranty.

Commercial use / redistribution / derivative works → contact ZeroDeadDrop@gmail.com

## Feedback & Contact

- 🐦 X / Twitter: @TheRedDressNeo (main announcements and crazy stuff cause it's a conspiracy account)  
- 📧 Email: ZeroDeadDrop@gmail.com  

Love it? Hate it? Found a bug? Want to sponsor an audit? Just say hi.

Kerckhoffs's principle: a system should remain secure even if everything about it is known except the key.
