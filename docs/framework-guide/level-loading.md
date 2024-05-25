# Level loading

Handled in <https://github.com/kevindeyne/azalea-prototype/blob/main/player/scene_transition.gd>

All levels should be added to a /levels folder and end with `_level` we do this to allow quick and easy lookups by name.

To maintain full control, we need a LevelManager class. Our game will always have a default scene that is loaded. This default scene sets up the GUI, Player, Weather, DayNightCycle, etc.

Loading another scene essentially means:

- Fading to black
- Loading the scene file
- Adding it as another node
- Getting rid of the ‘wrong’ node
- Spawning the player in the correct position

There should also be the option to keep a previous area in memory. This for ‘quick in-n-outs’, so for example the interior of a building. It’s a different scene, you load the small scene, but keep the big exterior scene in memory. That way, when you go back outside, it’s pretty much instant because it was never unloaded.
