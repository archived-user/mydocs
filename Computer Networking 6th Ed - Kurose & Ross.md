# Computer Networking, 6th Edition
*Kurose & Rose, 2013*

### 1. Computer Networks and the Internet
___
Two views of the Internet:
  1. a network of interconnected computing devices / hosts / end systems, with hardware and software components.
      - [End Sys] -> {Links, Switches, Routers] -> [ISPs] 
      - Running protocols TCP, IP, etc.
  2. an infrastructure that provides services to distributed applications.
      - [Distributed Apps] -> API Calls -> [over Internet] -> run program -> [Other End Systems]

&nbsp;

Network protocol
> defines the format and order of messages exchanged between communicating entities as well as the actions taken on transmission / receipt of a message or other events.

Network structure
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

Delays in the Network
> Nodal delay = Processing delay + Queuing delay + Transmission delay (Length/Rate) + Propagation delay
> Traffic Intensity affects Queuing delay = (average rate of packet arrival * length of packet) / transmission rate
> Packet Loss = packets arriving at a full Queue will be dropped
> End-to-end delay = Number of nodes * (Processing + Transmission + Propagation delays)
> Bottleneck Link = link between an end to end connection with lowest throughput (transmission rate)

Protocol Layering
- a layered architecture provides modularity, ease implementation of services provided by a layer
- the service model of a layer performs action in a layer to provide service and taps on the service of layers below
- OSI 7 layer is legacy
- each lower layer encapsulate the information from a higher layer as a *payload* and appends additional information to the packet header

> Application Layer: sends *messages* to applications distributed across end systems
> Transport Layer: transports *segments* between application endpoints (connection service)
> Network Layer: move *dataagrams* between hosts (has routing and addressing service)
> Link Layer: transmit *frames* over a link between two network nodes
> Physical Layer: sends individual *bits* across physical transmission medium

History of Internet
1. 1961-1972: Development of packet switching (ARPAnet)
2. 1972-1980: Proprietary Networks and Internetworking
3. 1980-1990: Proliferation of Networks (TCP/IP)
4. 1990: Internet Explosion (World Wide Web)
5. The New Millennium: Broadband, high-speed wireless, Social networks, Content Provider ISP, Cloud computing


### 2. Application Layer
___
(to be continued)
