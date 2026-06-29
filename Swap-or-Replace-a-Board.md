# Swap or Replace a Board

**What you'll do:** move a board's full configuration — panels, pin assignments, and calibration — to a replacement board without redoing the setup wizard.

This is useful when a board needs to be exchanged under warranty, or when you're re-using a pin map from one build in another.

## Before you begin

- You have access to the board you want to copy the config *from* (the source board), or you have a previously exported config file.
- The replacement board is connected to your cockpit network and showing as **NEW** or **UNCONFIGURED** in the manager.

---

## Export the config from the source board

1. Open the **Network** page and click the board you want to export from.
2. Click **Export Config**. The manager saves a `.json` file — save it somewhere you'll find it, like your desktop.

![Export Config button on a configured board's detail panel](images/swap-export-config.png)

> [!TIP]
> Export a config backup any time your board is fully set up and working. If you ever need to restore it — or adopt it onto a replacement — you'll be glad you have it.

---

## Import the config onto the replacement board

1. Click the replacement board (the one showing **NEW** or **UNCONFIGURED**).
2. Click **Import Config** instead of going through the wizard.
3. Select the `.json` file you exported.
4. The manager pushes the full configuration — name, panels, pin assignments, calibration — to the replacement board.

![Import Config button on a new board's row](images/swap-import-config.png)

The board reboots, applies the config, and reappears with the same name as the original. All controls should work exactly as they did on the source board.

---

## If the boards are different models

A Sidewinder config imported onto a Phoenix (or vice versa) will import what it can, but some assignments may not transfer:

- **GPIO pins** that exist on the source board but not the destination are left unassigned — you'll see them highlighted in the pin assignment view.
- **ADC channels** follow the same rule.

After importing, check the live view for each panel and reassign any controls that didn't transfer.

---

## Removing a board from the registry

If a board is permanently gone and you want to remove it from the manager's board list:

1. Click the board on the Network page.
2. Click **Delete**. The manager will ask you to confirm before removing it.

> [!NOTE]
> Removing a board from the manager doesn't reset the board itself. If you plug the old board back in, it will reappear as a new board — you can then import a saved config onto it. See [Export the config from the source board](#export-the-config-from-the-source-board) above for why keeping a config backup is a good habit.

---

**See also:** [[Add Your First Board]], [[Assign Controls to Pins]], [[Troubleshooting]]
