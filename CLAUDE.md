# PCB Wiring Skill

A Claude Code skill that provides PCB pinout knowledge and wiring guidance.

## Project Structure

```
pcb-wiring-skill/
  skill.md              -- Skill instructions (loaded by Claude Code)
  boards/               -- Board reference files with ASCII pinouts
    xiao-esp32s3.md     -- XIAO ESP32-S3 / Sense / Plus
  reference-images/     -- Source pinout images (not used at runtime)
  README.md             -- User-facing documentation
  CHANGELOG.md          -- Change log
```

## Conventions

- All board diagrams orient USB port facing north
- Pin labels on left side read right-to-left (outward)
- Pin labels on right side read left-to-right (outward)
- Source of truth for pin data: manufacturer wiki/docs (URL at top of each board file)

## Adding Boards

1. Download reference images from manufacturer into `reference-images/`
2. Read the images to extract pin positions and functions
3. Create ASCII art in `boards/<board-name>.md` following existing format
4. Include: front/back ASCII diagrams, pin table, bus defaults, power notes, variant differences

## Key Decisions

- ASCII art chosen over image references because Claude Code operates in a terminal
- GPIO numbers always paired with board pin names for unambiguous identification
- Separate board files to keep context small when only one board is relevant
