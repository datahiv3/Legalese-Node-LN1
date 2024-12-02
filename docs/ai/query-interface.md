# Query Interface Documentation

The Query Interface module provides a secure and efficient way for users and applications to interact with the DataHive legal data ecosystem. This interface allows for querying legal documents, metadata, and insights generated from the processing pipeline. The Query Interface is designed to support both RESTful API calls and WebSocket connections for real-time data retrieval.

## Core Features

- **Document Retrieval**: Access legal documents stored within the DataHive network based on various search criteria.

- **Metadata Access**: Fetch associated metadata for documents, including authorship, jurisdiction, document type, and timestamps.

- **Search Functionality**: Perform complex queries to find relevant legal documents using keywords, phrases, or specific fields.

- **Real-Time Updates**: Receive notifications and updates on document status changes or new submissions through WebSocket connections.

## API Endpoints

### Base URL
```plaintext
https://api.datahive.com/v1/query
```

### Authentication
All API requests require authentication using an API key:
```http
Authorization: Bearer YOUR_API_KEY
```

### Endpoints

#### 1. Retrieve Document
```http
GET /documents/{documentId}
Authorization: Bearer <token>
```
**Response Format**
```json
{
    "status": "success",
    "data": {
        "id": "string",
        "title": "string",
        "content": "string",
        "metadata": {
            "jurisdiction": "string",
            "type": "string",
            "created_at": "ISO8601"
        }
    }
}
```

#### 2. Search Documents
```http
GET /documents/search?query={searchTerm}&limit={number}
Authorization: Bearer <token>
```
**Query Parameters**
- `query`: The search term or phrase.
- `limit`: The maximum number of results to return.

**Response Format**
```json
{
    "status": "success",
    "data": [
        {
            "id": "string",
            "title": "string",
            "snippet": "string"
        }
    ],
    "pagination": {
        "currentPage": 1,
        "totalPages": 10,
        "totalItems": 100,
        "itemsPerPage": 10
    }
}
```

#### 3. Fetch Metadata
```http
GET /documents/{documentId}/metadata
Authorization: Bearer <token>
```
**Response Format**
```json
{
    "status": "success",
    "data": {
        "id": "string",
        "metadata": {
            "jurisdiction": "string",
            "type": "string",
            "author": "string",
            "created_at": "ISO8601"
        }
    }
}
```

## WebSocket Connection

### Real-Time Updates
To receive real-time updates about document status or new submissions:
```javascript
const ws = new WebSocket('wss://api.datahive.com/v1/query/ws');

ws.onopen = () => {
    console.log('WebSocket connection established');
};

ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('Received update:', data);
};
```

### Subscribe to Document Updates
To subscribe to updates for specific documents:
```json
{
    "action": "subscribe",
    "documentId": "{documentId}"
}
```

## Rate Limiting

- Each API key is limited to 1000 requests per hour.
- Rate limit headers are included in responses to help monitor usage.

## Error Handling

Common error codes include:
- **400**: Bad Request - Invalid parameters.
- **401**: Unauthorized - Invalid API key.
- **403**: Forbidden - Insufficient permissions.
- **404**: Not Found - Document does not exist.
- **429**: Too Many Requests - Rate limit exceeded.
- **500**: Internal Server Error - Server-side issue.

### Error Response Format
```json
{
    "status": "error",
    "error": {
        "code": "string",
        "message": "string"
    }
}
```

## Conclusion

The Query Interface is a powerful tool for accessing and interacting with legal data within the DataHive ecosystem. By providing both RESTful and WebSocket capabilities, it allows users to efficiently retrieve documents, access metadata, and receive real-time updates. For further details on implementation and best practices, please refer to the [API Documentation](./api.md) and [Integration Guide](./integration.md).

