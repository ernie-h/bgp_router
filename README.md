# Project 2 Mileston
## Team Neutron (Ernie Hao, Elizabeth Cho)

Our router is based off the skeleton code provided by instructors. The command line parsing and socket establishing connections have been handled by code from the skeleton.

When a message is received by our router, we dispatch it `handle_packet` which delegates the message to appropriate handlers depending on the the message type.

If it is an update message, the packet is passed to update, where our forwarding table is updated with the given information, a copy of the route announcment is made, and the announcement is broadcasted to all devices in the network.

If a data message is received, we pass the packet to `forward` where we first find a viable next-hop by calling `get_route`. `get_route` for now finds viable routes based on best pre-fix matching, and more precise cases for route narrowing will be implemented shortly. Once a route is returned, forward with broadcast a message to the designated network.

If a dump message is received, the `dump` handler will be called, and our forwarding table will be sent to the netowrk that requested it.
