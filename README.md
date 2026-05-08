Architecture du Projet : Jeu RPG Java (MVC Strict)

Ce projet repose sur une implémentation rigoureuse du motif d'architecture **Model-View-Controller (MVC)**. L'objectif est de garantir une séparation totale entre la logique métier, le rendu graphique et la gestion des entrées utilisateur.

## 🏗 Architecture Globale

### 1. Le Modèle (Model)
Le Modèle est totalement indépendant et "aveugle". Il gère l'état interne du jeu, les calculs mathématiques et la logique métier sans aucune dépendance graphique.

#### 🌍 La classe World
Point d'entrée unique du Modèle, elle contient :
* Le `Player`.
* Les listes d'entités (`List<InteractableLivingEntity>`).
* Les objets au sol (`List<InteractableItem>`).
* Les limites physiques de la carte.

#### 🧬 Hiérarchie des Entités
* **Entity** : Racine contenant les coordonnées (X, Y) et les informations de base.
* **LivingEntity** : Gère les statistiques vitales (HP, Attack, Defense), l'inventaire et les effets de statut.
    * *Spécialisations* : `Player`, `Enemy` (ex: `Slime`), `NPC` (ex: `Merchant`).
* **Item** : Objets inertes pouvant être stockés ou utilisés.
    * *Spécialisations* : `Equippable` (Armor, Weapon) et `Consumable` (Potion).

#### ⚔️ Logique de Combat
Le combat est traité exclusivement au sein du Modèle via un échange de messages entre objets :
1.  `Attack(target)` : Calcule les dégâts en fonction des statistiques et des `StatusEffect`.
2.  `takeDamage(amount)` : La cible réduit les dégâts par sa défense et met à jour ses HP.
3.  `OnDeath()` : Gère les conséquences logiques (XP, loot, état `DEAD` etc...).

---

### 2. Le Contrôleur (Controller) - *En prévision*
Le Contrôleur est le "cerveau" moteur du jeu.
* **GameEngine** : Gère la boucle de jeu (*Game Loop*). Il appelle la méthode `Update()` du `World` à intervalle régulier.
* **InputManager** : Traduit les touches clavier/souris en ordres logiques pour le Modèle (ex: `Z` -> `player.moveUp()`).

### 3. La Vue (View) - *En prévision*
La Vue est purement contemplative.
* Elle lit les données du `World` (positions, états).
* Elle affiche les sprites correspondants.
* Elle n'a aucune logique de décision.

---

## 🛠 Interfaces & Contrats
Pour assurer la modularité, le projet utilise des interfaces strictes :
* **Updatable** : Contrat de base pour tout objet nécessitant une mise à jour par frame.
* **InteractableLivingEntity** : Définit les comportements de combat et de dialogue.
* **InteractableItem** : Définit la logique des items (ex ramassage).

## 🚀 État d'avancement
- [x] Conception UML du Modèle (v12)
- [x] Hiérarchie des classes et héritage
- [x] Système d'effets de statut et buffs
- [x] Architecture du World
- [ ] Conception UML du Controller
- [ ] Conception UML de la vue
- [ ] Implémentation du Modèle
- [ ] Implémentation du Controller
- [ ] Implémentation de la Vue


