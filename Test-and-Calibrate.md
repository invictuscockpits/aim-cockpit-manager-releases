# Test and Calibrate

**What you'll do:** verify that every wired control reads correctly in the manager, and calibrate your potentiometers so their full travel maps cleanly to the sim.

## Before you begin

- At least one panel has pins assigned. See [[Assign Controls to Pins]].
- Your controls are physically wired to the board. See [[Wiring Your Switches, Knobs, and Pots]].

---

## Live panel view

Every panel in the manager has a **Live** view that shows real-time state for every control on that panel — no simulator needed.

Open a panel, then click the **Live** tab (or **Test** button, depending on your manager version).

![Live panel view showing switch states and pot positions](images/test-live-view.png)

Flip a switch or turn a knob on the physical board. The matching control in the live view should respond immediately. Work through each control one at a time.

### Reading the live view

| What you see | What it means |
|---|---|
| Switch flips in sync with the physical switch | Correct wiring and pin assignment |
| Switch doesn't respond at all | Wrong pin number, or wiring issue — see below |
| Switch always shows as ON | GND and GPIO are shorted, or the switch is normally-closed |
| Pot bar moves when you turn the knob | Correct wiring and ADC assignment |
| Pot bar doesn't move | Wrong ADC channel or wiring issue — see below |
| Pot bar moves but is noisy/jittery | Long wiring run picking up noise, or an unwired pot channel — see below |

---

## Calibrate a potentiometer

Raw pot readings rarely span the full range the sim expects. Calibration tells the manager what the physical minimum and maximum positions are, so it can translate them accurately.

### Steps

1. In the live view, right-click the pot you want to calibrate and select **Calibrate**.
2. Slowly turn the knob back and forth through its full range of travel several times. The manager watches the incoming values and captures the range automatically — no buttons to click while sweeping.
3. When the reading looks stable and the bar spans the full range, click **Save**.

![Right-click context menu on a pot showing the Calibrate option, and the calibration dialog with a live bar auto-capturing the range](images/test-calibrate-pot.png)

If the result doesn't look right — the bar starts mid-range, or stops short — click **Clear** to discard the captured values and sweep the knob again from scratch.

> [!TIP]
> If the pot reads backwards (turning clockwise decreases the value instead of increasing it), swap the 3.3V and GND wires on the pot.

---

## Diagnosing problems

### A switch doesn't respond

1. **Check the pin assignment.** In the panel view, confirm the control is assigned to the correct GPIO pin number. See [[Board Pin Reference]] for the physical pin layout.
2. **Check the wiring.** With the board powered, use a multimeter in continuity mode across the switch terminals to confirm it's switching. Then confirm the wire from the GPIO pin goes all the way back to the board header — no broken joints.
3. **Try a neighboring pin.** Temporarily assign the control to an adjacent pin and bridge that pin to GND with a wire. If the manager responds, the original pin is fine and the issue is in the wiring to that pin. If it still doesn't respond, the pin may be damaged — try a different one.

### A pot doesn't move

1. **Check the ADC channel.** Confirm the pot is assigned to an ADC channel (not a GPIO pin number).
2. **Check the supply wires.** The wiper wire carries the signal, but the pot needs 3.3V and GND connected to the outer terminals to produce a signal. Confirm both are wired.


### A pot is jittery or noisy

- **Unassigned potentiometer channels** float and read random values if nothing is connected to them. If you see jitter on a control you don't plan to wire, right-click it and select **Mute** to disable it. If you do plan to wire it later, you can ignore the jitter for now — it goes away once a pot is connected and calibrated.
- **Long wiring runs** can pick up interference. Try a shorter run or twisted-pair wiring between the pot and the board.
- **Dirty pot wiper.** On older pots, a worn wiper causes noise. Try exercising the knob through its full range a few times; if it doesn't improve, the pot may need replacing.

---

**Next:** [[Swap or Replace a Board]] or continue to [[Set Up DCS]]
