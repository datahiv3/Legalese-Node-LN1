# LN1 Legal Data API

## Overview
The LN1 Legal Data API provides programmatic access to the DataHive legal document indexing and curation system. This API enables developers to interact with legal documents, metadata, and the curation system.

## Documentation Structure
- [Endpoints Documentation](ENDPOINTS.md) - Detailed API endpoints
- [REST API Guide](rest-api.md) - REST implementation details
- [API Specification](SPEC.md) - OpenAPI/Swagger specification

## Quick Start

### Base URL
```bash
https://api.datahive.com/v1

### Authentication
All API requests require authentication using an API key:
```bash
Authorization: Bearer YOUR_API_KEY
```

## Core Features

### Document Management
- Document retrieval
- Content search
- Metadata access
- Version control
- Citation extraction

### Indexing Operations
- Document submission
- Status checking
- Quality metrics
- Source verification

### Curation Functions
- Validation requests
- Node status
- Consensus information
- Reward distribution

## Integration Examples

### Document Retrieval
```python
import requests

headers = {
    'Authorization': 'Bearer YOUR_API_KEY'
}

response = requests.get(
    'https://api.datahive.com/v1/documents/{id}',
    headers=headers
)
```

### Search Documents
```python
params = {
    'query': 'legal term',
    'limit': 10
}

response = requests.get(
    'https://api.datahive.com/v1/documents/search',
    headers=headers,
    params=params
)
```

## Rate Limiting
- 1000 requests per hour per API key
- Rate limit headers included in responses
- Exponential backoff recommended

## Best Practices
- Implement proper error handling
- Cache responses when appropriate
- Use pagination for large result sets
- Monitor rate limits
- Keep API keys secure

## Error Handling
Common error codes and their meanings:
- 400: Bad Request - Invalid parameters
- 401: Unauthorized - Invalid API key
- 403: Forbidden - Insufficient permissions
- 404: Not Found - Resource doesn't exist
- 429: Too Many Requests - Rate limit exceeded
- 500: Internal Server Error - Server-side issue

## Support
- [Technical Documentation](../technical/LEGAL_DATA_SYSTEM.md)
- [Development Guidelines](../guidelines/DEVELOPMENT.md)
- [Security Considerations](../guidelines/infrastructure/SECURITY.md)

## Versioning
The API follows semantic versioning (MAJOR.MINOR.PATCH):
- MAJOR: Breaking changes
- MINOR: New features, backward compatible
- PATCH: Bug fixes, backward compatible

## Changelog
- v1.0.0 - Initial release
  - Basic document operations
  - Search functionality
  - Authentication system
```

This API.md file:
- Provides a high-level overview of the API
- Links to detailed documentation
- Includes quick start examples
- References related documentation
- Follows the project structure shown in VS Code
- Aligns with the technical requirements visible in the repository

