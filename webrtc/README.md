# STUN Server and ICE Candidate Generation in WebRTC

The **STUN server** plays a critical role in the **Interactive Connectivity Establishment (ICE)** process, which is used in WebRTC to establish peer-to-peer (P2P) connections, even when peers are behind NAT (Network Address Translation) or firewalls.

## Role of the STUN Server in ICE Candidate Generation

When a browser generates ICE candidates for WebRTC, it uses a STUN server to discover its public-facing IP address and port (external address). This is important for enabling communication between peers when at least one is behind NAT.

---

## How the STUN Server Works in ICE Candidate Generation

### 1. Local Candidate Discovery
- The browser first determines its **local IP address and port** (within its local network).
- This information is useful for peers on the same local network.

### 2. STUN Request
- The browser sends a **request** to the STUN server over **UDP** from its local IP and port.
- The STUN server responds with the **public IP address and port** that the request originated from.

### 3. Public Candidate Creation
- Using the STUN server's response, the browser creates a **"public" ICE candidate**.
- This candidate can be used to communicate with peers outside the local network.

### 4. Candidate Sharing via Signaling
- The browser shares all gathered **ICE candidates** (local and public) with the remote peer via the **signaling server**.

### 5. Connectivity Check
- During connection negotiation, **ICE connectivity checks** ensure the best candidate pair (e.g., direct P2P or relay) is selected for communication.

---

## Example Workflow

1. **Scenario**: Peer A's browser is behind a NAT with a private IP, e.g., `192.168.1.2`.
2. **STUN Usage**:
   - Peer A uses a STUN server to determine its **public IP**, e.g., `203.0.113.4:54321`.
3. **ICE Candidate Creation**:
   - Peer A creates the following **ICE candidate**:
   ```plaintext
   candidate:842163049 1 udp 2122260223 203.0.113.4 54321 typ srflx raddr 192.168.1.2 rport 12345

