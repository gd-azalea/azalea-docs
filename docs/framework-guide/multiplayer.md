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

Two players can be in different scenes/areas. If the player is in the same area and 'close enough', they will follow along with conversations and cutscenes.
This means we need info on where to 'start' a conversation, lock the conversation choices/speed to the owner of the conversation (whomever starts it) and sync it.
