# Aegis Http GPG Login (Firefox) | En / [TR](README.tr.md)

![Logo](icons/logo.png)

Aegis Http is an autonomous, End-to-End Encrypted (E2E) HTTP gateway extension mapped for Mozilla Firefox. It seamlessly intercepts REST API requests sent by frontend web applications, passing them to the locally running `Aegis Http Native Host` (Rust Daemon) where they are encrypted using PGP before hitting the network.

## Features

- **Transparent Interception:** Intercepts `XMLHttpRequest` transparently; meaning the frontend code doesn't need to know anything about cryptography.
- **Native Security:** Cryptographic private keys NEVER touch the JavaScript context or the browser. It securely communicates via Firefox's Native Messaging API.
- **Auto-Decryption:** Once the server responds with a GPG encrypted tunnel, this extension transparently decrypts and proxies the JSON response back to the original function call automatically.

## Installation

1. Go to `about:debugging#/runtime/this-firefox` in Firefox.
2. Under "Temporary Extensions", click **Load Temporary Add-on...**
3. Select the `manifest.json` file inside this `/firefox-extension` directory.
4. **Important! Make sure your Native Host daemon is installed!** Ensure that the `aegis-http.json` is correctly installed in your `~/.mozilla/native-messaging-hosts/` directory, pointing to the Daemon binary.

## Files Overview

- `manifest.json`: Defines the Firefox Gecko ID and properties (`nativeMessaging` permissions).
- `background.js`: Persistent background script to interface with the Mozilla Native process.
- `content.js`: Injects the `inject.js` code dynamically into the webpage's DOM.
- `inject.js`: Highly privileged override script that patches the `XMLHttpRequest.prototype.send` object.
- `icons/`: High-resolution extension brand icons for the browser UI.
