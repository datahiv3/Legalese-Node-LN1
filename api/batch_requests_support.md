# Batch Request Support in LN1 Legalese Node

The LN1 Legalese Node supports batch requests, enabling multiple JSON-RPC operations to be sent in a single HTTP request. This feature is designed to optimize network usage and improve performance by reducing the number of individual requests sent to the node.

## Key Features
- **Batching Capability**: Multiple JSON-RPC calls can be included in a single request.
- **Efficiency**: Reduces overhead by minimizing the number of HTTP connections required.

## Limitations
- **Request Limit**: A single batch request can include up to **100 JSON-RPC calls**.
- **Payload Size**: The total payload size for a batch request must not exceed **1 MB**.

## Usage Example
Here is an example of a batch request:

### Request:
```
[
  {"jsonrpc": "2.0", "method": "eth_blockNumber", "params": [], "id": 1},
  {"jsonrpc": "2.0", "method": "eth_getBalance", "params": ["0xaddress", "latest"], "id": 2}
]
```

### Response:
```
[
  {"jsonrpc": "2.0", "result": "0x10d4f", "id": 1},
  {"jsonrpc": "2.0", "result": "0x0234c8a3397aab58", "id": 2}
]
```

## Error Handling
- If any request in the batch fails, the response will include an error object for that specific request.
- Other requests in the batch will still be processed successfully.

### Example Error Response:
```
[
  {"jsonrpc": "2.0", "result": "0x10d4f", "id": 1},
  {
    "jsonrpc": "2.0",
    "error": {
      "code": -32602,
      "message": "Invalid params"
    },
    "id": 2
  }
]
```

## Best Practices
- Group related operations in a single batch to minimize latency and improve efficiency.
- Ensure that the total number of requests and payload size remain within the specified limits.
- Validate all parameters before sending batch requests to avoid processing errors.

For more details, refer to the [LN1 Legalese Node API Documentation](./api_overview.md).
