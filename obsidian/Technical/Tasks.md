This lists tasks we need to do.

## Bringup

 **Goal**: Get us to where we can focus on story and content.  Get all infrastructure stuff out of the way (with exception of minigames)
 
**Tasks:**
* Walk around
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
* ~~Collision detection for obstacles.~~
	* 1/8/24 - Got this working.
* Tilemap workflow
	* ~~Need to figure out how to make character appear "behind" layers.~~
		* Explainer of Y-Sorting: https://www.youtube.com/watch?v=UdmD_2EcEgU
* Clickable regions for dialogue.
* Transition between scenes.
* Inventory system (for puzzles)
	* Draggable inventory to objects on screen (to activate something).
* Skill system integration with dialogue and such.
* Dialogue manager integration (Articy? Godot DM?)
* Minigame transition.
## Milestone 1
