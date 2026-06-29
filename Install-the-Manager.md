# Install the Manager

**What you'll do:** download the installer, run it, and get the manager open for the first time.

## Before you begin

- Windows 10 (21H2+) or Windows 11. See [[What You Need]] for the full checklist.

## Steps

### 1. Download the installer

Go to the [Releases](../../releases) page and download the latest `AIM-Cockpit-Manager-vX.X.X-Setup.exe`. Pick the most recent version at the top of the list.

### 2. Run the installer

Double-click the downloaded file. Windows will show a User Account Control prompt before anything is installed.

![Windows UAC prompt showing Invictus Machine LLC as the verified publisher](images/install-uac-prompt.png)

The **Verified publisher** line should read **Invictus Machine LLC** — the company behind Invictus Cockpit Systems. If it reads "Unknown publisher" or anything else, stop and contact support before continuing.

Click **Yes** to allow the install.

### 3. Complete the installer

The installer is straightforward — click through the wizard. It places the manager under `Program Files` and adds a Start Menu entry and an optional desktop shortcut.

![Installer welcome screen](images/install-wizard.png)

### 4. Launch the manager

Open **AIM Cockpit Manager** from the Start Menu or desktop shortcut.

On the very first launch, Windows Defender Firewall may ask whether to allow the app on your network. Click **Allow access** and make sure the **Private networks** box is checked. The manager needs to listen for boards on your cockpit network; if you dismiss or block this prompt, boards won't appear — see [[Troubleshooting]] if that happens.

![Windows Firewall prompt for AIM Cockpit Manager](images/install-firewall-prompt.png)

### 5. Check for updates

The manager checks for a newer version each time it launches. If an update is available, a banner appears across the top of the window. You can install updates from there — no need to re-download the installer from the releases page.

## Check it worked

The manager should open to the **Network** page and show a status bar at the bottom. It's normal to see "No boards connected" at this point — you haven't set up the network yet.

## If something's wrong

| Problem | Fix |
|---|---|
| "Unknown publisher" in the UAC prompt | Download the installer again directly from the [Releases](../../releases) page. |
| Installer won't run / Windows blocks it | Right-click the installer → **Properties** → **Unblock** → try again. |
| Manager won't open after install | Check Start Menu for "AIM Cockpit Manager." If it's not there, re-run the installer. |
| Boards not appearing after launch | Continue to [[Set Up the Cockpit Network]] — discovery needs the network configured first. |

---

**Next:** [[Set Up the Cockpit Network]]
