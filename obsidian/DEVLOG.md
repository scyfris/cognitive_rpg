1/29 - Billy
* Completed the hooks for minigame.
	* A MinigameManager is set to autoload.
	* A MinigameDef defines the path to a minigame.
	* A Minigame script node is the root of a minigame.  
	* Minigame uses signal to pass a MinigameResults back up to MinigameManager.
	* The ActionableResourceMinigame executes the Minigame action, and then when the signal occurs it will trigger the dialogue for pass/fail.
	* TODO: I've notice that we need multiple levels of globals.  The first level is Plugin globals - these are Autoloads like MinigameManager, LevelManager, etc, that don't have any game-specific data but only contain the infrastructure for doing things.  We need a second level of global: Game Globals , to hold any game-specific data such as the Level list, or the Minigame list (mapping name -> minigame so that we can look up results by name later).  This will require we don't load entire scenes as roots, but instead have the Game-specific globals stay constant and load the tilemap/minigames as children in the same scen.  I'll work on that next.