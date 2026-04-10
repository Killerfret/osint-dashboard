# OSINT Hub

A unified, self-contained OSINT lookup dashboard that queries multiple intelligence APIs from a single search bar. Built as a single HTML file — deployable directly to GitHub Pages with zero backend.

## Features

- **Password-protected** — PBKDF2-SHA256 encrypted login (100k iterations), hardcoded hash
- **Dual API integration** — OsintCat + See-Know queried simultaneously
- **Universal search** — auto-detects input type or manual selection
- **9 search types** — Breach, Email OSINT, IP, Domain, Phone, Discord, GitHub, Twitter + auto-detect
- **Side-by-side results** — each API gets its own scrollable panel with result counts and timestamps
- **Persistent settings** — API keys saved to localStorage (never leaves your browser)
- **Export** — download all results as a JSON file
- **Copy** — copy individual results or entire panels to clipboard
- **Error handling** — clear messages for CORS issues, rate limits, invalid keys, and network errors
- **Brute-force protection** — 3 attempt lockout with 30s cooldown
- **Dark cyberpunk UI** — responsive design that works on desktop and mobile
- **Zero dependencies** — pure HTML + CSS + vanilla JavaScript

## Setup

### 1. Set a login password

1. Open `index.html?setup` in your browser
2. Choose a strong password and click **Generate Hash**
3. Copy the HASH and SALT values
4. Open `index.html` in a text editor
5. Find `const AUTH_HASH = '';` and paste the hash between the quotes
6. Find `const AUTH_SALT = '';` and paste the salt between the quotes
7. Save the file

### 2. Configure API keys

1. Open `index.html` in your browser and log in
2. Click **API Settings** to expand the configuration panel
3. Enter your API keys:
   - **OsintCat**: Get your API key from [osintcat.net](https://osintcat.net)
   - **See-Know**: Get your API key from [see-know.eu](https://see-know.eu) and set the base URL
4. Click **Save**

## Deploy to GitHub Pages

1. Create a new GitHub repository (e.g., `osint-dashboard`)
2. Push the `index.html` file to the `main` branch
3. Go to **Settings** > **Pages**
4. Under **Source**, select `main` branch and `/ (root)` folder
5. Click **Save**
6. Your dashboard will be live at `https://<username>.github.io/osint-dashboard/`

## API Reference

### OsintCat
- **Base URL**: `https://www.osintcat.net/api`
- **Auth**: `X-API-KEY` header
- **Method**: GET with `?query=` parameter
- **Rate limit**: 3 requests/second (30 min timeout if exceeded)
- **Docs**: [docs.osintcat.net](https://docs.osintcat.net/api-reference/introduction)

**Available endpoints:**
| Endpoint | Description |
|----------|-------------|
| `/breach` | Breach data search (email, username) |
| `/email-osint` | Email address intelligence |
| `/phone-osint` | Phone number intelligence |
| `/ip` | IP geolocation, ISP, stealer logs |
| `/domain` | Domain info from stealer logs |
| `/discord` | Discord user lookup |
| `/github-osint` | GitHub profile intelligence |
| `/twitter-osint` | Twitter profile data |

### See-Know
- **Base URL**: Configurable in settings (default: `https://see-know.eu/api/`)
- **Auth**: Bearer token + X-API-KEY header
- **Docs**: [see-know.eu/api-docs](https://see-know.eu/api-docs)

## CORS Note

Since this is a client-side only application, some APIs may block direct browser requests due to CORS policies. If you encounter CORS errors:
- Use a browser extension like "CORS Unblock" for local testing
- Set up a lightweight CORS proxy
- Some APIs may work directly depending on their CORS configuration

## Security

- Login password is hashed with PBKDF2-SHA256 (100,000 iterations + 16-byte salt)
- Hash is hardcoded in the file — no plaintext password stored anywhere
- Session expires when browser tab closes (sessionStorage)
- Brute-force lockout after 3 failed attempts (30s cooldown)
- API keys stored only in browser localStorage

## Disclaimer

**This tool is provided for educational and authorized research purposes only.**

- Only search for data that you own or have explicit written permission to query
- Unauthorized access to personal data may violate laws including GDPR, CFAA, and local privacy regulations
- The authors assume no liability for misuse of this tool
- By using this tool, you agree to comply with all applicable laws and the terms of service of each API provider

## License

MIT
