# Folder structure

Several pieces of framework code depend on the folder structure being consistent. We expect it to be structured as follows:

- Scenes
	- Framework
	- Levels
    		- Abstract folder (base class to inherit from)
		- Woods
		- House1
		- ...
  	- Characters (this contains the NPCs)
  		- Abstract folder (base class to inherit from)
  	 - GUI (in game overlays)
  	 - Menus (full screen menus)
- Scripts
	- Framework
 	- GUI
	- Levels
		- Woods
		- House1
		- ...
- Assets
	- Audio
	- Images
		- Characters
		- Areas
		- ...
	- ...
- Shaders
- Dialogue (dialogue scripts)
- Translations
	- Dialogue
 	- main_menu
  	- ...

Any generic script or scene should be added under /Framework/. Anything specific to the level should be added under /Levels/.

The level scenes are also important for [level loading](http://localhost:8000/azalea-docs/framework-guide/level-loading/). A level should inherit from the abstract level node.

Since NPCs can be spawned anywhere, they all need to be in Scenes/Characters. They need to inherit from the abstract NPC node.
