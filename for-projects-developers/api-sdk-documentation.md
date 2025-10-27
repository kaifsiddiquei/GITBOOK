# API & SDK Documentation

DEXGO's comprehensive API and SDK documentation provides developers with everything they need to build powerful Web3 applications with integrated AI capabilities. Our documentation covers all aspects of the platform, from basic authentication to advanced AI features, with detailed examples and best practices.

## API Overview

### REST API
- **Base URL**: `https://api.dexgo.com/v1`
- **Authentication**: Bearer token authentication
- **Rate Limiting**: 1000 requests per hour per API key
- **Response Format**: JSON responses with consistent error handling
- **Versioning**: API versioning with backward compatibility

### GraphQL API
- **Endpoint**: `https://api.dexgo.com/graphql`
- **Real-Time Subscriptions**: WebSocket support for real-time data
- **Schema Introspection**: Full schema introspection available
- **Query Optimization**: Automatic query optimization and caching

### WebSocket API
- **Endpoint**: `wss://api.dexgo.com/ws`
- **Real-Time Updates**: Real-time updates for all platform events
- **Connection Management**: Automatic reconnection and heartbeat
- **Message Format**: JSON message format with type safety

## Authentication

### API Key Authentication
```javascript
// JavaScript example
const apiKey = 'your-api-key';
const headers = {
  'Authorization': `Bearer ${apiKey}`,
  'Content-Type': 'application/json'
};

fetch('https://api.dexgo.com/v1/user/profile', {
  headers: headers
})
.then(response => response.json())
.then(data => console.log(data));
```

### OAuth 2.0 Authentication
```javascript
// OAuth 2.0 flow
const oauthConfig = {
  clientId: 'your-client-id',
  redirectUri: 'https://your-app.com/callback',
  scope: 'read write'
};

// Redirect to authorization URL
const authUrl = `https://api.dexgo.com/oauth/authorize?` +
  `client_id=${oauthConfig.clientId}&` +
  `redirect_uri=${oauthConfig.redirectUri}&` +
  `scope=${oauthConfig.scope}&` +
  `response_type=code`;

window.location.href = authUrl;
```

### Web3 Wallet Authentication
```javascript
// Web3 wallet authentication
import { DEXGOAuth } from '@dexgo/sdk';

const auth = new DEXGOAuth({
  network: 'ethereum',
  rpcUrl: 'https://mainnet.infura.io/v3/your-project-id'
});

// Connect wallet
const wallet = await auth.connectWallet();

// Sign message for authentication
const signature = await wallet.signMessage('Authenticate with DEXGO');

// Authenticate with signature
const token = await auth.authenticate(signature);
```

## Core APIs

### User Management API
```javascript
// Get user profile
const user = await fetch('/api/v1/user/profile', {
  headers: { 'Authorization': `Bearer ${token}` }
});

// Update user profile
const updatedUser = await fetch('/api/v1/user/profile', {
  method: 'PUT',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    displayName: 'New Display Name',
    bio: 'Updated bio'
  })
});

// Get user's communities
const communities = await fetch('/api/v1/user/communities', {
  headers: { 'Authorization': `Bearer ${token}` }
});
```

### Community API
```javascript
// Create community
const community = await fetch('/api/v1/communities', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    name: 'My Community',
    description: 'Community description',
    isPublic: true
  })
});

// Join community
await fetch('/api/v1/communities/123/join', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` }
});

// Get community members
const members = await fetch('/api/v1/communities/123/members', {
  headers: { 'Authorization': `Bearer ${token}` }
});
```

### Communication API
```javascript
// Send message
const message = await fetch('/api/v1/communities/123/messages', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    content: 'Hello, community!',
    type: 'text'
  })
});

// Get messages
const messages = await fetch('/api/v1/communities/123/messages', {
  headers: { 'Authorization': `Bearer ${token}` }
});

// Start voice call
const call = await fetch('/api/v1/calls', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    participants: ['user1', 'user2'],
    type: 'voice'
  })
});
```

## AI APIs

### Translation API
```javascript
// Real-time translation
const translation = await fetch('/api/v1/ai/translate', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    text: 'Hello, world!',
    sourceLanguage: 'en',
    targetLanguage: 'es'
  })
});

// Batch translation
const batchTranslation = await fetch('/api/v1/ai/translate/batch', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    texts: ['Hello', 'World', 'DEXGO'],
    sourceLanguage: 'en',
    targetLanguage: 'fr'
  })
});
```

### AI Assistant API
```javascript
// Chat with AI assistant
const response = await fetch('/api/v1/ai/assistant/chat', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    message: 'What is DeFi?',
    context: 'web3',
    userId: 'user123'
  })
});

// Get AI recommendations
const recommendations = await fetch('/api/v1/ai/assistant/recommendations', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    userId: 'user123',
    type: 'defi_strategies'
  })
});
```

### Analytics API
```javascript
// Get user analytics
const analytics = await fetch('/api/v1/ai/analytics/user', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    userId: 'user123',
    timeRange: '30d',
    metrics: ['engagement', 'participation', 'growth']
  })
});

// Get community analytics
const communityAnalytics = await fetch('/api/v1/ai/analytics/community', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    communityId: '123',
    timeRange: '7d',
    metrics: ['activity', 'growth', 'sentiment']
  })
});
```

## Web3 APIs

### Wallet API
```javascript
// Get wallet balance
const balance = await fetch('/api/v1/wallet/balance', {
  headers: { 'Authorization': `Bearer ${token}` }
});

// Send transaction
const transaction = await fetch('/api/v1/wallet/send', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    to: '0x742d35Cc6634C0532925a3b8D4C9db96C4b4d8b6',
    amount: '1.0',
    token: 'ETH'
  })
});

// Get transaction history
const history = await fetch('/api/v1/wallet/transactions', {
  headers: { 'Authorization': `Bearer ${token}` }
});
```

### DeFi API
```javascript
// Get DeFi protocols
const protocols = await fetch('/api/v1/defi/protocols', {
  headers: { 'Authorization': `Bearer ${token}` }
});

// Get yield farming opportunities
const opportunities = await fetch('/api/v1/defi/yield-farming', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    chain: 'ethereum',
    minAPY: 5.0,
    riskLevel: 'medium'
  })
});

// Execute DeFi transaction
const defiTransaction = await fetch('/api/v1/defi/execute', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    protocol: 'uniswap',
    action: 'swap',
    params: {
      tokenIn: 'ETH',
      tokenOut: 'USDC',
      amount: '1.0'
    }
  })
});
```

### NFT API
```javascript
// Get NFT collections
const collections = await fetch('/api/v1/nft/collections', {
  headers: { 'Authorization': `Bearer ${token}` }
});

// Get user's NFTs
const userNFTs = await fetch('/api/v1/nft/user', {
  headers: { 'Authorization': `Bearer ${token}` }
});

// Transfer NFT
const transfer = await fetch('/api/v1/nft/transfer', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    tokenId: '123',
    contractAddress: '0x...',
    to: '0x...'
  })
});
```

## SDKs

### JavaScript SDK
```bash
npm install @dexgo/sdk
```

```javascript
import { DEXGOClient } from '@dexgo/sdk';

const client = new DEXGOClient({
  apiKey: 'your-api-key',
  network: 'ethereum'
});

// Initialize client
await client.init();

// Get user profile
const user = await client.user.getProfile();

// Send message
await client.communication.sendMessage({
  communityId: '123',
  content: 'Hello, world!'
});

// Get AI translation
const translation = await client.ai.translate({
  text: 'Hello, world!',
  targetLanguage: 'es'
});
```

### Python SDK
```bash
pip install dexgo-sdk
```

```python
from dexgo import DEXGOClient

client = DEXGOClient(
    api_key='your-api-key',
    network='ethereum'
)

# Initialize client
client.init()

# Get user profile
user = client.user.get_profile()

# Send message
client.communication.send_message(
    community_id='123',
    content='Hello, world!'
)

# Get AI translation
translation = client.ai.translate(
    text='Hello, world!',
    target_language='es'
)
```

### React Components
```bash
npm install @dexgo/react-components
```

```jsx
import React from 'react';
import { DEXGOProvider, ChatComponent, AIAssistant } from '@dexgo/react-components';

function App() {
  return (
    <DEXGOProvider apiKey="your-api-key">
      <div>
        <ChatComponent 
          communityId="123"
          onMessage={(message) => console.log(message)}
        />
        <AIAssistant 
          onResponse={(response) => console.log(response)}
        />
      </div>
    </DEXGOProvider>
  );
}
```

## Error Handling

### Standard Error Format
```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "The request is invalid",
    "details": {
      "field": "email",
      "reason": "Invalid email format"
    },
    "timestamp": "2024-01-01T00:00:00Z",
    "requestId": "req_123456789"
  }
}
```

### Error Codes
- `INVALID_REQUEST`: Invalid request parameters
- `UNAUTHORIZED`: Authentication required
- `FORBIDDEN`: Insufficient permissions
- `NOT_FOUND`: Resource not found
- `RATE_LIMITED`: Rate limit exceeded
- `INTERNAL_ERROR`: Internal server error

### Error Handling Example
```javascript
try {
  const response = await fetch('/api/v1/user/profile', {
    headers: { 'Authorization': `Bearer ${token}` }
  });
  
  if (!response.ok) {
    const error = await response.json();
    throw new Error(error.error.message);
  }
  
  const data = await response.json();
  console.log(data);
} catch (error) {
  console.error('Error:', error.message);
}
```

## Rate Limiting

### Rate Limits
- **Free Tier**: 1000 requests per hour
- **Pro Tier**: 10000 requests per hour
- **Enterprise**: Custom rate limits

### Rate Limit Headers
```
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1640995200
```

### Rate Limit Handling
```javascript
const response = await fetch('/api/v1/user/profile', {
  headers: { 'Authorization': `Bearer ${token}` }
});

const rateLimitRemaining = response.headers.get('X-RateLimit-Remaining');
const rateLimitReset = response.headers.get('X-RateLimit-Reset');

if (rateLimitRemaining === '0') {
  const resetTime = new Date(rateLimitReset * 1000);
  console.log(`Rate limit exceeded. Reset at: ${resetTime}`);
}
```

## Webhooks

### Webhook Setup
```javascript
// Create webhook
const webhook = await fetch('/api/v1/webhooks', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${token}` },
  body: JSON.stringify({
    url: 'https://your-app.com/webhook',
    events: ['message.created', 'user.joined'],
    secret: 'your-webhook-secret'
  })
});
```

### Webhook Payload
```json
{
  "event": "message.created",
  "data": {
    "messageId": "msg_123",
    "communityId": "123",
    "userId": "user_456",
    "content": "Hello, world!",
    "timestamp": "2024-01-01T00:00:00Z"
  },
  "timestamp": "2024-01-01T00:00:00Z"
}
```

### Webhook Verification
```javascript
const crypto = require('crypto');

function verifyWebhook(payload, signature, secret) {
  const expectedSignature = crypto
    .createHmac('sha256', secret)
    .update(payload)
    .digest('hex');
  
  return signature === `sha256=${expectedSignature}`;
}
```

## Testing

### Test Environment
- **Base URL**: `https://api-test.dexgo.com/v1`
- **Test API Key**: Use test API keys for development
- **Mock Data**: Mock data for testing scenarios

### Testing Examples
```javascript
// Test user creation
const testUser = await fetch('/api/v1/test/users', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${testToken}` },
  body: JSON.stringify({
    email: 'test@example.com',
    displayName: 'Test User'
  })
});

// Test message sending
const testMessage = await fetch('/api/v1/test/messages', {
  method: 'POST',
  headers: { 'Authorization': `Bearer ${testToken}` },
  body: JSON.stringify({
    communityId: 'test_123',
    content: 'Test message'
  })
});
```

## Best Practices

### API Usage
- **Use HTTPS**: Always use HTTPS for API requests
- **Handle Errors**: Implement proper error handling
- **Rate Limiting**: Respect rate limits and implement backoff
- **Caching**: Implement appropriate caching strategies

### Security
- **API Key Security**: Keep API keys secure and rotate regularly
- **Input Validation**: Validate all input data
- **HTTPS Only**: Use HTTPS for all communications
- **Authentication**: Implement proper authentication

### Performance
- **Pagination**: Use pagination for large datasets
- **Filtering**: Use filtering to reduce data transfer
- **Caching**: Implement client-side caching
- **Compression**: Use compression for large responses

---

*Ready to explore setting up a project space? Continue to the next section to learn about DEXGO's project management tools.*
