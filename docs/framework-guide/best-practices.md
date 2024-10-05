# Best practices
Keep direct changes as close as possible to their component. Keep reusable logic parts in a globally accessible class.
For example: The WorldTime with GUI. The changes for the GUI, updating the labels and such - keep that in the actual GUI/WorldTimeMarginContainer (the wrapper for the labels).
That way, in order to see how they get updated, you only have to find the GUI element itself.
However the main code is in a global WorldTime class, which has its own test

Areas should inherit from abstract/BaseArea. NPCs should inherit from abstract/NPC.

# How to:

## How to set up signals
From the place you’re sending from:

```gdscript
signal day_end
...
day_end.emit()
day_end.emit("hit", "Dark lord", 5)
```

From the place you’re listening to:

```gdscript
GlobalSignals.day_end.connect(my_method)

func my_method() -> void:
	pass
```

## How to spawn new entities:

```gdscript
SpawnUtils.spawn(packedSceneToSpawn, level_node, position)
OR
var plant = plantScene.instantiate()
var level_node = GlobalState.find_level_node()
level_node.add_child(plant)

plant.name = "planted_" + str(loc)
plant.set_owner(level_node)
plant.add_to_group("persist")

plant.position = loc
```

## How to destroy object:

```gdscript
level_node.queue_free()
```

## Load a resource, like audio?

```gdscript
load("res://path/to/audio/file")
```

## How to add a ttl:

```gdscript
var ttl = 10 #in secs
var init: int = 0

func _ready() -> void:
	init = Time.get_ticks_msec()

func _physics_process(delta: float) -> void:
	if (Time.get_ticks_msec() - init) > (ttl*1000):
		queue_free()
```

## How to get locale:

```gdscript
OS.get_locale_language()

returns a value like 'fr'
	cmn = mandarin chinese
	ko = korean
	nl = dutch
	'else' = english
Can use this to default to a locale
see also https://www.youtube.com/watch?v=Lw-3Tnwv4Ds&ab_channel=jitspoe

TranslationServer.set_locale()
```

## Create a timer via code

```gdscript
var timer := Timer.new()
timer.wait_time = 1.0 # 1 second
timer.one_shot = false
timer.autostart = true
timer.connect("timeout", WorldTime.on_global_timer_timeout)
add_child(timer)
```

## On button press:

```gdscript
	if Input.is_action_just_pressed("undo"):
		undo()
```

## Logging:

```gdscript
static var logger: Log = Log.new("StorageRepository")
logger.debug("add_to_player_inventory: ")
```

## Export with options:

```gdscript
enum Direction {LEFT, RIGHT, UP, DOWN}

@export var dir: Direction
```
