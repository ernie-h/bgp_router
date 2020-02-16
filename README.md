# Project 2 Mileston
## Team Neutron (Ernie Hao, Elizabeth Cho)

Our router is based off the skeleton code provided by instructors. The command line parsing and socket establishing connections have been handled by code from the skeleton.

When a message is received by our router, we dispatch it `handle_packet` which delegates the message to appropriate handlers depending on the the message type.

If it is an update message, the packet is passed to update, where our forwarding table is updated with the given information, a copy of the route announcment is made, and the announcement is broadcasted to all devices in the network.

If a data message is received, we pass the packet to `forward` where we first find a viable next-hop by calling `get_route`. `get_route` for now finds viable routes based on best pre-fix matching, and more precise cases for route narrowing will be implemented shortly. Once a route is returned, forward with broadcast a message to the designated network.

If a dump message is received, the `dump` handler will be called, and our forwarding table will be sent to the netowrk that requested it.

With aggregation, we check if the networks are adjacent or if the network is not adjacent but the result of applying a netmask in the forwarding table equals the network of that entry in the forwarding table. 

With disaggregation, the forwarding table is rebuilt based on the update and revoke messages from the past. This happens any time revoke is called.  

At a high level, our approach was to follow the steps as outlined in the project description.

One of the main challenges we faced with this project was keeping a clear understanding of the meaning of the IP addresses. It was often easy to confuse what the purpose of the peer address was, what the source and destination addresses meant for any given chunk of network information we stored, and on. We also learned it was important to remember that Python passes references, so we utilized a library to make deep copies of any data we were changing the values of if we didn't intend to mutate it.

Throughout the progression of this project, we tested our code by running the simulator tests, and also printing various statements and values to ensure our program was behaving as intended.

