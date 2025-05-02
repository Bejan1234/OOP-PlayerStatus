# 🕹️ PlayerStatus

Clasă Java ce păstrează starea unui jucător într-un joc, respectând principiile OOP: **incapsulare**, **modularitate**, **reutilizare**, și **ascunderea detaliilor de implementare**.

---

## ✅ Scopul proiectului

- Reprezentarea logică a unui jucător și actualizarea stării sale în joc.
- Respectarea principiilor OOP: vizibilitate corectă, separarea conceptelor, metode clare și reutilizabile.

---

## 📦 Stare internă (atribute)

| Atribut        | Tip     | Descriere                                        |
|----------------|---------|--------------------------------------------------|
| `nickname`     | String  | Numele jucătorului *(read-only)*                |
| `score`        | int     | Scorul jucătorului                               |
| `lives`        | int     | Număr de vieți                                   |
| `health`       | int     | Sănătatea (0 - 100)                              |
| `weaponInHand` | String  | Arma curentă                                     |
| `positionX`    | double  | Poziția pe axa OX                                |
| `positionY`    | double  | Poziția pe axa OY                                |
| `gameName`     | String  | Numele jocului *(static - comun tuturor)*        |

---

## 🎮 Reguli de joc importante

1. **Health**:
   - Scade până la 0 → se pierde 1 viață, `health` revine la 100.
   - Dacă `lives` = 0 → Game Over.
   - `health > 100` → se trunchiază la 100.

2. **Arme (`weaponInHand`)**:
   - `knife` (1000 puncte), `sniper` (10000 puncte), `kalashnikov` (20000 puncte).
   - Comparare cu `.equals()`, nu cu `==`.
   - Poate fi cumpărată doar dacă `score` ≥ costul armei.

3. **Duel între jucători**:
   - Arme identice: câștigătorul e jucătorul cu scor mai mare, calculat astfel:
     \[
     (3 × health + score ÷ 1000) ÷ 4
     \]
   - Arme diferite: câștigă jucătorul cu arma mai puternică în funcție de distanță.

4. **Distanță**:
   - Se calculează cu formula euclidiană:
     \[
     \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}
     \]

---

## ⚙️ Metode necesare

### ✅ Inițializare
- `initPlayer(String nickname)`
- `initPlayer(String nickname, int lives)`
- `initPlayer(String nickname, int lives, int score)`

### ✨ Artefacte
- `findArtifact(int artifactCode)`
  - **Perfect** → +5000 puncte, +1 viață, `health = 100`
  - **Prim** → +1000 puncte, +2 vieți, `health +25 (max 100)`
  - **Capcană (divizibil cu 3 și suma cifrelor div. cu 3)** → -3000 puncte, -25 `health`
  - **Alt cod** → +`artifactCode` puncte

### 🔫 Arme
- `setWeaponInHand(String weapon)` – setează arma dacă e validă și scorul permite
- `getWeaponInHand()` – returnează arma curentă

### 📍 Poziționare
- `movePlayerTo(double x, double y)` – actualizează poziția

### 🎮 Nume joc
- `gameName` – trebuie să fie `static`, accesat prin getter & setter

### 🧑‍🚀 Nume jucător
- `nickname` – `read-only`, doar getter

### ⚔️ Luptă
- `shouldAttackOpponent(PlayerStatus opponent)` – întoarce `true` dacă jucătorul actual ar câștiga lupta

---

## 🧠 Observații OOP

- `nickname` este `read-only` → doar getter
- `gameName` este `static`, acces controlat prin getter/setter
- Calculul distanței trebuie implementat într-o metodă separată
- Respectă principiile OOP:
  - Incapsulare (atribute private)
  - Acces controlat (public methods)
  - Separare logică și modularitate

---


