# 🏎️ Rocket League: The Ultimate Technical & Strategic Master Manual

Welcome to the definitive, high-level documentation guide for **Rocket League**. This repository contains deep technical specifications, underlying physics engine mechanics, UI/Main Menu architecture, control setups, advanced mechanical executions, and competitive team rotation dynamics.

---

## 1. Main Menu & Interface Architecture

The main interface is structured for fast navigation across competitive playlists, garage customization, social management, and technical settings.

* **Play:** 
  * **Casual:** 1v1, 2v2, 3v3, 4v4 Chaos. Unranked matchmaking designed for practice, warm-ups, or casual sessions with friends.
  * **Competitive:** 1v1 Duel, 2v2 Doubles, 3v3 Standard. Ranked playlists utilizing MMR (Matchmaking Rating) and skill tiers ranging from Bronze to Supersonic Legend.
  * **Extra Modes:** Rumble (power-ups), Dropshot (floor tile destruction), Hoops (basketball physics), Snow Day (puck physics on ice).
  * **Tournaments:** Automated bracket competitions scheduled hourly across different regions and rank groups.
  * **Custom Games:** Exhibition matches against bots or private matches with customizable mutators (gravity, ball size, respawn time).
  * **Training:** Freeplay (unlimited boost, infinite ball control), Custom Training (user-created packs for shots, saves, and aerials), and Tutorial modes.
* **Garage:** 
  * **Customize Car:** Modify body presets, decals, paints (primary and secondary finishes), wheels, rocket boosts, topper hats, goal explosions, engine audio, and antennas.
  * **Manage Inventory:** Trade-in system for duplicate items, blueprint crafting, and archiving items.
  * **Edit Presets:** Switching between custom-built vehicle profiles and loadouts.
* **Item Shop:** 
  * **Featured Items:** Rotating selection of exotic wheels, painted goal explosions, and Black Market decals available for Credits.
  * **Daily Items:** Single individual items refreshing every 24 hours.
  * **Esports Shop:** Official RLCS team decals, banners, and wheels allowing direct revenue support for professional organizations.
* **Rocket Pass:** 
  * **Tier Progression Path:** Free and Premium tiers unlocking cosmetic items, XP boosts, and tournament credits as you play matches.
  * **Weekly & Season Challenges:** Specific gameplay objectives (e.g., "Get 10 saves in online matches") providing massive XP drops to accelerate tier progression.
* **Settings:** 
  * **Gameplay:** Chat restrictions, cross-play toggle, colorblind filters, weather effects, and game speed modifiers.
  * **Camera:** FOV, distance, height, angle, stiffness, swivel speed, and transition speed.
  * **Controls:** Controller layout configuration, deadzones, and sensitivities.
  * **Video / Graphics:** Resolution, display mode, vertical sync (V-Sync), frame rate limit, render quality, and world detail sliders.
  * **Audio:** Master volume, game sounds, crowd volume, music track player, and voice chat options.
  * **Interface:** UI scale, team color options, performance graphs (FPS, ping, packet loss indicators).
* **Profile:** 
  * **Career Stats:** Comprehensive cumulative metrics including total matches played, win/loss percentage, goals scored, saves, shots on goal, and MVPs earned.
  * **Leaderboards:** Global and friend rankings for competitive playlists and wins.
  * **Replays:** Saved match recordings allowing full theater-mode camera control, timeline scrubbing, and spectator analysis.
  * **Title Selection:** Equip unlocked tournament winner titles, season rewards, or special event tags.

### Top Bar & Sidebar Controls
* **Currency Display:** Displays available Credits, Esports Tokens, and Tournament Credits.
* **Party Management:** Allows joining, inviting, and managing friends via Epic Games or platform social lists.
* **Notification Center:** Logs recent trade offers, tournament alerts, party invites, and system announcements.

---

## 2. Physics Engine & Core Vehicle Dynamics

Rocket League operates on a modified **Unreal Engine 3 PhysX** framework. Understanding vehicle physics constants is key to precise car control.

### Speed & Velocity Thresholds
* **Base Driving Speed:** Max ground velocity without boost is **1,410 Unreal Units (uu/s)** (~50.7 km/h / 31.5 mph).
* **Boosting Speed Limit:** Max speed achieved via boost alone is **2,300 uu/s** (~82.8 km/h / 51.4 mph).
* **Supersonic Threshold:** Activated at **2,200 uu/s**.
  * Visual/audio indicators: Wheel trail effects and a sonic boom sound.
  * Maintaining supersonic: Holding accelerate maintains supersonic speed in a straight line without spending boost.
* **Hard Speed Cap:** **2,300 uu/s** is the absolute engine cap. Boosting while supersonic yields no extra speed and wastes boost.

### Hitbox Classes & Collision Profiles

| Hitbox Class | Length (uu) | Width (uu) | Height (uu) | Primary Characteristics |
| :--- | :--- | :--- | :--- | :--- |
| Octane | 118.01 | 84.20 | 36.16 | Balanced height and turns; standard meta choice for aerials and 50/50s. |
| Dominus | 127.93 | 83.28 | 31.30 | Longer, flatter profile; exceptional for powerful flicks and pinches. |
| Plank (Batmobile) | 128.82 | 84.67 | 29.39 | Widest and lowest profile; incredible surface area coverage for ground hits. |
| Breakout | 131.50 | 80.52 | 30.15 | Longest narrow chassis; specialized for sharp angle redirects. |
| Hybrid | 127.02 | 82.20 | 34.16 | Blends Octane and Dominus features; versatile turning circle. |
| Merc | 120.72 | 76.81 | 41.56 | Tallest and boxiest profile; massive vertical surface area for demoing and blocking. |

* **Surface Power Dynamics:**
  * **Front Bumper:** Highest force transfer (ideal for power shots).
  * **Corners:** Maximum directional vector force for long clears.
  * **Roof:** Medium power, optimal for soft catches, dribbles, and upward pops.
  * **Underside / Wheels:** Lowest force transfer (soft contact). Used to cushion flip resets or catch heavy aerial balls.

---

## 3. Advanced Movement & Ground Mechanics

Ground Control Flow: `Normal Drive` -> `Powerslide Turn` -> `Wave Dash` -> `Speed Flip` -> `Supersonic`

### Powerslide & Drift Management
* **Friction Reduction:** Holding powerslide drops lateral wheel friction close to zero.
* **Micro-Powerslide Taps:** Tapping powerslide for **0.05 – 0.15s** upon landing at awkward angles prevents momentum loss and wheel drag.

### Flip Timers & Dodge Deadzones
* **Flip Window:** After jumping off a surface, you have **1.25 to 1.45 seconds** to use your second dodge.
* **Infinite Flip Window:** Leaving a surface *without jumping* (ceiling drop, bump, or wheel reset) grants a flip with **no time limit**.
* **Dodge Deadzone:** Controls stick displacement required to register a flip vs. a double jump (Recommended: **0.55 – 0.70**).

### Speed Flip Execution Sequence
1. Execute a **diagonal flip forward** (30° to 45° angle left or right).
2. **Flip Cancel:** Instantly pull the stick straight down (180° opposite) within **100ms** of dodging.
3. Hold **Air Roll Left/Right** and **Powerslide** on contact to keep the nose aligned straight while the impulse propels you forward.

---

## 4. Aerial Dynamics & Flight Physics

### Fast Aerial Technique
1. Hold **Boost** and tilt stick back.
2. Press **Jump** (1st Jump).
3. **Release stick** to neutral (prevents accidental backflip).
4. Press **Jump** again while maintaining **continuous boost**.

### Directional Air Roll (DAR) Control
Using dedicated Air Roll Left or Right enables simultaneous 3-axis flight manipulation (Pitch, Yaw, and Roll).
* **Tornado Spin:** Hold Air Roll Left while holding the stick to the Right (or vice versa) to adjust your trajectory without losing momentum.

---

## 5. Ball Mechanics, Pinches & Flicks

### Ball Elasticity & Impact Physics
* **Spherical Collider:** The ball uses a high-restitution spherical collider.
* **Hit Velocity Equation:** 
  $$\text{Hit Velocity} = (\text{Car Velocity} \times \text{Hitbox Angle Multiplier}) + (\text{Ball Incoming Velocity} \times \text{Restitution})$$

### Musty Flick Physics
Tilt the car nose downward past 90° forward, then execute a **backflip**. Because the car nose is tilted past vertical, the backflip vector launches both the car and the ball forward at high speed.

### Pinch Mechanics
Simultaneously compressing the ball between the car bumper and a surface (wall, floor, crossbar) converts compression force into explosive speed.
* **Kuxir Pinch:** Pinched against the side wall at a 45° angle to shoot directly across the field into the opponent's net.
* **Ground Pinch:** Air dribbling downward and pinching the ball into the turf right upon contact, launching it upward into the top corner at velocities exceeding 120 km/h.

---

## 6. Rotations, Positioning & Defensive Tactics

### 3v3 Field Positioning
* **First Man (Pressure):** Forces early opponent touches, disrupts defenses via bumps/demos, and challenges the ball handler.
* **Second Man (Support):** Collects winning 50/50s, finishes passes, maintains support spacing, and intercepts weak opposition clears.
* **Third Man (Safety):** Last line of defense behind the ball's center line. Never commits fully unless possession is 100% secured to prevent counter-attacks.

### Shadow Defense
Drive in the same direction as the attacking player while maintaining a 1–2 car-length gap:
* Matches attacker speed seamlessly.
* Covers top-shelf shots with back-facing aerials.
* Covers ground shots with quick powerslide challenges.
* Removes the risk of a head-on whiff that leaves an open net.

---

## 7. Esports Benchmark Settings

### Camera Settings
* **Camera Shake:** OFF
* **Field of View (FOV):** 110.0
* **Distance:** 260.0 - 280.0
* **Height:** 90.0 - 110.0
* **Angle:** -3.0 - -5.0
* **Stiffness:** 0.35 - 0.55
* **Swivel Speed:** 4.50 - 6.00
* **Transition Speed:** 1.20 - 1.40

### Control Sensitivities
* **Controller Deadzone:** 0.05 - 0.08
* **Dodge Deadzone:** 0.60 - 0.70
* **Steering Sensitivity:** 1.30 - 1.60
* **Aerial Sensitivity:** 1.30 - 1.60

---

## 8. Warm-Up & Training Packs

* **Fast Aerials:** A154-AD0E-8820-2216
* **Ultimate Warm-Up:** FA24-B2B7-2E3E-56B6
* **Wall Shots:** 9F6D-4387-4C57-231B
