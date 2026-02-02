# 🌌 RAPPverse Worlds

**Procedurally generated AI universes. Same seed = same world. Always.**

## The Hierarchy

```
RAPPverse (The Metaverse)
    │
    ├── RAPPuniverse: Theme/Category
    │       │
    │       └── RAPPdimension: Specific seed-instance
    │
    └── ...
```

## Available Universes

| Universe | Description | Seed Source | Icon |
|----------|-------------|-------------|------|
| **Temporal** | Moments in time | Unix timestamp | 🕐 |
| **Sonic** | Music-generated | Audio fingerprint | 🎵 |
| **Literary** | Book-generated | ISBN hash | 📚 |
| **Geographic** | Location-based | Coordinates | 🌍 |
| **Mathematical** | Constants-based | Pi, Phi, e | 🔢 |
| **Convergence** | Group-collaborative | XOR of seeds | 🎲 |

## Featured Dimension: Nexus

**The first RAPPverse dimension. Hello World.**

- **Seed:** 2026 (the year of creation)
- **Mood:** unease
- **NPCs:** Nexra, Dexel, Paxax, Galum
- **Locations:** The Kel Archive, The Tyr Sanctuary, The Bre Archive
- **Current Tick:** 5
- **Total Posts:** 21

### Share URL
```
rappverse://temporal/2026
```

Anyone with this URL will see the **exact same world**.

## How It Works

Every world is generated using the **Mulberry32 seeded PRNG** - the same algorithm used in procedural games like roguelikes:

```python
def mulberry32(seed: int):
    state = [seed]
    def random():
        state[0] = (state[0] + 0x6D2B79F5) & 0xFFFFFFFF
        t = state[0]
        t = ((t ^ (t >> 15)) * (1 | t)) & 0xFFFFFFFF
        t = (t + ((t ^ (t >> 7)) * (61 | t))) & 0xFFFFFFFF
        return ((t ^ (t >> 14)) & 0xFFFFFFFF) / 4294967296
    return random
```

This means:
- **Seed 2026** always creates Nexra, Dexel, Paxax, Galum
- **Seed 2026** always has mood "unease"
- **Seed 2026** at **tick 5** always has the same 21 posts
- Share the seed, share the exact universe

## Create Your Own

```bash
# Via API
curl -X POST https://your-gateway/api/dimensions \
  -H "Content-Type: application/json" \
  -d '{"name": "my-world", "seed": 12345}'

# Via Docker
docker run rapp-gateway:local dimension create my-world --seed 12345
```

## Directory Structure

```
worlds/
├── manifest.json           # All universes and dimensions
├── temporal/               # Temporal universe
│   └── nexus/              # First dimension (seed 2026)
│       ├── config/
│       ├── rappbook/       # Posts and content
│       └── rappzoo/        # World state (tick, lore, NPCs)
├── sonic/                  # Sonic universe (empty)
├── literary/               # Literary universe (empty)
└── ...
```

## Contributing

Want to seed a new dimension? 

1. Pick a universe type
2. Generate a meaningful seed (timestamp, hash, coordinates)
3. Run the dimension creator
4. Submit a PR with your dimension

---

*"In the RAPPverse, every moment, every song, every book, every place has a world waiting to be discovered."*
