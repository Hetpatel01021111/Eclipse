# Authentication Feature Design

## Architecture

### Components
1. **Key Generator** - Creates 32-character access keys
2. **Auth API** - Handles create/login requests
3. **Session Manager** - Issues and validates tokens
4. **Account ID Generator** - Creates temporary connection codes

### Data Flow

```
Account Creation:
User → Enter Name → Generate Access Key → Store Hash → Issue Token → Done

Login:
User → Enter Access Key → Validate Hash → Issue Token → Done

Connection:
User A → Generate Account ID → Share Code → User B Enters → Connected
```

## Security Properties

### Property 1: Anonymous Identity
- No PII required or stored
- Identity = cryptographic key hash
- Display name is user-chosen, not verified

### Property 2: Key Security
- Access keys generated with crypto.randomBytes
- Only SHA-256 hash stored on server
- Original key never transmitted after creation

### Property 3: Session Security
- JWT tokens with expiration
- Tokens stored in localStorage (encrypted)
- Automatic token refresh

## API Design

### POST /api/auth/create
```json
Request: { "displayName": "John" }
Response: { "accessKey": "abc123...", "sessionToken": "jwt...", "user": {...} }
```

### POST /api/auth/login
```json
Request: { "accessKey": "abc123..." }
Response: { "sessionToken": "jwt...", "user": {...} }
```

### POST /api/auth/generate-account-id
```json
Response: { "accountId": "ABC123", "expiresAt": "..." }
```
