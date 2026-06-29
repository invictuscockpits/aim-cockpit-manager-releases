# Set Up the Cockpit Network

**What you'll do:** give your PC a second IP address on the cockpit subnet so the manager can find your boards.

Your boards and the manager talk to each other on a private subnet — `192.168.100.x`. Your PC needs to have the address `192.168.100.1` on the Ethernet adapter that's connected to the cockpit switch. This doesn't affect your internet connection; your other adapter (Wi-Fi or the one plugged into your router) keeps working normally.

## Before you begin

- Your cockpit Ethernet adapter is physically connected to your PoE switch.
- The PoE switch is powered on.
- The manager is installed and running. See [[Install the Manager]].

## Option A — Let the manager do it (recommended)

The manager checks your network configuration when it launches. If it detects that the cockpit adapter doesn't have the right IP, it shows an alert on the **Network** page.

![Network page alert showing "Cockpit network not reachable" with a Fix button](images/network-fix-banner.png)

1. Click the adapter name in the alert to confirm it's your cockpit adapter (not your internet connection).
2. Click **Fix** — the manager will ask for administrator permission (one UAC prompt), add `192.168.100.1` to that adapter, and verify the change.
3. The alert disappears and the status updates to **Listening**.

That's it. The fix persists across reboots; you won't need to do this again unless Windows resets the adapter (sometimes happens after a major Windows update or driver reinstall — the manager will alert you again if it does).

## Option B — Set it manually

Use this if the automatic fix didn't work, or if you prefer to set it yourself.

### If your adapter is on a static IP (no DHCP)

1. Press `Win + R`, type `ncpa.cpl`, and press Enter.
2. Right-click your **cockpit Ethernet adapter** → **Properties**.
3. Select **Internet Protocol Version 4 (TCP/IPv4)** → **Properties**.
4. Click **Advanced…**
5. Under **IP addresses**, click **Add…**
6. Enter IP `192.168.100.1`, subnet mask `255.255.255.0` → **Add**.
7. Click **OK** through all three dialogs.

### If your adapter is set to DHCP

The Advanced → Add button is grayed out on DHCP adapters. Use PowerShell instead:

1. Right-click Start → **Terminal (Admin)** or **Windows PowerShell (Admin)**.
2. Find your cockpit adapter name:

    ```powershell
    Get-NetAdapter | Where-Object Status -eq 'Up'
    ```

    Note the `Name` column — it's usually `Ethernet`, `Ethernet 2`, or similar. Don't pick your Wi-Fi adapter.

3. Add the IP (replace `Ethernet` with your adapter's actual name):

    ```powershell
    New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress 192.168.100.1 -PrefixLength 24
    ```

4. Confirm it took:

    ```powershell
    Get-NetIPAddress -InterfaceAlias "Ethernet" | Format-Table IPAddress, PrefixLength
    ```

    You should see both your original DHCP-assigned address **and** `192.168.100.1` in the list.

## Check it worked

Switch back to the manager. The Network page should show:

- Status: **Listening**
- No alert banner

Power on a board. Within a few seconds of it booting, a row should appear in the board list with a green or amber dot and the board's IP address. If you see it, you're done — move on to [[Add Your First Board]].

## If boards still don't appear

Work through these checks in order:

**1. Link light on the switch port.** Look at the port your board is plugged into — there should be a green or amber LED. No light at all means a cable, PoE, or power issue. Swap the cable first.

**2. PoE standard.** Confirm your switch supports **IEEE 802.3at** (PoE+). Boards will not power up from an 802.3af (standard PoE) switch. Check your switch's specs.

**3. Right adapter.** The `192.168.100.1` address has to be on the adapter that's physically connected to the cockpit switch, not a virtual adapter or your Wi-Fi. Run `ipconfig` in a terminal and look for `192.168.100.1` under the correct adapter.

**4. Windows Firewall.** If you dismissed the firewall prompt when the manager first launched, port 8888 inbound may be blocked. Check **Windows Defender Firewall → Allow an app through Windows Firewall** and make sure **AIM Cockpit Manager** is checked for **Private networks**.

**5. Still nothing?** See [[Troubleshooting]] for deeper steps.

---

**Next:** [[Add Your First Board]]
