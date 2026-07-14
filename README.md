# 🎮 2D Retro Platformer Game (Godot Basics)

Welcome to the **2D Retro Platformer** project! This is my **first tutorial game** built with the **[Godot Engine](https://godotengine.org/) (v4.7)**. It was created as a hands-on learning project to explore and master the fundamentals of 2D game development in Godot, including character physics, basic AI patrolling, game state management, and audio integration.

---

## 🚀 Play the Game
A pre-compiled standalone version of the game is ready to play! 
- Download and extract the **[2D Retro Game.zip](file:///c:/Users/Sagnick/Downloads/new-game/2D%20Retro%20Game.zip)** archive in the root directory.
- Double-click the extracted executable to run the game immediately on Windows (compiled with embedded PCK resource packaging).

---

## 🛠️ Tech Stack & Engine Configuration
- **Game Engine**: Godot Engine 4.7
- **Renderer**: Forward Plus (configured in [project.godot](file:///c:/Users/Sagnick/Downloads/new-game/project.godot))
- **Physics**: 2D standard physics for platforming, plus Jolt Physics configured for 3D queries.
- **Pixel Art Optimization**: Nearest-neighbor texture filtering (Default Texture Filter set to `Nearest`) to maintain clean, crisp pixel art scaling.
- **Audio Autoload**: A persistent global audio player singleton ([music.tscn](file:///c:/Users/Sagnick/Downloads/new-game/scenes/music.tscn)) is configured to play ambient adventure background tracks smoothly across scene resets.

---

## 🎮 Game Controls
The input mappings are configured in the Input Map of [project.godot](file:///c:/Users/Sagnick/Downloads/new-game/project.godot):

| Action | Keyboard Controls | Gamepad Controls |
| :--- | :--- | :--- |
| **Move Left** | `A` or `Left Arrow` | D-Pad Left / Left Analog Stick Left |
| **Move Right**| `D` or `Right Arrow`| D-Pad Right / Left Analog Stick Right |
| **Jump** | `Space`, `W`, or `Up Arrow` | Controller Button (A/Cross) |

---

## 📂 Project Structure

```
├── 📂 assets/                     # Game asset resources
│   ├── 📂 fonts/                  # Custom retro pixel fonts (PixelOperator8)
│   ├── 📂 music/                  # Loopable background music
│   ├── 📂 sounds/                 # Sound effects (jump, death, coin pickup)
│   └── 📂 sprites/                # 2D Sprite sheets (player, slimes, tilemap)
├── 📂 scenes/                     # Packaged Godot scene files (.tscn)
│   ├── game.tscn                  # Main game world scene
│   ├── player.tscn                # Player character scene
│   ├── green_slime.tscn           # Patrolling green slime scene
│   ├── purple_slime.tscn          # Patrolling purple slime scene
│   ├── coin.tscn                  # Collectible coin scene
│   └── platform.tscn              # Moving/stationary platform scene
└── 📂 scripts/                    # GDScript logic files
    ├── player.gd                  # Character controller
    ├── slime.gd                   # Patrolling enemy logic
    ├── coin.gd                    # Coin collision & scoring
    ├── killzone.gd                # Trap/hazard controller
    └── game_manager.gd            # Score & UI manager
```

---

## 💻 Script-by-Script Breakdown

Here is an overview of the GDScript code implementation powering the game mechanics:

### 👤 Player Controller ([player.gd](file:///c:/Users/Sagnick/Downloads/new-game/scripts/player.gd))
Manages character movement, gravity, and animations.
* **Physics**: Uses `CharacterBody2D` with velocity integration and `move_and_slide()`.
* **Animations**: Controls the `AnimatedSprite2D` node to transition between `idle`, `run`, and `jump` animations based on speed, ground status, and moving direction.
* **Sound Effects**: Plays the jump sound effect via an `AudioStreamPlayer2D` node on action trigger.

### 👾 Slime Patrolling AI ([slime.gd](file:///c:/Users/Sagnick/Downloads/new-game/scripts/slime.gd))
Provides the movement and direction control logic for the basic slime enemies.
* **Direction Detection**: Uses left and right `RayCast2D` sensors.
* **Movement**: Moves horizontally at a constant speed of `60` units.
* **Flipping behavior**: When a sensor detects an obstacle/wall collision, the direction flips (`-1` or `1`) and the animated sprite flips horizontally (`flip_h`) dynamically.

### 🪙 Collectible Coin ([coin.gd](file:///c:/Users/Sagnick/Downloads/new-game/scripts/coin.gd))
Handles the coin pick-up event.
* **Collection**: When a `CharacterBody2D` (the Player) enters the `Area2D` collision shape, it triggers the collection logic.
* **Point Dispatch**: Calls `add_point()` on the `%GameManager` node.
* **Pickup Animation**: Plays a pickup animation sequence which triggers the sound effect and handles clean-up (`queue_free()`).

### 💀 Death Zone Hazard ([killzone.gd](file:///c:/Users/Sagnick/Downloads/new-game/scripts/killzone.gd))
Manages the player death penalty when touching enemies or falling off the map.
* **Tragical Effect**: Triggers a slow-motion effect by setting `Engine.time_scale = 0.5`.
* **Player Deactivation**: Disables/frees the player's `CollisionShape2D` to visually drop the player character off the screen.
* **Reset Loop**: Plays the death sound effect, starts a timer, and reloads the current scene (`get_tree().reload_current_scene()`) upon timeout, resetting the time scale back to `1.0`.

### 🎛️ Game Manager ([game_manager.gd](file:///c:/Users/Sagnick/Downloads/new-game/scripts/game_manager.gd))
A centralized node tracking game score and HUD details.
* **Score State**: Increments score when coins are collected.
* **HUD Refresh**: Updates the screen's `Label` text dynamically.

---

## 🛠️ How to Load the Project in Godot

If you want to view, play, or edit the source code inside Godot:
1. Download and install **Godot Engine 4.7** (or compatible 4.x release).
2. Clone this repository or download the source code zip.
3. Open the Godot Project Manager, click **Import**, and navigate to the project directory.
4. Select the [project.godot](file:///c:/Users/Sagnick/Downloads/new-game/project.godot) file and open it.
5. Press **F5** to run the project directly from the editor!

---

*Made with 💖 while learning the Godot Engine.*
