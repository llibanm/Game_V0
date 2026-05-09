# Project Architecture: Java RPG Game (Strict MVC)

This project is built on a rigorous implementation of the **Model-View-Controller (MVC)** architectural pattern. The goal is to ensure a complete separation between business logic, graphical rendering, and user input handling.

## 🏗 Global Architecture

### 1. The Model
The Model is fully independent and "blind". It manages the internal game state, mathematical calculations, and business logic with no graphical dependencies.

#### 🌍 The World Class
The single entry point of the Model, it contains:
* The `Player`.
* The entity lists (`List<InteractableLivingEntity>`).
* Items on the ground (`List<InteractableItem>`).
* The physical boundaries of the map.

#### 🧬 Entity Hierarchy
* **Entity**: Root class containing coordinates (X, Y) and basic information.
* **LivingEntity**: Manages vital statistics (HP, Attack, Defense), inventory, and status effects.
    * *Specializations*: `Player`, `Enemy` (e.g. `Slime`), `NPC` (e.g. `Merchant`).
* **Item**: Inert objects that can be stored or used.
    * *Specializations*: `Equippable` (Armor, Weapon) and `Consumable` (Potion).

#### ⚔️ Combat Logic
Combat is handled exclusively within the Model through message passing between objects:
1. `Attack(target)`: Calculates damage based on statistics and `StatusEffect`.
2. `takeDamage(amount)`: The target reduces incoming damage by its defense and updates its HP.
3. `OnDeath()`: Handles logical consequences (XP, loot, `DEAD` state, etc.).

---

### 2. The Controller - *Planned*
The Controller is the game engine's "brain".
* **GameEngine**: Manages the game loop. It calls the `Update()` method of `World` at regular intervals.
* **InputManager**: Translates keyboard/mouse inputs into logical commands for the Model (e.g. `Z` -> `player.moveUp()`).

### 3. The View - *Planned*
The View is purely observational.
* It reads data from `World` (positions, states).
* It renders the corresponding sprites.
* It has no decision-making logic.

---

## 🛠 Interfaces & Contracts
To ensure modularity, the project uses strict interfaces:
* **Updatable**: Base contract for any object requiring a per-frame update.
* **InteractableLivingEntity**: Defines combat and dialogue behaviours.
* **InteractableItem**: Defines item logic (e.g. picking up).

## 🚀 Progress
- [x] UML design of the Model (v12)
- [x] Class hierarchy and inheritance
- [x] Status effect and buff system
- [x] World architecture
- [ ] UML design of the Controller
- [ ] UML design of the View
- [ ] Model implementation
- [ ] Controller implementation
- [ ] View implementation
