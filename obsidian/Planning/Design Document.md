Passing time is a story-based game that is directed towards people with cognitive disabilities from stroke or TBI, but can be enjoyed by anyone.  This document will serve as the design document.

## Structure of story

Broken into chapters.

## Stats

Stats can be improved by completing minigame tasks.  Dialogue is influenced by the stats of a player.  Additionally, action in-game may require certain stats in order to perform.

The stats we are using:

* Strength - How strong the player is.
	* This stat might influence certain dialogue options , or actions the player can perform in the world.
* Perception - How perceptive the player is
	* Could allow player to deduce more information about someone.  Perhaps they could even recognize when someone is lying during dialogue.  Perhaps this also provides more context clues when figuring out a certain puzzle (ex: a broken pipe - with high enough perception, when they click on it the narrative might say "This pipe could possibly be fixed with a wrench", whereas if they didn't have a high enough perception it would say "This is a broken pipe.".  And the UI would indicate over it that they could get a different description with a certain perception, that way if character really can't figure out what to do, they know if they increase their perception high enough the game will kind of give them a hint via the narrative.)
* ???
* ???

Stats are persistent across chapters.  We must have a way to ensure stats are at a certain level before a chapter or group of chapters begins, in order to keep a baseline.

## Story Variables

Variables can also be set on a per-chapter basis.  These variables might influence parts of the story in that chapter.  For instance, a "do_coffee" variable could be set if they complete the coffee minigame.  This ariable can be checked later in the chapter to modify dialogue responses, or other things.

Variables can **not** persist across chapters.  Only stats persist across chapters.

## Minigames

Minigames are designed to be the main exercises the player does. They are divided into the following categories:

Memory
* Sequenced/unsequenced recall
* Pill bottle game is example

Linguistics
* Phone message game is example

Spatial
* Bubble game is example

When player clicks on a minigame in-game, it will show a box preview showing them what stats they will earn by completing the minigame.  
**?** How should this UI look in-game without them clicking?  Should we have a little icon over the thingy with symbol indicating what stats they will get, or that it is in a minigame.

#### Memory

#### Linguistics

#### Spatial

## In-game

### Viewpoint

Orthographic view

#### Movement

Touching the location to move to.

#### Interactions

Objects in game are interactable.  The player can touch an object which will interact with it.  Usually this starts a dialogue.

#### UI

Most items can be touched and dialogue comments on it.  Some items may do something special, and there will be a UI component indicating the player should touch on it (trigger minigame, obtain some stat increase, etc).  The player will also have an inventory with items, they can touch an item in inventory and drag it onto some in-game object which would create an interaction.

##### Dialogue

Dialogue in dialogue boxes can have the following:
* Voice - coming from a person.
	* Text is normal.
* Thoughts - coming from within Alex
	* Text is italizised
* Narration - coming from narrator.
	* Text is italizised similar to thoughts.





