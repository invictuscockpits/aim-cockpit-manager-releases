# Set Up DCS

**What you'll do:** install the DCS integration from the manager with one click, so your cockpit controls send commands to DCS World and your cockpit lights and displays update from the sim.

## Before you begin

- DCS World 2.9 or newer is installed and has been launched at least once (so its Saved Games folder exists).
- The manager is installed and running. See [[Install the Manager]].
- At least one board is configured. See [[Add Your First Board]].

## Steps

### 1. Open the DCS Integration card

From the manager home page, click the **DCS** icon, then scroll down to the **DCS Integration** card.

![DCS Integration card showing detected DCS variants and install status](images/dcs-setup-button.png)

The card lists every DCS variant the manager detected under your Saved Games folder — **DCS**, **DCS.openbeta**, and **DCS.openalpha** — and shows the install status for each. If a variant you expect to see isn't listed, it means DCS hasn't been launched yet and its Saved Games folder doesn't exist.

### 2. Install the integration

Click **Install**. The manager installs the integration into every detected variant at once:

- Copies **AIM_export.lua** and its supporting library files into `Saved Games\[variant]\Scripts\AIM\`
- Adds a single load line to `Scripts\Export.lua` so DCS picks them up automatically on launch

If you already have other tools hooked into `Export.lua` (such as other export scripts), the manager adds its line alongside them without disturbing anything else.

![DCS Integration card after a successful install showing green status per variant](images/dcs-setup-dialog.png)

> [!NOTE]
> If the card shows **Update available** rather than **Install**, a newer version of the integration is bundled with this version of the manager. Click **Update** to replace the older files — the process is identical to a fresh install.

### 3. Launch DCS

Start DCS World and load into the F-16C. The integration activates automatically — no in-game steps required.

### 4. Confirm the connection

Back in the manager, the DCS Integration card should show **Connected**. If you're sitting on the DCS main menu rather than in a cockpit it may show **Waiting** — that's normal; it connects once you're in an aircraft.

![DCS Integration card showing Connected status](images/dcs-connected.png)

## Check it worked

Flip a switch on your cockpit panel. The corresponding switch in DCS should move. If your aircraft has cockpit indicator lights or displays wired to your panel hardware, they should update to match the sim state.

## If something's wrong

| Problem | Fix |
|---|---|
| Status stays at "Not installed" after installing | Check that DCS has been launched at least once so the Saved Games folder exists, then reinstall. |
| Status shows "Installed" but never "Connected" | Make sure DCS is running and you're loaded into a mission, not sitting on the main menu. |
| Controls reach the manager but nothing happens in DCS | Confirm you're in the F-16C — the integration is aircraft-specific. Other aircraft are not yet supported. |
| A switch moves in the manager live view but not in DCS | The control may not be simulated in DCS. Hover the control in the manager — the tooltip will say if it's not modeled. |

---

**Next:** [[Cockpit Displays in DCS]]
