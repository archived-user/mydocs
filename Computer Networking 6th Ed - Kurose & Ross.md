# Computer Networking, 6th Edition
*Kurose & Rose, 2013*

### 1. Computer Networks and the Internet
___
#### Two views of the Internet:
  1. a network of interconnected computing devices / hosts / end systems, with hardware and software components.
      - [End Sys] -> {Links, Switches, Routers] -> [ISPs] 
      - Running protocols TCP, IP, etc.
  2. an infrastructure that provides services to distributed applications.
      - [Distributed Apps] -> API Calls -> [over Internet] -> run program -> [Other End Systems]

#### Network protocol
> defines the format and order of messages exchanged between communicating entities as well as the actions taken on transmission / receipt of a message or other events.

#### Network structure
  1. Network Edge - hosts such as clients and servers.
  2. Access Network - connecting end devices to edge router.
      - DSL (digital subscriber line) - modem connects to telephone infrastructure to gain internet access. Uses twisted pair copper wire.
      - Cable - modem connects to cable television infrastructure to gain internet access. Uses coaxial cable.
      - FTTH (fiber to the home) - OLT connects to optical splitter, aggregating back to ISP's ONT. Uses fiber cables.
      - Ethernet - connects end systems to Ethernet switch to router. It is a LAN, uses Ethernet cable (twisted pair copper wire).
      - WiFi - connects end systems to APs to router. It is a wireless LAN, uses 802.11 technology.
      - 3G/4G/LTE - WAN technologies. Connects end systems wirelessly to internet through cellular telephony infrastructure.
  3. Physical Medium - Twisted pair copper wire, Coaxial cable, Fiber optics, Terrestrial radio channels.
  4. Network Core
      - Packet Switching - store-and-forward transmission, queuing delay, packet loss, forwarding tables, routing protocols.
      - Circuit Switching - FDM (frequency-division multiplexing), TDM (time-division multiplexing)
      Circuit switching pre-allocates use of transmission link which most of the time is less efficient than packet switching.
  5. Network of Networks
      - End systems connect to access ISPs
      - Access ISPs connect to regional ISPs
      - Regional ISPs connect to tier-1 ISPs (global transit ISPs)
      - Content provider networks, as large scale as tier-1 ISPs, has global presence and may be able to connect directly to any tiers of ISPs.
      - PoP (Point of Presence) is a group of routers at one location, to allow customer ISPs to connect to provider ISP network.
      - Multi-home is the arrangement for a customer ISP to connect to multiple provider ISP for better reliability.
      - Peer is the arrangement between same tier ISPs to directly connect and pass traffic to each others network for free.
      - IXP (Internet Exchange Point) is a meeting point where multiple ISPs can peer together.

#### Delays in the Network
> Nodal delay = Processing delay + Queuing delay + Transmission delay (Length/Rate) + Propagation delay
> Traffic Intensity affects Queuing delay = (average rate of packet arrival * length of packet) / transmission rate
> Packet Loss = packets arriving at a full Queue will be dropped
> End-to-end delay = Number of nodes * (Processing + Transmission + Propagation delays)
> Bottleneck Link = link between an end to end connection with lowest throughput (transmission rate)

#### Protocol Layering
- a layered architecture provides modularity, ease implementation of services provided by a layer
- the service model of a layer performs action in a layer to provide service and taps on the service of layers below
- OSI 7 layer is legacy
- each lower layer encapsulate the information from a higher layer as a *payload* and appends additional information to the packet header

> Application Layer: sends *messages* to applications distributed across end systems
> Transport Layer: transports *segments* between application endpoints (connection service)
> Network Layer: move *dataagrams* between hosts (has routing and addressing service)
> Link Layer: transmit *frames* over a link between two network nodes
> Physical Layer: sends individual *bits* across physical transmission medium

#### History of Internet
1. 1961-1972: Development of packet switching (ARPAnet)
2. 1972-1980: Proprietary Networks and Internetworking
3. 1980-1990: Proliferation of Networks (TCP/IP)
4. 1990: Internet Explosion (World Wide Web)
5. The New Millennium: Broadband, high-speed wireless, Social networks, Content Provider ISP, Cloud computing

&nbsp;

### 2. Application Layer
___
#### Principles of Network Applications
Network applications run on end systems and communicate with each other over the network.
Two predominant architectural paradigms in modern network applications:
1. Client-Server Architecture - an always-on host (Server) services requests from many other hosts (Clients).
2. P2P Architecture - direct communication between pairs of intermittenly connected hosts (Peers) with minimal reliance on dedicated servers. P2P is more cost effective and self-scalable, but it may not be ISP Friendly (asymmetrical consumer bandwidth subscriptions), has security risks, and lacks incentive for peers to volunteer resources.

> To be more specific, in the context of a communication session between a pair of processes, the process that initiates the communication (that is, initially contacts the other process at the beginning of the session) is labeled as the client. The process that waits to be contacted to begin the session is the server.
- A Socket is the interface between the application layer and thje transport layer within a host (API between application and the network).
- Multiple processes may run on a single host.
- Hosts are addressed and identified in the network using *IP address*.
- Processes on the host are identified using *port number*.

#### Transport Services Available to Applications
Application push messages through the socket and the transport-layer protocol on  the other side is responsible for getting the messages to the socket of receiving process. Services that can **possibly** be provided by transport-layer protocol includes:
1. Reliable Data Transfer - guarantee that data will be delivered to destination process. May not be critical for loss-tolerant apps (e.g. multimedia).
2. Throughput - guarantee that throughput is available at some specified rate. Good for bandwidth-sensitive apps (e.g. multimedia) but less critical for elastic apps (e.g. email, file transfer).
3. Timing - guarantee that messages do not take more than some specified time/delay to reach destination. Good for real-time applications (e.g. multiplayer game).
4. Security - ensure confidentiality between communicating proceses by encrypting all data transmitted.

TCP Services - connection-oriented service that provides reliable data transfer and can be extended to provide secure encrypted connection.

UDP Services - no-frills, lightweight, connectionless, with no guarantee that messages will reach the destination and no congestion control.

Timing and Throughput guarantees are *not* provided by today's internet protocol. Applications make use of clever designs to overcome these limitations and provide satisfactory service to time-sensitive requirements.

#### Application-Layer Protocols
Defines:
- Types of messages exchanged.
- Syntax of the various message types (fields in message and how fields are delineated).
- Semantics of the fields (meaning of the information in the fields).
- Rules for determining when and how a process sends messages and responds to messages.

#### App-layer Protocol - HTTP (HyperText Transfer Protocol)
Protocol of the World Wide Web, for the requesting and delivery of websites.
- Web page = a document consisting of objects.
- Object = a file (e.g. HTML, JPEG, Java applet, video clip).
- Most web pages consists of a base HTML file and serveral referenced objects.
- URL = reference to an object, consists of a hostname + object's path name.
- Web browser = client program that requests for web content.
- Web server = server program that delivers web content.
- HTTP = defines how web clients request web pages from web servers and how servers transfer web pages to clients. Uses TCP as underlying transport protocol.
- Stateless protocol = HTTP is stateless as the server does not remember any client states.

HTTP with Non-Persistent Connections - each TCP connection is closed after the server sends a response object and will not persist for transmitting other objects. Each new connection incurr an additional RTT (round-trip time) and TCP buffers. (but subsequent objects may be transmitted over *parallel* TCP connections).

HTTP with Persistent Connections - TCP connection is open and persists after server respond. Subsequent requests and responses can be sent over the same connection. These requests can be made back-to-back without waiting for replies to pending requests (**pipelining**).

HTTP Message Format (Pls Google for more details)
- Request message methods: GET, POST, HEAD, PUT, DELETE.
- Response message status: 200 OK, 400 Bad Request, 404 Not Found, 500 Internal Server Error etc.

Cookies -  mechanism to allow servers to identify users connecting and save user state information.
1. Client: make HTTP request to Server.
2. Server: creates ID for user, store (user ID:state info) into backend DB, send HTTP response with "set-cookie: ID" header line.
3. Client: stores ID in cookie file. Interact with website.
4. Server: saves user state changes in DB, with user ID as key.
5. Client: visits the same site in future, sends HTTP request with user ID attached (retrieve from cookie file).
6. Server: retrieves user state based on ID, restore user session.
7. Client: continue browsing from previous saved state.

Web Cache - also known as Proxy Server, keeps copies of recently requested web objects from the network and serves subsequent requests on behalf of the original web server. *Content Distribution Networks (CDN)* provides web caches as a service for websites to distribute contents by geographically localising traffic. Web caches use the *Conditional GET* HTTP requests to fetch updated web objects from the original server *If-Modified-Since* a certain date.
- improves response time for a client request
- reduce load on bandwidth bottleneck
- reduce overall web traffic of the network

#### App-layer Protocol - FTP (File Transfer Protocol)
Protocol to allow user to transfer files to or from a remote host.
- Runs on two parallel TCP connection, control connection and data connection.(control information sent *out-of-band* from data transmission).
- Client authenticates and change remote directory through control connection.
- Server maintains user state information. Sends file over data connection and closes it.
- Control connection is persistent for a user session. Data connection opens and closes for each individual file transfer. Helps to limit number of concurrent connections to reduce server load.

(continue 146)
