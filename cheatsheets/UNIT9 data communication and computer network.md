# UGC NET – Unit 9: Data Communication and Computer Networks

## 1. Data Communication

### 1.1 Components of a Data Communication System

| Component | Role |
|---|---|
| **Message** | Information to be communicated (text, audio, video, data) |
| **Sender** | Device that sends the data message |
| **Receiver** | Device that receives the message |
| **Transmission Medium** | Physical path between sender and receiver |
| **Protocol** | Set of rules governing data communication |

### 1.2 Communication Modes

| Mode | Direction | Example |
|---|---|---|
| **Simplex** | One direction only | Keyboard to CPU, TV broadcast |
| **Half Duplex** | Both directions, but not simultaneously | Walkie-talkie |
| **Full Duplex** | Both directions simultaneously | Telephone, video call |

### 1.3 Analog and Digital Signals

- **Analog Signal:** Continuous, smooth waveform. Represented by sine wave.
  - Characterised by: **Amplitude** (peak strength), **Frequency** (f = 1/T Hz), **Phase** (position in time).
- **Digital Signal:** Discrete; uses finite number of states (usually 0 and 1).
  - Characterised by: **Bit rate** (bits per second), **Bit interval** (time for one bit = 1/bit rate).

**Periodic Analog Signal (Sine Wave):**
`s(t) = A sin(2πft + φ)`
where A = amplitude, f = frequency, φ = phase.

**Wavelength:** `λ = v/f` where v = propagation speed (≈ 3×10⁸ m/s in vacuum).

### 1.4 Noiseless and Noisy Channels — Channel Capacity

**Nyquist Theorem (Noiseless Channel):**
`Maximum Bit Rate = 2 × Bandwidth × log₂(L)` bps
where L = number of discrete signal levels.

**Shannon's Theorem (Noisy Channel):**
`Channel Capacity C = B × log₂(1 + SNR)` bps
where B = bandwidth in Hz, SNR = Signal-to-Noise Ratio (dimensionless).

**SNR in decibels:** `SNR_dB = 10 × log₁₀(SNR)`

- Nyquist gives theoretical maximum based on signal levels.
- Shannon gives theoretical maximum based on noise; cannot be exceeded regardless of L.

### 1.5 Bandwidth, Throughput, and Latency

- **Bandwidth:** Maximum data rate possible on a link (bps). Property of the medium.
- **Throughput:** Actual data rate achieved in practice (bps). Always ≤ Bandwidth.
- **Latency (Delay):** Time taken for a message to travel from sender to receiver.

**Latency Components:**
```
Latency = Propagation Delay + Transmission Delay + Queuing Delay + Processing Delay
```
- **Propagation Delay** = Distance / Propagation Speed
- **Transmission Delay** = Message Size (bits) / Bandwidth (bps)
- **Bandwidth-Delay Product** = Bandwidth × Propagation Delay
  - Represents number of bits that can be "in flight" in the pipe at any time.

### 1.6 Digital and Analog Transmission

- **Digital Transmission:** Transmits digital signals directly; requires digital medium.
- **Analog Transmission:** Transmits analog signals; can carry both analog and digital data.

### 1.7 Data Encoding and Modulation Techniques

**Digital-to-Digital Encoding (Line Coding):**

| Scheme | Description |
|---|---|
| **NRZ-L** | Level determines bit value (0 = high, 1 = low) |
| **NRZ-I** | Transition at start of bit = 1; no transition = 0 |
| **Manchester** | Mid-bit transition; Low-to-High = 1, High-to-Low = 0 (used in Ethernet) |
| **Differential Manchester** | Mid-bit transition always; transition at start = 0, no transition = 1 |
| **AMI (Alternate Mark Inversion)** | 0 = zero voltage; 1 = alternating +V and -V |
| **B8ZS / HDB3** | AMI variants that handle long strings of zeros |

**Block Coding:** Insert redundancy; divide data into groups and map to larger codewords.
- Example: 4B/5B — 4-bit groups encoded as 5-bit codewords (no more than two leading 0s or trailing 0s).
- Used with NRZ-I to provide synchronisation.

**Analog-to-Digital Conversion (PCM — Pulse Code Modulation):**
1. **Sampling:** Sample analog signal at rate ≥ 2 × highest frequency (Nyquist Sampling Theorem).
   - `Sampling Rate ≥ 2 × f_max`
2. **Quantisation:** Round sampled values to discrete levels.
   - Quantisation error/noise introduced.
3. **Encoding:** Represent quantised values in binary.
   - Bit rate = Sampling Rate × Number of bits per sample.

**Digital-to-Analog Modulation:**

| Technique | Parameter Varied | Formula |
|---|---|---|
| **ASK (Amplitude Shift Keying)** | Amplitude | `s(t) = A_c cos(2πf_c t)` — amplitude varies |
| **FSK (Frequency Shift Keying)** | Frequency | `s(t) = A cos(2πf_i t)` — f_i varies per symbol |
| **PSK (Phase Shift Keying)** | Phase | `s(t) = A cos(2πf_c t + φ_i)` — φ_i varies |
| **QAM (Quadrature AM)** | Amplitude + Phase | `s(t) = A_i cos(2πf_c t) + B_i sin(2πf_c t)` |

- **BPSK:** 2 phases → 1 bit/symbol.
- **QPSK:** 4 phases → 2 bits/symbol.
- **QAM-16:** 16 combinations → 4 bits/symbol.
- **QAM-64:** 64 combinations → 6 bits/symbol.
- **Baud Rate (Symbol Rate):** Number of signal changes per second.
- `Bit Rate = Baud Rate × log₂(L)` where L = number of signal levels.

**Analog-to-Analog Modulation:**
- **AM (Amplitude Modulation):** Carrier amplitude varies with message signal.
- **FM (Frequency Modulation):** Carrier frequency varies; more resistant to noise than AM.
- **PM (Phase Modulation):** Carrier phase varies; closely related to FM.

### 1.8 Broadband and Baseband Transmission

| Aspect | Baseband | Broadband |
|---|---|---|
| Signal Type | Digital | Analog (modulated) |
| Medium Usage | Entire bandwidth for one channel | Multiple channels via FDM |
| Direction | Bidirectional possible | Unidirectional typical |
| Example | Ethernet | Cable TV, DSL |

### 1.9 Multiplexing

**Frequency Division Multiplexing (FDM):**
- Divide bandwidth into frequency bands; each channel uses one band.
- Guards bands separate channels to prevent interference.
- Analog technique; used in radio, cable TV.

**Time Division Multiplexing (TDM):**
- Each channel gets a time slot in rotation.
- **Synchronous TDM:** Fixed slots; unused slots wasted.
- **Statistical (Asynchronous) TDM:** Slots allocated dynamically; more efficient.
- `Link Rate = n × Channel Rate` for synchronous TDM with n channels.

**Wavelength Division Multiplexing (WDM):**
- Multiple wavelengths (colors) of light on a single optical fiber.
- **DWDM (Dense WDM):** Very closely spaced wavelengths; very high capacity.

**Code Division Multiplexing (CDM/CDMA):**
- Each channel assigned a unique chip sequence (code); all transmit simultaneously on full bandwidth.
- Separation done using orthogonal codes.
- `Received signal · chip sequence = original data` (if orthogonal codes: `d_i = (1/N) Σ r_k · c_ik`)

### 1.10 Transmission Media

**Guided (Wired) Media:**

| Medium | Bandwidth | Distance | Interference | Use |
|---|---|---|---|---|
| Twisted Pair (UTP/STP) | Up to 1 Gbps | 100 m (Cat 6) | High | Ethernet (LAN) |
| Coaxial Cable | Up to 1 Gbps | Several km | Medium | Cable TV, older Ethernet |
| Optical Fiber | Up to 100 Tbps | 100+ km | None (light) | Backbone, WAN, FTTH |

**Unguided (Wireless) Media:**

| Medium | Frequency | Range | Use |
|---|---|---|---|
| Radio Waves | 3 Hz – 1 GHz | Long | AM/FM radio, WiFi |
| Microwaves | 1 – 300 GHz | Line-of-sight | Satellite, cellular, WiFi |
| Infrared | 300 GHz – 400 THz | Short | TV remotes, IrDA |

### 1.11 Transmission Errors

- **Single-bit Error:** Only one bit is changed.
- **Burst Error:** Two or more consecutive bits are corrupted.
  - Burst length = distance from first to last corrupted bit.

### 1.12 Error Handling Mechanisms

**Error Detection:**

**Parity Check:**
- **Even Parity:** Add bit so total 1s is even.
- **Odd Parity:** Add bit so total 1s is odd.
- Detects single-bit errors; cannot detect even number of bit errors.

**LRC (Longitudinal Redundancy Check):**
- Parity bit for each column of a block of bits.

**CRC (Cyclic Redundancy Check):**
- Most powerful error detection method.
- Treat data as polynomial `M(x)`; divide by generator polynomial `G(x)`.
- Remainder R(x) appended to message; receiver divides and checks remainder = 0.
- Generator polynomials: CRC-12 (12 bits), CRC-16, CRC-CCITT, CRC-32.
- **Detects:** All single-bit errors, all burst errors of length ≤ degree of G(x), most burst errors of longer length.

**Checksum:**
- Sum all segments; take 1's complement; attach as checksum.
- Receiver sums all segments including checksum; result should be all 1s.
- Used in IP, TCP, UDP, ICMP.

**Checksum Calculation:**
```
1. Divide data into 16-bit segments.
2. Add all segments using 1's complement arithmetic.
3. Take 1's complement of result = checksum.
Verification: Sum of all segments + checksum = all 1s (0xFFFF).
```

**Hamming Distance:**
- `d(v₁, v₂)` = number of positions where v₁ and v₂ differ.
- **Minimum Hamming Distance of a code (d_min):**
  - To detect up to s errors: `d_min ≥ s + 1`
  - To correct up to t errors: `d_min ≥ 2t + 1`
  - To detect s errors and correct t errors: `d_min ≥ s + t + 1` (where s ≥ t)

**Hamming Code (Error Correction):**
- Positions that are powers of 2 (1, 2, 4, 8, ...) are parity bits; rest are data bits.
- For m data bits, need r parity bits where `2^r ≥ m + r + 1`.
- Each parity bit checks specific positions.

---

## 2. Computer Networks

### 2.1 Network Topologies

| Topology | Structure | Advantages | Disadvantages |
|---|---|---|---|
| **Bus** | Single shared cable | Simple, cheap | Single point failure (cable), limited scalability |
| **Ring** | Circular chain | Equal access | Single point failure; troubleshooting hard |
| **Star** | Central hub/switch | Easy to manage, fault isolation | Hub/switch = single point of failure |
| **Mesh** | Every node connected to every other | Highly reliable, redundant | Expensive, complex wiring |
| **Tree (Hierarchical)** | Star networks connected to bus | Scalable | Complex; root failure critical |
| **Hybrid** | Combination of above | Flexible | Complex |

**Full Mesh:** `n(n-1)/2` links for n nodes.

### 2.2 Network Types

| Type | Geographic Scope | Speed | Technology |
|---|---|---|---|
| **PAN** | ~1 m | Low | Bluetooth, USB |
| **LAN** | Building | 1 Mbps – 10 Gbps | Ethernet, WiFi |
| **MAN** | City | 10 – 100 Mbps | WiMAX, ATM |
| **WAN** | Country/Global | Varies | Leased lines, MPLS, Internet |
| **WLAN** | Building (wireless) | Up to 9.6 Gbps (WiFi 6) | 802.11 a/b/g/n/ac/ax |

---

## 3. Network Models

### 3.1 Layered Architecture

- Reduces complexity; each layer provides services to the layer above.
- Layer N communicates logically with layer N of the remote system.
- Physically, data passes down the stack, across the medium, and up the stack.

### 3.2 OSI Reference Model (7 Layers)

| Layer | Number | Function | Key Protocols |
|---|---|---|---|
| **Physical** | 1 | Bit transmission over medium | RS-232, DSL, 802.11 |
| **Data Link** | 2 | Framing, MAC, error detection, flow control | Ethernet, PPP, HDLC |
| **Network** | 3 | Logical addressing, routing | IP, ICMP, ARP, OSPF |
| **Transport** | 4 | End-to-end delivery, error recovery, flow control | TCP, UDP, SCTP |
| **Session** | 5 | Session establishment, management, termination | NetBIOS, RPC |
| **Presentation** | 6 | Data translation, encryption, compression | SSL/TLS, JPEG, ASCII |
| **Application** | 7 | User interface, network services | HTTP, FTP, SMTP, DNS |

**Mnemonic (top to bottom):** All People Seem To Need Data Processing.

**PDU Names:**
- Layer 7-5: **Message/Data**
- Layer 4: **Segment** (TCP) / **Datagram** (UDP)
- Layer 3: **Packet** / **Datagram**
- Layer 2: **Frame**
- Layer 1: **Bits**

### 3.3 TCP/IP Protocol Suite (4 or 5 Layers)

| TCP/IP Layer | OSI Equivalent | Protocols |
|---|---|---|
| **Application** | 7, 6, 5 | HTTP, HTTPS, FTP, SMTP, DNS, SNMP, DHCP |
| **Transport** | 4 | TCP, UDP, SCTP |
| **Internet (Network)** | 3 | IPv4, IPv6, ICMP, ARP, RARP, IGMP |
| **Network Access (Data Link + Physical)** | 2, 1 | Ethernet, WiFi, PPP, Frame Relay |

### 3.4 Addresses in Networks

| Address Type | Layer | Size | Example |
|---|---|---|---|
| **Physical (MAC)** | Data Link (L2) | 48 bits (6 bytes) | `AA:BB:CC:DD:EE:FF` |
| **Logical (IP)** | Network (L3) | 32 bits (IPv4) / 128 bits (IPv6) | `192.168.1.1` |
| **Port** | Transport (L4) | 16 bits | `80` (HTTP), `443` (HTTPS) |
| **Specific (URL)** | Application (L7) | Variable | `www.example.com` |

**Well-known ports (0–1023):** FTP=21, SSH=22, SMTP=25, DNS=53, HTTP=80, POP3=110, IMAP=143, HTTPS=443.
**Registered ports:** 1024–49151.
**Dynamic/Ephemeral ports:** 49152–65535.

### 3.5 Switching Techniques

| Technique | Method | Delay | Use |
|---|---|---|---|
| **Circuit Switching** | Dedicated path established before transfer | Setup delay; no queuing after | PSTN (telephone) |
| **Packet Switching** | Data divided into packets; each routed independently | Store-and-forward; variable delay | Internet |
| **Message Switching** | Entire message stored at each hop | High delay; large storage | Old email systems |
| **Cell Switching (ATM)** | Fixed-size cells (53 bytes) | Low, predictable delay | ATM networks |

**Store-and-Forward Delay:** Each node stores entire packet then forwards.
`Total Transmission Delay = n × (L/B)` where n = number of links, L = packet size, B = bandwidth.

---

## 4. Functions of OSI and TCP/IP Layers

### 4.1 Framing (Data Link Layer)

- Divides bit stream into discrete units called frames.
- **Framing Methods:**
  - **Character Count:** First field states number of characters in frame (fragile).
  - **Byte Stuffing:** Special flag byte marks frame boundaries; ESC byte inserted before any flag appearing in data.
  - **Bit Stuffing:** Flag = `01111110`; sender inserts a 0 after five consecutive 1s in data; receiver removes it.
  - **Physical Layer Coding Violations:** Use invalid signals to mark frame boundaries.

### 4.2 Error Detection and Correction

See Section 1.12 for CRC, Hamming Code, Parity, and Checksum.

### 4.3 Flow Control

- Prevents fast sender from overwhelming slow receiver.

**Stop-and-Wait:**
- Send one frame; wait for ACK; then send next.
- Efficiency: `η = 1/(1 + 2a)` where `a = Propagation Delay / Transmission Time = T_p / T_t`

**Sliding Window Protocol:**
- Sender can have up to W frames outstanding (unacknowledged).
- **Go-Back-N (GBN):**
  - Sender window: W_s = 2^n - 1 (for n-bit sequence numbers).
  - Receiver window: W_r = 1.
  - On error: retransmit errored frame and all subsequent frames.
  - Efficiency: `η = W/(1 + 2a)` if `W < 1 + 2a`; else `η = 1`.
- **Selective Repeat (SR):**
  - Sender window: W_s = 2^(n-1).
  - Receiver window: W_r = 2^(n-1).
  - On error: retransmit only the errored frame; receiver buffers out-of-order frames.
  - Efficiency: `η = W/(1 + 2a)` if `W < 1 + 2a`; else `η = 1`.
  - **Requires twice the buffer size of GBN but better efficiency.**

**Window Size Constraint (SR):** `W_s + W_r ≤ 2^n` to avoid ambiguity.

### 4.4 HDLC (High-Level Data Link Control)

- Bit-oriented protocol; uses bit stuffing.
- **Frame Types:**
  - **I-frame (Information):** Carries user data; has N(S) (send sequence number) and N(R) (receive/acknowledgement).
  - **S-frame (Supervisory):** Flow and error control — RR (Receive Ready), RNR (Receive Not Ready), REJ (Reject), SREJ (Selective Reject).
  - **U-frame (Unnumbered):** Connection management — SABM, UA, DISC, DM.
- **Frame Format:** Flag | Address | Control | Data | FCS | Flag
- **Modes:** NRM (Normal Response Mode), ARM (Asynchronous Response Mode), ABM (Asynchronous Balanced Mode — most common).

### 4.5 Multiple Access Protocols

**Random Access (Contention-based):**

| Protocol | Mechanism |
|---|---|
| **ALOHA** | Send anytime; retransmit on collision after random wait. Throughput S = G·e^(-G); max S = 1/2e ≈ 18.4% at G=0.5 |
| **Slotted ALOHA** | Send only at slot start. Throughput S = G·e^(-G); max S = 1/e ≈ 36.8% at G=1 |
| **CSMA (1-persistent)** | Listen before transmit; send immediately if idle; retransmit after random time if busy |
| **CSMA/CD** | Carrier Sense Multiple Access with Collision Detection (Ethernet 802.3); detect collision during transmission; jam signal; binary exponential backoff |
| **CSMA/CA** | Carrier Sense Multiple Access with Collision Avoidance (WiFi 802.11); use IFS, backoff, ACK; RTS/CTS optional |

**CSMA/CD Condition:** `Frame Size ≥ 2 × Propagation Delay × Bandwidth`
- Minimum frame size in Ethernet: 64 bytes.
- `T_t ≥ 2T_p` (transmission time must be at least twice the propagation delay).

**Binary Exponential Backoff (CSMA/CD):**
- After kth collision, choose random r from {0, 1, ..., 2^k - 1} and wait r × slot time.
- k capped at 10; after 16 collisions, report failure.

**Controlled Access:**

| Protocol | Description |
|---|---|
| **Reservation** | Slots reserved; contention in reservation frames |
| **Polling** | Primary device polls each secondary in turn |
| **Token Passing** | Token Ring (802.5); token circulates; station must hold token to transmit |

**Channelisation:**

| Protocol | Method |
|---|---|
| **FDMA** | Each station assigned distinct frequency band |
| **TDMA** | Each station assigned distinct time slot in frame |
| **CDMA** | Each station assigned unique orthogonal chip code; all share same frequency simultaneously |

**CDMA Data Recovery:**
`d_i = (1/N) (r · c_i)` where r = received signal, c_i = chip code, N = chip length.
- Orthogonality: `c_i · c_j = 0` for i ≠ j.
- `c_i · c_i = N`

### 4.6 Network Devices

| Device | Layer | Function |
|---|---|---|
| **Hub** | L1 | Broadcasts all frames to all ports; repeater |
| **Repeater** | L1 | Amplifies/regenerates signal to extend distance |
| **Bridge** | L2 | Filters frames based on MAC address; connects LANs |
| **Switch** | L2 | Multi-port bridge; maintains MAC table; full duplex |
| **Router** | L3 | Routes packets using IP addresses; connects networks |
| **Gateway** | L4-L7 | Protocol conversion between different networks |
| **Modem** | L1 | Modulates/demodulates digital-analog signal |
| **NIC** | L1-L2 | Network Interface Card; has MAC address |

### 4.7 Virtual LANs (VLANs)

- Logically segment a physical LAN into multiple virtual LANs.
- Members of a VLAN can be on different physical segments.
- Traffic isolation without physical separation.
- Configured on managed switches.
- **802.1Q tagging:** 4-byte VLAN tag inserted into Ethernet frame containing VLAN ID (12-bit → 4096 VLANs).
- Inter-VLAN routing requires a router or Layer-3 switch.

### 4.8 Backbone Networks

- High-speed networks that connect LANs and provide campus-wide or enterprise-wide connectivity.
- Types: **Bus backbone**, **Star backbone**, **Distributed backbone**.
- Technologies: Gigabit Ethernet, 10 Gbps Ethernet, MPLS.

---

## 5. Network Layer — IP Addressing and Routing

### 5.1 IPv4 Structure and Address Space

- 32-bit address; written in **dotted decimal notation**: 4 octets separated by dots.
- Total address space: `2^32 = 4,294,967,296` addresses.
- **IPv4 Datagram Header (20 bytes minimum):**

| Field | Size | Description |
|---|---|---|
| Version | 4 bits | 4 for IPv4 |
| IHL | 4 bits | Header length in 32-bit words (min 5 = 20 bytes) |
| DSCP/ToS | 8 bits | Differentiated services |
| Total Length | 16 bits | Header + data in bytes (max 65,535) |
| Identification | 16 bits | For reassembly of fragments |
| Flags | 3 bits | DF (Don't Fragment), MF (More Fragments) |
| Fragment Offset | 13 bits | Position of fragment in units of 8 bytes |
| TTL | 8 bits | Decremented at each router; drop if 0 |
| Protocol | 8 bits | TCP=6, UDP=17, ICMP=1, OSPF=89 |
| Header Checksum | 16 bits | Checksum of header only |
| Source IP | 32 bits | — |
| Destination IP | 32 bits | — |
| Options | Variable | — |

### 5.2 Classful Addressing

| Class | First Bits | First Octet Range | Default Mask | Networks | Hosts/Network |
|---|---|---|---|---|---|
| **A** | 0 | 1 – 126 | /8 (255.0.0.0) | 126 | 2^24 − 2 = 16,777,214 |
| **B** | 10 | 128 – 191 | /16 (255.255.0.0) | 16,384 | 2^16 − 2 = 65,534 |
| **C** | 110 | 192 – 223 | /24 (255.255.255.0) | 2,097,152 | 2^8 − 2 = 254 |
| **D** | 1110 | 224 – 239 | — | Multicast | — |
| **E** | 1111 | 240 – 255 | — | Reserved/Experimental | — |

- `127.x.x.x` reserved for loopback.
- Host address all 0s = Network address; all 1s = Broadcast address.
- Usable hosts = `2^h − 2` where h = number of host bits.

**Private IP Ranges (RFC 1918):**
- `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`

### 5.3 Classless Addressing (CIDR)

- **CIDR (Classless Inter-Domain Routing):** IP/prefix notation. Example: `192.168.1.0/24`.
- Prefix length (n) specifies the number of network bits.
- Number of addresses = `2^(32-n)`.

**Subnet Mask:** n ones followed by (32-n) zeros.
- `/24` → `255.255.255.0`
- `/20` → `255.255.240.0`

**Subnetting:**
- Borrow bits from host portion to create subnets.
- If borrowing s bits: Number of subnets = `2^s`; hosts per subnet = `2^(h-s) − 2`.

**VLSM (Variable Length Subnet Masking):** Different subnets of different sizes carved from the same address space.

**Supernetting/Route Aggregation:** Combine multiple networks into one prefix (CIDR block).
- Networks must be contiguous and a power-of-2 block.

**Network Address Calculation:**
```
Network Address = IP Address AND Subnet Mask (bitwise)
Broadcast Address = Network Address OR (NOT Subnet Mask)
First Host = Network Address + 1
Last Host = Broadcast Address − 1
```

### 5.4 Fragmentation and Reassembly

- Required when datagram size exceeds MTU (Maximum Transmission Unit) of a link.
- **MTU of Ethernet:** 1500 bytes.
- Each fragment has its own IP header; identified by same ID field.
- **Fragment Offset:** Position in original datagram; measured in units of 8 bytes.
  `Fragment Offset = Byte Offset / 8`
- **MF bit:** Set in all fragments except the last.
- **Reassembly:** Done only at the destination host.

**Example:** Original datagram = 4000 bytes (payload 3980 bytes); MTU = 1500 bytes.
- Fragment 1: bytes 0–1479; offset = 0; MF = 1.
- Fragment 2: bytes 1480–2959; offset = 185; MF = 1.
- Fragment 3: bytes 2960–3979; offset = 370; MF = 0.

### 5.5 IPv6

- 128-bit addresses; `2^128 ≈ 3.4 × 10^38` addresses.
- Written as eight 16-bit groups in hex, separated by colons.
  Example: `2001:0DB8:0000:0000:0000:0000:0000:0001` → `2001:DB8::1`

**IPv6 Header (40 bytes — fixed size):**

| Field | Size | Description |
|---|---|---|
| Version | 4 bits | 6 for IPv6 |
| Traffic Class | 8 bits | Like ToS in IPv4 |
| Flow Label | 20 bits | Identifies flows for QoS |
| Payload Length | 16 bits | Length of data after header |
| Next Header | 8 bits | Type of next header (like Protocol in IPv4) |
| Hop Limit | 8 bits | Like TTL in IPv4 |
| Source Address | 128 bits | — |
| Destination Address | 128 bits | — |

**IPv6 Improvements over IPv4:**
- No fragmentation by routers (only source).
- No header checksum (faster processing).
- Simplified header.
- Built-in IPsec support.
- No NAT needed (enough addresses).
- ICMPv6 replaces ARP (NDP — Neighbor Discovery Protocol).

**IPv6 Address Types:**
- **Unicast:** One-to-one. Global, Link-local (`FE80::/10`), Loopback (`::1`).
- **Multicast:** One-to-many (`FF00::/8`).
- **Anycast:** One-to-nearest.
- No broadcast in IPv6.

### 5.6 ARP (Address Resolution Protocol)

- Maps logical (IP) address to physical (MAC) address.
- Operates within a single network (LAN segment).

**ARP Process:**
1. Source knows destination IP; needs MAC.
2. Source broadcasts **ARP Request**: "Who has IP X? Tell IP Y."
3. Device with IP X replies with **ARP Reply** (unicast): "IP X is at MAC M."
4. Source caches the mapping in **ARP Cache** (TTL ≈ minutes).

**Proxy ARP:** Router responds to ARP requests on behalf of hosts on another network.
**Gratuitous ARP:** Host broadcasts ARP for its own IP (announces itself / updates caches).
**RARP:** Reverse ARP — maps MAC to IP (obsolete; replaced by DHCP).
**InARP:** Inverse ARP — used in Frame Relay to find IP from DLCI.

### 5.7 Network Layer Delivery

- **Direct Delivery:** Sender and receiver on the same network; sender delivers directly.
- **Indirect Delivery:** Receiver on different network; sender sends to a router (default gateway).

### 5.8 Routing Algorithms

**Classification:**
- **Static (Non-Adaptive):** Routes configured manually; do not change with topology.
- **Dynamic (Adaptive):** Routes updated automatically based on current topology.
  - **Distance Vector (DV):** Each router knows distance to all destinations.
  - **Link State (LS):** Each router knows complete topology.

**Distance Vector Routing (Bellman-Ford):**
`D_x(y) = min_v {c(x,v) + D_v(y)}` for all destinations y and neighbours v.
- Each router maintains a routing table.
- Routers exchange distance vectors with direct neighbours periodically.
- **Count-to-Infinity Problem:** Bad news propagates slowly.
- **Solutions:** Split Horizon, Poison Reverse, Triggered Updates.
- **Protocol:** RIP (Routing Information Protocol) — max 15 hops; metric = hop count.

**Link State Routing (Dijkstra's Algorithm):**
```
1. Each router floods Link State Advertisements (LSAs) to all routers.
2. Each router builds complete topology (LSDB — Link State Database).
3. Each router runs Dijkstra's shortest path algorithm:
   - N' = {u} (source)
   - D(v) = c(u,v) for all neighbours v; else ∞
   - Loop:
       Find w not in N' with min D(w)
       Add w to N'
       Update D(v) = min(D(v), D(w) + c(w,v)) for all neighbours v of w not in N'
   - Until N' contains all nodes
```
- **Protocol:** OSPF (Open Shortest Path First) — uses Dijkstra; metric = cost; supports VLSM/CIDR; hierarchical with areas.

**Path Vector Routing:**
- Maintains complete path (list of AS numbers) to each destination.
- **Protocol:** BGP (Border Gateway Protocol) — inter-domain routing on the Internet.

**Comparison:**

| Feature | Distance Vector (RIP) | Link State (OSPF) | Path Vector (BGP) |
|---|---|---|---|
| Algorithm | Bellman-Ford | Dijkstra | Path vector |
| Knowledge | Neighbour info | Complete topology | Path info |
| Convergence | Slow | Fast | Moderate |
| Scalability | Poor | Good | Excellent |
| Metric | Hop count | Cost (bandwidth) | Policy-based |
| Scope | Intra-domain | Intra-domain | Inter-domain |

---

## 6. Transport Layer

### 6.1 UDP (User Datagram Protocol)

- Connectionless; unreliable; no flow/congestion control.
- **Header (8 bytes):** Source Port | Destination Port | Length | Checksum.
- Low overhead; suitable for: DNS, DHCP, VoIP, video streaming, SNMP.
- Checksum covers UDP header + data + pseudo-header (source IP, dest IP, protocol, UDP length).

### 6.2 TCP (Transmission Control Protocol)

- Connection-oriented; reliable; byte-stream service; full-duplex.

**TCP Header (20 bytes minimum):**

| Field | Size | Description |
|---|---|---|
| Source Port | 16 bits | — |
| Destination Port | 16 bits | — |
| Sequence Number | 32 bits | Byte number of first byte in segment |
| Acknowledgement Number | 32 bits | Next expected byte from other side |
| Data Offset (HLEN) | 4 bits | Header length in 32-bit words |
| Control Flags | 9 bits | URG, ACK, PSH, RST, SYN, FIN |
| Window Size | 16 bits | Receive window size (flow control) |
| Checksum | 16 bits | — |
| Urgent Pointer | 16 bits | — |

**TCP Connection Management:**

**Three-Way Handshake (Connection Establishment):**
```
Client → Server: SYN (seq=x)
Server → Client: SYN+ACK (seq=y, ack=x+1)
Client → Server: ACK (seq=x+1, ack=y+1)
```

**Four-Way Handshake (Connection Termination):**
```
Client → Server: FIN (seq=x)
Server → Client: ACK (ack=x+1)
Server → Client: FIN (seq=y)
Client → Server: ACK (ack=y+1)
[Client waits 2×MSL in TIME_WAIT state]
```
MSL = Maximum Segment Lifetime (typically 2 minutes).

**TCP Flow Control (Sliding Window):**
- Receiver advertises **receive window (rwnd)** in each ACK.
- Sender cannot have more than rwnd bytes unacknowledged.
- **Effective Window = min(cwnd, rwnd)** where cwnd = congestion window.

**TCP Congestion Control:**

| Phase | Algorithm | Behaviour |
|---|---|---|
| **Slow Start** | cwnd starts at 1 MSS; doubles each RTT (exponential) | Until cwnd ≥ ssthresh |
| **Congestion Avoidance** | cwnd increases by 1 MSS per RTT (linear) | After cwnd ≥ ssthresh |
| **Congestion Detected (Timeout)** | ssthresh = cwnd/2; cwnd = 1 MSS; restart Slow Start | Severe congestion |
| **Congestion Detected (3 Dup ACKs)** | ssthresh = cwnd/2; cwnd = ssthresh + 3 (Fast Recovery) | Mild congestion (TCP Reno) |

**TCP Tahoe:** On any congestion → cwnd = 1, restart Slow Start.
**TCP Reno:** On timeout → cwnd = 1; On 3 dup ACKs → Fast Retransmit + Fast Recovery.
**TCP NewReno, CUBIC, BBR:** Modern variants with improved performance.

**RTT Estimation:**
`EstimatedRTT = (1 - α) × EstimatedRTT + α × SampleRTT` (α = 0.125 typically, EWMA)
`DevRTT = (1 - β) × DevRTT + β × |SampleRTT - EstimatedRTT|` (β = 0.25)
`Timeout Interval = EstimatedRTT + 4 × DevRTT`

### 6.3 SCTP (Stream Control Transmission Protocol)

- Message-oriented (unlike TCP's byte-stream); preserves message boundaries.
- Multi-streaming: Multiple independent streams within one association; head-of-line blocking avoided.
- Multi-homing: Each endpoint can have multiple IP addresses for redundancy.
- Four-way handshake with cookie mechanism (prevents SYN flooding).
- Supports both reliable and unreliable delivery per stream.
- Used in: Telephony signalling (SS7 over IP), WebRTC.

**SCTP Association Establishment:**
```
INIT → INIT-ACK (with cookie) → COOKIE-ECHO → COOKIE-ACK
```

---

## 7. World Wide Web (WWW)

### 7.1 URL (Uniform Resource Locator)

```
protocol://host:port/path?query#fragment
http://www.example.com:80/index.html?id=1#section2
```
- **Protocol:** http, https, ftp, mailto, telnet.
- **Default ports:** HTTP = 80, HTTPS = 443, FTP = 21.

### 7.2 DNS (Domain Name System)

- Distributed hierarchical naming system; maps domain names to IP addresses.

**DNS Hierarchy:**
```
Root (.) → Top-Level Domain (TLD: .com, .org, .in) → Second-Level (example) → Subdomain (www)
```

**DNS Server Types:**
- **Root Name Servers:** 13 sets (a–m); know TLD server addresses.
- **TLD Name Servers:** Responsible for .com, .net, .org, country codes.
- **Authoritative Name Servers:** Have actual DNS records for a domain.
- **Local (Recursive Resolver):** Client's first contact; caches answers.

**DNS Resolution (Recursive Query):**
```
Client → Local Resolver → Root Server → TLD Server → Authoritative Server → IP address returned
```

**DNS Record Types:**

| Record | Description |
|---|---|
| **A** | IPv4 address for a hostname |
| **AAAA** | IPv6 address for a hostname |
| **MX** | Mail exchange server for domain |
| **CNAME** | Canonical name (alias) |
| **NS** | Name server for domain |
| **PTR** | Reverse DNS — IP to hostname |
| **SOA** | Start of Authority — primary name server info |
| **TXT** | Text record (SPF, DKIM) |

**Inverse DNS (Reverse Lookup):** Uses `in-addr.arpa` domain.
IP `192.168.1.1` → query `1.1.168.192.in-addr.arpa` → PTR record → hostname.

### 7.3 Electronic Mail Architecture

**Components:** MUA (Mail User Agent), MSA (Mail Submission Agent), MTA (Mail Transfer Agent), MDA (Mail Delivery Agent), Mailbox.

**SMTP (Simple Mail Transfer Protocol):**
- Port 25 (server-to-server), Port 587 (client submission), Port 465 (SMTPS).
- Commands: HELO/EHLO, MAIL FROM, RCPT TO, DATA, QUIT.
- Push protocol — sender pushes mail to receiver's server.

**POP3 (Post Office Protocol v3):**
- Port 110 (or 995 for SSL).
- Download-and-delete model; mail stored locally.
- States: Authorization, Transaction, Update.
- Commands: USER, PASS, STAT, LIST, RETR, DELE, QUIT.

**IMAP (Internet Message Access Protocol):**
- Port 143 (or 993 for SSL).
- Mail stored on server; multiple device access; folder management.
- More powerful than POP3; supports searching, partial fetch.
- Commands: LOGIN, SELECT, FETCH, SEARCH, STORE, LOGOUT.

### 7.4 TELNET and FTP

**TELNET:**
- Remote login protocol; port 23.
- Transmits data in plaintext (insecure).
- Replaced by **SSH (Secure Shell)** on port 22.
- Uses NVT (Network Virtual Terminal) for terminal emulation.

**FTP (File Transfer Protocol):**
- File transfer; uses two connections: **Control (port 21)** and **Data (port 20 for active mode)**.
- **Active Mode:** Server initiates data connection to client from port 20.
- **Passive Mode (PASV):** Client initiates data connection to server (used when client is behind NAT/firewall).
- Commands: USER, PASS, LIST, RETR, STOR, DELE, MKD, CWD, QUIT.
- Plaintext (insecure); replaced by SFTP (over SSH) or FTPS (FTP over TLS).

---

## 8. Network Security

### 8.1 Malware Types

| Type | Description |
|---|---|
| **Virus** | Attaches to programs; replicates when host runs |
| **Worm** | Self-replicating; spreads without host program |
| **Trojan Horse** | Disguised as legitimate software |
| **Ransomware** | Encrypts data; demands ransom |
| **Spyware** | Collects user information covertly |
| **Adware** | Displays unwanted advertisements |
| **Rootkit** | Hides its presence; gains root/admin access |
| **Botnet** | Network of infected machines (bots) controlled by C&C |
| **Phishing** | Deceptive messages to steal credentials |
| **DoS/DDoS** | Overwhelm target to deny service |

### 8.2 Cryptography

**Goals (CIA + Non-repudiation):**
- **Confidentiality:** Only intended parties read the message.
- **Integrity:** Message has not been altered.
- **Authentication:** Verify identity of sender.
- **Non-repudiation:** Sender cannot deny sending.

**Cryptography vs Steganography:**
- **Cryptography:** Makes message unreadable (hides content).
- **Steganography:** Hides the existence of the message (in image, audio, etc.).

### 8.3 Secret-Key (Symmetric) Algorithms

- Same key for encryption and decryption.
- **Key distribution problem:** How to securely share the key.

| Algorithm | Key Size | Block Size | Notes |
|---|---|---|---|
| **DES** | 56 bits | 64 bits | Insecure; vulnerable to brute force |
| **3DES (Triple DES)** | 112/168 bits | 64 bits | DES applied 3 times; slow |
| **AES** | 128/192/256 bits | 128 bits | Current standard; secure and fast |
| **RC4** | Variable | Stream cipher | Used in WEP/WPA; now considered insecure |
| **Blowfish** | 32–448 bits | 64 bits | Fast; used in bcrypt |

**Block Cipher Modes:**
- **ECB (Electronic Codebook):** Same plaintext → same ciphertext; insecure for patterns.
- **CBC (Cipher Block Chaining):** XOR each block with previous ciphertext; IV used for first block.
- **CTR (Counter Mode):** Turns block cipher into stream cipher; parallelisable.
- **GCM (Galois/Counter Mode):** CTR + authentication; AEAD.

### 8.4 Public-Key (Asymmetric) Algorithms

- Two keys: **Public Key** (encrypt/verify) and **Private Key** (decrypt/sign).
- No key distribution problem; private key never shared.
- Much slower than symmetric; typically used to exchange symmetric keys.

**RSA Algorithm:**
1. Choose two large primes p and q.
2. Compute `n = p × q`.
3. Compute `φ(n) = (p−1)(q−1)`.
4. Choose e such that `1 < e < φ(n)` and `gcd(e, φ(n)) = 1`.
5. Compute d such that `d × e ≡ 1 (mod φ(n))` (modular inverse).
6. **Public Key:** (e, n); **Private Key:** (d, n).
7. **Encryption:** `C = M^e mod n`
8. **Decryption:** `M = C^d mod n`

Security based on difficulty of factoring large integers.

**Diffie-Hellman Key Exchange:**
- Allows two parties to establish a shared secret over an insecure channel.
```
Public: prime p, generator g.
Alice: choose secret a; send A = g^a mod p
Bob:   choose secret b; send B = g^b mod p
Alice: computes K = B^a mod p = g^(ab) mod p
Bob:   computes K = A^b mod p = g^(ab) mod p
Shared secret K = g^(ab) mod p
```
Security based on difficulty of discrete logarithm problem.

**Other algorithms:** DSA (signatures), ECC (Elliptic Curve Cryptography — smaller keys, same security), ElGamal.

**Hash Functions:**
- One-way; fixed-length output; any change in input changes output significantly.
- MD5: 128-bit digest (broken; do not use for security).
- SHA-1: 160-bit (deprecated).
- SHA-256, SHA-512 (SHA-2 family): Current standard.
- SHA-3: Keccak algorithm; different design from SHA-2.
- `H(M) ≠ H(M')` for M ≠ M' (collision resistance).

**MAC (Message Authentication Code):** `MAC = H(K || M)` or HMAC — provides integrity and authentication but not non-repudiation.

### 8.5 Digital Signature

- Provides integrity, authentication, and non-repudiation.

**Process:**
```
Signing:    Signature = Encrypt_PrivateKey(Hash(Message))
Verification: Decrypt_PublicKey(Signature) == Hash(Message) ?
```

**RSA Signature:**
- Sign: `S = M^d mod n`
- Verify: `M = S^e mod n`

**Digital Certificate (X.509):** Binds public key to identity; issued by Certificate Authority (CA).
**PKI (Public Key Infrastructure):** Framework of CAs, RAs, certificates for managing public keys.

### 8.6 Virtual Private Networks (VPN)

- Creates encrypted tunnel over public network; extends private network.
- **Types:**
  - **Site-to-Site:** Connect two networks via VPN gateway.
  - **Remote Access:** Individual connects to corporate network.
- **Protocols:**
  - **IPsec:** Layer 3; two modes — Transport (encrypts payload) and Tunnel (encrypts entire IP packet).
  - **SSL/TLS VPN:** Layer 4; browser-based; easier for remote access.
  - **PPTP, L2TP/IPsec:** Layer 2 tunnelling protocols.
- **IPsec Components:**
  - **AH (Authentication Header):** Integrity and authentication; no encryption.
  - **ESP (Encapsulating Security Payload):** Encryption + integrity + authentication.
  - **IKE (Internet Key Exchange):** Negotiates security associations (SAs).

### 8.7 Firewalls

- Controls incoming and outgoing network traffic based on security rules.

| Type | Layer | How it works |
|---|---|---|
| **Packet Filter** | L3/L4 | Filters based on IP, port, protocol; stateless |
| **Stateful Inspection** | L3/L4 | Tracks connection state; allows established sessions |
| **Application Gateway (Proxy)** | L7 | Deep packet inspection; understands application protocols |
| **Next-Generation Firewall (NGFW)** | L3–L7 | IDS/IPS, user identity, application awareness |

**DMZ (Demilitarized Zone):** Network segment between internal and external networks; hosts public-facing servers.

---

## 9. Mobile Technology

### 9.1 GSM (Global System for Mobile Communications)

- 2G standard; digital; circuit-switched for voice; TDMA + FDMA.
- **Frequency Bands:** 900 MHz and 1800 MHz (Europe/Asia); 850/1900 MHz (Americas).

**GSM Architecture:**

| Component | Description |
|---|---|
| **MS (Mobile Station)** | User device + SIM card |
| **BTS (Base Transceiver Station)** | Radio transceiver; communicates with MS |
| **BSC (Base Station Controller)** | Controls multiple BTS; handover management |
| **MSC (Mobile Switching Centre)** | Routes calls; connects to PSTN/other MSCs |
| **HLR (Home Location Register)** | Database of all subscribers of a network |
| **VLR (Visitor Location Register)** | Temporary database of roaming subscribers |
| **AuC (Authentication Centre)** | Authentication and encryption |
| **EIR (Equipment Identity Register)** | Database of valid/blocked IMEI numbers |

**GSM Channel Types:**
- **Traffic Channels (TCH):** Carry user voice/data.
- **Control Channels (CCH):** BCCH, PCH, RACH, SDCCH, SACCH.

### 9.2 CDMA (Code Division Multiple Access)

- 2.5G–3G technology (cdmaOne, CDMA2000).
- All users share same frequency simultaneously; separated by unique codes.
- Better capacity than GSM; soft handoff (connect to multiple towers simultaneously).
- No SIM card; MEID/ESN identifies handset.

### 9.3 Mobile Computing Architecture

- **Middleware:** Software layer between mobile OS and applications (handles communication, data sync, session management).
- **Mobile Gateway:** Connects mobile networks to Internet/corporate networks.
  - **WAP Gateway:** Converts WAP (Wireless Application Protocol) to HTTP.
- **Challenges:** Limited bandwidth, intermittent connectivity, limited power, small screens, security.

### 9.4 Mobile IP

- Allows mobile device to maintain same IP address while moving between networks.
- **Nodes:**
  - **Home Agent (HA):** Router on home network; forwards packets to current location.
  - **Foreign Agent (FA):** Router on visited network; provides care-of address.
  - **Mobile Node (MN):** The mobile device.
  - **Care-of Address (CoA):** Temporary address on visited network.
- **Operation:**
  1. MN registers CoA with HA via FA.
  2. Correspondent sends packet to MN's home address.
  3. HA intercepts; tunnels (IP-in-IP encapsulation) to CoA.
  4. FA/MN receives tunnelled packet.
  5. MN sends reply directly to Correspondent (triangular routing).
- **Triangle Routing Problem:** Return path not via HA; can be optimised using Route Optimisation.

### 9.5 Communication Satellites

| Type | Altitude | Orbit Period | Latency | Example |
|---|---|---|---|---|
| **LEO** (Low Earth) | 200–2000 km | ~90 min | ~20 ms | Starlink, Iridium |
| **MEO** (Medium Earth) | 2000–35786 km | 2–24 hrs | ~70 ms | GPS, Galileo |
| **GEO** (Geostationary) | 35,786 km | 24 hrs | ~250–300 ms | DirecTV, INTELSAT |
| **HEO** (Highly Elliptical) | Variable | Variable | Variable | Molniya |

- GEO satellites appear stationary; minimum 3 needed for global coverage (except poles).

### 9.6 Wireless Networks and Topologies

**IEEE 802.11 Standards (WiFi):**

| Standard | Band | Max Speed | Notes |
|---|---|---|---|
| 802.11a | 5 GHz | 54 Mbps | OFDM |
| 802.11b | 2.4 GHz | 11 Mbps | DSSS |
| 802.11g | 2.4 GHz | 54 Mbps | OFDM; backward-compatible with b |
| 802.11n (WiFi 4) | 2.4/5 GHz | 600 Mbps | MIMO |
| 802.11ac (WiFi 5) | 5 GHz | 3.5 Gbps | MU-MIMO, beamforming |
| 802.11ax (WiFi 6) | 2.4/5/6 GHz | 9.6 Gbps | OFDMA, BSS Colouring |

**Wireless Topologies:**
- **Infrastructure Mode:** Devices connect through AP (Access Point); AP connects to wired network.
- **Ad Hoc (IBSS):** Direct device-to-device; no AP; peer-to-peer.

### 9.7 Cellular Topology

- Coverage area divided into **cells**; each served by a BTS.
- **Frequency Reuse:** Same frequencies reused in non-adjacent cells to avoid interference.
- **Cluster Size (N):** N = i² + ij + j² (where i, j are non-negative integers not both zero): 1, 3, 4, 7, 9, 12, 13, ...
- **Handover/Handoff:** Transfer of call from one cell to another as user moves.
  - **Hard Handoff:** Disconnect from old cell before connecting to new.
  - **Soft Handoff (CDMA):** Connected to multiple cells simultaneously.

### 9.8 Mobile Ad Hoc Networks (MANETs)

- Self-organising; no fixed infrastructure; nodes act as routers.
- Highly dynamic topology; multihop routing.
- **Challenges:** Dynamic topology, limited bandwidth, battery constraints, security.
- **Routing Protocols:**
  - **Proactive (Table-driven):** DSDV, OLSR — maintain routing tables at all times.
  - **Reactive (On-demand):** AODV (Ad hoc On-demand Distance Vector), DSR (Dynamic Source Routing) — discover routes only when needed.
  - **Hybrid:** ZRP (Zone Routing Protocol).

### 9.9 GPRS and SMS

**GPRS (General Packet Radio Service):**
- 2.5G; packet-switched data over GSM network.
- Data rates: 56–114 kbps (theoretical).
- Always-on connectivity; billed by data volume.
- Added new network elements: SGSN (Serving GPRS Support Node), GGSN (Gateway GPRS Support Node).

**SMS (Short Message Service):**
- Store-and-forward text messaging.
- Max 160 characters (7-bit encoding) per message.
- Transported via GSM control channels.
- **SMSC (Short Message Service Centre):** Stores and forwards SMS messages.

### 9.10 Wireless Geolocation Systems

| System | Method | Accuracy |
|---|---|---|
| **GPS** | Trilateration from ≥4 satellites; measures signal travel time | ~5–10 m |
| **A-GPS (Assisted GPS)** | GPS + network data for faster fix | ~5–10 m |
| **Cell ID** | Identify serving cell tower | 100 m – several km |
| **Wi-Fi Positioning** | Match detected APs against database | ~15–40 m |
| **Bluetooth Beacons** | Indoor positioning | ~1–3 m |

**GPS Principle:** `Distance = Speed of light × Travel time`; trilateration from 3+ satellites gives 3D position; 4th satellite for time correction.

---

## 10. Cloud Computing and IoT

### 10.1 Cloud Service Models

| Model | Provider Manages | Customer Manages | Example |
|---|---|---|---|
| **IaaS** (Infrastructure as a Service) | Hardware, networking, storage, hypervisor | OS, middleware, runtime, apps, data | AWS EC2, Azure VMs, GCP Compute |
| **PaaS** (Platform as a Service) | IaaS + OS, middleware, runtime | Applications and data | Heroku, Google App Engine, Azure App Service |
| **SaaS** (Software as a Service) | Everything | User configuration | Gmail, Salesforce, Office 365, Dropbox |

**Hierarchy:** IaaS → PaaS → SaaS (each layer abstracts the one below).

### 10.2 Cloud Deployment Models

| Model | Access | Control | Example |
|---|---|---|---|
| **Public Cloud** | Open to all | Provider | AWS, Azure, GCP |
| **Private Cloud** | Single organisation | Organisation | On-premises VMware, OpenStack |
| **Community Cloud** | Shared by organisations with common interest | Shared | Government cloud, healthcare cloud |
| **Hybrid Cloud** | Mix of public and private | Shared | Sensitive data on private; public for burst |

### 10.3 Virtualisation

- **Virtualisation:** Creating virtual version of hardware resources.
- **Hypervisor (VMM — Virtual Machine Monitor):**
  - **Type 1 (Bare Metal):** Runs directly on hardware; guests run on hypervisor. Example: VMware ESXi, Xen, Hyper-V.
  - **Type 2 (Hosted):** Runs on top of host OS. Example: VirtualBox, VMware Workstation.
- **Container Virtualisation:** OS-level virtualisation; share host kernel; lighter than VMs. Example: Docker, Kubernetes.

**Benefits of Virtualisation:** Resource utilisation, isolation, rapid provisioning, live migration, snapshot.

### 10.4 Cloud Storage and Database Storage

- **Object Storage:** Stores data as objects with metadata; flat namespace. Example: AWS S3, GCS.
- **Block Storage:** Low-level storage; used by VMs as disk volumes. Example: AWS EBS.
- **File Storage:** Hierarchical; shared file system. Example: AWS EFS, Azure Files.
- **Cloud Database Services:**
  - Relational: Amazon RDS, Cloud SQL.
  - NoSQL: DynamoDB, Firestore, Cosmos DB.
  - Data Warehouse: Amazon Redshift, BigQuery.

### 10.5 Resource Management

- **Auto-Scaling:** Automatically add/remove resources based on demand.
- **Load Balancing:** Distribute traffic across multiple servers.
- **Elasticity:** Scale up or down on-demand; pay as you go.
- **Resource Pooling:** Provider's resources pooled for multi-tenant use (location independence).

### 10.6 Service Level Agreement (SLA)

- Formal contract between cloud provider and customer.
- **Key SLA Metrics:**
  - **Availability:** `Availability (%) = (Uptime / Total Time) × 100`
  - **Five Nines (99.999%):** Allows ~5.26 minutes downtime per year.
  - **RTO (Recovery Time Objective):** Maximum acceptable time to restore service after failure.
  - **RPO (Recovery Point Objective):** Maximum acceptable data loss measured in time.
- SLA defines penalties for non-compliance (credits, refunds).

### 10.7 IoT (Internet of Things) Basics

- Network of physical devices embedded with sensors, actuators, software, and connectivity.

**IoT Architecture Layers:**

| Layer | Function |
|---|---|
| **Perception/Device Layer** | Sensors, actuators collect physical data |
| **Network/Communication Layer** | Transmit data via WiFi, BLE, Zigbee, LoRa, LTE, 5G |
| **Middleware/Processing Layer** | Data processing, storage, analytics (edge or cloud) |
| **Application Layer** | Smart home, healthcare, agriculture, industrial IoT |

**IoT Communication Protocols:**
- **Short-range:** Bluetooth, Zigbee (802.15.4), Z-Wave, NFC, RFID.
- **Medium-range:** WiFi, WiMAX.
- **Long-range (LPWAN):** LoRa, Sigfox, NB-IoT, LTE-M.
- **Application layer:** MQTT (publish-subscribe, port 1883), CoAP (REST for IoT), AMQP, HTTP.

**IoT Challenges:** Security (large attack surface), interoperability, scalability, privacy, power consumption, standardisation.

**Edge Computing:** Process data close to where it is generated (at the edge) rather than in a centralised cloud; reduces latency and bandwidth.

---

## Quick Recap Table

| Topic | Key Formulas / Concepts |
|---|---|
| Nyquist Theorem | `Max Bit Rate = 2 × B × log₂(L)` |
| Shannon's Theorem | `C = B × log₂(1 + SNR)` |
| Latency | Propagation + Transmission + Queuing + Processing delay |
| Transmission Delay | `L (bits) / B (bps)` |
| Propagation Delay | `Distance / Speed` |
| Hamming Distance | Detect s errors: `d_min ≥ s+1`; Correct t errors: `d_min ≥ 2t+1` |
| Stop-and-Wait Efficiency | `η = 1/(1 + 2a)` where `a = T_p/T_t` |
| Go-Back-N Window | `W_s = 2^n − 1` |
| Selective Repeat Window | `W_s = W_r = 2^(n-1)` |
| Sliding Window Efficiency | `W/(1+2a)` if `W < 1+2a`; else `η = 1` |
| CSMA/CD Min Frame | `Frame Size ≥ 2 × T_p × Bandwidth` |
| Slotted ALOHA Max | `1/e ≈ 36.8%` at G=1 |
| Pure ALOHA Max | `1/2e ≈ 18.4%` at G=0.5 |
| IPv4 Addresses | `2^32`; Subnet hosts = `2^h − 2` |
| IPv6 Addresses | `2^128` |
| Fragment Offset | `Byte Offset / 8` |
| RSA Encrypt/Decrypt | `C = M^e mod n` ; `M = C^d mod n` |
| Diffie-Hellman | Shared secret `K = g^(ab) mod p` |
| TCP Congestion | Slow Start → Congestion Avoidance → Fast Retransmit |
| RTT Estimate | `EstRTT = (1-α)×EstRTT + α×SampleRTT` (α = 0.125) |
| GPS Distance | `d = c × Δt` (trilateration from 4+ satellites) |
| Cloud SLA Availability | `(Uptime/Total Time) × 100%` |
| CDMA Recovery | `d_i = (1/N)(r · c_i)` |
| Full Mesh Links | `n(n-1)/2` |

---

