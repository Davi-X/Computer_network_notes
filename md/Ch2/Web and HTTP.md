## The Web and HTTP 
Web operates on demand

### Overview of HTTP
HyperText Transfer Protocol defines 
* the structure of messages 
* how th eclient and servcer exchange the messages

Web page consists of objects
Each URL has two components
1. hostname of the server
2. object's path name
   
```md
http://www.someSchool.edu/someDepartment/picture.gif
* host name: www.someSchool.edu
* object's path name: /someDepartment/picture.gif
```

Precedure (Non-presistent connections)
1. HTTP first initiates a TCP connection with the server (host name server)(Handshaking)
2. Both sides then processes access TCP through their socket interfaces
3. Client sends a message into its socket (out of client, into TCP) (request message includes the path name)
4. Server process request message via its socket, encapsulates the object in HTTP resoponse message, sends back to the client via its socket
5. HTTP server process tells TCP to close connection
6. After TCP 4-step termination, connection would be closed

* HTTP would not worry about how to send and how to deal with lost data and reordering
* The server would not store any state of the client, HTTP is stateless protocol, it maintains no information about the clients 
  
### Non-Persistent and Persistent Connections
* Persistent connections:
  *separate* TCP connection
  * HTTP default mode
* Non-Persistent connections:
  *same* TCP connection
  * Each TCP connection is closed after thh server sends the object, does not persist for other objects