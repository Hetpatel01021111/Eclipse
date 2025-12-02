# Privacy Network Feature Design

## Architecture

### Onion Routing
```
User A → [Encrypt for Relay3] → [Encrypt for Relay2] → [Encrypt for Relay1]
       → Relay1 (decrypt layer) → Relay2 (decrypt layer) → Relay3 (decrypt layer)
       → Recipient
```

### Traffic Padding
- Random interval: 3-10 seconds
- Message size: Normalized to 512 bytes
- Dummy content: Encrypted random data

### P2P Architecture
```
1. Try WebRTC direct connection
2. Use STUN for NAT traversal
3. Fallback to TURN relay
4. Final fallback to server relay
```

## Security Properties

### Property 1: IP Anonymity
- Onion routing hides source IP
- Each relay sees only adjacent nodes
- Recipient cannot trace sender

### Property 2: Traffic Analysis Resistance
- Constant traffic flow with padding
- Uniform message sizes
- Random timing intervals

### Property 3: P2P Privacy
- Direct connections bypass server
- DTLS encryption
- No server logging of P2P traffic

## Implementation

### Files
- `web-app/src/privacyNetwork.js` - Main privacy module
- `web-app/src/socket.js` - WebSocket with privacy
- `backend/modules/privacy/` - Server-side relay
