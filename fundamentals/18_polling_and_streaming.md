# Polling and Streaming

### Terms before Beginning
- Polling
	- the act of fethcing a resource or piece of data regularly at an interval
	- this makes sure the data is not too stale
- Streaming
	- the act of continuously getting a feed of information from a server by keeping an open connection between the two machines or processes 


### Getting into it
so far we've only talked about clients requesting info from server, server gives the info back \
what if we design a system where a client wants some data that will change very quickly or often \
eg the temp outside \
client wants to see all the changes \
or, a chat app. needs comms in real time \
how to reflect these regularly updated pieces of data \
polling and streaming solve for this

polling 
- very simple to understand and implement
- client issues request, with a set interval 
- ie every x seconds, client will issue the request 
- supports the temp use case we mentioned above
- but, has limits
	- what about chat room
	- you wwant to receive the message instantly 
	- live feeling of messages 
	- polling is limited here, poll every 30seconds sucks 
	- can reduce time between requests (1sec, 0.5sec) 
	- will get more instant experience
	- trade off, lots of load on the sever
	- if you poll very freq, issuing loads of requests per client. scales badly with loads of loads of clients  
	- this is where streaming comes into play

streaming
- open a long live connection with the server from the client
- write to and read from the server through a socket
- lives as long at the network is healthy, or one side kills it
- listens for data that the server pushs
- ie new messages as they arrive, gets pushed to client
- key point: client is saying "im listening to you server, not requesting, but listening"
- then servers job to push out to clients 
- streaming allows for a continuous stream of data
- clients get new mesages without having to request every time
- important to note that its not defo better than polling, all depends on the use case
- your job in an interview to decide which one you want to use

if you need instant experience, then use streaming \
if you need not so instant (minute, 5mins) then polling 


 








