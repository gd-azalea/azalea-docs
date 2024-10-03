NPC schedules are defined in the npc_schedule table of data.db. In-game there are only Marker2Ds at various locations that can be referenced.

The idea is that a central script controls these NPCs and simulates their movement. There is no actual movement going on behind the scenes:
- When an area is loaded, we determine where everyone in that area would be at that time, and spawn them there
- In any given area, when time strikes for a schedule, an NPC in the area with that tag will get the command to move to the marker location
- If the NPC is not yet in the area, it will spawn on that marker

The schedule can have wildcards by the use of *. It can also reference conditions, tbd later.

If the area is loaded in between two schedules, a best guess to the location is made. IE if time has passed 20% between two schedules, the user would be somewhere 20% between the two markers. We should have a unity prototype code for this.

See I:\Unity\FarmGame\FarmGame\Assets\Scripts\NPC

