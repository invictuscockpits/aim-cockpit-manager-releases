# Cockpit Displays in BMS

**What you'll do:** configure BMS to send your MFD, DED, RWR, EHSI, and HUD views to your secondary monitors using the BMS RTTRemote display system.

## Before you begin

- BMS is installed. The RTTRemote tool (`RTTClient64.exe`) lives at `[BMS install]\Tools\RTTRemote\`. If that folder doesn't exist, RTTRemote may not have been included in your BMS installation — check your BMS version.
- You have already assigned your monitors in the **Multi-Display Management** dialog. This is shared with DCS — the role assignments (Left MFD, Right MFD, DED, etc.) are set once and used for both sims. See [[Cockpit Displays in DCS]] for how to set this up.

## How BMS display output works

BMS can render cockpit views to external monitors using **RTTRemote** — a helper tool included with BMS that reads textures from BMS and paints them into windows on your secondary monitors. The manager configures RTTRemote automatically by writing `RTTClient.ini` and enabling the texture export flag in `Falcon BMS.cfg`. You only need to click **Apply BMS Displays** — no manual INI editing required.

## Steps

### 1. Open the display setup

On the manager home page, find the **DISPLAY MANAGEMENT** card and click **Setup displays**.

In the **3. EXPORT** section at the bottom of the dialog, you'll see the **APPLY BMS DISPLAYS** button and a BMS status line.

### 2. Check the BMS display helper status

The status line shows:
- **BMS display helper not found** — RTTRemote isn't installed at the expected path. Check your BMS installation.
- **BMS displays: not applied yet** — RTTRemote is found but not yet configured.
- **BMS displays: update available** — configured but your role assignments have changed since the last apply.
- **BMS displays: installed** — configured and current.

The **APPLY BMS DISPLAYS** button is only enabled when RTTRemote is found.

### 3. Apply BMS displays

Click **APPLY BMS DISPLAYS**. The manager:

- Writes `[BMS install]\Tools\RTTRemote\RTTClient.ini` with a display entry for each assigned role, at the pixel coordinates the dialog calculated.
- Sets `g_bExportRTTTextures 1` in `Falcon BMS.cfg` to enable texture export.

The status line updates to **BMS displays: installed**.

> [!IMPORTANT]
> **Always launch BMS using "Launch without any Setup override."**
>
> Launching with a Setup override causes BMS to regenerate `Falcon BMS.cfg` — which overwrites the texture export flag the manager just set. Your displays go black and your keyfile gets clobbered at the same time. "Launch without any Setup override" is the only safe launch mode.

### 4. Start RTTClient

RTTClient64.exe is the tray app that actually paints the display windows on your monitors. You can start it manually or have the manager start it automatically.

**Manual:** Navigate to `[BMS install]\Tools\RTTRemote\` and run `RTTClient64.exe`. It appears in your system tray.

**Automatic:** In the manager, go to **Settings** and enable **Auto-launch BMS display tool**. The manager detects when BMS starts running and launches RTTClient64 automatically.

### 5. Launch BMS and fly

Start BMS using **"Launch without any Setup override."** Load into a mission. Your secondary monitors should show the assigned cockpit views as soon as you're in the cockpit.

## Check it worked

Each assigned monitor should display its cockpit view — Left MFD, Right MFD, DED, and so on. RTTClient64 will be visible in the system tray.

The dialog's BMS status line reads **BMS displays: installed**.

## If something's wrong

| Problem | Fix |
|---|---|
| APPLY BMS DISPLAYS button is grayed out | RTTRemote wasn't found. Check that `[BMS]\Tools\RTTRemote\RTTClient64.exe` exists. |
| Displays are black after launching BMS | BMS was likely launched with a Setup override, which reset the cfg. Re-apply in the manager and relaunch BMS using "Launch without any Setup override." |
| RTTClient tray icon appears but displays are empty | Make sure you're loaded into a mission. BMS only exports textures once an aircraft is active, not from the main menu. |
| Display is assigned but doesn't appear on that monitor | Check that RTTClient64 is running (system tray). If it's not there, start it manually or enable auto-launch in Settings. |
| Status shows "BMS displays: update available" | Your monitor assignments changed since you last applied. Click APPLY BMS DISPLAYS again and relaunch BMS. |

---

**See also:** [[Cockpit Displays in DCS]], [[Set Up Falcon BMS]], [[Load the Keyfile]]
