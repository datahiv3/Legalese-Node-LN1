# API Overview for LN1 Legalese Node

The LN1 Legalese Node provides a robust JSON-RPC API interface for interacting with blockchain data, enabling developers to perform a wide range of operations such as retrieving blockchain state, querying historical data, and monitoring node health.

---

## **Key Features**
- **JSON-RPC 2.0 Compliance**: The API adheres to the JSON-RPC 2.0 specification, ensuring compatibility with standard tools and libraries.
- **WebSocket Support**: Real-time updates and subscriptions are available via WebSocket connections.
- **Batch Requests**: Multiple RPC calls can be grouped into a single request for efficiency.
- **Extensibility**: Designed to support future enhancements and integrations.

---

## **Available Endpoints**
The LN1 Legalese Node exposes multiple endpoints for different use cases:

### 1. **HTTP Endpoint**
   - URL: `http://<node-address>:<port>`
   - Use Cases: Standard JSON-RPC requests for querying blockchain data.

### 2. **WebSocket Endpoint**
   - URL: `ws://<node-address>:<port>`
   - Use Cases: Subscriptions for real-time updates (e.g., new blocks, pending transactions).

---

## **Supported RPC Methods**
The API supports a variety of JSON-RPC methods categorized as follows:

### Blockchain Data Retrieval
- `eth_blockNumber`: Fetch the latest block number.
- `eth_getBlockByNumber`: Retrieve block details by block number.
- `eth_getTransactionByHash`: Get transaction details by hash.

### Account and State Queries
- `eth_getBalance`: Retrieve account balance at a specific block.
- `eth_call`: Execute a read-only smart contract function.

### Historical Data (Archive Nodes Only)
- `eth_getLogs`: Query logs from historical blocks.
- `debug_traceTransaction`: Trace transaction execution (requires archive node).

### Node Health and Sync Status
- `net_version`: Get the network ID.
- `eth_syncing`: Check if the node is syncing.
- `web3_clientVersion`: Retrieve client version information.

For a full list of supported methods, refer to [RPC Methods Documentation](./rpc_methods.md).

---

## **Batch Requests**
Batch requests allow multiple RPC calls in a single HTTP request:
- Maximum batch size: 100 requests.
- Refer to [Batch Requests Documentation](./batch_requests_support.md) for details.

---

## **WebSocket Subscriptions**
The WebSocket endpoint supports real-time subscriptions:
- **New Blocks**: Subscribe to new block headers (`newHeads`).
- **Pending Transactions**: Monitor pending transactions (`newPendingTransactions`).
- For more details, see [WebSocket Subscriptions](./websocket_subscriptions.md).

---

## **Caching Guidelines**
To optimize performance:
1. Cache frequently accessed data (e.g., latest block number) with short expiration times.
2. Avoid caching dynamic queries (e.g., pending transactions).
3. Refer to [Caching Best Practices](./caching_guidelines.md) for detailed recommendations.

---

## **Error Handling**
API responses follow JSON-RPC error conventions:
- Example Error Response:
```
{
  "jsonrpc": "2.0",
  "error": {
    "code": -32601,
    "message": "Method not found"
  },
  "id": 1
}
```
For a list of error codes and their meanings, refer to [Error Codes Reference](./error_codes.md).

---

## **Rate Limiting**
The LN1 Legalese Node enforces rate limits on API usage to ensure fair access:
- Rate limits apply per IP address or API key (if configured).
- Refer to [Rate Limiting Guidelines](./rate_limiting.md) for details.

---

## **Getting Started**
To start using the LN1 Legalese Node API:
1. Set up your node by following the [Node Deployment Guide](../deployment/setup_guide.md).
2. Test connectivity using basic RPC calls like `eth_blockNumber`.
3. Explore advanced features such as batch requests and WebSocket subscriptions.

For further assistance, consult the [Developer Onboarding Guide](../onboarding/developer_guide.md).

---

## **Additional Resources**
- [Full RPC Methods Documentation](./rpc_methods.md)
- [WebSocket Subscriptions](./websocket_subscriptions.md)
- [Batch Requests Support](./batch_requests_support.md)
