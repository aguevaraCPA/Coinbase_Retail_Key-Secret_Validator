# Coinbase Retail API Key Validator

This project provides a simple Python script to safely validate a **Coinbase Retail (CDP)** API Key and Secret (ECDSA private key) before using them in crypto tax or accounting platforms.

## Who This Is For

This tool is designed for **accounting professionals, crypto finance teams, and administrators** who:

* Need to validate a **Coinbase Retail API key and secret**
* Want to confirm the credentials work **before** plugging them into accounting/tax platforms
* Prefer a simple, safe, and testable Python-based approach

## Protect Your API Key and Secret

Your API key and secret grant access to your Coinbase data. Treat them like passwords.

* **Never share** your private key or upload it to public sites (like GitHub).
* Store your `cdp_api_key.json` file **in a secure folder** on your machine.
* Immediately **revoke the key** if you believe it was copied or used unsafely.

## What This Script Does

* Loads your Coinbase Retail API key and ECDSA private key
* Creates a JWT (JSON Web Token) used for authentication
* Sends a test request to the Coinbase Retail API
* Confirms whether your key and secret are valid

If validation fails, the script will help identify issues like:

* Malformed or incomplete private key
* System time issues
* Copy/paste corruption of the private key

## What Is `cdp_api_key.json`?

This is the file you download from the Coinbase Developer Portal when generating a Retail API Key. It contains two important fields:

```json
{
  "name": "organizations/.../apiKeys/your-key-id",
  "privateKey": "-----BEGIN EC PRIVATE KEY-----\n...\n-----END EC PRIVATE KEY-----"
}
```

You can either use this file directly, or paste the contents into the script manually (use caution).

## Fixing `\n` in the Private Key

When copying the secret key from the `cdp_api_key.json` file or a message:

* You may see `\n` characters in the key like this:

  ```
  -----BEGIN EC PRIVATE KEY-----\nMHcCAQEE...==\n-----END EC PRIVATE KEY-----\n
  ```

* You **must convert these escaped `\n` values into real line breaks**. For example:

  **Wrong (one-liner with `\n`):**

  ```
  -----BEGIN EC PRIVATE KEY-----\nMHcCAQEE...==\n-----END EC PRIVATE KEY-----\n
  ```

  **Correct (multiline PEM format):**

  ```
  -----BEGIN EC PRIVATE KEY-----
  MHcCAQEE...==
  -----END EC PRIVATE KEY-----
  ```

* If you're copying from a screenshot or chat, **check for spacing or missing characters**, and always verify the formatting.

## API Version Supported

This validator uses the [Coinbase Retail (CDP) API v3 Authentication](https://docs.cdp.coinbase.com/cdp-apis/docs/welcome), specifically:

* JWT-based auth
* ECDSA (ES256) private keys
* OAuth token flow (for `cdp_service` audience)

It is **not** compatible with Coinbase Exchange or Coinbase Pro API keys.

## Getting Started

1. Clone this repo or copy the script.
2. Make sure Python 3.7+ is installed.
3. Run the script with your `cdp_api_key.json` file or paste your credentials.
4. The script will tell you if your key/secret are valid.

## Disclaimer

This script is provided as a convenience tool for credential validation only. You are solely responsible for safeguarding your credentials and ensuring secure use of your API keys.
