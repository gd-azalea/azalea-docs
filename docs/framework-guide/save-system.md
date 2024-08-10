# Save system

Handled in <https://github.com/gd-azalea/azalea/blob/main/prototype/save_games.gd>

There is a base file of the database for the game in the game's resources, available from res://data.db. This contains things like item lists, etc.
When starting the game (see [code](https://github.com/gd-azalea/azalea/blob/main/scripts/framework/database/meta/AbstractRepository.gd#L22)), the resource is copied over into the user's persistent app data. This is the database that will be loaded as current.db.

As the game progresses, the current.db gets updated. This means that if you stop the game and continue, this same persistent file can just be reloaded and the game continued.

When you make a save game, you're calling the backup function of the current.db into a new file (https://github.com/2shady4u/godot-sqlite?tab=readme-ov-file#functions). This allows you to copy the database file while it is in use (because open database files are locked).

When loading a game it's doing a restore of the file into current.db, overwriting the current.db file.
