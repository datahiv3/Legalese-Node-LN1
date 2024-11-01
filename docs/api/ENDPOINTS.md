# LN1 API Endpoints

## Overview

This document details the API endpoints available in the LN1 node system. These endpoints provide interfaces for document management, validation, and node operations.

## Base URL

```
https://api.ln1.datahive.network/v1
```

## Authentication

```typescript
interface AuthHeader {
    Authorization: `Bearer ${string}`;
    'X-API-Key': string;
}
```

## Endpoints

### Document Management

#### Create Document
```http
POST /documents
Content-Type: application/json
Authorization: Bearer <token>

{
    "content": "string",
    "metadata": {
        "title": "string",
        "type": "string",
        "jurisdiction": "string"
    }
}
```

#### Retrieve Document
```http
GET /documents/{documentId}
Authorization: Bearer <token>
```

#### Update Document
```http
PUT /documents/{documentId}
Content-Type: application/json
Authorization: Bearer <token>

{
    "content": "string",
    "metadata": {
        "version": "string",
        "lastModified": "timestamp"
    }
}
```

### Validation Operations

#### Submit for Validation
```http
POST /validation/submit
Content-Type: application/json
Authorization: Bearer <token>

{
    "documentId": "string",
    "validationType": "LEGAL|TECHNICAL|COMPLIANCE"
}
```

#### Check Validation Status
```http
GET /validation/status/{validationId}
Authorization: Bearer <token>
```

### Node Operations

#### Node Status
```http
GET /node/status
Authorization: Bearer <token>
```

#### Node Configuration
```http
PUT /node/config
Content-Type: application/json
Authorization: Bearer <token>

{
    "networkMode": "MAINNET|TESTNET",
    "validationThreshold": "number",
    "storageConfig": {
        "replicationFactor": "number",
        "storageType": "DISTRIBUTED|LOCAL"
    }
}
```

## Response Formats

### Success Response
```json
{
    "status": "success",
    "data": {
        "id": "string",
        "timestamp": "ISO8601",
        "result": {}
    }
}
```

### Error Response
```json
{
    "status": "error",
    "error": {
        "code": "string",
        "message": "string",
        "details": {}
    }
}
```

## Status Codes

| Code | Description |
|------|-------------|
| 200  | Success |
| 201  | Created |
| 400  | Bad Request |
| 401  | Unauthorized |
| 403  | Forbidden |
| 404  | Not Found |
| 500  | Internal Server Error |

## Rate Limiting

```http
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1640995200
```

## Pagination

### Request Parameters
```http
GET /documents?page=1&limit=10
```

### Response Format
```json
{
    "data": [],
    "pagination": {
        "currentPage": 1,
        "totalPages": 10,
        "totalItems": 100,
        "itemsPerPage": 10
    }
}
```

## Filtering

### Query Parameters
```http
GET /documents?type=legal&jurisdiction=US&dateFrom=2024-01-01
```

## Versioning

All API endpoints are versioned using URL path versioning:
```
/v1/documents
/v2/documents
```

## WebSocket Endpoints

### Real-time Updates
```javascript
const ws = new WebSocket('wss://api.ln1.datahive.network/v1/ws');

ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('Received:', data);
};
```

## SDK Examples

### Node.js
```javascript
const LN1Client = require('@ln1/client');

const client = new LN1Client({
    apiKey: 'your-api-key',
    environment: 'production'
});

async function createDocument(content) {
    try {
        const response = await client.documents.create({
            content,
            metadata: {
                type: 'legal',
                jurisdiction: 'US'
            }
        });
        return response.data;
    } catch (error) {
        console.error('Error:', error);
    }
}
```

### Python
```python
from ln1_client import LN1Client

client = LN1Client(
    api_key='your-api-key',
    environment='production'
)

async def create_document(content):
    try:
        response = await client.documents.create(
            content=content,
            metadata={
                'type': 'legal',
                'jurisdiction': 'US'
            }
        )
        return response.data
    except Exception as e:
        print(f'Error: {e}')
```

## Security Considerations

- All endpoints require authentication
- TLS 1.3 required for all connections
- API keys must be rotated every 90 days
- Rate limiting applies to all endpoints
- IP whitelisting recommended