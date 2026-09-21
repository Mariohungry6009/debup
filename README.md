<div align="center">
<img src="https://api.iconify.design/lucide:package-check.svg?color=%23d70a53&width=130&height=130" alt="debup logo" />
<h1>debup</h1>
<p><strong>The AUR-like CLI package manager for Debian/Ubuntu-based distributions, WSL, and Android Linux Terminals.</strong></p>
<p>Search, discover, track, install, and upgrade <code>.deb</code> packages directly from GitHub Releases via <strong>APT</strong>.</p>
<p><em>No PPAs, no bloated sandboxes, no third-party repositories — just native <code>.deb</code> binaries fetched straight from upstream.</em></p>
</div>

<br/>

<div align="center">
<a href="LICENSE"><img src="https://img.shields.io/badge/License-GPLv3-blue.svg" alt="GPL v3"></a> &nbsp;
<a href="https://debian.org"><img src="https://img.shields.io/badge/Platform-Debian%20%7C%20Ubuntu-red.svg" alt="Platform"></a> &nbsp;
<ahref="#"><img src="https://img.shields.io/badge/Arch-all%20(any)-orange.svg" alt="Arch"></a> &nbsp;
<a href="https://www.gnu.org/software/bash/"><img src="https://img.shields.io/badge/Language-Bash-4EAA25.svg" alt="Bash"></a>
</div>

<div align="center">
<a href="https://github.com/Ruraam/debup/releases"><img src="https://img.shields.io/github/v/release/Ruraam/debup?color=brightgreen" alt="Release"></a> &nbsp;
<a href="#"><img src="https://img.shields.io/badge/Package_Size-6.24_Ko-success.svg" alt="Size"></a> &nbsp;
<a href="https://github.com/Ruraam/debup/releases"><img src="https://img.shields.io/github/downloads/Ruraam/debup/total?color=blueviolet" alt="Total Downloads"></a>
</div>

<br/>

<div align="center">

| [Usage](https://github.com/Ruraam/debup/tree/main#%EF%B8%8F-usage) | [GitHub Token](https://github.com/Ruraam/debup/blob/main/README.md#-configure-a-github-token-optionnal--dbp-token-) | [Search & Install](https://github.com/Ruraam/debup/tree/main#-discover-search--install-packages--dbp-search) | [Uninstallation](https://github.com/Ruraam/debup/tree/main#%EF%B8%8F-uninstallation) |
| :---: | :---: | :---: | :---: |
| [Configuration](https://github.com/Ruraam/debup/blob/main/README.md#%EF%B8%8F-configuration) | [Screenshots](https://github.com/Ruraam/debup/tree/main#screenshoots) | [Changelog](https://github.com/Ruraam/debup/releases) | [License](LICENSE) |
</div>

---

### debup (`dbp`) — The Missing Bridge Between GitHub & APT

Missing the AUR convenience on Debian/Ubuntu? **debup** turns GitHub Releases into your personal rolling third-party repository.
**Discover, inspect, install, and update Debian packages directly from GitHub Releases with the simplicity of `apt`.**

### ✨ Core Features

*🔍 **Discover** [`dbp search <query>`] : Find tools and applications directly on GitHub without leaving your terminal, pre-filtered for Debian-compatible repositories.
* 📦 **Direct Add** [`dbp add <owner/repo>`] :No need to hunt down release URLs. Point to any repository, and debup detects, matches your architecture (`amd64` / `arm64`), downloads, and installs the right `.deb`.
* ℹ️ **Inspect** [`dbp info <owner/repo>`] : Preview metadata before touching your system (stars, license, description, latest release, asset architecture compatibility).
* 🔄 **Native APT Lifecycle** : Seamlessly install, update [`dbp upgrade`], and remove [`dbp remove`] tracked packages using your system's native APT engine.
* ⚡ **High-Rate API Tracking**[`dbp token`] : Securely store a personal GitHub token (`chmod 600`) to unlock 5,000 req/h for heavy searches and automated background update checks.

### 🛡️ Package Pinning (`apt-mark hold`)

* **Freeze package updates :** Lock specific packages to their current version using the `pin` (or `hold`) command to prevent unwanted updates.
* **Unfreeze updates :** Restore automatic updates anytime with `unpin` (or `unhold`).
* **Native APT integration :** Relies directly on Debian's standard `apt-mark` mechanism under the hood, ensuring 100% consistency with native system tools.

---

### 🎯 Smart Asset Detection

`debup` automatically picks the right `.deb` binary from GitHub Releases without guesswork:

***Flexible Architectures:** Matches standard & alias names:
* **x86_64:** `amd64`, `x86_64`, `x86-64`, `x64`, `all`
* **ARM64:** `arm64`, `aarch64`, `armv8`, `arm64v8`, `all`
* **Cross-Architecture Protection:** Actively filters out conflicting assets (e.g., prevents downloading `arm64` on `amd64` machines).
* **Distro Prioritization:** Prefers distro-specific builds (`debian` vs `ubuntu`) when multiple compatible packages are published.
* **Safe Fallback:** Cleanly aborts with an explicit warning if no compatible package exists for your CPU architecture.

---

## ⚡Quick First Install
**One-liner to install the latest release:**

```bash
curl -fsSL https://github.com/Ruraam/debup/releases/latest/download/debup_3.3.1_all.deb -o /tmp/debup.deb && sudo apt-get install -y /tmp/debup.deb && rm -f /tmp/debup.deb
```
## 🛠️ Build it yourself from source

***If you prefer to inspect the source code and build the `.deb` package manually:***

1. **Clone the repository:**
```bash
git clone https://github.com/Ruraam/debup.git
cd debup
```
2. **Ensure proper file permissions:**
```bash
chmod 755 debup-pkg/DEBIAN/postinst debup-pkg/DEBIAN/postrm
chmod 755 debup-pkg/usr/local/bin/debup
```
3. **Build the `.deb` package:**
```bash
dpkg-deb --build --root-owner-group debup-pkg debup.deb
```
4. **Install it:**

Via Apt (recommended for dependancies):
```bash
sudo apt install -y ./debup.deb
```
or

Via dpkg:
```bash
sudo dpkg -i debup.deb
```

---

### 🔑 Configure a GitHub Token (optionnal) [ `dbp token` ]

By default, GitHub limits anonymous requests to 60 requests/hour. Adding a token increases this limit to 5000 requests/hour.

**1.Generate a token:**
Go to GitHub > Settings > Developer settings > Personal access tokens > Tokens (classic) > Generate new token (no scopes/permissions needed, leave everything unchecked).

**2.Link it to debup:**
```bash
dbp auth
```
Paste your token and confirm. That's it!

`debup` will automatically detect and use it, boosting your limit to 5,000 requests per hour.

---

## 🛠️ Usage

### Package Management
**Add a repository to install `.deb` & track:**
```bash
dbp add <owner>/<repo>
```
for exemple:
```bash
dbp add fastfetch-cli/fastfetch
```

**List tracked repositories**
```bash
dbp list
```
**Remove a tracked repository**
```bash
dbp remove <package-name>
```

### Package Updates/Upgrade
**Download and upgrade tracked packages with confirmation**
```bash
dbp upgrade 
```
skip confirmation
```bash
dbp upgrade
```
**Prevent an app from updating**
```bash
dbp pin <package-name>
```
**Allow an app to update again**
```bash
dbp unpin <package-name>
```
### 🔍 Discover, Search & Install Packages [ `dbp search`] 

Find & discover any GitHub project providing .deb packages compatible with your architecture and install it in one click:
Search informations on a repository:
```bash
dbp info <owner>/repo>
```
##### Exemple: dbp info fastfetch-cli/fastfetch

```bash
dbp search <keyword>
```
##### Example: [ `dbp search fastfetch`] 
**How it works:**

Enter the package number from the list and press Enter. debup downloads the matching .deb, installs it via apt, and automatically adds it to your tracking list for future updates.

<p align="center">
<img src="/assets/debup_search1.png" width="200"> <img src="/assets/debup_search2.png" width="200"> <img src="/assets/debup_search3.png" width="200"></p>

---
>|
>**💡 Tip:** Combine official repos and GitHub releases by aliasing `sudo apt update && sudo apt upgrade -y && dbp upgrade` in your `~/.bashrc`.
>|

---

## ⚙️ Configuration

**Tracked sources are stored in:** `/etc/debup/sources.list`

**Format:** `<package-name>|<github-user>/<github-repo>`

**Github Token is stored in:** `/etc/debup/debup.conf`

---

## 🗑️ Uninstallation
**Remove package sudo**
```bash
dbp remove debup [-y]
```
Prompted for purge configuration or not.

or
```bash
sudo apt remove debup 
```
**Remove package and clean configuration**
```bash
sudo apt --purge debup
```

---

## Screenshoots
<p align="center">
<img src="/assets/debup_1.png" width="400"> <img src="/assets/debup_2.png" width="400"> <img src="/assets/debup3.png" width="400"> <img src="/assets/debup4.png" width="400"></p>

---

## 📄 License

This project is licensed under the [GNU General Public License v3.0](LICENSE).
