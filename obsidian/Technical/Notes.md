## Info for Wiki online

### Components

#### Autoloads/Globals

LevelManager
* Contains functionality for loading different levels/tilemaps and initializing those maps.
	* LoadLevel() - Primary function to load a new tilemap scene.  Specify the level enum and an optional entrance name (must correspond to the name of a TilemapEntrance component somewhere in that tilemap.)

#### Tilemap Components

* Actionable
	* This class can be attached to an object to perform some action.  Typically, the object this is attached to will also have some class like "Clickable" whose signal would be hooked up to Actionable::Action().  This class won't do anything without a signal or other code executing Action().  The action that gets executed must also be set to the _action_ member via the Godot inspector.  The action contains the actual action function.
		* ActionResource
			* This is an actual action function.  There are different kinds, browse the subclasses of ActionResource.
* TilemapEntrance
* TileMap references:
	* Reddit discussion with some useful info on how many tiles needed
		* https://www.reddit.com/r/godot/comments/xzeovf/how_would_you_autotile_this_pulling_my_hair_out_d/
	* Another reddit post, referring to the name of these type of tiles: Wang or Blob tile sets.
		* https://www.reddit.com/r/godot/comments/u6f0v4/what_tiles_do_i_need_for_each_autotile_bitmask/
	*  A git issue post that describes all the different combinations of tiles for autotiling!
		* https://github.com/godotengine/godot-docs/issues/3316
	* TilePipe -  A tool to help make tileset generation easier
		* https://aleksandrbazhin.itch.io/tilepipe2
	* 3x3minimal:
		* ![[Pasted image 20240117113859.png]]


#### SceneActionManager and Cutscenes

#### Actor Animation names

These are requirements for actors that move left/right/down/up and can remain idle.
walk_down
walk_up
walk_side
walk_side (reversed)
default (idle)

Optional:
surprised - trigged by cutscenes

### Workflow


Minigame