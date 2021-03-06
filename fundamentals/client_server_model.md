# Client-Server Model

### Terms before beginning
- Client
  - machine or process that requests data or service from a server.
  - note, can be a server and client simultaneously
- Server
  - machine or process that provides data or service to a client
  - listens for incoming network calls
- Client-Server Model
  - paradigm for system design
  - clients request data from servers, servers provide data to clients
- IP Address
  - unique address given to a machine connected to the public internet
  - IPv4 address are four numbers (between 0 and 255) separated by dots
  - example is 127.0.0.1 which is localhost
  - computers (connected to internet) have the ability to find routes to ip address
- Port
  - each program running on a machine listens for new network connections on a different port, to prevent colliding
  - a port is an integer between 0 and 65535
  - ports 0-1023 are system ports, shouldn't be used for user-level processes
  - some ports have predefined users, like 22: secure shell, 53: DNS lookup
- DNS
  - domain name system
  - describes the entities and protocols invovled in translating domain names to IP addresses (so tieing *google.com* to an actual machine to service the requets).
  - machines make DNS querys to well know entities, which are responsible for returning the IP address of the requested domain name in the response
  - so it gives you the ip address of something that will server a clients request

### Getting into it
foundation of the modern internet and how computers talk to each other

#### what happens when you go to algoexpert.io
browser is a client, algoexpert is the server (or, it has a server to act on its behalf) \
client doesnt know what the server is, but knows that it can communicate with it. Ask it for stuff, doesnt know what the server represents. it asks for info, then does stuff based on that info \
At first, browser doesnt know how to talk to the server. instead, it makes a DNS query to get the IP address of algoexpert. \
Then, it can talk to the algoexpert server directly \
When algoexpert was set up on google cloud, they asked for to be provisioned an ip address that a DNS server can resolve to
- interesting aside, use the `dig` command in terminal followed by a website url to get a bunch of info including ip addresses

so browser can talk to algoexpert. it sends a HTTP (will cover in next video, a way of sending info that server can understand) request to algoexperts server. this means it sends bytes that are packaged into packets that get sent to servers, also includes source address of request (so that server can send info back to the requesters ip address). \
servers listens for requests, on specfic ports \
servers have tones of ports, that programs on the server can listen for requests on \
when communicating with another machine, you need to say what port you want to use (client needs to specify this) \
ip address == mail box in apt complex. port is the number within the complex. \
most clients know what port they need to use depending on the protocol they are using
- if client is using http to talk to a server, they know its port 80
- if they are using https, its port 443

back to the example, algoexpert returns html of the webpage to the client which renders the content to the user.
