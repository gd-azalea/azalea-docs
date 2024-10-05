NPC schedules are defined in the npc_schedule table of data.db. In-game there are only Marker2Ds at various locations that can be referenced.

The idea is that a central script controls these NPCs and simulates their movement. There is no actual movement going on behind the scenes:
- When an area is loaded, we determine where everyone in that area would be at that time, and spawn them there
- In any given area, when time strikes for a schedule, an NPC in the area with that tag will get the command to move to the marker location
- If the NPC is not yet in the area, it will spawn on that marker

The schedule can have wildcards by the use of *. It can also reference conditions, tbd later.

If the area is loaded in between two schedules, a best guess to the location is made. IE if time has passed 20% between two schedules, the user would be somewhere 20% between the two markers. We should have a unity prototype code for this.

See I:\Unity\FarmGame\FarmGame\Assets\Scripts\NPC

Looks like in Unity we did this with a NavMeshAgent. It would be appropriate to use something like https://docs.godotengine.org/en/stable/tutorials/navigation/navigation_introduction_2d.html here too. The Unity code does not spawn NPCs, we should still have a global script do so per timeframe (perhaps this can link to WorldTime.(signal)update_time).

I suggest we run this per map. We'd need to:
- Find a way to figure out who is supposed to be on map right now -> spawns in relevant location
- Where is everybody going next and at what time?

Additionally:
- There should be a data test to verify a schedule fits and doesn't 'end'

##


NPC schedules get initially loaded at scene switch. This is done in SceneLoader in the complete_load_with_npc_spawn.

In root there is also an NPCScheduleManager that syncs with the WorldTime changing. Upon change it checks two things:
- Does any NPC need to spawn in the current map?
- Do any of the NPCs in the current map need to move or despawn?
