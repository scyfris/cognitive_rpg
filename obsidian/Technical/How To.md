#### Creating new Level

Create Scene
Add TileMap
* Add script TileMapScene
* Make sure positioned at 0,0
* Ordering: Set Y Sort Enabled: ON
* I usually have 3 layers:
	* ground - Y Sort Enabled = OFF, Z index = 0
	* on_ground - Y Sort Enabled = ON, Z index = 1
	* above_ground - Y Sort Enabled = OFF, Z index = 2
	* EX: Painting ground, or things player walks on will be on Layer Ground.  Painting walls, or things that block players , statues, etc will be OnGround, while AboveGround is reserved for things that are above player like birds, clouds, or whatever 
* CanvasItem::Texture::Filter == Nearest
* Add a TileMapPlayerController
* Add a TilemapEntrance
* Add a TileMapComponents
	* Resize the  InputArea2D/CollisionShape2D as-needed (Make editable children)
* Add a TileObject and attach an Actionable for clicking on things.  Add a sprite etc if needed.


Set Tileset for TileMap
* Since Tilesets encode information about tiling, terrains, corner matching, and tile properties, you shouldn't need a new Tileset for each level/tilemap.  Only when you bring in a new tileset spritesheet do you need to define a new tileset.  And even then, you don't need to have seaprate ones since a TileSet can have multiple Atlas / spritesheets defined in it.
* **Creating TileSet:**
* I like to Create new Tileset on disk.  You don't have to, but I do so we can share between maps.  If you know this tileset is specific to just this one map, you don't have to save it to disk.
* You'll have to define the tileset
	* Make sure you texture sheet is set.
	* Add a custom data layer "blocked" to the tileset, type "bool"
	* Add a Terrain layer and a terrain
		* Set up the corner matches (depends on tileset)
			* See https://github.com/godotengine/godot-docs/issues/3316 , for 3x3minimal you need 48 tiles.
Start painting with Terrain tool on the TileMap.
* MAKE SURE YOU SELECT THE RIGHT LAYER !!!*
* 

TileObject
* Add a TileObject
* Attach an Actionable
	* You can choose an actionable resource like ActionableDialogue, etc.  Just set the params appropriately.*