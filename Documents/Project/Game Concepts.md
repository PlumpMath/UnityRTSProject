# Unity RTS Game Concepts
## Overview
The game will be a real-time strategy (RTS) combat game with a third-person isometric view. The game will eschew general resource collection and building construction in favor of more in-depth tactical controls and an emphasis on unit-to-unit engagement; there will however be the ability to capture points, zones, or wreckage in order to upgrade or purchase new units.

## Menu System
### Main Menu
The main menu will be what the user first views on opening the game. This system should support resource-driven templates in order to facilitate future modifications.

1. New Game
  * The user can select a single map or campaign where resources will carry from map to map
  * The user will select the AI parameters
2. Load Game
  * The user can select to load a saved single map or campaign.
3. Options
  * This screen will contain options to change graphics settings, mouse/keyboard settings, and audio settings.
4. Exit

### In Game

1. Save Game
  * The user will save their current progress to disk. This should have the necessary file browser, overwrite warnings, and generate a summary of the map.
2. Load Game
  * The user can select a game, choose to lose saved progress, and load a separate map.
3. Return to Main Menu

## Gameplay
### Concepts
At the start of any single level, the user will be able to select units to use, load a map, and engage in combat against an AI opponent. Each unit will have a separate status and intelligence that will track skill, fatigue, morale, weapon(s), armor(s), ammunition type(s), and movement capabilities. Each vehicle and weapon will have their own modifiers, such as damage, range, accuracy, failure rate, reload time, turn speed, movement speed (where applicable) and weight.

Once the units are chosen and the level loaded, the user will select starting positions and formations based on the map and starting status. Once placed, the AI will place and the game will turn to real-time mode. The map will have a “fog of war” concept where units outside of visible range of all units will not appear on the screen (or to the AI).

The user can dictate movement, offensive/defensive posture and preparation, targeting, and blind firing.

Various units can deal and take damage when being hit and can be disabled, destroyed, or routed.

Throughout the map will be control points, resource points, and certain areas that allow a better offensive sight line or more defensible area. These can be taken and held by the user or the AI.

The map will end when all units on one side are destroyed, routed, or disabled, or when the time runs out.

### Levels
Levels will consist of at least some traversable terrain, potential still and moving waterways, limited hills and cliffs, jungle or forest, brush, and village/town/city scapes. Each map will have a defined moveability chart and at least a few capture points.

### Campaigns
Campaigns will be maps strung together where units and scores are carried from map to map.

### User Interactions
The user can:

1. Select a single friendly unit
2. Select a group of friendly units via shift-click or dragging a box.
3. Order selected units to move, fire, or change stance.
4. Stats for selected units will be visible on the screen.
5. On hovering a visible unit, the user will have a separate pop-up of unit variables. The amount of data will determine on friendly or not.

### Data to User
The user will have the entire map visible at the start, but will suffer from "fog of war." This may not literally be represented as an obscured area of the map but will be areas where the user cannot see current situations (i.e. opposing units and actions will go invisible). The user will always have visibility on command point changes (such as losing control of a non-visible point).

The user will have an on screen menu system providing feedback on their current mission status, unit status (by group or individual), and environmental status.

## AI Components
The AI should have the following behaviour:

1. Dynamic pathfinding
  * Using A* against a grid defined for each map, the unit should be able to direct themselves independently to a target point.
    * This map will need to be weighted for each type of unit.
    * This will be a 3D non-smoothed Astar path using diagonals
    * Tie breaking heuristics will use a value weighted to the end of the path
  * Upgrade this later to Theta-star
    * This will only exist in 2D at first, LOS calculated by Bresenham's algorithm.
    * Upgrade to 3D later
  * This will later be changed to use either HPA or HPT calculations
    * Need to understand this more
  * The units travelling should not have abrupt turning points when reaching a node; in other words, bezier curves or some other form of linear smoothing should be used. Consider DStar if still using AStar at that point.
2. Tactical decision making
  * The AI engine should have the overall ability to determine near-optimal placement of units based on terrain type, unit variables, and user behaviour.
  * This placement can be considered a number of ways
    1. Zoned: the map is broken into zones of various strenghts and weaknesses
    2. Remaining units: reach and combat value of remaining units is considered
    3. Passivity/Aggression: will determine how units are moved
3. Individual decision making
  * Each unit should have a limited ability to react to immediate prospects.
  * This includes firing, limited retreating, limited advancing, ammunition type choice, and morale influenced behaviour (such as flee/surrender).
  * Firing controls will automatically calculate trajectory based on speed, ammunition, opposing target, and a variance introduced based on experience and skill.
  * A unit can optimize their own placement within the scope of the tactical commands
  * This behaviour will be available to both AI and player vehicles.

## Vehicles
Vehicles will be identified by two factors: Epoch and Modifications.

### Air Vehicles
Not sure if we want real-world aircraft/vehicles other than as stand-ins for abstract concepts.

1. Epoch: Classical (Vietnam)
  * Scout/Recon (Prop/Helo - Sandy/Huey)
  * Precision Attack (A6)
  * Bombing (B52)
  * Tank busting (A1 Skyraider)
  * AA? (F4)
2. Epoch: Modern (Gulf War)
  * Scout/Recon (Drone)
  * Precision Attack (F16)
  * Bombing (B1)
  * Tank Busting (A10)
  * AA (F15)
3. Epoch: Next Gen (Current)
  * Scout/Recon (Stealth Drone)
  * Precision Attack (F35)
  * Bombing (B2)
  * Tank Busting (F35)
  * AA (F22)
4. Epoch: Future (near-term future)
  * Scout/Recon (hover/vstol drone - - think Terminator tilt-jets)
  * Precision Attack (?)
  * Bombing (?)
  * Tank Busting (?)
  * AA (?)
5. At least one more epoch.
	
### Ground Vehicles
## Modifications
### Weapons
### Armor
### Speed
