# API Contracts - ReFi.Trading REST API
**Base URL:** `https://api.refi.trading` (production)  
**Base URL:** `https://api-staging.refi.trading` (staging)  
**Version:** v1.0  
**Authentication:** Bearer token (JWT from SIWE)

---

## Authentication

### POST /auth/siwe/nonce
Get a nonce for Sign-In with Ethereum (SIWE) flow.

**Request:**
```json
{
  "walletAddress": "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb"
}
```

**Response (200 OK):**
```json
{
  "nonce": "abcd1234-random-nonce",
  "expiresAt": "2026-01-15T10:30:00Z"
}
```

---

### POST /auth/siwe/verify
Verify signed SIWE message and create session.

**Request:**
```json
{
  "message": "refi.trading wants you to sign in...",
  "signature": "0x123abc...def",
  "walletAddress": "0x742d35Cc..."
}
```

**Response (200 OK):**
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIs...",
  "refreshToken": "dGhpc19pc19hX3JlZnJlc2g...",
  "user": {
    "id": "uuid-here",
    "walletAddress": "0x742d35Cc...",
    "email": null,
    "createdAt": "2026-01-10T12:00:00Z"
  }
}
```

---

## Broker Integration

### GET /brokers
List supported brokers.

**Response (200 OK):**
```json
{
  "brokers": [
    {
      "id": "ibkr",
      "name": "Interactive Brokers",
      "logo": "https://cdn.refi.trading/logos/ibkr.png",
      "assetClasses": ["equities", "options", "futures", "forex"],
      "supported": true
    },
    {
      "id": "alpaca",
      "name": "Alpaca",
      "logo": "https://cdn.refi.trading/logos/alpaca.png",
      "assetClasses": ["equities", "options", "etfs"],
      "supported": true
    },
    {
      "id": "kraken",
      "name": "Kraken",
      "logo": "https://cdn.refi.trading/logos/kraken.png",
      "assetClasses": ["crypto"],
      "supported": true
    }
  ]
}
```

---

### POST /brokers/connect
Initiate broker OAuth connection.

**Request:**
```json
{
  "brokerId": "ibkr",
  "redirectUrl": "https://app.refi.trading/dashboard"
}
```

**Response (200 OK):**
```json
{
  "oauthUrl": "https://snaptrade.com/oauth/redirect?user_id=...",
  "connectionId": "temp-connection-uuid",
  "expiresAt": "2026-01-15T10:45:00Z"
}
```

---

### GET /brokers/connections
List user's connected brokers.

**Headers:** `Authorization: Bearer {token}`

**Response (200 OK):**
```json
{
  "connections": [
    {
      "id": "connection-uuid",
      "broker": "ibkr",
      "status": "connected",
      "accountNumber": "U1234567",
      "totalValue": 85000.00,
      "cashBalance": 12000.00,
      "connectedAt": "2026-01-10T14:30:00Z",
      "lastSyncedAt": "2026-01-15T09:00:00Z"
    }
  ]
}
```

---

## Portfolio

### GET /portfolio
Get user's aggregated portfolio across all brokers.

**Headers:** `Authorization: Bearer {token}`

**Query Params:**
- `brokerId` (optional): Filter by specific broker

**Response (200 OK):**
```json
{
  "totalValue": 85000.00,
  "cashBalance": 12000.00,
  "positions": [
    {
      "symbol": "AAPL",
      "name": "Apple Inc.",
      "quantity": 50,
      "costBasis": 175.00,
      "currentPrice": 180.00,
      "marketValue": 9000.00,
      "unrealizedPnL": 250.00,
      "unrealizedPnLPct": 2.86,
      "broker": "ibkr"
    },
    {
      "symbol": "BTC",
      "name": "Bitcoin",
      "quantity": 0.5,
      "costBasis": 40000.00,
      "currentPrice": 42000.00,
      "marketValue": 21000.00,
      "unrealizedPnL": 1000.00,
      "unrealizedPnLPct": 5.00,
      "broker": "kraken"
    }
  ],
  "lastSyncedAt": "2026-01-15T09:00:00Z"
}
```

---

### POST /portfolio/sync
Force portfolio sync from broker (rate-limited to 4x/day).

**Headers:** `Authorization: Bearer {token}`

**Request:**
```json
{
  "brokerId": "ibkr"
}
```

**Response (202 Accepted):**
```json
{
  "message": "Sync initiated",
  "estimatedCompletionAt": "2026-01-15T10:01:00Z",
  "syncId": "sync-job-uuid"
}
```

---

## Trading

### POST /trades/propose
AI proposes trade based on selected strategy.

**Headers:** `Authorization: Bearer {token}`

**Request:**
```json
{
  "brokerId": "ibkr",
  "symbol": "AAPL",
  "strategyId": "td3-momentum"
}
```

**Response (200 OK):**
```json
{
  "tradeId": "trade-uuid",
  "proposal": {
    "symbol": "AAPL",
    "side": "buy",
    "quantity": 5,
    "limitPrice": 180.00,
    "estimatedCost": 900.00,
    "aiConfidence": 0.85,
    "marketRegime": "trending",
    "reasoning": "Bullish momentum signal: 50-day MA crossover above 200-day MA. VIX < 15 indicates low market volatility."
  },
  "riskCheck": {
    "status": "pending",
    "proofGenerationStartedAt": "2026-01-15T10:05:00Z"
  }
}
```

---

### GET /trades/:id/proof
Get zk-VaR proof for proposed trade.

**Headers:** `Authorization: Bearer {token}`

**Response (200 OK):**
```json
{
  "tradeId": "trade-uuid",
  "proof": {
    "status": "verified",
    "proofHash": "0xabcd1234...",
    "zkSyncTxHash": "0x5678efgh...",
    "generatedAt": "2026-01-15T10:05:02.345Z",
    "generationTimeMs": 2.8,
    "riskMetrics": {
      "portfolioVaR": 0.032,
      "userVaRLimit": 0.050,
      "passed": true
    },
    "explorerUrl": "https://explorer.zksync.io/tx/0x5678efgh..."
  }
}
```

---

### POST /trades/:id/confirm
User confirms trade (human-in-the-loop).

**Headers:** `Authorization: Bearer {token}`

**Request:**
```json
{
  "tradeId": "trade-uuid",
  "confirmationType": "manual"
}
```

**Response (200 OK):**
```json
{
  "tradeId": "trade-uuid",
  "status": "submitted",
  "submittedAt": "2026-01-15T10:06:00Z",
  "brokerOrderId": "IBKR-ORDER-123456",
  "estimatedFillTime": "2026-01-15T10:06:05Z"
}
```

---

### GET /trades
List user's trade history.

**Headers:** `Authorization: Bearer {token}`

**Query Params:**
- `status` (optional): Filter by status (proposed, filled, rejected)
- `startDate` (optional): ISO date
- `endDate` (optional): ISO date
- `limit` (default: 50, max: 200)
- `offset` (default: 0)

**Response (200 OK):**
```json
{
  "trades": [
    {
      "id": "trade-uuid",
      "symbol": "AAPL",
      "side": "buy",
      "quantity": 5,
      "limitPrice": 180.00,
      "fillPrice": 180.05,
      "status": "filled",
      "aiConfidence": 0.85,
      "marketRegime": "trending",
      "proofHash": "0xabcd...",
      "createdAt": "2026-01-15T10:05:00Z",
      "filledAt": "2026-01-15T10:06:02Z"
    }
  ],
  "pagination": {
    "total": 127,
    "limit": 50,
    "offset": 0,
    "hasMore": true
  }
}
```

---

## Risk & Strategy

### GET /risk-profiles
List available risk profiles.

**Response (200 OK):**
```json
{
  "profiles": [
    {
      "id": "conservative",
      "name": "Conservative",
      "description": "Low risk, suitable for cautious investors",
      "maxVaRPct": 0.03,
      "maxPositionSizePct": 0.05,
      "maxDailyTrades": 5,
      "leverageAllowed": false
    },
    {
      "id": "moderate",
      "name": "Moderate",
      "description": "Balanced risk-reward",
      "maxVaRPct": 0.05,
      "maxPositionSizePct": 0.10,
      "maxDailyTrades": 10,
      "leverageAllowed": false
    },
    {
      "id": "aggressive",
      "name": "Aggressive",
      "description": "Higher risk for experienced traders",
      "maxVaRPct": 0.08,
      "maxPositionSizePct": 0.15,
      "maxDailyTrades": 20,
      "leverageAllowed": true
    }
  ]
}
```

---

### POST /risk-profiles/select
Set user's risk profile.

**Headers:** `Authorization: Bearer {token}`

**Request:**
```json
{
  "profileId": "moderate"
}
```

**Response (200 OK):**
```json
{
  "message": "Risk profile updated",
  "profile": {
    "id": "moderate",
    "name": "Moderate",
    "maxVaRPct": 0.05
  },
  "effectiveAt": "2026-01-15T10:10:00Z"
}
```

---

## Error Responses

### 400 Bad Request
```json
{
  "error": "INVALID_REQUEST",
  "message": "Invalid brokerId: 'invalid-broker'",
  "details": {
    "field": "brokerId",
    "allowedValues": ["ibkr", "alpaca", "kraken", "coinbase"]
  }
}
```

### 401 Unauthorized
```json
{
  "error": "UNAUTHORIZED",
  "message": "Invalid or expired access token"
}
```

### 429 Rate Limit Exceeded
```json
{
  "error": "RATE_LIMIT_EXCEEDED",
  "message": "Portfolio sync limit reached. Try again in 6 hours.",
  "retryAfter": "2026-01-15T16:00:00Z"
}
```

### 500 Internal Server Error
```json
{
  "error": "INTERNAL_ERROR",
  "message": "An unexpected error occurred. Please contact support.",
  "incidentId": "inc-uuid-here"
}
```

---

## Rate Limits
- **Authentication:** 10 requests/minute per IP
- **Portfolio Sync:** 4 requests/day per user
- **Trading:** 100 requests/hour per user
- **General API:** 1000 requests/hour per user

---

**Versioning:** All endpoints prefixed with `/v1/` for future API versions.
**Documentation:** Full OpenAPI 3.0 spec available at `https://api.refi.trading/docs`
