# Usecases

The framework is very data centric. This page illustrates usecases and how the code approaches this.

## Cutting down a tree (obj_tree_1)
- Get tree object coordinates
- Remove the tree object from the scene
  - Add an entry to `destructable`:
    - object_name = obj_tree_1
    - map = current map
    - save_id = current runtime savestate
- Spawn in place some resources (wood)
  - Add entry to `placeable`:
    - save_id = current runtime savestate
    - item_id = wood
    - map = current map
    - coordinates = obj_tree_1 location
    - amount = 3 (or similar)
  - Trigger a signal placeable_added
    - The scene then needs to listen to this signal and spawn items
    - Instead of each scene implementing this, there is a global PlaceableListener that can interact with any active scene

## Picking up an item from the ground
- Get object coordinates, item_id and amount
- Add to inventory
  - Add item_id + amount to `storage` where save_id = 'temp_save' and inventory = true
  - Though if this item already exists, stack the amounts. So first do a WHERE item_id = ... and if match, append amount
- Remove from `placeable`
  - DELETE FROM PLACEABLE WHERE MAP = 'current_map' AND save_id = 'temp_save' AND coordinates = 'object_coordinates'
- Remove the object from scene

## Placing a seed in the ground
- Remove from inventory
  - Reduce amount from `storage` where save_id = 'temp_save' and inventory = true for item_id
  - If amount = 0, remove the entry entirely
- Add to `placeable`
- Add object to scene via instantiate

## Determining an NPC location
As time moves, NPCs can switch locations. NPC schedules are stored in 'npc_schedule'. <br>
Every 'time tick', this table is queried to see if changes occur. It looks at start_time only. <br>
If a start_time is matching, then we look at the NPC and the map. <br>
If the NPC is currently in the map scene and they are moving within the map, they start moving to the marker_id. <br>
If a condition is present, we run the condition logic first. If they have an animation, we run the animation. <br>
<br>
An NPC cannot move outside of a map without passing a transition marker_id. If they hit a transition marker, they should disappear from the scene. <br>
The map might show the current location of all NPCs. We can show details for those in our loaded map, the others we can show which map they are in.

## Loading an area
Loading an area always happens in the background and through a swap. Read more about this in level-loading.
Once a scene is loaded, but before it is shown, we correct the scene to match the data.
This includes going over `placeable` and `destructable` items (in that order) where map = 'new_scene_location'
NPC schedules are also read (see above) and the appropriate characters are loaded.

## Making a save
Similar to level loading, this should freeze the game and turn to a status screen.
A new entry should be made in `save`. This gives a new ID.
Anything tied to the temp_save_id should get duplicated to both temp_save and the new ID.
