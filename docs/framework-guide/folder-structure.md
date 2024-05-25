# Folder structure

Several pieces of framework code depend on the folder structure being consistent. We expect it to be structured as follows:

- Scenes
	- Framework
	- Levels
		- Woods
		- House1
		- ...
- Scripts
	- Framework
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

Any generic script or scene should be added under /Framework/. Anything specific to the level should be added under /Levels/.

The level scenes are also important for [level loading](http://localhost:8000/azalea-docs/framework-guide/level-loading/).