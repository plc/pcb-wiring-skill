# pcb-wiring-skill

A Claude Code skill that gives Claude knowledge of PCB development board pinouts and wiring best practices.

## What It Does

When installed, this skill lets Claude:

- Display accurate ASCII pinout diagrams for supported boards
- Guide wiring between boards and peripherals using correct pin names and GPIO numbers
- Warn about voltage mismatches, current limits, and pin conflicts
- Understand board variants (e.g., XIAO ESP32S3 vs Sense vs Plus)

## Supported Boards

| Board | Manufacturer | File |
|-------|-------------|------|
| XIAO ESP32-S3 | Seeed Studio | `boards/xiao-esp32s3.md` |
| XIAO ESP32-S3 Sense | Seeed Studio | `boards/xiao-esp32s3.md` |

## Installation

Add to your project or global Claude Code skills:

```bash
# As a global skill (available in all projects)
# Add to ~/.claude/skills/ or reference in ~/.claude/settings.json
```

## Diagram Convention

All diagrams orient the board with the USB port facing north (top):

```
         +--USB-C--+
         |         |
  pin  -|o       o|- pin
  pin  -|o       o|- pin
         |         |
         +---------+
```

## Adding New Boards

See `skill.md` for the board file format and contribution guidelines. Each board needs:

1. Official manufacturer documentation as source of truth
2. ASCII front and back pinout diagrams
3. Complete pin function table
4. Bus defaults, power notes, and variant differences

## Data Sources

All pin data is sourced from official manufacturer documentation:

- XIAO ESP32-S3: [Seeed Studio Wiki](https://wiki.seeedstudio.com/xiao_esp32s3_getting_started/)
