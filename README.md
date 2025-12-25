# homebrew-tap

This repository contains Homebrew formulae for OpenSource Tools (and related utilities) so you or others can install them easily via Homebrew on macOS and Linux.

This README explains:
- how Homebrew taps map to this repo,
- how to install Homebrew (if needed),
- how to tap this repository and install formulae from it on macOS and Linux,
- how to install from a local copy for development,
- how to update/uninstall,
- basic troubleshooting and contributing notes.

Table of contents
- Requirements
- Quick start (remote tap + install)
- Installing Homebrew (macOS & Linux)
- Tapping this repository (remote)
- Installing formulae from this tap
- Installing from a local clone (development)
- Updating / upgrading formulae
- Uninstalling / untapping
- Developing & testing formulae
- Troubleshooting
- Contributing
- License & contact

Requirements
- macOS or a Linux distribution with a POSIX-compatible shell.
- Homebrew installed. (Homebrew is supported on macOS and Linux; instructions below.)
- Git (for tapping from a repository or working locally).

Quick start (recommended)
1. Install Homebrew (if you don’t already have it) — see the “Installing Homebrew” section below.
2. Tap this repo:
   - brew tap 004Ongoro/tap
3. Install the formula you want from the tap:
   - brew install 004Ongoro/tap/<formula-name>

Note: Replace <formula-name> with the actual formula filename (without the .rb) or the name the formula declares. Example placeholders in this README use "tidyup" as an example but check the repo for the actual formula names.

Installing Homebrew

macOS
- Official installation (recommended):
  - /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
- After install, follow the on-screen instructions to add Homebrew to your PATH (on macOS with Apple Silicon it is typically /opt/homebrew).

Linux
- Official installation (recommended):
  - /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
- After the script completes, run:
  - echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> ~/.profile
  - eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
- Confirm installation:
  - brew --version

Tapping this repository (remote)
Homebrew converts repository names with the `homebrew-` prefix to shorter tap names automatically. For this repository:
- Repo: 004Ongoro/homebrew-tap
- Tap name: 004Ongoro/tap

To add the tap from GitHub:
- brew tap 004Ongoro/tap

Alternative (explicit Git URL):
- brew tap 004Ongoro/tap https://github.com/004Ongoro/homebrew-tap

Verify the tap:
- brew tap
- brew tap-info 004Ongoro/tap

Finding available formulae in this tap
- After tapping, list formulae:
  - brew search 004Ongoro/tap
- To show formulae in the tap:
  - brew tap-info 004Ongoro/tap --installed
  - or check the tap repository files (Formula/ or root) to see formula filenames: ls $(brew --repo 004Ongoro/tap)/Formula || ls $(brew --repo 004Ongoro/tap)

Installing formulae from this tap
- Install a formula (remote tap):
  - brew install 004Ongoro/tap/<formula-name>
  Example:
  - brew install 004Ongoro/tap/tidyup
  (Replace tidyup with the real formula name from the repo.)

- Install and force build from source:
  - brew install --build-from-source 004Ongoro/tap/<formula-name>

Installing from a local clone (development / testing)
If you want to develop or test formulae locally, clone the repo and either tap the local copy or install directly from the file.

1) Clone the repository:
- git clone https://github.com/004Ongoro/homebrew-tap.git
- cd homebrew-tap

2a) Tap the local copy (register local repo as a tap)
- brew tap 004Ongoro/tap /full/path/to/homebrew-tap
  - Example:
    - brew tap 004Ongoro/tap $(pwd)
- Then install normally:
  - brew install 004Ongoro/tap/<formula-name>

2b) Install a formula file directly (no tap needed)
- brew install ./Formula/<formula-name>.rb
- Or from repository root if formula is at top-level:
  - brew install ./<formula-name>.rb

Updating the tap and installed formulae
- Update all taps and Homebrew:
  - brew update
- Upgrade installed formulae (all):
  - brew upgrade
- Upgrade a specific formula:
  - brew upgrade 004Ongoro/tap/<formula-name>

Uninstalling and untapping
- Uninstall a formula:
  - brew uninstall <formula-name>
  - If installed from the tap: brew uninstall 004Ongoro/tap/<formula-name>
- Remove the tap:
  - brew untap 004Ongoro/tap

Developing & testing formulae
- Check the formula syntax and style:
  - brew audit --new-formula --style ./Formula/<formula-name>.rb
- Install from local file to test:
  - brew install --build-from-source ./Formula/<formula-name>.rb
- Run formula tests (if the formula defines test do ... end):
  - brew test ./Formula/<formula-name>.rb
- Use brew bump-formula-pr or other Homebrew tooling if you plan to submit to Homebrew/core (not required for a personal tap).

Common troubleshooting
- Permission errors (e.g., "Permission denied"): ensure Homebrew is not run as root. Homebrew should be installed under your user directory (macOS: /opt/homebrew or /usr/local depending on system) and run as the current user.
- "brew: command not found": ensure Homebrew is installed and added to PATH. See "Installing Homebrew" section.
- Formula not found after tapping:
  - Confirm tap is present: brew tap
  - List files in the tapped repo: ls $(brew --repo 004Ongoro/tap)
  - Run brew update and try again.
- Build failures:
  - Make sure build dependencies are installed (Xcode Command Line Tools on macOS: xcode-select --install)
  - Check the formula for missing or outdated resource URLs.
- If you run into issues, run:
  - brew doctor
  - brew config
  - brew update-reset (if your Homebrew state is corrupted) — use with caution.

Contributing
- Fork the repo, create a new branch, make changes to the formula(s) (formula files typically go in Formula/ or the repository root).
- Run tests and audits locally:
  - brew audit --new-formula --strict ./Formula/<formula-name>.rb
  - brew install --build-from-source ./Formula/<formula-name>.rb
  - brew test ./Formula/<formula-name>.rb
- Open a pull request describing changes and how you tested them.
- Follow Homebrew best practices for formula style. If you need help with Ruby formula style, consult Homebrew’s developer documentation: https://docs.brew.sh/Formula-Cookbook

Security & signing
- Homebrew downloads upstream tarballs / releases. Ensure resources referenced by formulae are from trusted upstreams and preferably have checksums (sha256) specified in the formula. Maintainers should update checksums when updating versions.

Repository layout suggestions (if you’re maintaining this tap)
- Formula/ — optional directory for formula files
- <formula-name>.rb — alternative location (root) for formula
- LICENSE
- README.md (this file)
- .github/ (CI/workflows)

License & contact
- Add or check the LICENSE file in this repository for license terms.
- For issues and questions, open issues in this repo or contact the owner at their GitHub: https://github.com/004Ongoro

Notes & examples summary
- Tap the repo:
  - brew tap 004Ongoro/tap
- Install formula:
  - brew install 004Ongoro/tap/<formula-name>
- Install from local clone:
  - git clone https://github.com/004Ongoro/homebrew-tap.git
  - brew tap 004Ongoro/tap /path/to/homebrew-tap
  - brew install 004Ongoro/tap/<formula-name>
- Install Homebrew (macOS & Linux):
  - /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
