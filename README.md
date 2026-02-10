<img width="1879" height="1010" alt="image" src="https://github.com/user-attachments/assets/bf4554e5-0c21-4e1d-ae87-8eeca5f9c805" />

# Kemonofox Universal Proxy Worker

A powerful, serverless web proxy built on **Cloudflare Workers**.
This project goes beyond simple CORS bypassing. It intelligently **rewrites HTML attributes** and handles **dynamic JavaScript imports** (SPA/chunks) using smart session management.

## ✨ Key Features

### 1. 🔓 Advanced CORS Bypass
- Sets `Access-Control-Allow-Origin: *` for all requests.
- Solves CORS errors during frontend development or API scraping.

### 2. 🔄 Automatic HTML & Asset Rewriting
- Uses Cloudflare's `HTMLRewriter` to intercept and modify HTML on the fly.
- Automatically converts relative paths (e.g., `/assets/style.css`) into absolute proxy URLs.
- **Security Stripping:** Removes `integrity` and `nonce` attributes to prevent browser blocking of modified resources.

### 3. 🧠 Smart Session Handling (Dynamic Imports Fix)
- **The Problem:** Modern frameworks (SvelteKit, Next.js) load JS chunks dynamically (e.g., `import "./_app/chunk.js"`), causing 404 errors because the `?url=` parameter is lost.
- **The Solution:** This worker saves the target domain in a **Session Cookie (`__proxy_target_origin`)**. If a request arrives without a URL parameter, the worker automatically routes it to the correct origin based on the cookie.

### 4. 🍪 Custom Cookie Injection
- Pre-configured to inject specific cookies (e.g., Google, Pinterest) to bypass consent screens or access restricted content.

### 5. 🛡️ Security Header Removal
- Strips `Content-Security-Policy`, `X-Frame-Options`, and `X-Content-Type-Options`.
- Allows websites to be embedded in `<iframe>` tags or accessed from different origins without restrictions.

---

## 🚀 Usage

### Basic Format
Append the target URL to your worker's query parameter:

> Server1 (99.9999% Online)
```http
GET https://proxy.kemono-server.workers.dev/?url={TARGET_URL}
```
> Server2 (99.9999% Online)
```http
GET https://proxy.kemono-server2.workers.dev/?url={TARGET_URL}
```
