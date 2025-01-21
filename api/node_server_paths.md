# Node Server Paths in LN1 Legalese Node

The LN1 Legalese Node supports multiple URL paths, each exposing specific RPC methods. This design allows developers to interact with the node flexibly, depending on the type of operation being performed.

---

## **Overview of Node Server Paths**

The LN1 node servers are structured to provide distinct paths for various functionalities, ensuring efficient handling of requests and separation of concerns. Each path corresponds to a specific set of RPC methods.

- **Base URL**: `http://<node-address>:<port>`
  Replace `<node-address>` and `<port>` with your node's address and port.

---

## **Available URL Paths**

### 1. **General Blockchain Operations**
- **Path**: `/rpc`
- **Description**: Provides access to general blockchain data and state queries.
- **Supported Methods**:
  - `eth_blockNumber`: Retrieve the latest block number.
  - `eth_getBlockByNumber`: Fetch details of a specific block.
  - `eth_getTransactionByHash`: Get details of a transaction by its hash.

#### Example Request:
```
POST http://<node-address>:<port>/rpc
{
  "jsonrpc": "2.0",
  "method": "eth_blockNumber",
  "params": [],
  "id": 1
}
```

---

### 2. **WebSocket Connections**
- **Path**: `/ws`
- **Description**: Enables real-time subscriptions and push-based notifications for blockchain events.
- **Supported Methods**:
  - `eth_subscribe`: Subscribe to new blocks, pending transactions, or logs.
  - `eth_unsubscribe`: Cancel an active subscription.

#### Example WebSocket Endpoint:
```
ws://<node-address>:<port>/ws
```

---

### 3. **Debugging and Tracing**
- **Path**: `/debug`
- **Description**: Provides advanced debugging and tracing capabilities (requires archive node).
- **Supported Methods**:
  - `debug_traceTransaction`: Trace the execution of a transaction.
  - `debug_storageRangeAt`: Inspect storage changes for a specific contract.

#### Example Request:
```
POST http://<node-address>:<port>/debug
{
  "jsonrpc": "2.0",
  "method": "debug_traceTransaction",
  "params": ["0xTransactionHash"],
  "id": 1
}
```

---

### 4. **Node Health and Metrics**
- **Path**: `/health`
- **Description**: Provides health checks and synchronization status for the node.
- **Supported Methods**:
  - `net_version`: Retrieve the network ID.
  - `web3_clientVersion`: Get client version information.
  - `eth_syncing`: Check if the node is syncing.

#### Example Request:
```
POST http://<node-address>:<port>/health
{
  "jsonrpc": "2.0",
  "method": "eth_syncing",
  "params": [],
  "id": 1
}
```

---

## **Best Practices for Using Node Server Paths**
1. **Use Specific Paths for Targeted Operations**:
   - Direct requests to the appropriate path based on the operation (e.g., `/rpc` for general queries, `/debug` for tracing).

2. **Optimize Performance with Caching**:
   - Cache frequently accessed data (e.g., latest block number) to reduce redundant requests.

3. **Secure Access**:
   - Restrict access to sensitive paths like `/debug` using authentication or IP whitelisting.

4. **Monitor Health Regularly**:
   - Use `/health` endpoints to monitor node status and ensure it is in sync with the network.

---

## Additional Resources
For more details on supported methods and their usage, refer to:
- [RPC Methods Documentation](./rpc_methods.md)
- [WebSocket Connections](./websocket_connections.md)
- [Batch Requests Support](./batch_requests_support.md)
