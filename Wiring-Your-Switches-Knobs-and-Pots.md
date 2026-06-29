# Wiring Your Switches, Knobs, and Pots

**What you'll do:** physically connect your cockpit controls to the AIM board using the correct wiring pattern for each type.

This page covers the three main control types — switches, rotary encoders, and potentiometers. For the exact pin locations on your board, see [[Board Pin Reference]].

## Before you begin

- You know which board each panel is assigned to. See [[Add Your First Board]].
- You have your panel hardware ready — switches, pots, and/or encoders mounted in your cockpit panel.
- You have suitable wiring: 22–26 AWG stranded wire works well for most cockpit wiring runs.

All board headers use **JST PH** connectors. Pre-crimped wires and mating headers are available at **invictuscockpits.com** — buying these saves a significant amount of time over crimping your own.

---

## Switches and momentary buttons

Toggle switches, flip switches, guarded switches, push buttons — all wire the same way.

**Connection:** one leg to the GPIO pin, the other leg to **GND**.

```
GPIO pin  ──┤ switch ├──  GND
```

The board reads **closed = on/pressed**. It does not matter which leg goes to which terminal on the switch — switches have no polarity.  However, for stadardization's sake, I typically wire the GPIO pins to the outer leg of the switch, and the GND to the inner.  For two position switches,indicators, and other items that only require one GPIO a good way to save board space is to tie the grounds of two switches together, and connect GPIOs to the individual switch legs, allowing you to connect two switches to one header.

> [!NOTE]
> You do not need a pull-up resistor. The board's GPIO pins have internal pull-ups enabled; they read high when the switch is open and low when it's closed. Each header also has series resistors on the GPIO lines for protection — the board is ready to wire directly.

### Three-position switches

A three-position (ON-OFF-ON or ON-ON-ON) switch needs **two GPIO pins** — one for each end position. Wire the center tap to GND, and each outer terminal to its own GPIO pin.

```
GPIO pin A  ──┤ terminal 1 ├──
                               common ── GND
GPIO pin B  ──┤ terminal 2 ├──
```

The manager reads the combination: both pins open = center/off, pin A closed = position 1, pin B closed = position 2.

### Spring-loaded (momentary) switches

Wire identically to standard switches. The momentary behavior is handled in software — you don't need to do anything different in the wiring.

---

## Rotary encoders

Rotary encoders (used for knobs that turn continuously without a fixed stop) use two GPIO pins for the A and B pulse signals. Most encoders also have a common pin.

**Connection:**

```
GPIO pin A  ──  encoder A output
GPIO pin B  ──  encoder B output
GND         ──  encoder common / GND
```

If your encoder has a push-to-click function (the knob also acts as a button), wire the click terminals as a standard switch to a third GPIO pin and assign it separately in the manager.

> [!TIP]
> Encoder direction (clockwise vs counter-clockwise) depends on which way you wire A and B. If the encoder counts backwards in the manager's live view, swap the A and B wires — no need to change anything in the software.

---

## Potentiometers and Hall-effect sensors

Pots are used for analog controls — volume knobs, the BARO knob, trim wheels, and any other control that has a range of positions rather than discrete stops. Hall-effect sensors wire identically.

**Connection (three terminals):**

```
3.3V  ──  one outer terminal   (supply)
P1–P8 ──  wiper (center tap)   (signal)
GND   ──  other outer terminal (return)

```

> [!IMPORTANT]
> Use the board's **3.3V** supply pin, not 5V. Feeding 5V into an ADC channel will damage the board.

It doesn't matter which outer terminal gets 3.3V and which gets GND — swapping them reverses the direction (minimum becomes maximum). Either orientation works; you can flip it in the calibration step if needed. See [[Test and Calibrate]].

### Multiple pots on one panel

Each pot uses its own potentiometer channel (P1–P8). Sidewinder boards have 8 potentiometer channels; the Phoenix has none and cannot accept potentiometers or Hall-effect sensors. 

---

## Wiring runs and connector tips

- Keep runs under about 1 meter where possible. Longer unshielded runs can pick up noise on potentiometer channels and cause jitter in the live view.
- All board headers use **JST PH** connectors — use JST PH throughout your harnesses for consistency. The one exception is the backlighting channels, which use **Micro MATE-N-LOK** connectors (board header: TE Connectivity 2-1445093-2; wire-side housing: 1445022-2, 3mm pitch, 2-position). Pre-crimped wires and headers for both types are available at invictuscockpits.com.
- Label both ends of your harness before routing. Once cables are bundled and routed through the cockpit, tracing an unlabeled wire is painful.

---

**Next:** [[Test and Calibrate]]

**See also:** [[Board Pin Reference]], [[Assign Controls to Pins]]
