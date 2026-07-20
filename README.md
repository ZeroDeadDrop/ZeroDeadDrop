# ZeroDeadDrop

**Most Recent Version:** v12.0.0  
**Last Updated:** July 20, 2026

**A Stateless, Client-Side, Privacy-First Encryption App**

**Zero Servers**  
**Zero Remote Network Requests**  
**Zero Telemetry**  
**Zero Dependencies**  
**Zero Backend**  
**Zero Install**  
**Zero Data Out**

Symmetric Encryption · Asymmetric Encryption · Plausible Deniability · Decoy Generator

---

This is **not** a messaging app.  
It is a **Digital DeadDrop Preparation Tool**. You encrypt files locally in your browser and receive encrypted outputs that can be transferred through any channel you choose (USB, email, physical transfer, anonymous upload, etc.). The recipient can then decrypt the file using the same HTML application, either online or fully offline. Same version recommended for best compatibility; older formats are supported.

The application is designed around ephemeral browser-based memory, meaning no persistent user data is stored beyond the session in any meaningful or recoverable way.  
It is intentionally built as a single self-contained HTML file to maximize portability and allow use anywhere, at any time, enabling true ZeroDeadDrop workflows.

To maintain the "zero external dependencies" design principle, cryptographic primitives not natively available through the browser's Web Crypto API — including a full Argon2id (RFC 9106) implementation — are hand-written from scratch directly in this file rather than pulled in as libraries. This is a deliberate tradeoff: it costs real engineering effort and, for Argon2id specifically, more raw CPU time than an optimized native or WASM library would need, in exchange for strict self-containment and the ability to audit every line that touches your data.

Even if encrypted data is recovered through forensic means, it remains protected by AES-256-GCM encryption. With a sufficiently high-entropy password, the data is intended to be computationally infeasible to decrypt.

More details are available in the in-app instructions.

**AES-256-GCM + ECDH P-384** asymmetric encryption running entirely in the browser using the Web Crypto API.  
No accounts. No uploads. No telemetry. No external trust required.  
Just open the HTML file and it works completely offline.

**Repository:** https://github.com/ZeroDeadDrop/ZeroDeadDrop.git

---

## Why You Should Actually Use It

- Per-message forward secrecy in asymmetric mode without needing Signal, PGP, or any app installation.
- Give someone your public key once — they can encrypt files for you indefinitely without ever sharing a passphrase.
- **Strong plausible deniability** (symmetric mode): the decoy password reveals innocent files; the real password reveals your actual sensitive data.
- Aggressive memory sanitization — everything is wiped from RAM after 5 minutes of inactivity or when the page closes (adaptive pressure + multi-pass overwrite).
- Single HTML file **(~1.13 MB)** — save it, air-gap it, burn it to USB, email it, or run it from anywhere.
- Works best in an air-gapped system offline with a long, high-entropy password for maximum security.

---

## Core Features

| Feature                        | Symmetric (passphrase) | Asymmetric (public key) | Notes |
|--------------------------------|------------------------|--------------------------|-------|
| AES-256-GCM                    | Yes                    | Yes                      | Per-chunk unique IV + salt |
| PBKDF2 key derivation          | Yes                    | No                       | 4M–20M iterations, SHA-512 |
| Argon2id key derivation        | Yes                    | No                       | RFC 9106, memory-hard (64 MB / 3 passes by default); hand-written pure-JS implementation, selectable as an alternative to PBKDF2 |
| ECDH P-384                     | No                     | Yes                      | Ephemeral keys destroyed after encryption |
| Multiple recipients            | No                     | Yes                      | Encrypt once, many can decrypt |
| Compression (gzip)             | Yes                    | Yes                      | Applied before encryption |
| Chunked processing             | Yes                    | Yes                      | 4–8 MB per chunk depending on file size |
| Manifest + bundle system       | Yes                    | Yes                      | Auto-split for very large payloads |
| Plausible deniability / decoys | Yes                    | No                       | Hidden Volume support |
| Memory sanitization            | Yes                    | Yes                      | 8–32 MB adaptive pressure + multi-pass wipe |
| Auto-purge after inactivity    | Yes                    | Yes                      | 5 minutes default |
| CSP                            | Partial                | Partial                  | `unsafe-inline` required (single-file) |
| Offline                        | Yes                    | Yes                      | No network calls ever |

**Streaming Encryption v9** — Per-chunk HKDF key derivation with improved forward secrecy and reduced fingerprinting.

---

## A Note on Plausible Deniability

In **Hidden Volume** mode, the app produces a single binary container with two independently encrypted volumes. These volumes are placed at password-derived positions inside a noise header. Each volume uses its own password-derived key and a unique random salt.

- Entering the **decoy password** reveals only the innocent decoy files.  
- Entering the **real password** reveals only your actual sensitive files.

Neither password can derive the other volume's key. A forensic examiner can recognize the file as a ZeroDeadDrop container, but cannot access either volume without the correct password.

The Hidden Volume workflow includes a dedicated UI with separate real/decoy password handling and a secure password copy dialog.

---

## Quick Start (2 minutes)

### As Receiver
1. Open `ZeroDeadDrop.html`
2. Click **Generate Asymmetric Keypair**
3. Save your **private key** somewhere very secure (offline storage or password manager)
4. Share your **public key** with anyone who should be able to send you files

You only need to do this once.

### As Sender

**Asymmetric mode (recommended — no passphrase sharing)**
1. Paste the receiver's public key
2. Enable Asymmetric Mode
3. Optionally add more recipients
4. Add your files or text and click **Start Encryption**
5. Send the resulting manifest and bundle(s) via any channel

**Symmetric mode (classic passphrase)**
1. Enter a strong passphrase (16+ characters recommended)
2. Add your files or text and click **Start Encryption**
3. Send the manifest, bundle(s), and passphrase via **separate channels**

### Decrypt
1. Open the same HTML file
2. Import the manifest and bundle(s)
3. Paste your private key (asymmetric) or passphrase (symmetric)
4. Click **Decrypt** and download your files

---

## Security Posture (July 2026)

✅ Strong primitives (Web Crypto AES-GCM + ECDH P-384)  
✅ Per-message forward secrecy in asymmetric mode via ephemeral keys  
✅ **Streaming v9** with per-chunk HKDF key derivation  
✅ Aggressive memory sanitization and auto-purge  
✅ No external dependencies or network calls ever  
✅ Hidden volume offsets derived from password + per-container random salt  
⚠️ CSP allows `unsafe-inline` (unavoidable in a single-file app)  
⚠️ Extensively self-tested (crypto primitives checked against reference implementations, full functional test suite, real-browser execution testing) but not yet independently audited by a professional third party  
⚠️ Decoy generator can be fingerprinted on some browsers/devices  

**Use for non-state-level-threat data until an independent audit is completed.**

---

## License

Licensed under the **ZeroDeadDrop Software License v1.0**  
(see [LICENSE.md](./LICENSE.md) for full terms)

Free for personal and non-commercial use. Attribution required. No warranty.  
Commercial use, redistribution, or derivative works: contact ZeroDeadDrop@gmail.com

© 2025–2026 ZeroDeadDrop. All rights reserved.

---

## Feedback & Contact

🐦 X / Twitter: [@TheRedDressNeo](https://x.com/TheRedDressNeo) (main announcements)  
📧 Email: ZeroDeadDrop@gmail.com

Love it? Hate it? Found a bug? Want to sponsor an audit? Just say hi.

---

*Kerckhoffs's principle: A system should remain secure even if everything about it is known except the key.*
