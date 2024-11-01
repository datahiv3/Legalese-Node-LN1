# LN1 REST API Documentation

## API Overview

The LN1 REST API provides programmatic access to the LegalNode network for document management, validation, and node operations.

## Base URL

```
https://api.ln1.datahive.network/v1
```

## Authentication

All API requests require authentication using either JWT tokens or API keys.

```http
Authorization: Bearer <jwt_token>
X-API-Key: <api_key>
```

## API Endpoints

### Documents API

#### Create Document
```http
POST /documents
Content-Type: application/json

{
    "title": "string",
    "content": "string",
    "metadata": {
        "jurisdiction": "string",
        "docType": "string",
        "tags": ["string"]
    }
}
```

**Response**
```json
{
    "documentId": "uuid",
    "status": "PENDING|PROCESSING|COMPLETED",
    "timestamp": "ISO8601",
    "location": "/documents/{documentId}"
}
```

#### Retrieve Document
```http
GET /documents/{documentId}
```

#### Update Document
```http
PUT /documents/{documentId}
Content-Type: application/json

{
    "content": "string",
    "metadata": {
        "version": "string"
    }
}
```

### Validation API

#### Submit Validation Request
```http
POST /validation
Content-Type: application/json

{
    "documentId": "uuid",
    "validationType": "LEGAL|TECHNICAL|COMPLIANCE",
    "priority": "HIGH|MEDIUM|LOW"
}
```

#### Check Validation Status
```http
GET /validation/{validationId}
```

### Node Operations API

#### Node Status
```http
GET /node/status
```

**Response**
```json
{
    "nodeId": "string",
    "status": "ACTIVE|INACTIVE",
    "metrics": {
        "uptime": "number",
        "processedDocuments": "number",
        "validationScore": "number"
    }
}
```

#### Update Node Configuration
```http
PUT /node/config
Content-Type: application/json

{
    "networkMode": "MAINNET|TESTNET",
    "validationThreshold": "number",
    "storageConfig": {
        "replicationFactor": "number"
    }
}
```

## Response Codes

| Status Code | Description |
|------------|-------------|
| 200 | Success |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 429 | Too Many Requests |
| 500 | Internal Server Error |

## Error Handling

### Error Response Format
```json
{
    "error": {
        "code": "ERROR_CODE",
        "message": "Human readable message",
        "details": {
            "field": "Additional information"
        }
    }
}
```

## Rate Limiting

```http
X-RateLimit-Limit: 1000
X-RateLimit-Remaining: 999
X-RateLimit-Reset: 1640995200
```

## Data Models

### Document Model
```typescript
interface Document {
    id: string;
    title: string;
    content: string;
    metadata: {
        version: string;
        jurisdiction: string;
        docType: string;
        created: string;
        modified: string;
    };
    status: DocumentStatus;
    validations: Validation[];
}
```

### Validation Model
```typescript
interface Validation {
    id: string;
    documentId: string;
    type: ValidationType;
    status: ValidationStatus;
    result: ValidationResult;
    timestamp: string;
}
```

## WebSocket API

### Connection
```javascript
const ws = new WebSocket('wss://api.ln1.datahive.network/v1/ws');
```

### Subscribe to Updates
```json
{
    "action": "subscribe",
    "channel": "documents",
    "filter": {
        "documentId": "uuid"
    }
}
```

## Code Examples

### Node.js
```javascript
const axios = require('axios');

const api = axios.create({
    baseURL: 'https://api.ln1.datahive.network/v1',
    headers: {
        'Authorization': `Bearer ${token}`,
        'Content-Type': 'application/json'
    }
});

async function createDocument(document) {
    try {
        const response = await api.post('/documents', document);
        return response.data;
    } catch (error) {
        console.error('API Error:', error.response.data);
        throw error;
    }
}
```

### Python
```python
import requests

class LN1Client:
    def __init__(self, token):
        self.base_url = 'https://api.ln1.datahive.network/v1'
        self.headers = {
            'Authorization': f'Bearer {token}',
            'Content-Type': 'application/json'
        }
    
    def create_document(self, document):
        response = requests.post(
            f'{self.base_url}/documents',
            json=document,
            headers=self.headers
        )
        response.raise_for_status()
        return response.json()
```

## Security

- All endpoints require HTTPS
- JWT tokens expire after 1 hour
- API keys must be rotated every 90 days
- Rate limiting applies to all endpoints
- IP whitelisting available for production use

## Versioning

The API uses URL versioning:
- Current version: `v1`
- Beta features: `v1-beta`
- Legacy support: Minimum 6 months notice before deprecation