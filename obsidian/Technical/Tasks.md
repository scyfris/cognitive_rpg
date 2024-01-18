This lists tasks we need to do.

## Bringup

 **Goal**: Get us to where we can focus on story and content.  Get all infrastructure stuff out of the way (with exception of minigames)
 
**Tasks:**
* ~~Transition between scenes.~~
* ~~Animations (idle, walk, etc)~~
* Inventory system (for puzzles)
	* Draggable inventory to objects on screen (to activate something).
* Skill system integration with dialogue and such.
* Dialogue manager integration (Articy? Godot DM?)
* Minigame transition.
* Art:
	* Lospec.com
	* Figure out how to make tilesets (take some tutorials)
	* Make a character
* ~~Walk around~~
	* 1/8/24 - Got this working with wasd
	* TODO: Get working with clicks (path planning based on collisions).
		* Found this Subreddit and link
			* Subreddit: https://www.reddit.com/r/godot/comments/13vbcck/point_and_click_movement_in_grid_pattern/
			* Link: https://www.gdquest.com/tutorial/godot/2d/tactical-rpg-movement/
		* For tilemap navigation data:
			* https://www.reddit.com/r/godot/comments/zxmqte/navigation_on_tilemap_in_godot_4/
			* MUST READ for setting collision avoidance on the path planning properly.  IT's for 3.5, but still lead me to find the problem (hint cell size!): https://www.reddit.com/r/godot/comments/x7s4z1/guide_for_how_to_fix_navigationagents_getting/
	* 1/9/24 - Okay, I instead switched to AStarGrid as the whole collision detection and AStar algorithm was a bit messy (I would have to account for the NavigationAgent's size somehow which Godot's built-in navigation stuff doesn't account for).  So instead, we are doing away with the collision detection and AStar stuff and going with AStarGrid.  The tilemap's custom data has a "blocked" boolean which will set a tile cell as offlimits.  I've been needed to adjust the Texture Offset and Y Sort origin for certain tiles thogh to make sure things work well, but now it works good.
		* **TODO** - Clean up code and document process for tilemap.
		* **TODO** - Investigate if Tiled should be used?  Or just move straight to the dialogue system.
			* Explainer of Y-Sorting: https://www.youtube.com/watch?v=UdmD_2EcEgU
			* Tiled 1.10.2 now has native Godot export to Godot's tilemap format as a scene ([https://doc.mapeditor.org/en/latest/manual/export-tscn/](https://doc.mapeditor.org/en/latest/manual/export-tscn/))  I tried it , I think a couple major things I didn't like about it and am choosing to go with Godot's built-in for my game:
				* Defining custom tile set data layers was easy , I could specify it in Tiled, and the export would create a Godot Tilemap with that data layer. BUT I didn't see a way to specify _built-in tile data_ (like per-tile Y Sort Origin or Z Index). That was really important for me, so I couldn't use it.
				* Every time I save it overwrites the tilemap in Godot - so custom settings like my CanvasItem::Texture::Filter on the object gets reset ! (I like it set to nearest for pixel art).
				* This video states some potential problems with Godot 4's tilemap system:
					* https://www.youtube.com/watch?v=9HMIbGLLrSk
    

* ~~Collision detection for obstacles.~~
	* 1/8/24 - Got this working.
* Tilemap workflow
	* ~~Need to figure out how to make character appear "behind" layers.~~
		* 
		* One problem though 
* ~~Clickable regions for dialogue.~~
	* Need to be able to click on objects and walk there.  Get that working with the path system.
		* InputEvent tutorial shows ordering for _input, unhandled_nput, and CollisionObject._input_event() !: https://docs.huihoo.com/godotengine/godot-docs/godot/tutorials/engine/inputevent.html
		* **TODO**: Figure out how to add those cool yellow explanation marks for scene dependencies!
* Nice picture: https://diogo-vernier.itch.io/animated-character-16-x-16
* pokemon sprites: https://www.youtube.com/watch?v=gwF0L55kIgg&t=464s
* aseprite animation tutorial: https://www.youtube.com/watch?v=B0enS9BJne4
*

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


### Workflow




## Proto 1
* Make a game based on the Pilot's first part (Alex in his house waking up).  These will exercise:
	* Opening sequence/cinematic
	* Minigame initiation / interface 
	* Animation/sequences (dialogue, visual, etc)
	* Tilemap for apartment - workflow to create tiles.
	* Camera following player
