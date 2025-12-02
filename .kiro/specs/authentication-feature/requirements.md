# Authentication Feature Requirements

## Overview
Anonymous authentication system using cryptographic keys instead of personal information.

## Acceptance Criteria

### AC1: Anonymous Account Creation
- Users can create accounts without email or phone number
- Only display name required (not verified)
- 32-character cryptographic access key generated
- Access key is the ONLY way to authenticate

### AC2: Secure Key Generation
- Keys generated using cryptographically secure random
- Keys are unique and collision-resistant
- Keys never stored on server in plaintext

### AC3: Session Management
- Session tokens issued upon successful authentication
- Tokens expire after configurable period
- Secure token storage in browser

### AC4: Account Recovery
- Access key is the only recovery method
- No password reset (by design)
- Users must save their access key

### AC5: Connection System
- Users can generate temporary Account IDs
- Account IDs expire after 5 minutes
- Friends can connect using Account ID

## Non-Functional Requirements
- Key generation < 50ms
- Login validation < 100ms
- Zero personal data collection
