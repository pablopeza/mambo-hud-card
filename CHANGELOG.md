# Changelog

## 0.1.0

First release.

### Added

- Jar that shows what the Mambo is doing: the blades turn with the speed and
  steam rises while it heats.
- State, a big clock with the time left (or the timer that will be used) and
  the current temperature.
- Start / pause / resume / stop. Starting a cook with heat takes two taps:
  the first one says what it will do ("Heat to 80 °C? Tap again").
- Temperature and timer steppers, speed (0-10) and heat power (1-10)
  selectors. Taps are gathered and sent once you stop tapping, since during a
  cook every change goes to the robot.
- Error and broker connection banner.
- Visual editor that pre-fills the entities of the
  [Mambo Touch integration](https://github.com/pablopeza/ha-mambo-touch).
- Follows Home Assistant's light/dark theme; English and Spanish.
