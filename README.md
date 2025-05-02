# 🕹️ PlayerStatus

A Java class that stores and manages a player's state in a game, following OOP principles: **encapsulation**, **modularity**, **reusability**, and **information hiding**.

---

## ✅ Project Goal

- Represent a player's game state and update it based on game rules.
- Apply OOP principles: proper visibility, logical separation, clean and reusable methods.

---

## 📦 Internal State (Attributes)

| Attribute       | Type    | Description                                       |
|------------------|---------|---------------------------------------------------|
| `nickname`       | String  | Player's name *(read-only)*                      |
| `score`          | int     | Player's score                                   |
| `lives`          | int     | Number of lives                                  |
| `health`         | int     | Health level (0 - 100)                           |
| `weaponInHand`   | String  | Current weapon                                   |
| `positionX`      | double  | Position on the X-axis                           |
| `positionY`      | double  | Position on the Y-axis                           |
| `gameName`       | String  | Game name *(static - shared by all players)*     |

---

## 🎮 Game Rules

1. **Health**:
   - Drops to 0 → player loses 1 life, `health` resets to 100.
   - If `lives` = 0 → Game Over.
   - `health > 100` → clamped to 100.

2. **Weapons (`weaponInHand`)**:
   - `knife` (1000 points), `sniper` (10000 points), `kalashnikov` (20000 points).
   - Compare using `.equals()`, not `==`.
   - Can only be purchased if `score` ≥ weapon cost.

3. **Player duels**:
   - Same weapons: the winner is the player with the higher calculated power:
     \[
     (3 × health + score ÷ 1000) ÷ 4
     \]
   - Different weapons: the winner depends on weapon strength and distance.

4. **Distance**:
   - Calculated using the Euclidean formula:
     \[
     \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}
     \]

---

## ⚙️ Required Methods

### ✅ Initialization
- `initPlayer(String nickname)`
- `initPlayer(String nickname, int lives)`
- `initPlayer(String nickname, int lives, int score)`

### ✨ Artifacts
- `findArtifact(int artifactCode)`
  - **Perfect** → +5000 points, +1 life, `health = 100`
  - **Prime** → +1000 points, +2 lives, `health +25` *(max 100)*
  - **Trap (divisible by 3 and digit sum divisible by 3)** → -3000 points, -25 `health`
  - **Other codes** → +`artifactCode` points

### 🔫 Weapons
- `setWeaponInHand(String weapon)` – sets weapon if valid and score is sufficient
- `getWeaponInHand()` – returns current weapon

### 📍 Positioning
- `movePlayerTo(double x, double y)` – updates the player's position

### 🎮 Game Name
- `gameName` – should be `static`, accessed via getter & setter

### 🧑‍🚀 Player Name
- `nickname` – read-only, accessible only via getter

### ⚔️ Combat
- `shouldAttackOpponent(PlayerStatus opponent)` – returns `true` if the player should attack the opponent

---

## 🧠 OOP Notes

- `nickname` is read-only → only a getter is provided
- `gameName` is `static`, accessed through controlled methods
- Distance is computed in a separate method for modularity
- Fully adheres to OOP principles:
  - Encapsulation (private attributes)
  - Controlled access (public methods)
  - Logical separation and modular structure
