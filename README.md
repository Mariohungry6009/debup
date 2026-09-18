<div align="center">
<img src="https://api.iconify.design/lucide:package-check.svg?color=%23d70a53&width=130&height=130" alt="debup logo" />
<h1 >debup</h1>
<p><strong>The Obtainium-like CLI package manager for Debian/Ubuntu-based distributions, WSL, Android Linux Terminal.</strong>
</p>
<p><strong>Search, discover, track, install, and upgrade <code>.deb</code> packages directly from GitHub Releases via <strong>APT</strong>.
</p>
<p><strong>No PPAs, no bloated sandboxes, no third-party repositories - just native `.deb` binaries fetched straight from upstream.</strong>
</p>
</div>

<div>
&nbsp; 
</div>

<div align="center">
<a href="LICENSE"><img src="https://img.shields.io/badge/License-GPLv3-blue.svg" alt="GPL v3"></a> &nbsp;
<a href="https://debian.org"><img src="https://img.shields.io/badge/Platform-Debian%20%7C%20Ubuntured.svg" alt="Platform"></a> &nbsp;
<a href="#"><img src="https://img.shields.io/badge/Arch-all%20(any)-orange.svg" alt="Arch"></a> &nbsp;
<a href="https://www.gnu.org/software/bash/"><img src="https://img.shields.io/badge/Language-Bash-4EAA25.svg" alt="Bash"></a>
</p>
</div>
<div align="center">
<a href="https://github.com/Uraam/debup/releases"><img src="https://img.shields.io/github/v/release/Uraam/debup?color=brightgreen" alt="Release"></a> &nbsp;
<a href="#"><img src="https://img.shields.io/badge/Package_Size-3.41_Ko-success.svg" alt="Size"></a> &nbsp;
<a href="https://github.com/Uraam/debup/releases"><img src="https://img.shields.io/github/downloads/Uraam/debup/total?color=blueviolet" alt="Total Downloads"></a>
</p>
</div>

<div>
<h1 > </h1>
</div>

<div align="center">
  
|&nbsp; [Usage](https://github.com/Ruraam/debup/tree/main#%EF%B8%8F-usage) &nbsp;|&nbsp; [Configure a GitHub Token](https://github.com/Ruraam/debup#-configure-a-github-token-debup-auth) &nbsp;|&nbsp; [Discover, Search & Install Packages](https://github.com/Ruraam/debup#-discover-search--install-packages-debup-search) &nbsp;|&nbsp; [Highlights](https://github.com/Ruraam/debup#-highlights) &nbsp;|&nbsp; [Uninstallation](https://github.com/Ruraam/debup#%EF%B8%8F-uninstallation)&nbsp; |

|&nbsp; [Screenshoots](https://github.com/Ruraam/debup#screenshoots)  &nbsp;|&nbsp; [License](https://github.com/Ruraam/debup/blob/main/LICENSE)&nbsp; |

</div>

---

## ⚡ Quick First Install
**First installation : One-command for latest release.**

```bash
curl -fsSL https://github.com/Ruraam/debup/releases/latest/download/debup_3.1.1_all.deb -o /tmp/debup.deb && sudo apt-get install -y /tmp/debup.deb && rm -f /tmp/debup.deb
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

### 🔑 Configure a GitHub Token (`debup auth`)

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
## 🔍 Discover, Search & Install Packages (`debup search`) 

Find & discover any GitHub project providing .deb packages compatible with your architecture and install it in one click:
```bash
dbp search <keyword>
```
### Example: debup search fastfetch
**How it works:**

Enter the package number from the list and press Enter. debup downloads the matching .deb, installs it via apt, and automatically adds it to your tracking list for future updates.

<p align="center">
<img src="/assets/debup_search1.png" width="200"> <img src="/assets/debup_search2.png" width="200"> <img src="/assets/debup_search3.png" width="200"></p>

---
>|
>**💡 Tip:** Combine official repos and GitHub releases by aliasing `sudo apt update && sudo apt upgrade -y && dbp upgrade` in your `~/.bashrc`.
>|
---

## ✨ Highlights

- **Native Workflow:** Standard `search`, `add`, `list`, `remove`, `update`, and `upgrade` syntax.
- **Architecture Aware:** Automatically detects CPU architecture (`amd64`, `arm64`, `all`).
- **Self-Updating:** Automatically tracks and updates it self via `debup upgrade`.
- **Dependency Handling:** Leverages native `apt` under the hood to resolve package dependencies.

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
