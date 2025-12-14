# PowerShell Dotfiles (Oh My Posh Setup)

Personal PowerShell configuration using **Oh My Posh**, **posh-git**, and quality-of-life modules for a modern dev workflow.

Designed for **Windows + PowerShell 7**.  
If you’re on legacy Windows PowerShell, expect pain.

---

## Preview

- Custom Oh My Posh prompt (`thomas.omp.json`)
- Git status integration
- Node.js version + package manager detection
- Icons, fuzzy finding, history-based autocomplete
- Minimal aliases, no magic nonsense

---

## Requirements

You need the following installed **before** this works:

### 1. PowerShell 7+
```powershell
winget install Microsoft.PowerShell
```

Verify:
```powershell
pwsh --version
```

---

### 2. Scoop (package manager)
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex
```

Verify:
```powershell
scoop --version
```

---

### 3. Git for Windows
```powershell
scoop install git
```

Verify:
```powershell
git --version
```

---

## Dependencies

Install all required tools with Scoop:

```powershell
scoop install `
  oh-my-posh `
  fzf `
  z `
  neovim
```

PowerShell modules:

```powershell
Install-Module posh-git -Scope CurrentUser -Force
Install-Module Terminal-Icons -Scope CurrentUser -Force
Install-Module PSReadLine -Scope CurrentUser -Force
Install-Module PSFzf -Scope CurrentUser -Force
```

Restart PowerShell after installing modules.

---

## Nerd Font (Required)

This setup **requires a Nerd Font**, or icons will break.

Recommended:
```powershell
scoop bucket add nerd-fonts
scoop install Hack-NF
```

Then set your terminal font to:
```
Hack Nerd Font
```

(Windows Terminal → Settings → Profile → Appearance)

---

## Setup

### 1. Clone the repo
```powershell
git clone https://github.com/<your-username>/<repo-name>.git $HOME\.dotfiles
```

---

### 2. Symlink the Oh My Posh config
```powershell
New-Item -ItemType SymbolicLink `
  -Path $HOME\thomas.omp.json `
  -Target $HOME\.dotfiles\thomas.omp.json `
  -Force
```

---

### 3. Symlink the PowerShell profile

Check your profile path:
```powershell
$PROFILE
```

Then:
```powershell
New-Item -ItemType SymbolicLink `
  -Path $PROFILE `
  -Target $HOME\.dotfiles\user_profile.ps1 `
  -Force
```

> If symlinks fail, run PowerShell **as Administrator once**.

---

## What This Profile Does

- Loads **Oh My Posh** with `thomas.omp.json`
- Enables **posh-git** branch + status info
- Adds **Terminal-Icons** for file listings
- Configures **PSReadLine**:
  - History-based predictions
  - Emacs keybindings
  - Disabled bell
- Enables **fzf** for:
  - Ctrl+F → provider search
  - Ctrl+R → reverse history
- Adds common aliases:
  - `g` → git
  - `ll` → ls
  - `vim` → nvim
  - `tig`, `less`, `grep`

No telemetry. No startup bloat. No shell hijacking.

---

## Troubleshooting

### Icons are broken
- You didn’t set a Nerd Font
- Restart the terminal after changing fonts

### Prompt doesn’t load
```powershell
oh-my-posh --version
```
If that fails, Oh My Posh isn’t installed correctly.

### Git info not showing
```powershell
Import-Module posh-git
```
If that errors, reinstall the module.

---

## Notes

- This setup assumes **Node.js is installed** for the Node segment to appear
- If Node isn’t present, that segment silently hides (by design)
- Works best in **Windows Terminal**

---

## License

Use it, fork it, break it, improve it.  
Just don’t blame me if you can’t go back to the default prompt.
