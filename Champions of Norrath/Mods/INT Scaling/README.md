# INT Scaling

Spell damage now scales with Intelligence. In the base game, INT has no effect on spell damage.

## Effect

Each point of INT above 20 increases all spell damage by 0.5%. Melee and physical attacks are unaffected.

| INT | Damage Bonus |
|---|---|
| 20 | +0% |
| 60 | +20% |
| 100 | +40% |
| 200 | +90% |

## Installation

1. Place the `.pnach` file in your PCSX2 `patches/` folder
2. Enable patches in PCSX2 settings
3. Boot the game normally

> **Note:** Save states require booting the game first. Load your save state after reaching the title screen.

## Compatibility

NTSC-U (v1.0) — CRC `90E66BC5` (clean) or `84056BCA` (DNAS patched)

## Customization

Two values control the scaling curve. Edit them directly in the `.pnach` file.

### Base INT (line 27)

The INT value where scaling begins. Below this, spells deal normal damage.

`patch=1,EE,208D9050,extended,________`

| Value | Base INT | Meaning |
|---|---|---|
| `25080000` | 0 | Every point of INT adds damage |
| `2508FFF6` | 10 | Scaling starts at INT 10 |
| `2508FFEC` | 20 | **(default)** Scaling starts at INT 20 |
| `2508FFE2` | 30 | Scaling starts at INT 30 |
| `2508FFD8` | 40 | Scaling starts at INT 40 |
| `2508FFCE` | 50 | Scaling starts at INT 50 |

### Coefficient (line 30)

How much each point of INT above the base adds to the multiplier.

`patch=1,EE,208D905C,extended,________`

| Value | Per-INT Bonus | INT 60 | INT 100 | INT 200 |
|---|---|---|---|---|
| `3C093A03` | 0.1% | +4% | +8% | +18% |
| `3C093A84` | 0.2% | +8% | +16% | +36% |
| `3C093BA4` | **0.5% (default)** | +20% | +40% | +90% |
| `3C093C24` | 1.0% | +40% | +80% | +180% |
| `3C093CA4` | 2.0% | +80% | +160% | +360% |
| `3C093D4C` | 5.0% | +200% | +400% | +900% |

> Damage examples assume base INT of 20. Formula: `bonus = (INT - base) × coefficient`
