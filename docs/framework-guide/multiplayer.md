Our multiplayer is peer-to-peer. But p2p has some common issues, like discovery and network setup required. We use Steam to alleviate these.

We mostly use GodotSteam (https://godotsteam.com/)

See prototype: https://github.com/gd-azalea/multiplayer-prototype

As a user you can choose to 'host' a lobby. Once you do so, you can show up in the lobby list of other players (friends only). They can select your name and ask to join.

When asking to join a handshake p2p message is sent. With the handshake comes the request to the host to accept a user joining (?). If they choose to agree, a p2p message will be send back telling you of the succesful join.

With the join success message a player gets spawned. The player has a multiplayerSynchronizer which somehow sends p2p data. https://www.youtube.com/watch?v=e0JLO_5UgQo

https://github.com/expressobits/steam-multiplayer-peer ?
