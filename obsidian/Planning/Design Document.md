Passing time is a story-based game that is directed towards people with cognitive disabilities from stroke or TBI, but can be enjoyed by anyone.  This document will serve as the design document.

## Structure of story

Broken into chapters.


## Story Variables

Variables can also be set on a per-chapter basis.  These variables might influence parts of the story in that chapter.  For instance, a "do_coffee" variable could be set if they complete the coffee minigame.  This variable can be checked later in the chapter to modify dialogue responses, or other things.

Variables can **not** persist across chapters.

## Minigames

Minigames are designed to be the main exercises the player does. They are divided into the following categories, sometimes called categories:

Memory
* Sequenced/unquenched recall
	* Pill bottle game is example
* Gap fill game for remembering what is happening in the story.

Linguistics
* Phone message game is example

Spatial
* Bubble game is example

When player clicks on a minigame in-game, it will show a box preview showing them what stats they will earn by completing the minigame.  
**?** How should this UI look in-game without them clicking?  Should we have a little icon over the thingy with symbol indicating what stats they will get, or that it is in a minigame.

#### Memory Prototype

* sequence/unsequenced recall

#### Linguistics

* Phone message, email game, etc.  Remembering what is said in *

#### Spatial
* something like bubble pop
* puzzles where you fit in the pieces - this is based on obtaining the proper items through the game/ dialogue.

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





