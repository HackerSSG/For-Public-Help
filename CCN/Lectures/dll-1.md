# Data-Link Layer: An Introduction

## Logical Connections
- In communication at the data-link layer:
  - One data-link layer is involved at the source and one at the destination.
  - Two data-link layers are involved at each router since intermediate nodes need to both encapsulate and decapsulate.

**Q:** Why need both encapsulation and decapsulation at each intermediate node?  
1. Each link of the intermediate node may use different protocol, hence the requirement for different frame format.
2. Even when links use the same protocol, encapsulation and decapsulation are still needed since the link-layer addresses are different.

**Example:**
- Consider a packet sent from Host A to Host B through a router. At the router, the packet is decapsulated to extract the data, and then re-encapsulated into a new frame for the next hop.

---

## Sublayers
- The data-link layer is divided into two sub-layers:
  1. **Data-link control (DLC)**: Deals with all point-to-point and multipoint links (broadcast links).
  2. **Media access control (MAC)**: Deals with broadcast links.

**Example:**
- **DLC**: In a point-to-point network, the DLC sublayer handles the framing, error control, and flow control.
- **MAC**: On an Ethernet network, the MAC sublayer manages access to the shared channel (the wire).

---

## Addressing
- The source and destination IP addresses define communication between two ends but cannot define the links which the data should pass through.
- The datagram is encapsulated into a frame, where two data-link layer addresses are added.
- Types of link-layer addresses:
  1. **Unicast Address**: One-to-one communication.
  2. **Multicast address**: One-to-many communication.
  3. **Broadcast address**: One-to-all communication.

**Example:**
- **Unicast**: A packet sent from one computer to another, e.g., Host A sending data to Host B.
- **Multicast**: A video stream sent to multiple receivers at the same time.
- **Broadcast**: A message sent to all devices on the local network, e.g., ARP request.

---

## Address Resolution Protocol (ARP)
- **Address Resolution Protocol (ARP)** is an auxiliary protocol defined in the network layer that maps the IP addresses into a link-layer address.

**Q:** Why do we need the ARP protocol?  
Any time a node has an IP datagram to send to another node in a link, it has the IP address of the receiving node. However, the IP address of the next node is not helpful in moving a frame through a link, where we need the link-layer address of the next node. For that, ARP is used.

### ARP Process:
1. Host/router sends an ARP request packet through broadcast.
2. The ARP request packet includes: 
   - Link-layer and IP addresses of the sender 
   - IP address of the receiver.
3. Every host/router that receives the ARP request processes the packet.
4. Only the intended recipient sends back an ARP response packet through unicast.
5. The ARP response packet includes the recipient's IP and link-layer addresses.

**Example:**
- Host A needs to send data to Host B, but only knows Host B's IP address. Host A sends an ARP request asking "Who has IP 192.168.1.2?" Host B responds with its MAC address, allowing Host A to send the data.

---

# Data-Link Layer: Media Access Control (MAC)

## Media Access Control (MAC)
- Protocols designed to handle access to shared links belong to the MAC sublayer. These protocols can be categorized into three subgroups:

---

## Channelization
- **Channelization** is channel partitioning and a multiple access method where available bandwidth of a link is shared in frequency, time, or through code among different nodes.
- Three channelization protocols are:
  1. **Frequency-division multiple access (FDMA)**
  2. **Time-division multiple access (TDMA)**
  3. **Code-division multiple access (CDMA)**

### Example of FDMA, TDMA, and CDMA:
1. **FDMA**: Radio stations broadcasting on different frequencies.
2. **TDMA**: A mobile network where different users are assigned different time slots to use the same frequency.
3. **CDMA**: Multiple users transmit simultaneously on the same frequency, but with unique codes that distinguish their transmissions.

---

### CDMA (Code Division Multiple Access)
- In CDMA, only one channel occupies the entire bandwidth, and all nodes can send data simultaneously.
- CDMA means communication with different codes. For example:
  - 𝑑1 is data from node 1, while 𝐶1 is the code assigned to node 1.
  - 𝑑2 is data from node 2, while 𝐶2 is the code assigned to node 2, and so on.

**Example:**
- Node 1 sends the data `d1` encoded with code `C1`, and Node 2 sends `d2` encoded with code `C2`. The receiver can separate the data based on the codes.

### CDMA Details
- In CDMA, each node is assigned a code, which is a sequence of numbers called chips.
- These sequences are carefully selected (called orthogonal sequences).
- In orthogonal sequences, each sequence is made of N elements, where N is the number of possible nodes.
- If a node is sending bit 0, it encodes it as -1.
- If a node is sending bit 1, it encodes it as +1.
- If a node is idle, it sends no signals, which is interpreted as 0.

**Example of Orthogonal Sequences:**
- Sequence for Node 1: `[+1, +1, -1, -1]`
- Sequence for Node 2: `[+1, -1, +1, -1]`

---

### Chip Sequences and Data Representation in CDMA
- Arithmetic rules of orthogonal sequence:
  1. When multiplying a sequence by a scalar value, every element in the sequence is multiplied by that scalar value.  
     Example: `[+1 +1 -1 -1] * 2 = [+2 +2 -2 -2]`
  2. When multiplying two equal sequences, every element is multiplied by its corresponding element. Adding the multiplication results would generate the value N.  
     Example: `[+1 +1 -1 -1] * [+1 +1 -1 -1] = +1 +1 +1 +1 = 4`
  3. When multiplying two different sequences, every element is multiplied by its corresponding element. Adding the multiplication results would generate the value 0.  
     Example: `[+1 +1 -1 -1] * [+1 +1 +1 +1] = +1 +1 -1 -1 = 0`
  4. When adding two sequences, every element is added to its corresponding element. This would generate another sequence.  
     Example: `[+1 +1 -1 -1] + [+1 +1 +1 +1] = [+2 +2 0 0]`

**Example:**
- Sequence 1: `[+1, +1, -1, -1]`
- Sequence 2: `[+1, -1, +1, -1]`
- Multiply Sequence 1 with Sequence 2: `[1×1 + 1×-1 + -1×1 + -1×-1] = [1 - 1 - 1 + 1] = 0`

---

### Receiving Data in CDMA
- If a node wants to receive data from another node, it multiplies the received composite data by the node’s code and divides by N.

**Example for N=4:**
- **Node 1's Data** = `[𝑑1. 𝑐1 + 𝑑2. 𝑐2 + 𝑑3. 𝑐3 + 𝑑4. 𝑐4 . 𝑐1] ÷ 4`
- **Node 1's Data** = `[𝑑1 × 4] ÷ 4 = 𝑑1`

---

### Example of Data Reception:
- Two stations **S1** and **S2** received the composite signal: `[-1 -1 -3 -3 +3 -1 +1 -3]`
- Provided the two codes below, what are the received data at these two stations?
  - For **S1**, **C1** = `[+1 -1 -1 +1 +1 -1 -1 +1]`
  - For **S2**, **C2** = `[+1 +1 +1 +1 -1 -1 -1 -1]`

**S1’s Data Calculation:**
- Multiply the received signal `[-1 -1 -3 -3 +3 -1 +1 -3]` by `C1`, and divide by N (e.g., 4) to get `d1`.

**S2’s Data Calculation:**
- Multiply the received signal `[-1 -1 -3 -3 +3 -1 +1 -3]` by `C2`, and divide by N (e.g., 4) to get `d2`.
