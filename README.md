# Coinbase Retail API Key Validator (Advanced Trade API v3)

This tool validates a **Coinbase Retail API Key and Secret** for the **Advanced Trade API (v3)** using ECDSA (ES256) authentication. It's designed for **accounting professionals** and **admins** who need to confirm credentials **before integrating with a crypto tax platform**.

---

## 🚨 API Key Security Warning

API keys and secrets allow full access to sensitive account data. Always:

* **Keep your key and secret private**
* Avoid sharing or storing them in insecure locations
* Revoke any key if you suspect it has been compromised

---

## ✅ What This Tool Does

* Accepts your `API Key ID` and `ECDSA Private Key`
* Creates a JWT for Coinbase's OAuth-style authentication
* Sends a secure test request to `/api/v3/brokerage/accounts`
* Confirms whether your credentials are **valid and active**

---

## 🔐 Input Format

Paste your credentials directly into the script:

```py
API_KEY_NAME = "organizations/.../apiKeys/your-key-id"

PRIVATE_KEY_PEM = """-----BEGIN EC PRIVATE KEY-----
MHcCAQEE...
-----END EC PRIVATE KEY-----"""
```

You may also use the `cdp_api_key.json` file downloaded from Coinbase. It contains:

```json
{
  "name": "organizations/.../apiKeys/your-key-id",
  "privateKey": "-----BEGIN EC PRIVATE KEY-----\\n...\\n-----END EC PRIVATE KEY-----"
}
```

---

## 🛠️ Fixing the `\n` Format

If your private key looks like this:

```
-----BEGIN EC PRIVATE KEY-----\nMHcCAQEE...\n-----END EC PRIVATE KEY-----
```

You **must fix it** by converting escaped `\n` into actual new lines:

**Incorrect:**

```python
PRIVATE_KEY_PEM = "-----BEGIN EC PRIVATE KEY-----\\nMHcCAQEE...\\n-----END EC PRIVATE KEY-----"
```

**Correct:**

```python
PRIVATE_KEY_PEM = """-----BEGIN EC PRIVATE KEY-----
MHcCAQEE...
-----END EC PRIVATE KEY-----"""
```

Copying from screenshots or formatted messages may corrupt the key. When in doubt:

* Use a plaintext editor
* Redownload `cdp_api_key.json` from the Developer Portal
* Verify line breaks and remove extra characters

---

## 📦 API Version

This script is built for:

* **Coinbase Advanced Trade API (v3)**
* Using [JWT-based authentication](https://docs.cdp.coinbase.com/advanced-trade/docs/rest-api-auth)
* Works with `/api/v3/brokerage/...` endpoints only

---

## 🔗 Key Resources

* [🔐 Authentication Guide](https://docs.cdp.coinbase.com/advanced-trade/docs/rest-api-auth)
* [📚 API Reference (v3)](https://docs.cdp.coinbase.com/advanced-trade/reference)
* [📄 API Overview](https://docs.cdp.coinbase.com/advanced-trade/docs/api-overview)
* [🚀 Getting Started](https://docs.cdp.coinbase.com/advanced-trade/docs/welcome)

---

## 🧪 How to Use

1. Copy the script from this repo
2. Install dependencies: `pip install PyJWT[crypto] cryptography requests`
3. Paste your `API_KEY_NAME` and properly formatted `PRIVATE_KEY_PEM`
4. Run the script — it will output validation success or error messages

---

## 🧯 Common Issues

* **Malformed Private Key**: Check for line breaks, invalid characters
* **Wrong API Version**: This only supports **Advanced Trade v3**, not Pro/Exchange
* **Missing Permissions**: Ensure your key includes **View accounts** permission
* **Incorrect System Time**: JWTs are time-sensitive — ensure your system clock is accurate

---

## 📝 License

This script is provided for educational and operational validation purposes only. You are responsible for the secure handling and storage of your credentials.
