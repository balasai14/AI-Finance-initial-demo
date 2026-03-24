# Finova AI - API Documentation

## Base URL
```
http://localhost:5000/api
```

## Authentication

All protected endpoints require JWT authentication via HTTP-only cookies or Bearer token.

### POST /auth/signup
Create a new user account.

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword123"
}
```

**Response:**
```json
{
  "status": "success",
  "token": "jwt_token_here",
  "data": {
    "user": {
      "_id": "user_id",
      "name": "John Doe",
      "email": "john@example.com",
      "createdAt": "2026-03-23T10:00:00.000Z"
    }
  }
}
```

### POST /auth/login
Login to existing account.

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "securepassword123"
}
```

**Response:** Same as signup

### POST /auth/demo
Login with pre-configured demo account.

**Request Body:** None

**Response:** Same as signup with demo user data

### GET /auth/me
Get current authenticated user.

**Headers:** `Authorization: Bearer <token>` or Cookie

**Response:**
```json
{
  "status": "success",
  "data": {
    "user": {
      "_id": "user_id",
      "name": "John Doe",
      "email": "john@example.com"
    }
  }
}
```

### POST /auth/logout
Logout current user.

**Response:**
```json
{
  "status": "success"
}
```

---

## Financial Profile Management

### POST /finance/save
Save or update user's financial profile.

**Headers:** Requires authentication

**Request Body:**
```json
{
  "income": 120000,
  "expenses": 55000,
  "investments": {
    "stocks": 350000,
    "mutual_funds": 280000,
    "bonds": 100000,
    "gold": 180000,
    "real_estate": 2500000,
    "epf": 450000,
    "ppf": 200000,
    "nps": 150000,
    "fd": 300000,
    "crypto": 50000
  },
  "loans": {
    "home_loan": 1800000,
    "car_loan": 250000,
    "personal_loan": 0,
    "education_loan": 0,
    "credit_card_debt": 35000
  },
  "insurance": {
    "life_insurance": 5000000,
    "health_insurance": 1000000,
    "term_insurance": 10000000
  },
  "credit_score": 780,
  "age": 32,
  "dependents": 2,
  "risk_profile": "moderate"
}
```

**Response:**
```json
{
  "status": "success",
  "data": {
    "profile": { /* saved profile */ }
  }
}
```

### GET /finance/get
Retrieve user's financial profile.

**Headers:** Requires authentication

**Response:**
```json
{
  "status": "success",
  "data": {
    "profile": {
      "income": 120000,
      "expenses": 55000,
      "investments": { /* ... */ },
      "loans": { /* ... */ },
      "insurance": { /* ... */ },
      "credit_score": 780,
      "age": 32,
      "dependents": 2,
      "risk_profile": "moderate"
    }
  }
}
```

---

## AI Intelligence

### POST /ai/analyze
Get AI-powered financial advice based on user query.

**Headers:** Requires authentication

**Request Body:**
```json
{
  "query": "Should I invest in stocks or pay off my home loan first?",
  "privacyMode": false
}
```

**Response:**
```json
{
  "status": "success",
  "data": {
    "recommendation": "Based on your 54% savings rate and moderate risk profile...",
    "reasoning": [
      "Your debt-to-asset ratio is 45%, which is manageable",
      "Home loan interest (8-10%) is lower than expected stock returns (12-15%)",
      "Tax benefits on home loan under Section 80C and 24(b)"
    ],
    "comparison": {
      "optionA": 2475000,
      "optionB": 3250000,
      "labelA": "Pay Loan First",
      "labelB": "Invest in Equity"
    },
    "confidence": 85,
    "metrics": {
      "savingsRate": "54.17",
      "debtRatio": "45.72",
      "netWorth": 2475000
    }
  }
}
```

### POST /simulate
Run financial scenario simulation.

**Headers:** Requires authentication

**Request Body:**
```json
{
  "monthlyInvestment": 25000,
  "years": 20,
  "returnRate": 12,
  "initialEquity": 0,
  "repayDebtFirst": false,
  "debtAmount": 1500000,
  "debtRate": 10.5
}
```

**Response:**
```json
{
  "status": "success",
  "data": {
    "timeSeries": [
      { "year": 0, "value": 0, "debt": 0 },
      { "year": 1, "value": 320000, "debt": 0 },
      { "year": 20, "value": 24750000, "debt": 0 }
    ],
    "finalValue": 24750000,
    "growth": 18750000
  }
}
```

### POST /compute
Calculate financial metrics without AI.

**Request Body:**
```json
{
  "income": 120000,
  "expenses": 55000,
  "stocks": 350000,
  "mutual_funds": 280000,
  "home_loan": 1800000
}
```

**Response:**
```json
{
  "status": "success",
  "data": {
    "savingsRate": 54.17,
    "debtRatio": 285.71,
    "netWorth": -1170000
  }
}
```

---

## MCP Data Exchange

### GET /mcp/export
Export financial data in MCP-compatible format.

**Headers:** Requires authentication

**Response:**
```json
{
  "status": "success",
  "format": "MCP-compatible",
  "data": {
    "version": "1.0",
    "timestamp": "2026-03-23T10:00:00.000Z",
    "user": { /* user info */ },
    "financial_profile": {
      "income": { /* structured income data */ },
      "expenses": { /* structured expense data */ },
      "assets": { /* categorized assets */ },
      "liabilities": { /* categorized liabilities */ },
      "insurance": { /* insurance coverage */ },
      "metrics": { /* calculated metrics */ },
      "demographics": { /* user demographics */ }
    }
  }
}
```

### POST /mcp/import
Import financial data from MCP-compatible format.

**Headers:** Requires authentication

**Request Body:** Same structure as export response

**Response:**
```json
{
  "status": "success",
  "message": "MCP data imported successfully",
  "data": {
    "profile": { /* imported profile */ }
  }
}
```

---

## Error Responses

All endpoints return errors in this format:

```json
{
  "status": "fail" | "error",
  "message": "Error description"
}
```

**Common Status Codes:**
- `200` - Success
- `201` - Created
- `400` - Bad Request (validation error)
- `401` - Unauthorized (authentication required)
- `404` - Not Found
- `500` - Internal Server Error

---

## Rate Limiting

Currently no rate limiting implemented. For production, consider:
- 100 requests per 15 minutes per IP
- 1000 AI queries per day per user
- Exponential backoff for failed requests

---

## Data Privacy

### Privacy Mode
When `privacyMode: true` is sent to `/ai/analyze`:
- Absolute financial values are masked
- Only ratios and percentages are shared with AI
- Recommendations based on derived metrics

### Data Storage
- All financial data encrypted at rest (MongoDB)
- Passwords hashed with bcrypt
- JWT tokens stored in HTTP-only cookies
- No third-party data sharing

---

## Testing

### Using cURL

**Signup:**
```bash
curl -X POST http://localhost:5000/api/auth/signup \
  -H "Content-Type: application/json" \
  -d '{"name":"Test User","email":"test@example.com","password":"test123"}'
```

**Login:**
```bash
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -c cookies.txt \
  -d '{"email":"test@example.com","password":"test123"}'
```

**Get Profile:**
```bash
curl -X GET http://localhost:5000/api/finance/get \
  -b cookies.txt
```

### Using Postman

1. Import the API endpoints
2. Set base URL to `http://localhost:5000/api`
3. Enable "Send cookies" in settings
4. Login first to get authentication cookie
5. All subsequent requests will include the cookie automatically

---

## Performance Benchmarks

- **AI Analysis**: ~2-3 seconds (depends on Gemini API)
- **Simulation**: ~100-300ms (local computation)
- **Profile CRUD**: ~50-100ms (MongoDB query)
- **Authentication**: ~200-500ms (bcrypt hashing)

---

## Future API Enhancements

- [ ] Pagination for transaction history
- [ ] Bulk data import/export
- [ ] Webhook notifications
- [ ] GraphQL endpoint
- [ ] Real-time WebSocket updates
- [ ] API versioning (v2, v3)
- [ ] OpenAPI/Swagger documentation
