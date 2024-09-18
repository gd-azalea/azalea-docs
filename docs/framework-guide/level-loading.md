# Level loading

Gameplay is consistently run from [Root.tscn](https://github.com/gd-azalea/azalea/blob/main/scenes/framework/Root.tscn). This default scene initializes essential components such as the GUI, Player, Weather, and Day/Night Cycle. Importantly, it contains a `🌏 Level` node, where the active level is loaded as a child node.

This setup allows for persistent audio and GUI elements across different scenes, minimizing noticeable transitions and hard cuts during level loading.

All levels should be stored in `res://scenes/levels/` for quick and easy name-based lookups.

## Scene Loading Process
Loading a new scene involves the following steps:

- Fading to black.
- Loading the scene file.
- Adding the new scene as a child node.
- Removing the previous scene node.
- Spawning the player in the correct position.

The primary class responsible for this process is SceneLoader. You can load a level with the following call:

``` gdscript
SceneLoader.load(get_tree(), "MyLevelName")
```

Additionally, you have the option to keep the previous level in memory by using a flag. This is useful for scenarios like transitioning between the interior and exterior of a building. By 
retaining the larger exterior scene in memory, returning outside becomes nearly instantaneous since it was never fully unloaded.

``` gdscript
SceneLoader.load_w_memory_flag(get_tree(), "MyLevelName", true)
```

## Example
You would only need to do this one way. For example: let's say you have a city and a building. The city is a big map to load, the building a small one. You would load into the city originally like this:
``` gdscript
SceneLoader.load(get_tree(), "City")
```
Then the area transition to the building could be like this:
``` gdscript
SceneLoader.load_w_memory_flag(get_tree(), "Building", true)
```
The quick building scene gets loaded, but the city remains in memory. This allows you to hop into the building, do a quick action, then switch back to the city really quickly like this:
``` gdscript
SceneLoader.load(get_tree(), "City")
```
Calling the above would remove the building from memory. Since the city never got unloaded, there is practically no loading. The downside to this is that more memory is used, so it is not advised to do this with two back to back heavy levels.

ref: [scene_transition.gd - prototype](https://github.com/kevindeyne/azalea-prototype/blob/main/player/scene_transition.gd) and [SceneLoader.gd - new impl](https://github.com/gd-azalea/azalea/blob/main/scripts/framework/SceneLoader.gd)
