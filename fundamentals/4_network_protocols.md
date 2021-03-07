# Network Protocols

### Terms before beginning
- IP
  - Internet protocol
  - defines how machine-to-machine comms should happen
  - other protocols like TCP, UDP and HTTP are built on top of IP
- TCP
  - internet protocol built on top of IP
  - creates a connection that facilitates ordered and reliable data delivery from machine to machine
  - usually implemented in the kernal, which exposes sockets to applications that they can use to stream data through the open connection
    - kernal:program at core of operating system, that has control over everything in the system. facilitates interactions between hardware and software
    - socket: one endpoint of a two-way communicationg link between two programs running on a network. bound to a port number so that the TCP layer can identify the application that data is destined to be sent to
- HTTP
  - HyperText Transfer Protocol
  - very common, built on top of TCP
  - clients make HTTP requests, servers respond with a response
  - typically have the following schema
    - host, like `algoexpert.io`
    - port, like `80` or `443`
    - method, like `GET` / `PUT` / `POST`
    - headers, like ``"Content-type" => "application/json"``
    - body, opaque sequence of bytes
  - response then comes back with something using the below schema
    - status, like `200` or `401`
    - headers, same a above
    - body, same as above
- IP Packet
  - smallest unit used to describe data being send over IP (aside from bytes)
  - also known as a network packet
  - consists of
    - IP header: contains source and destination IP addresses
    - payload: the data being sent over the network

### Getting into it
This is some pretty low level stuff \
Quite simple from a systems design POV \
`Protocol` is an aggreed upon set of rules for an interaction between two parties \
A network protocol describes the type of messages that are sent over the network / internet, the format of those messages, the order if needed, and whether or not the message needs a response.

#### IP
Internet Protocol, same as IP Address \
There are numerous versions, IPv4 and IPv6 \
What we need to know here is that the modern internet runs on IP, means a machine or client tries to interact with another machine and sends data, the data is sent in the form of an IP packet. \
thats a fundamental unit of data sent from machine to machine, they are building blocks (there are others, like bytes which they are made up of). \
packets have two sections (all info in stored in bytes)
- IP header: at the beginning, contains useful info about the packet. contains source IP addr, destination IP addr (all packets have this). this is how info flows over the internet. tells you the total size of the packet too, and version of IP that the packet is using (IPv4, IPv6). between 20~60bytes.
- data: this is the info that the machine is trying to send is stored. limited in size, 2^16 bytes (not that big). all data you want to send will not fit in one packet, you'll have multiple.

If you are only using IP, you have
- no guartantee that packets won't get lost over the network, no guartantee that all packets will be received by the other machine
- no guaranteeing the order that the packets will be read

This is where the IP alone falls apart. \
this is where TCP comes into play.

#### TCP
built on top of IP, stands for Transmission Control Protocol \
solves the issues mentioned above
- guaranteeing order that the packets will be read by the destination machine
- and you are sure to know if some packets keep failing to be received
- error free. if packets get corrupted, you will know and you can re-send.

if you have an IP packet that implements TCP
- the data portion of the IP packet has a TCP header that contains info about the packet (the TCP part, like ordering)
- less space for actual data

when using TCP, the client establishes a TCP connection with the destination server \
that happens through a **handshake**, which is a TCP interaction whereby one computer sends another a couple packets saying *\"I want to connect\"*, the server says *\"sure\"*, then the client responds saying *\"we've now got a connection\"* \
when connection done, machines can send data back and forth \
when one machines doesnt send data for some time, connection times out. one machine can also end the connection by sending a message saying that


IP is functional wrapper around IP \
but, lacks framework that is robust enough to be used in production between clients and servers \
you are only sending arbitary data that fits into packets

#### HTTP
This is where HTTP comes in, built on TCP. introduces high level abstraction on top. \
this is the request reponse paradigm - makes very easy for developers to built robust and easy to use systems \
this is what modern day systems use \
here, we forget about IP packets and TCP. all we care about is HTTP requests and responses \
these requests will have a lot of properties that are defined by the protocol \
good to visualise these (see video)

request attributes
- host:
- port:
- method: the purpose of the request like `GET`
- path: this is where logic comes into the server. a server might have multiple paths, depending on the path diff business logic might happen
- header: metadata about the request (content type, content length for example)
- body: the data that the request is sending to the server

response attributes
- statusCode: meaning of the response
- headers:
- body:


#### Summary of IP / TCP / HTTP
IP and TCP are really just for transferring data \
HTTP on the otherhand introduces the opportunity to add business logic on top of those transfers of packets/data. \
HTTP gives you the ability to implement logic at the end of endpoints. \
IP, TCP, HTTP very important protocols that any system on internet relies on \
IP and TCP are very low level, HTTP is more relevant. \
must be familar with HTTP terminology like *request*, *response*, *method*, *path*
