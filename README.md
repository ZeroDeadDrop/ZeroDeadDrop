ZeroDeadDrop v1.0.0

Stateless, zero-dependency, zero-server, offline AES-256-GCM encryption system.

Here is a video of how to use it on X.

https://x.com/TheRedDressNeo/status/1983261035172876334

## Overview
ZeroDeadDrop is a browser-based encryption utility that operates fully offline.  
It performs AES-256-GCM encryption and decryption entirely within the browser,  
requiring no internet connection, no servers, and no external libraries.

The app is designed for ephemeral, private use all data resides in memory only  
and self-erases after expiration or inactivity. It is compatible with Tor Browser  
and all major desktop browsers.

Features
- 🔒 AES-256-GCM encryption using PBKDF2-SHA256 key derivation
- 🧱 Stateless, zero-server architecture
- 🕳️ Fully offline operation (no telemetry, no tracking, no requests)
- ⏱️ Time-based and inactivity-based auto-purge
- 🧩 Manifest + bundle system for chunked file encryption
- ⚙️ Browser-native Web Crypto API (no dependencies)
- 🕵️ CSP-hardened for zero data exfiltration
- 🌀 Works in Tor Browser (Standard & Safer modes)

Usage
1. Download `ZeroDeadDrop.html` and open it in a secure modern browser (no installation needed).
2. Choose files or enter text to encrypt.
3. Set a passphrase and encrypt.
4. Download or copy the encrypted manifest and bundle.
5. To decrypt, reload the app offline and supply the same inputs.

⚠️ Important:  
ZeroDeadDrop is stateless. Once you close or reload the page, all session data is erased.

Security
- AES-256-GCM with random salt and IV per chunk
- PBKDF2-SHA256 with 300,000 iterations
- Secure RNG via `crypto.getRandomValues()`
- No `localStorage`, `sessionStorage`, cookies, or network calls
- Strict CSP: `default-src 'none'`
- Optional monotonic (`performance.now()`) timers for tamper-proof expiration

Disclaimer
ZeroDeadDrop is provided "as is," with no warranty or guarantee of any kind.  
Use responsibly and in compliance with your local laws.

Copyright & License
© 2025 ZeroDeadDrop (a project by Tuyen Evans)  
Licensed under the **ZeroDeadDrop Software License v1.0** (see [LICENSE](LICENSE.md)).

Contact
For licensing or commercial use requests, contact:  
ZeroDeadDrop@gmail.com

Feedback
This is a side project built for privacy-conscious users. It gives them the flexibility to use it based on what security practices they want. If you want to deliver the bundle and manifest online or offline, you are able to through USB, email, voice, text, etc. Try it out and share your thoughts on it.

ZeroDeadDrop@gmail.com
