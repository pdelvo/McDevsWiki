This page presents a dissection of the current stable [Minecraft](http://minecraft.net/game/) protocol. The current pre-release protocol is documented [elsewhere](Pre-release_protocol.md). The protocol for Pocket Minecraft is substantially different, and is documented at [Pocket Minecraft Protocol](Pocket_Minecraft_Protocol.md).

If you're having trouble, check out the [FAQ](Protocol_FAQ.md) or ask for help in the IRC channel ([#mcdevs on irc.freenode.net](irc://irc.freenode.net/mcdevs)).

**Note**: While you may use the contents of this page without restriction to create servers, clients, bots, etc… you still need to provide attribution to #mcdevs if you copy any of the contents of this page for publication elsewhere.

                                     | Definition                               
 ----------------------------------- | --------------------------------------------------------------------------------------
 Player                              | When used in the singular, Player always refers to the client connected to the server
 Entity                              | Entity refers to any item, player, mob, minecart or boat in the world. This definition is subject to change as Notch extends the protocol
 EID                                 | An EID - or Entity ID - is a unique 4-byte integer used to identify a specific entity 
 XYZ                                 | In this document, the axis names are the same as those used by Notch. Y points upwards, X points South, and Z points West.

Packets
========

All packets begin with a single "Packet ID" byte. Listed packet size includes this byte. Packets are either "server to client", "client to server", or "Two-Way" (both). Packets are not prefixed with their length. For variable length packets, you must parse it completely to determine its length.

Keep Alive (0x00)
-----------------
*Two-Way*
The server will frequently send out a keep-alive, each containing a random ID. The client must respond with the same packet. The Beta server will disconnect a client if it doesn't receive at least one packet before 1200 in-game ticks, and the Beta client will time out the connection under the same conditions. The client may send packets with Keep-alive ID=0.

Packet ID   | Field Name    | Field Type | Example   | Notes
------------|---------------|------------|-----------|----------------------------
0x00        | Keep-alive ID | int        | 957759560 | Server-generated random id 
Total Size: | 5 bytes