ZeroDeadDrop

Stateless, zero-dependency, zero-server, offline-capable encryption tool with AES-256-GCM and ECDH-P-384 asymmetric support.

ZeroDeadDrop is a fully client-side, browser-based encryption application that operates entirely offline. All encryption and decryption occur within the user's browser using the native Web Crypto API—no servers, no external libraries, no network requests, and no data collection of any kind.

Data exists only in memory and is automatically purged after 5 minutes of inactivity or upon page closure. The tool is designed for privacy-conscious users who require secure, ephemeral file and text transfer without trusting third-party infrastructure.
It works seamlessly in modern desktop browsers (Chrome, Firefox, Edge) and Tor Browser (Standard and Safer modes).

Repository: https://github.com/ZeroDeadDrop/ZeroDeadDrop
Key Features


🔒 Military-grade encryption: AES-256-GCM with per-chunk random salts and IVs

🔑 Dual modes:

Symmetric (passphrase-based with configurable PBKDF2 iterations up to 10M and SHA-256/SHA-512)

Asymmetric (ECDH P-384 with forward secrecy and multi-recipient support – recommended)

🗜️ Optional gzip compression before encryption

🧩 Manifest + bundle output system (auto-split for large payloads)

🕵️ Plausible deniability mode (symmetric only – generates decoy outputs)

⏱️ Automatic secure memory purge (5-minute inactivity timeout + unload wipe)

🛡️ 180MB constant memory pressure + multi-pass overwrite to resist RAM recovery

⚙️ Zero dependencies – single self-contained HTML file

🕳️ Strict CSP (default-src 'none') – guaranteed no data exfiltration

📱 Works completely offline and in Tor Browser

Why ZeroDeadDrop?

In an era of increasing digital surveillance, true privacy requires eliminating trust in third parties. Most online tools rely on servers, dependencies, or accounts—each a potential point of compromise.
ZeroDeadDrop removes these entirely. When you "send" encrypted data, you are actually sending instructions on how to reconstruct the original using a shared credential. The sensitive content itself never leaves your device unencrypted. Even if an adversary intercepts the outputs, they learn nothing without the credential.
Privacy should be the default, not a premium feature reserved for high-risk users.
Usage
Download ZeroDeadDrop.html from the repository.
Open the file directly in a modern browser (no installation required).

Encrypt:

Add text and/or files (up to 1 GB total, 500 MB per file).
Choose symmetric (passphrase) or asymmetric mode (paste recipient public keys).
Configure options (compression, iterations, plausible deniability, etc.).
Click "Start Encryption" and download/copy the manifest and bundle(s).

Decrypt:

Reload the app (offline recommended).
Import manifest and bundle(s).
Provide the matching credential (passphrase or private key).
Download decrypted files immediately (auto-purge in 5 minutes).


Note: 
Large payloads (>500 MB) may temporarily pause the browser UI—this is normal Web Crypto behavior on a single thread. Wait for completion.

Security Notes

AES-256-GCM with unique salts/IVs per chunk

Forward secrecy in asymmetric mode (ephemeral sender keys destroyed after use)

Secure random via crypto.getRandomValues()

No storage mechanisms (localStorage, IndexedDB, cookies)

Aggressive memory sanitization on exit/inactivity

Not professionally audited yet – use for non-critical data and review the source

Disclaimer

ZeroDeadDrop is provided "as is" without warranty of any kind. The author assumes no liability for data loss, security incidents, or misuse.

Use responsibly and in accordance with applicable laws.

Copyright & License

© 2026 ZeroDeadDrop

Licensed under the ZeroDeadDrop Software License v1.0 (see LICENSE file).

For licensing inquiries or commercial use, contact: ZeroDeadDrop@gmail.com

Feedback & Support

This is an independent privacy project built for everyday users who value digital sovereignty. Try it out, share it, and let me know your thoughts.

Feedback, suggestions, and contributions welcome:

ZeroDeadDrop@gmail.com

Kerckhoffs's principle: a system should remain secure even if everything about it is known except the key. 
