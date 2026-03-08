# ZeroDeadDrop

A Stateless Client-based Privacy-first Application With Zero Servers, Zero Dependencies, Zero Data Collection, and Zero Knowledge of Your Data • Symmetric Encryption • Asymmetric Encryption • Plausible Deniability • Decoy File Generator • Offline

Military-grade AES-256-GCM + ECDH P-384 asymmetric encryption that runs entirely in your browser.

No accounts. No uploads. No telemetry. No trust required.

Just open the file and it works offline.

https://github.com/ZeroDeadDrop/ZeroDeadDrop.git

---

## Why You Should Actually Use It

- You get true forward secrecy (asymmetric mode) without needing Signal, PGP, or any app install
- You can give someone your public key once and they can encrypt for you forever, no passphrase sharing ever again
- Plausible deniability is built in (symmetric mode): the decoy password shows innocent files, the real password shows your actual data
- Everything is wiped from RAM after 5 minutes of inactivity or page close (5-pass overwrite + memory pressure)
- Single HTML file approximately 1.4 MB — save it, air-gap it, burn it to USB, email it, whatever
- Works in Chrome and Firefox with limited mobile support and more coming (Standard and Safer security levels)

---

## Core Features

| Feature | Symmetric (passphrase) | Asymmetric (public key) | Notes |
|---|---|---|---|
| AES-256-GCM | Yes | Yes | Per-chunk unique IV + salt |
| PBKDF2 key derivation | Yes | No | 300k to 10M iterations, SHA-256/512 |
| ECDH P-384 + forward secrecy | No | Yes | Ephemeral keys destroyed after encrypt |
| Multiple recipients | No | Yes | Encrypt once, many can decrypt |
| Compression (gzip) | Yes | Yes | Applied before encryption |
| Chunked processing (4 MB max) | Yes | Yes | Large-file friendly |
| Manifest + bundle system | Yes | Yes | Auto-split for huge payloads |
| Plausible deniability / decoys | Yes | No | Hidden volume + fake files |
| Memory sanitization | Yes | Yes | 8-32 MB adaptive pressure + 5-pass wipe |
| Auto-purge after inactivity | Yes | Yes | 5 minutes default |
| CSP | Partial | Partial | unsafe-inline required (single-file design) |
| Offline | Yes | Yes | No network at all |

---

## A Note on Plausible Deniability

In Plausible Deniability mode, the app generates one real encrypted set and one fake encrypted set. A forensic analyst can see two encrypted payload structures. They cannot distinguish which is real, but they can detect that two exist.

So: plausible deniability works psychologically, not cryptographically, for now. For normal use you still have a seamless experience. But in PD mode specifically it is not technically a single hidden container internally. This is something being actively worked on.

---

## Quick Start (2 minutes)

### As Receiver (you want people to send you encrypted files)

1. Open ZeroDeadDrop.html
2. Click Generate Asymmetric Keypair
3. Save your private key somewhere very safe (password manager or offline storage)
4. Copy your public key and send it to anyone who should be able to encrypt files for you

You never need to do this step again.

### As Sender

**Asymmetric mode (recommended — no passphrase hassle)**

1. Paste the receiver's public key
2. Enable Asymmetric Mode
3. Optionally add more recipients
4. Add files or text and click Start Encryption
5. Send the manifest and bundle(s) via any channel, even an insecure one

**Symmetric mode (classic passphrase)**

1. Enter a strong passphrase (16+ characters recommended)
2. Add files or text and click Start Encryption
3. Send the manifest, bundle(s), and passphrase via separate channels

### Decrypt (for receiver)

1. Open the same HTML file
2. Import the manifest and bundle(s)
3. Paste your private key (asymmetric) or passphrase (symmetric)
4. Decrypt and download your files immediately

---

## Security Posture (March 2026)

✅ Strong primitives (Web Crypto AES-GCM + ECDH P-384)  
✅ Forward secrecy in asymmetric mode  
✅ Memory sanitization + auto-purge  
✅ No external dependencies, no network calls ever  

⚠️ CSP allows unsafe-inline (unavoidable in a single-file app; no external script or style exfiltration is possible)  
⚠️ Not formally audited yet  
⚠️ Decoy generator is fingerprintable on mobile, Firefox, and Safari (often falls back to GIF or random bytes)  
⚠️ Hidden volume offset is currently deterministic from password only (should use per-file random salt)  

Use for non-state-level-threat data until an independent audit is completed.

---

## License

**ZeroDeadDrop Software License v1.0**  
(see Modified LICENSE file in repo)

Free for personal and non-commercial use. Attribution required. No warranty.

Commercial use, redistribution, or derivative works: contact ZeroDeadDrop@gmail.com

---

## Feedback & Contact

🐦 X / Twitter: @TheRedDressNeo (main announcements and general chaos because it is a conspiracy account)  
📧 Email: ZeroDeadDrop@gmail.com

Love it? Hate it? Found a bug? Want to sponsor an audit? Just say hi.

---

*Kerckhoffs's principle: a system should remain secure even if everything about it is known except the key.*
