# What You Need

Before you install the manager or plug anything in, make sure you have everything on this list. Missing any one item is the most common reason a first-time setup stalls.

## Computer

- **Windows 10 (21H2 or newer) or Windows 11** — 64-bit. The manager does not run on macOS or Linux.
- **Two network adapters** — one for your internet connection (Wi-Fi is fine), and one **wired Ethernet adapter** dedicated to the cockpit boards. Most desktop PCs already have a built-in Ethernet port; a USB-to-Ethernet adapter works if you don't have a spare port.

> [!IMPORTANT]
> The cockpit network runs on its own isolated subnet. Your cockpit Ethernet adapter must be separate from your internet adapter — if they share the same adapter or the same switch as your router, board discovery will not work.

## Network gear

- **An IEEE 802.3at PoE switch** — sometimes labeled "PoE+" or "802.3at." Your boards draw power from the Ethernet cable; a standard switch without PoE, or one that only supports the older 802.3af standard, will not power them. An unmanaged switch is fine; you do not need managed VLANs or QoS.
- **Standard Cat5e or Cat6 patch cables** — one per board, run from the board to the PoE switch. Length limit is 100 m (328 ft) per Ethernet spec.

> [!TIP]
> If you're building a full pit, a small 8-port 802.3at PoE switch mounted inside the cockpit keeps the wiring clean. You only need one Ethernet cable running from the pit to the PC.

## Flight simulators

Install whichever you plan to use before running through the sim setup steps.

- **DCS World 2.9 or newer** — the manager installs the integration automatically; you don't need to edit any files by hand.
- **Falcon BMS 4.37 or newer** — fully supported as of manager v1.1.0. BMS 4.38+ is recommended for cockpit displays (RTTRemote is more reliable on the newer build).

## Invictus AIM hardware

You'll need at least one configured AIM board to get anything working — a **Sidewinder** (46 GPIOs, 8 Potentiometers, 2 I2c Channels, and 2 SPI Channels) or a **Phoenix** (16 GPIOs, 8 I2C channels). See the product pages at invictuscockpits.com for details on what's in each board.

The **VFT5 force-transducer side-stick** connects via USB separately from the board network and has its own section: [[VFT5 Side-Stick]].

## What you do *not* need

- A separate driver install for the panel boards — they're discovered over the network with no additional software.
- Admin rights for day-to-day use — the manager runs as a normal user. You'll need to approve one elevated action when setting up the cockpit network for the first time (the manager walks you through it).
- A DHCP server — the boards and the PC use static IPs on the cockpit subnet.
> [!NOTE]
> **Falcon BMS users:** BMS requires a virtual joystick driver to receive button and axis inputs from your cockpit hardware. The manager installs this for you — it's a one-time step covered in [[Install the Virtual-Joystick Driver]]. DCS World does not require it.

---

**Next:** [[Install the Manager]]
