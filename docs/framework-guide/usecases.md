# Usecases

The framework is very data centric. This page illustrates usecases and how the code approaches this.

## Cutting down a tree (obj_tree_1)
Get tree object coordinates

Remove the tree object from the scene
  Add an entry to destructable: 
    object_name = obj_tree_1
    map = current map
    save_id = current runtime savestate
  
Spawn in place some resources (wood)
  Add entry to placeable:
    save_id = current runtime savestate
    item_id = wood
    map = current map
    coordinates = obj_tree_1 location
    amount = 3 (or similar)

## Picking up an item from the ground
...

## Placing a seed in the ground
...

## Determining an NPC location
...

## Loading an area
...

## Making a save
...
