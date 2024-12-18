Our multiplayer is peer-to-peer. But p2p has some common issues, like discovery and network setup required. We use Steam to alleviate these.

We mostly use GodotSteam (https://godotsteam.com/)

See prototype: https://github.com/gd-azalea/multiplayer-prototype

As a user you can choose to 'host' a lobby. Once you do so, you can show up in the lobby list of other players (friends only). They can select your name and ask to join.

When asking to join a handshake p2p message is sent. With the handshake comes the request to the host to accept a user joining (?). If they choose to agree, a p2p message will be send back telling you of the succesful join.

With the join success message a player gets spawned. As the player does actions, these get synchronized across clients.

Since the plugins for this (Steam Multiplayer Peer and GodotSteamSync) have various issues with them, we use our own implementation.

Upon load, a full sync is done via reliable p2p. Once playing, we send data to a bus which collects all changes until the tick time comes, which is when an unreliable p2p is sent out.

Sync expectation:
- Player position, orientation, action (explicitly not hash protected)
- Placeable
- Destructable
- Quest_progress
- Known_recipes
- Storage
- Weather, time, season determination (host, hash protected)

Unique to player (does not get synced):
- Controls
- Settings

Everything aside from player position/orientation/action is hash protected. Since this is synced through unreliable communication, we cannot be sure if we 'miss' a placeable or destructable, for example. Instead of sending the data of all placeables/destructables in a scene each time, we instead send a hash of all items. As long as the hash is the same, we know we're in sync. If the hash is different, we need a reliable call made to ensure we're back in sync.

Two players can be in different scenes/areas. If the player is in the same area and 'close enough', they will follow along with cutscenes.
This means we need info on where to 'start' a conversation, lock the conversation choices/speed to the owner of the conversation (whomever starts it) and sync it.

After the handshake, the player gets a welcome package. This contains where the other players are at that time, so the new player can spawn into that map. It also contains the details for the game (ie placeables, destructables, weather, time, etc). From the spawn point on, only sync data will be passed along.


Each item has a MultiplayerSync node attached to it. This runs through _process and takes any configured properties and sends them along to the MultiplayerBus.
The MultiplayerBus collects all events from everyone, and bundles them together in batches. It also does translations (ie 'Player' from host perspective is a lobby member from another perspective). It has an internal timer, and once the timer hits (usually 30/s) it sends an unreliable p2p bundle message across the relay known as "sync".

SteamNetwork will receive messages and send the incoming messages to MultiplayerUtils for translating to world updates.
