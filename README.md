<p align="center">
<img src="https://api.iconify.design/lucide:package-check.svg?color=%23d70a53&width=130&height=130" alt="debup logo" />
</p>

<h1 align="center">debup</h1>

<p align="center">
<strong>The Obtainium-like CLI package manager for Debian & Ubuntu distributions.</strong><br>
Track, install, and upgrade <code>.deb</code> packages directly from GitHub Releases.
</p>

<p align="center">
<a href="LICENSE"><img src="https://img.shields.io/badge/License-GPLv3-blue.svg" alt="GPL v3"></a> &nbsp;
<a href="https://debian.org"><img src="https://img.shields.io/badge/Platform-Debian%20%7C%20Ubuntured.svg" alt="Platform"></a> &nbsp;
<a href="#"><img src="https://img.shields.io/badge/Arch-all%20(any)-orange.svg" alt="Arch"></a> &nbsp;
<a href="https://www.gnu.org/software/bash/"><img src="https://img.shields.io/badge/Language-Bash-4EAA25.svg" alt="Bash"></a>
</p>

<p align="center">
<a href="https://github.com/Uraam/debup/releases"><img src="https://img.shields.io/github/v/release/Uraam/debup?color=brightgreen" alt="Release"></a> &nbsp;
<a href="#"><img src="https://img.shields.io/badge/Package_Size-3.41_Ko-success.svg" alt="Size"></a> &nbsp;
<a href="https://github.com/Uraam/debup/releases"><img src="https://img.shields.io/github/downloads/Uraam/debup/total?color=blueviolet" alt="Total Downloads"></a>
</p>

---

<h1>
debup <img src="https://api.iconify.design/lucide:package-check.svg?color=%23d70a53&width=30&height=30" alt="debup logo" style="vertical-align: middle;"/>
</h1>

</p> 

**debup** is a lightweight, zero-bloat CLI package manager for Debian and Ubuntu-based systems. Inspired by Android's **Obtainium**, it tracks, installs, and updates `.deb` packages directly from official **GitHub Releases** on **all architectures**.

No PPAs, no bloated sandboxes, no third-party repositories - just native `.deb` binaries fetched straight from upstream.

---

## ⚡ Quick First Install
**One-command installation:**

```bash
curl -fsSL https://github.com/Ruraam/debup/releases/latest/download/debup_2.1.1_all.deb -o /tmp/debup.deb && sudo apt install -y /tmp/debup.deb && rm -f /tmp/debup.deb
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

To uninstall cleanly later:
```bash
sudo apt remove --purge debup
```
---

### GitHub API Rate Limits (Optional)

By default, GitHub limits unauthenticated requests to 60 per hour. If you track many packages or encounter rate-limit errors, you can provide a GitHub Personal Access Token (classic withno special scopes needed, or fine-grained with public access).

**Set it in your shell environment:**

*Temporary (current session)*
```bash
export GITHUB_TOKEN="ghp_your_personal_access_token"
```
*Permanent*
```bash
echo 'export GITHUB_TOKEN="ghp_your_personal_access_token"' >> ~/.bashrc
source ~/.bashrc
```
`debup` will automatically detect and use it, boosting your limit to 5,000 requests per hour.

---

## 🛠️ Usage

### Package Management

**Add a repository to track:**
```bash
debup add <owner>/<repo>
```
for exemple:
```bash
debup add fastfetch-cli/fastfetch
```

**List tracked repositories**
```bash
debup list
```
**Remove a tracked repository**
```bash
debup remove <package-name>
```

### Package Updates/Upgrade
**Download and upgrade tracked packages with onfirmation**
```bash
debup upgrade 
```
skip confirmation
```bash
debup upgrade -y
```
or 
```bash
debup upgrade <package-name>
```

---
>|
>**💡 Tip:** Combine official repos and GitHub releases by aliasing `sudo apt update && sudo apt upgrade -y && debup upgrade` in your `~/.bashrc`.
>|
---

## ✨ Highlights

- **Native Workflow:** Standard `add`, `list`, `remove`, `update`, and `upgrade` syntax.
- **Architecture Aware:** Automatically detects CPU architecture (`amd64`, `arm64`, `all`).
- **Self-Updating:** Automatically tracks and updates itself via `debup`.
- **Dependency Handling:** Leverages native `apt` under the hood to resolve package dependencies.

---

## ⚙️ Configuration

**Tracked sources are stored in:**

`/etc/debup/sources.list`

**Format:**

`<package-name>|<github-user>/<github-repo>`

## 🗑️ Uninstallation
**Remove package sudo**
```bash
apt remove debup 
```
**Remove package and clean configuration**
```bash
sudo apt --purge debup
```
## Screenshoots
<p align="center">
<img src="/assets/debup_1.png" width="400"> <img src="/assets/debup_2.png" width="400"> <img src="/assets/debup3.png" width="400"> <img src="/assets/debup4.png" width="400">



---

##📄 License

This project is licensed under the [GNU General Public License v3.0](LICENSE).
