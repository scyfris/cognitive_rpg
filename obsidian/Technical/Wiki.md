# Overview of AGG Story Plugin

This Wiki will explain the core features of the AGG Story Plugin!

## Folder Structure

Right now the story is not a separate plugin but is part of the Rehab RPG repo at https://github.com/scyfris/RehabRPG.  The plugin resides in the AGGStoryPlugin folder, under `<root>/AGGStoryPlugin`.

### Icons

Contains various icons for game objects.

### Scenes

Contains pre-built scenes (i.e. module components) for Godot.  Which ones to use directly will be discussed later.  Some of these will be dragged into the scene by the user, others are components that aren't meant to be used directly.

### Scripts

Scripts for the various components and scenes.

## Creating a new Level

### Add autoloads.

Firstly, the plugin requires some autoloads.  In particular, the ones in this image:

![[Pasted image 20240201145436.png]]

All of these come from the AGGStoryPlugin directory, except for *DialogueManager* which is a third-party plugin.

### Create a new scene

Create a new directory for your game.  This should NOT be part of the AGGStoryPlugin dir.  In the following examples, our game will be stored under `<root>/Games/TutorialGame`.

Create a new 2D scene in that directory, deriving from Node2D (right click on your folder, go to New->Scene->2D Scene).  For this example, we will name it TutorialLevel1.  It should look like the following:

![[Pasted image 20240201145908.png]]

### Create TileMap and attach TileMapScene script to it.

The TileMapScene.cs script is located in `res://AGGStoryPlugin/Scripts/Components/TileMapScene.cs`.  This is the primary plugin script which serves as the glue for a lot of things.

Right click on the Root node in your new scene, and go to *Add Child Node*.  Type in "TileMap", and click Create.  It should now look like this:
![[Pasted image 20240201150246.png]]

After adding the TileMapScene.cs, the inspector should look like this:
![[Pasted image 20240201153431.png]]

For, now the TileMapScene properties blank - those will be discussed later.

#### Set Texture Filtering

By default the filter is "Inherit".  For pixel art, I like to use "Nearest" otherwise it might be a little blurry.
![[tileset setup 8.gif]]
#### Set Y-Sort on TileMap

You need to set the Y Sort Enabled on the TileMap itself, because its layers will be Y Sorted.  If you don't, you'll get a little red explanation mark.

![[tileset setup 10.gif]]

#### Create your Tile Layers

For isometric tiles, each layer in the "up" direction needs to be a separate layer.  The first layer, the one specified in the TileMapScene's `Walkable Layer` is special because that is what we use to know the walkable surface for the player.

Every other layer above that is for decoration mainly.  But in order to get Y sorting and stuff worked out, we need to set things up a little special.  For all layers *other* than the ground layer, set Y Sort Origin to 16 more than the previous.  Set Y Sort Enabled to true on all of them.  And set Z Index to 0 for ground layer, and 1 for all other layers.

Here is example of what it should look like (note the layer names don't matter):

![[Pasted image 20240201155014.png]]

### Set up the TileSet

The first thing you need to do is set up your TileSet.  TileSets are outside the scope of this tutorial, for more info see https://docs.godotengine.org/en/stable/classes/class_tilemap.html.

AGG Story Plugin supports isometric and square tilesets.  For an example of an isometric tileset and tilesheet, please see AGGStoryPlugin/ExampleGames/TutorialGame/TileSets.  The *.tres* file is the TileSet.  The *.png* file is the image (exported from Aseprite or somewhere else).

**NOTE: Only use TileMap for objects that are static in the scene.  For objects that move, or other objects, we will set those up as separate objects.  So when setting up your TileSet, if your PNG tilesheet contains other objects that aren't terrain, don't set up tiles for them since we won't be painting them in the TileMap!**

Create the TileSet , and set the TileMap's Tile Set property.  See next section for how to create a TileSet if you don't already have one.  

**NOTE: Different TileMaps can share same TileSet.  If you are using a already-setup TileSet, skip to the next section.**


![[Pasted image 20240201153510.png]]

#### TileSet settings

These are the settings for an Isometric tileset using the AGG Plugin:

Later we will add a custom data layer to this, but for now that's it for the settings.
![[Pasted image 20240201151612.png]]

#### Create tileset tiles

For editing TileSets, it's on the bottom (make sure you are highlighting either the TileSet .tres file in the Folder view, or highlighting the TileMap in the scene hierarchy)

![[Pasted image 20240201151723.png]]

Drag the tilesheet PNG to it, **select NO** to automatically create tiles.

![[tileset setup 1.gif]]

Now you need to setup your tiles.  In the TileSet window, make sure "Setup" tab is selected, and the eraser are NOT selected (sometimes this confused me because eraser was selected and it wouldn't do anything).  The isometric tilemap is 32x16, and each region in the TileSet is 16x16.  Our tiels however, need to be full 32x32. So we need to select multiple regions at once.  In order to create a 32x32 tile, we must **HOLD SHIFT** and drag over each square tiles you want to merge.  See below

![[tileset setup 2.gif]]

#### Set tile properties

To finish with the TileSet setup, you need to do just a couple more things.

##### Set Texture Origin on each tile.

This basically shows where sprite will lay compared to the ACTUAL isometric diamond tile.  What I will do is this:

* For ground tiles, make sure the diamond is set to the TOP of the tile.
* For tiles that sit on the ground, and all other levels above - make sure the diamond is set to the BASE of the tile.
See below for how I set these (and see example in the IsometricApartmentTileSet in the Tutorial example.).  In our example, the floors get a `Texture Origin` of `y==3` for the floors, and `y==8` for the blocks.  This puts the isometric tile face on the top of the floor, and at the base of the blocks that sit on the floors.

![[tileset setup 3.gif]]

##### Set Y Sort Origin on each tile

I don't fully understand this, but for now set the `Y Sort Origin` to the middle of the top face of the each tile.  See below (I set -16 for the big chungus to make the little dot in the center of the top face.  for the flatter tiles, the dot is already in the center of the top face when it is set to 0, so I leave them alone.):
![[tileset setup 6.gif]]

##### Set "blocked" custom data layer

In a game, will want certain terrain on top of the ground to block the players walk.  AGG Story Plugin has a solution for this!

This requires you to set the a custom data layer on both the TileSet, and let the TileMap know what it is.  By default, this layer is named `blocked` and is expected to be a `bool`.  You shouldn't have any reason to change it, but just FYI it's on the TileMapScene inspector:

![[Pasted image 20240201153749.png]]

You need to manually set `blocked` on the tileset tiles you want to block player.  This should NOT be any of the floor tiles, but could be anything sitting on top of the floor.  **Note: This is only for static tiles in the tilemap.  For objects we place in the scene, we use TileFootprints to block players.  That will come later**

Here's how:

In the TileSet settings (in inespector), set a new Custom Data Layer and name it "blocked"

![[tileset setup 5.gif]]



### Test out the tile map

You should now be able to paint your tiles.  Note that you need to make sure to choose the proper level.  Below GIF shows example of painting!

![[tileset setup 9.gif]]

### Add required Components

TODO

### Add Playercontroller

### Add TileObjects

### Add Dialogues

### Add Cutscenes



#### MISC

* Walkable levels of the TileMap are only from the level specified in `TileMapScene::Walkable Layer`.
* 