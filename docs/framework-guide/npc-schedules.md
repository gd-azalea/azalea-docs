### NPC Scheduling System Overview

NPC schedules are stored in the `npc_schedule` table within `data.db`, while in the game world, only `Marker2D` nodes are placed at various locations, representing points that NPCs can navigate to.

NPCs are controlled by a central script that simulates their movement. Rather than continuously moving behind the scenes, the system simulates NPC presence and movement based on game events and time:

- When an area is loaded, the system determines where each NPC in that area should be at the current in-game time and spawns them at the appropriate `Marker2D` locations.
- As time progresses within any given area, the system checks NPC schedules and triggers movement when needed. If an NPC is already in the area and their schedule dictates they should move, the NPC will receive a command to navigate to a specific marker. If they are not yet present in the area, they will be spawned directly at the marker.

NPCs inherit from a base abstract class called `NPC`, which provides shared functionality, including the `moveTo(markerId: String)` method. This method uses `NavigationRegion2D` to move the NPC towards a marker, identified by the provided `markerId`. The method is also utilized by the `NPCScheduleManager` to handle NPC movement based on schedule updates.

Schedules can include wildcard characters (e.g., `*`) to allow flexibility, and may also reference certain conditions (to be defined in the future). At the start of each scene, NPC schedules are initialized via the `SceneLoader`, specifically within the `complete_load_with_npc_spawn` function.

The `NPCScheduleManager` operates at the root level, syncing with changes in `WorldTime`. Whenever time updates, it checks whether NPCs need to spawn, move, or despawn based on the current schedule in the loaded map.

Additionally, there is a test to validate that schedules are coherent and don’t terminate abruptly, ensuring consistent NPC behavior throughout the game.

#### TODO
If the area is loaded in between two schedules, a best guess to the location is made. IE if time has passed 20% between two schedules, the user would be somewhere 20% between the two markers. We should have a unity prototype code for this.

See I:\Unity\FarmGame\FarmGame\Assets\Scripts\NPC

Looks like in Unity we did this with a NavMeshAgent. It would be appropriate to use something like https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_introduction_2d.html here too. The Unity code does not spawn NPCs, we should still have a global script do so per timeframe (perhaps this can link to WorldTime.(signal)update_time).
