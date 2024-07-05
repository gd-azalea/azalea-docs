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

## Picking up an item from the ground
- Get object coordinates, item_id and amount
- Add to inventory
  - Add item_id + amount to `storage` where save_id = 'temp_save' and inventory = true
  - Though if this item already exists, stack the amounts. So first do a WHERE item_id = ... and if match, append amount
- Remove from `placeable`
  - DELETE FROM PLACEABLE WHERE MAP = 'current_map' AND save_id = 'temp_save' AND coordinates = 'object_coordinates'
- Remove the object from scene

## Placing a seed in the ground
...

## Determining an NPC location
...

## Loading an area
Loading an area always happens in the background and through a swap. Read more about this in level-loading.
Once a scene is loaded, but before it is shown, we correct the scene to match the data.
This includes going over `placeable` and `destructable` items (in that order) where map = 'new_scene_location'

## Making a save
Similar to level loading, this should freeze the game and turn to a status screen.
A new entry should be made in `save`. This gives a new ID.
Anything tied to the temp_save_id should get duplicated to both temp_save and the new ID.
