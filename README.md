# Asteroids (Pygame)

A Python remake of the classic arcade game **Asteroids**, built entirely with [Pygame](https://www.pygame.org).  
Control your ship, avoid collisions, and destroy incoming asteroids. The game demonstrates object-oriented programming, sprite groups, and collision detection in Python.

---

## Overview

This project recreates the core mechanics of Asteroids:
- Player movement and rotation with configurable speeds  
- Shooting mechanics with cooldown and projectile velocity  
- Asteroids that spawn randomly and split upon impact  
- Continuous asteroid spawning and update loop  
- Collision detection using circular hitboxes  
- Smooth, frame rate-independent motion via delta time  

The code is structured around modular components: `Player`, `Asteroid`, `AsteroidField`, `Shot`, and `CircleShape`.

---

## Installation

**Requirements**
- Python 3.12 or newer  
- pygame 2.6.1  

**Setup and Run**
```bash
git clone https://github.com/nbishtawi/Asteroids-Pygame.git
cd Asteroids-Pygame
pip install -e .
python main.py
```

---

## Controls

| Action        | Key(s)         |
|----------------|----------------|
| Thrust Forward | W              |
| Reverse        | S              |
| Rotate Left    | A              |
| Rotate Right   | D              |
| Shoot          | Spacebar       |
| Quit Game      | Close Window   |

---

## Project Structure

```
Asteroids-Pygame/
├── main.py             # Main game loop and sprite group management
├── player.py           # Player class for movement and shooting
├── asteroid.py         # Asteroid class with split and collision behavior
├── asteroidfield.py    # Handles random asteroid spawning
├── shot.py             # Projectile class fired by the player
├── circleshape.py      # Base class providing position, radius, and collision logic
├── constants.py        # Game configuration values (screen size, speeds, etc.)
├── pyproject.toml      # Project metadata and dependencies
└── README.md
```

---

## Constants

All gameplay parameters are defined in `constants.py` for easy configuration:

```python
SCREEN_WIDTH = 1280
SCREEN_HEIGHT = 720

ASTEROID_MIN_RADIUS = 20
ASTEROID_KINDS = 3
ASTEROID_SPAWN_RATE = 0.8  # seconds
ASTEROID_MAX_RADIUS = ASTEROID_MIN_RADIUS * ASTEROID_KINDS

PLAYER_RADIUS = 20
PLAYER_TURN_SPEED = 300
PLAYER_SPEED = 200
PLAYER_SHOOT_SPEED = 500
PLAYER_SHOOT_COOLDOWN = 0.3  # seconds

SHOT_RADIUS = 5
```

These values control the game’s difficulty, speed, and dynamics.

---

## Game Logic Summary

### Main Loop (`main.py`)
- Initializes Pygame, sets up sprite groups, and runs the game loop.  
- Handles events, updates all active sprites, detects collisions, and redraws the screen each frame.  
- The delta time (`dt`) ensures movement remains smooth at different frame rates.

### Player (`player.py`)
- Inherits from `CircleShape` and defines rotation, movement, and shooting behavior.  
- Uses vector math for forward motion and projectile direction.

### Asteroids (`asteroid.py` and `asteroidfield.py`)
- `AsteroidField` spawns new asteroids along screen edges at intervals.  
- `Asteroid` instances move continuously and split into smaller asteroids when destroyed.

### Collision System (`circleshape.py`)
- All objects share circular collision detection via the `collides_with()` method.  
- When a shot intersects an asteroid, the asteroid is destroyed or split.

### Projectiles (`shot.py`)
- Simple circular objects that move in a straight line and disappear upon impact.

---

## Design Notes

- The project uses **Pygame sprite groups** (`updatable`, `drawable`, `asteroids`, `shots`) for efficient update and rendering cycles.  
- **CircleShape** acts as a base class providing shared physics and collision logic.  
- The code follows an **object-oriented structure** for maintainability and clarity.  
- Frame updates are tied to delta time to ensure consistent gameplay at varying frame rates.
