# Classes

Global functions:

- Lookups + cache
    - Find the current “level”, see https://github.com/kevindeyne/azalea-prototype/blob/main/generic/global_state.gd#L16
    - Find the “player”
    - Find the “player_spawn” Marker2D within a _level
    - Find the “placer”
    - Find the audio players
- Controller checks
    - Incl axis check w/ deadzone Input.is_action_just_released
- Logging (static)
    - Log with debug levels (should be easily turned off when going live)
        - Ideally you can turn on/off ‘groups’ of logging
- JSONUtils (static)
    - String to Vector2 array
- DialogueFunctions
    - Easy way to trigger methods from dialogue

GlobalSignals:

Easy place for all signals to connect to

Level Manager:

- Levels must understand if they’re exterior or interior

Weather:

x

Day/Night cycle:

x

Area transition (composition):

Add a collider to it

Can add an audio queue to play

Note if current area should stay in memory, keep_current_area_in_memory

Talkable (composition):

Ability to start a conversation (which dialogue?)

Shows the ‘available to talk’ hover icon
