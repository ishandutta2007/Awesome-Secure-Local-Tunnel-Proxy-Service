# Awesome-Secure-Local-Tunnel-Proxy-Service

# Awesome Secure Local Tunnel & Proxy Service

> A curated list of top Secure Local Tunnel and Proxy Service platforms — both SaaS/Hosted commercial solutions and open-source alternatives for exposing localhost services to the internet securely for testing, webhooks, and demos.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [BrowserStack Local Testing](#browserstack-local-testing)
  - [Sauce Connect Tunnel](#sauce-connect-tunnel)
  - [LambdaTest Underpass](#lambdatest-underpass)
  - [ngrok](#ngrok)
  - [LocalXpose](#localxpose)
  - [Cloudflare Tunnel](#cloudflare-tunnel)
  - [Tailscale Funnel](#tailscale-funnel)
  - [PageKite](#pagekite)
- [Open-Source Software](#-open-source-software)
  - [inlets](#inlets)
  - [localtunnel](#localtunnel)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Secure Local Tunnel and Proxy Service platforms. These are not fully open-source but are included as reference points for feature comparison.

### BrowserStack Local Testing
**Type:** Secure tunnel for cross-browser testing of localhost apps
BrowserStack Local Testing establishes a secure connection between your local machine and BrowserStack's cloud to test locally hosted applications across 3,500+ real devices and browsers . Two setup paths are available: a **Desktop App** for Windows/macOS and a **Local Binary** for all operating systems including Linux (recommended for Automate/App Automate) . The Local Binary v8.9 (March 2026) added include/exclude host functionality for individual IPs or subnets, a global `--timeout` flag, and a `--disable-ssl-validation` flag for testing with self-signed certificates . Integration is native to BrowserStack's testing platform, eliminating separate tunnel configuration.
**Best for:** Teams already using BrowserStack for cross-browser testing needing a purpose-built, low-configuration tunnel with enterprise-grade controls.

### Sauce Connect Tunnel
**Type:** Secure tunnel for Sauce Labs testing
Sauce Connect establishes a secure connection between your local network and Sauce Labs' cloud testing infrastructure, enabling testing of localhost and staging environments. It is the native tunnel solution for Sauce Labs users, with CLI-based management and support for proxy configurations.

### LambdaTest Underpass
**Type:** GUI-based secure tunnel for local testing
LambdaTest Underpass is a **desktop application** that establishes an SSH tunnel between your machine and LambdaTest's cloud without requiring terminal commands [citation:2]. It supports login via Email/Password, Google, GitHub, or organization SSO, with advanced configurations including **MITM mode** for testing sites with self-signed certificates and **local directory access** (using `local-folder.lambdatest.com` as the testing URL) [citation:2]. The CLI-based TestMu AI Tunnel remains available for automation workflows [citation:11].
**Best for:** QA teams wanting a no-CLI, GUI-driven tunnel for manual cross-browser testing, particularly those needing MITM for self-signed certificates.

### ngrok
**Type:** General-purpose ingress tunnel with generous free tier
ngrok is the most widely recognized general-purpose tunnel service. The **free plan** includes unlimited online endpoints (up to 3 concurrently), HTTPS tunnels with automatic TLS, 1 GB/month data transfer, 20,000 HTTP requests, and 4,000 requests/min rate limit [citation:4][citation:13]. A key limitation is the **interstitial warning page** on HTML traffic (deterring phishing), which can be bypassed with the `ngrok-skip-browser-warning` header or a non-standard User-Agent [citation:4]. Free endpoints have no timeout, making them suitable for background services [citation:4]. Custom domains and reserved URLs require paid plans.
**Best for:** Developers wanting a reliable, zero-config tunnel with a free tier for webhooks and demos, accepting the interstitial page and monthly quotas.

### LocalXpose
**Type:** Tunnel service with free tier
LocalXpose offers a **Starter free plan** with 2 active HTTP/HTTPS tunnels, SSL/TLS encryption, unique subdomains, and all platform builds available [citation:9]. The free tier includes an interstitial warning page (similar to ngrok). Paid plans unlock more tunnels, custom domains, and removal of the interstitial.
**Best for:** Developers wanting a free ngrok alternative with similar features, accepting the same interstitial trade-off.

### Cloudflare Tunnel
**Type:** Zero-trust tunnel with free named tunnels
Cloudflare Tunnel (`cloudflared`) provides secure, outbound-only connections from your local service to Cloudflare's edge, with no inbound ports required. **Ephemeral tunnels** generate a random public URL on each run, while **named tunnels** provide persistent subdomains across restarts and support **Cloudflare Access policies** for authentication in front of the tunnel [citation:12]. Named tunnels can be installed as a systemd service for unattended operation [citation:3]. The free tier includes unlimited bandwidth and requests, making it one of the most generous options.
**Best for:** Teams wanting a production-grade, zero-trust tunnel with persistent URLs and authentication, particularly those already using Cloudflare.

### Tailscale Funnel
**Type:** Tailnet-based public exposure with strict limitations
Tailscale Funnel routes public internet traffic to a local service running in your Tailscale network, without requiring visitors to use Tailscale [citation:6]. It requires Tailscale v1.38.3+, MagicDNS, HTTPS certificates, and a `funnel` node attribute in the tailnet policy [citation:6]. **Key limitations:** Funnel only uses DNS names in your `tailnet-name.ts.net` domain, only listens on ports 443/8443/10000, only works over TLS, and is subject to **non-configurable bandwidth limits** [citation:6]. It is beta and disabled by default. Funnel URLs persist across reboots as long as the device remains in the tailnet [citation:15].
**Best for:** Teams already using Tailscale wanting to expose a service to the public with minimal setup, accepting the strict port/domain restrictions and bandwidth caps.

### PageKite
**Type:** Long-standing tunnel with trial-based access
PageKite provides localhost tunneling with a **31-day free trial (2.5 GB transfer)** [citation:5]. The `pagekite.py` software is free and open-source, but the hosted service requires a paid plan after the trial. Free software developers can apply for sponsored accounts [citation:5]. Note that new subscriptions were temporarily unavailable per the signup page.
**Best for:** Developers wanting a mature, Python-based tunnel with a trial period, or those eligible for sponsored free software accounts.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Secure Local Tunnel and Proxy Service tools. Both listed projects are fully open-source and can be self-hosted.

### inlets
**Stack:** Go | **License:** MIT
inlets is a **cloud-native tunnel written in Go**, designed to expose local services through a public endpoint [citation:7]. It uses a client-server architecture where the inlets client runs in your local network and connects outbound to an inlets server running on a public host (cloud VM, Kubernetes, etc.). The server forwards incoming requests through the established tunnel to the local service. Because it is MIT-licensed and written in Go, it can be compiled for any platform and embedded in automation workflows. Unlike hosted services, inlets gives you full control over the public endpoint and bandwidth.
**Best for:** Teams wanting a self-hosted, fully open-source tunnel with no usage quotas, deployable on their own infrastructure for production-grade exposure.

### localtunnel
**Stack:** Node.js | **License:** MIT (client) / Open Source (server)
localtunnel is a **Node.js CLI** that exposes a local HTTP service on a public URL with a single command: `npx localtunnel --port 8000` [citation:8]. The client is distributed via npm, and the **server component is also open-source** and self-hostable, allowing you to run your own tunnel infrastructure instead of relying on the public `localtunnel.me` service [citation:8]. The project's adoption stems from its extremely low setup cost and the fact that both client and server are open-source. Advanced users can self-host the server, configure DNS wildcards, and point the client at it with `--host` [citation:8].
**Best for:** Developers wanting the simplest possible open-source tunnel with the option to self-host the server for full control.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Free Tier | Self-Hosted | Persistent URL | Best For |
|----------|---------|-------|-----------|-------------|----------------|----------|
| **BrowserStack Local** | Proprietary | Binary/App | (BrowserStack plan) | ❌ | ❌ | BrowserStack testing tunnel |
| **Sauce Connect** | Proprietary | CLI | (Sauce plan) | ❌ | ❌ | Sauce Labs testing tunnel |
| **LambdaTest Underpass** | Proprietary | GUI App | (LambdaTest plan) | ❌ | ❌ | GUI tunnel + MITM |
| **ngrok** | Proprietary | CLI | ✅ 1GB/mo | ❌ | ❌ (Paid) | General-purpose webhooks |
| **LocalXpose** | Proprietary | CLI | ✅ 2 tunnels | ❌ | ❌ (Paid) | Free ngrok alternative |
| **Cloudflare Tunnel** | Proprietary | CLI | ✅ Unlimited | ❌ | ✅ (Named) | Zero-trust + persistent URLs |
| **Tailscale Funnel** | Proprietary | CLI | ✅ (All plans) | ❌ | ✅ (Tailnet) | Tailnet users, strict ports |
| **PageKite** | Proprietary | Python | Trial (31d) | ❌ | ❌ | Mature trial-based tunnel |
| **inlets** | MIT | Go | ✅ (Self-host) | ✅ | ✅ (Your infra) | Fully self-hosted tunnel |
| **localtunnel** | MIT (client) | Node.js | ✅ (Public) | ✅ (Server) | ❌ | Simplest OSS tunnel |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Secure Local Tunnel or Proxy Service tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the ecosystem **splits** between **testing-platform-native tunnels** (BrowserStack Local, Sauce Connect, LambdaTest Underpass) that are purpose-built for cross-browser testing and **general-purpose tunnels** for webhooks and demos. Among general-purpose options, **Cloudflare Tunnel** offers the most generous free tier with persistent named tunnels and zero-trust access policies [citation:12], while **ngrok** remains the most familiar despite its free-tier quotas and interstitial page [citation:4]. For teams wanting **full self-hosting without quotas**, **inlets** (MIT, Go) and **localtunnel** (MIT client, open-source server) are the primary open-source options [citation:7][citation:8].

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
