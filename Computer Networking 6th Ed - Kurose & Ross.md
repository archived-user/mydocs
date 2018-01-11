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
