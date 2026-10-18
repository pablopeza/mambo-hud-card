<img src="https://cdn.jsdelivr.net/gh/pablopeza/mambo-hud-card@main/images/logo.svg?v=1" alt="Mambo HUD Card logo" width="96">

# Mambo HUD Card

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://github.com/hacs/integration)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/pablopeza/mambo-hud-card/blob/main/LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/pablopeza/mambo-hud-card)](https://github.com/pablopeza/mambo-hud-card/releases)

An instrument-panel Lovelace card for the **Cecotec Mambo Touch** food
processor in Home Assistant. State, time left, temperature, start / pause /
stop, and the temperature, speed, heat power and timer set points in a single
readable panel.

It uses the entities of the [Mambo Touch integration](https://github.com/pablopeza/ha-mambo-touch),
and it's the sibling of the [Vacuum HUD Card](https://github.com/pablopeza/vacuum-hud-card)
and the [Weather Station Card](https://github.com/luisanllo/ecowitt-hud-card),
so they sit well together on a dashboard.

<img src="https://cdn.jsdelivr.net/gh/pablopeza/mambo-hud-card@main/images/preview-light.png?v=1" alt="Light mode preview" width="380"> <img src="https://cdn.jsdelivr.net/gh/pablopeza/mambo-hud-card@main/images/preview-dark.png?v=1" alt="Dark mode preview" width="380">

*Light and dark mode: it follows your active Home Assistant theme.*

> ⚠️ **This is a heating appliance with blades.** The card asks for a second
> tap before it starts a cook with heat, but nobody can see the jar from a
> dashboard. Only start it when someone is next to it, and with the lid on.

## Features

- 🍲 A jar that shows what the Mambo is doing: the blades turn faster with the speed and steam rises while it heats
- ⏱️ Big clock with the time left during a cook, or the timer that will be used
- ▶️ Start, pause, resume and stop. **Starting with heat takes two taps**: the first one says what it will do
- 🌡️ Temperature and timer steppers, speed (0–10) and heat power (1–10) selectors. Taps are gathered and sent once you stop tapping, because during a cook every change goes straight to the robot
- 🔥 Heat power follows the temperature (40 °C → 4) until you pick one
- ⚠️ Banner for the robot's error code and for a lost broker connection
- 👆 Every value opens Home Assistant's more-info dialog when tapped
- 🎨 Visual editor that **pre-fills the integration's entities**
- 🌗 Follows Home Assistant's light/dark theme
- 🌍 UI in English or Spanish, picked from your Home Assistant language

## Requirements

The [Mambo Touch integration](https://github.com/pablopeza/ha-mambo-touch),
which connects Home Assistant to the robot and creates the entities this card
uses.

## Installation

### Via HACS (recommended)

1. HACS → **⋮** menu (top right) → **Custom repositories**
2. URL: `https://github.com/pablopeza/mambo-hud-card`, category **Dashboard**
3. Search for **"Mambo HUD Card"** in HACS → Download
4. Add the resource if HACS doesn't do it for you:
   - URL: `/hacsfiles/mambo-hud-card/mambo-hud-card.js`
   - Type: JavaScript Module

### Manual

1. Download [`mambo-hud-card.js`](https://github.com/pablopeza/mambo-hud-card/blob/main/mambo-hud-card.js) to `config/www/`
2. Settings → Dashboards → **⋮** menu → Resources → add:
   - URL: `/local/mambo-hud-card.js`
   - Type: JavaScript Module

## Configuration

Add the card from the card picker ("Mambo HUD Card") and the editor fills in
the integration's entities. Or use YAML with `type: custom:mambo-hud-card`.
Only `entity` is required; every block hides itself when its entities aren't set.

| Option | Required | Description |
|---|---|---|
| `entity` | ✅ | The integration's status sensor |
| `name` | | Card title (defaults to the device name) |
| `temperature` | | Current temperature sensor |
| `remaining` | | Time left sensor |
| `error` | | Error code sensor (0 = no error) |
| `connected` | | Broker connection `binary_sensor` |
| `target_temperature` | | Target temperature `number` (0 = no heat, else 37–120 °C) |
| `speed` | | Speed `number` (0–10) |
| `power` | | Heat power `number` (1–10) |
| `timer` | | Timer `number`, in seconds |
| `start` / `pause` / `resume` / `stop` | | The integration's buttons (or `script`s) |
| `show_controls` | | Show the control buttons (default `true`) |
| `show_setpoints` | | Show temperature, timer, speed and heat power (default `true`) |

### Example

```yaml
type: custom:mambo-hud-card
entity: sensor.mambo_touch_status
temperature: sensor.mambo_touch_temperature
remaining: sensor.mambo_touch_time_left
error: sensor.mambo_touch_error_code
connected: binary_sensor.mambo_touch_broker_connection
target_temperature: number.mambo_touch_target_temperature
speed: number.mambo_touch_speed
power: number.mambo_touch_heat_power
timer: number.mambo_touch_timer
start: button.mambo_touch_start
pause: button.mambo_touch_pause
resume: button.mambo_touch_resume
stop: button.mambo_touch_stop
```

The temperature stepper goes from no heat to 37 °C (the robot's minimum) and
then in 5 °C steps up to 120 °C. The timer stepper moves in 10 s steps under a
minute, 30 s under 10 minutes, 1 min under an hour and 5 min above. Start is
greyed out until there's a timer: the robot needs one.

While a cook runs, the card shows what the robot reports (the knob on the
robot wins), and the clock counts down in the color of the state: red while
heating, green without heat, amber when paused.

## Why

I wrote it for my own Mambo Touch, to run it from the same dashboard as its
sibling cards instead of from the official app.

## License

[MIT](https://github.com/pablopeza/mambo-hud-card/blob/main/LICENSE)
