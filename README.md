# Pinout Lookup Skill

A Claude Code skill for looking up component pinouts and generating wiring tables.

## Install

```bash
mkdir -p ~/.claude/skills/pinout-lookup
curl -sL https://raw.githubusercontent.com/plc/pcb-wiring-skill/main/skill.md \
  > ~/.claude/skills/pinout-lookup/SKILL.md
```

## Usage

Invoke with `/pinout-lookup` or just ask Claude a wiring question:

```
How do I wire an SSD1306 OLED to a XIAO ESP32-S3?
```

The skill fetches pinout data from this repo and outputs a wiring table with position notation:

```
SSD1306: pins 1-4 left to right, display facing you.
XIAO: L1-L7 left, R1-R7 right, top to bottom, USB at top.

| SSD1306 | #  | XIAO ESP32-S3 | #  |
|---------|----|---------------|----|
| GND     | 1  | GND           | R2 |
| VCC     | 2  | 3V3           | R3 |
| SCL     | 3  | D5 (GPIO6)    | L6 |
| SDA     | 4  | D4 (GPIO5)    | L5 |
```

The wiring is saved to a `WIRING.md` in your current project directory, along with a components list.

### Missing components

If a component isn't on file, the skill will offer to:
- Open a GitHub issue requesting it
- Guide you through contributing it yourself via PR

### Incorrect pinouts

If you spot an error, tell Claude what's wrong and it will open a PR to fix it.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Use [pinout_template.md](pinout_template.md) for the file structure and [WIRING_FORMAT.md](WIRING_FORMAT.md) for the wiring table format.
