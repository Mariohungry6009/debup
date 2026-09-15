# debup
Debup – A command-line (CLI) DEB package manager for Debian- and Ubuntu-based distributions. Add a Git repository, check for new versions, and perform updates or installations via APT.

for help type 'debup'

Usage

debup add owner/repo or url.          Install and track a GitHub deb package

debup update                          Check if update available

debup upgrade [-y]                    Check and upgrade all tracked packages

debup list                            List all tracked packages

debup remove <package_name>           Untrack (and optionally purge) a package
