
# AntWorldSim

A lightweight **ant colony simulation** environment built with Python and Pygame.  
It models how multiple ants explore a 2D grid world, collect food, and return to their nest, featuring individual memory, collision handling, and shared nest intelligence.

## Features
- Configurable map size (default 150×150).
- Nest area: 4×4, Food zone: 10×10 (supports multiple food sources in `Adam_ants_2`).
- Two ant types: **explorer ants** (with personal memory) and **defender ants**.
- BFS-based return path planning and turn-based environment updates.
- Centralized nest memory that merges explored regions and discovered food.
- Real-time **Pygame visualization** with two simulation entry scripts:
  - `scripts/main_visual.py` – Base version.
  - `scripts/main_visual_stage2.py` – Enhanced version with shared memory and path tracing.

## Project Structure
```
AntWorldSim/
├─ antagent/
│  ├─ __init__.py
│  ├─ AntAgent.py          # Main ant agent with memory and pathfinding
│  └─ AntAgent_1.py        # Simplified early version
├─ envs/
│  ├─ __init__.py
│  ├─ Adam_ants_1.py       # Single food source
│  └─ Adam_ants_2.py       # Multiple food sources (main)
├─ env_interface.py        # Interface v1
├─ env_interface_2.py      # Interface v2 with nest memory and scheduling
├─ scripts/
│  ├─ main_visual.py
│  └─ main_visual_stage2.py
├─ requirements.txt
├─ .gitignore
└─ README.md
```

## Requirements
- **Python** 3.10+
- **Packages:** `numpy`, `pygame`

Installation:
```bash
# (Recommended) create a virtual environment
python -m venv .venv
.\.venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt
```

## How to Run
From the project root:
```bash
# Version 1:
python -m scripts.main_visual

# Version 2 (recommended):
python -m scripts.main_visual_stage2
```
You can modify map size or random seed directly in the script by editing the `AntSimInterface(seed=...)` argument.

## Key Files
- **`antagent/AntAgent.py`**  
  Each ant maintains a 150×150 memory grid (0: unknown, 1: walkable, 2: food).  
  - `decide_move()`: prefers unexplored tiles during exploration mode.  
  - `plan_return_path()`: BFS to compute the shortest route back to the nest.  
- **`envs/Adam_ants_2.py`**  
  Randomly places the nest and several 10×10 food regions at a safe distance.  
- **`env_interface_2.py`**  
  Handles “decide first, resolve later” updates for multiple ants per round.  
  Aggregates nest-level knowledge and controls staggered departures.

## Common Issues
1. **Pygame window won’t open or GPU-related errors**  
   Check your GPU drivers, lower `clock.tick()` in the visualization loop, or reduce `MAP_SIZE`.

2. **ImportError: No module named 'envs.Adam_ants_2'**  
   Ensure you’re running from the project root using `python -m scripts.main_visual_stage2`.

3. **Too fast or too slow**  
   Adjust `clock.tick(...)` inside the visualization script.

## Git Setup (First Time)
Example for GitHub:
```powershell
# Initialize
git init
git add .
git commit -m "Initial commit: AntWorldSim v1"

# Create a new empty GitHub repo (e.g., AntWorldSim)
git branch -M main
git remote add origin https://github.com/<YOUR-USERNAME>/AntWorldSim.git
git push -u origin main
```

## Summary
**AntWorldSim** serves as a base simulation platform for experimenting with  
multi-agent coordination, swarm intelligence, and reinforcement learning concepts.
