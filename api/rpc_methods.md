# RPC Methods for LN1 Legalese Node

This document outlines the JSON-RPC methods supported by the LN1 Legalese Node, categorized by functionality. Each method includes details about its purpose, parameters, response format, and example usage.

---

## **General Information**
- **Protocol**: JSON-RPC 2.0
- **Endpoints**:
  - HTTP: `http://<node-address>:<port>`
  - WebSocket: `ws://<node-address>:<port>`
- **Batch Requests**: Supported (up to 100 calls per batch).

---

## **Method Categories**

### 1. **Blockchain Data Retrieval**
These methods allow querying blockchain state and transaction data.

#### `eth_blockNumber`
- **Description**: Returns the latest block number.
- **Parameters**: None.
- **Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": "0x10d4f", // Block number in hexadecimal
    "id": 1
  }
  ```
- **Example Request**:
  ```
  {"jsonrpc": "2.0", "method": "eth_blockNumber", "params": [], "id": 1}
  ```

#### `eth_getBlockByNumber`
- **Description**: Retrieves block details by block number.
- **Parameters**:
  - `blockNumber` (string): The block number (e.g., `"latest"`, `"0x10d4f"`).
  - `includeTransactions` (boolean): Whether to include full transaction objects.
- **Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": { ... }, // Block details
    "id": 1
  }
  ```
- **Example Request**:
  ```
  {"jsonrpc": "2.0", "method": "eth_getBlockByNumber", "params": ["latest", true], "id": 1}
  ```

---

### 2. **Account and State Queries**
These methods provide information about accounts and their states.

#### `eth_getBalance`
- **Description**: Returns the balance of an account at a specific block.
- **Parameters**:
  - `address` (string): The account address.
  - `blockNumber` (string): The block number (e.g., `"latest"`).
- **Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": "0x0234c8a3397aab58", // Balance in wei
    "id": 1
  }
  ```
- **Example Request**:
  ```
  {"jsonrpc": "2.0", "method": "eth_getBalance", "params": ["0x1234...", "latest"], "id": 1}
  ```

#### `eth_call`
- **Description**: Executes a read-only smart contract function call.
- **Parameters**:
  - `callObject` (object): Contains details like `to`, `data`, etc.
  - `blockNumber` (string): The block number (e.g., `"latest"`).
- **Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": "...", // Return value of the function call
    "id": 1
  }
  ```

---

### 3. **Historical Data Queries (Archive Nodes Only)**
These methods require an archive node for accessing historical data.

#### `eth_getLogs`
- **Description**: Retrieves logs from past blocks based on filter criteria.
- **Parameters**:
  - `filterObject` (object): Contains filter options like topics, address, etc.
- **Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": [...], // Array of log objects
    "id": 1
  }
  ```

#### `debug_traceTransaction`
- **Description**: Traces the execution of a transaction.
- **Parameters**:
  - `transactionHash` (string): The hash of the transaction to trace.
- **Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": { ... }, // Trace details
    "id": 1
  }
  ```

---

### 4. **Node Health and Sync Status**
These methods help monitor the health and synchronization status of the node.

#### `net_version`
- **Description**: Returns the network ID the node is connected to.
- **Parameters**: None.
- **Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": "1", // Network ID
    "id": 1
  }
  ```

#### `eth_syncing`
- **Description**: Checks if the node is syncing with the network.
- **Parameters**: None.
- **Response**:
   - If syncing:
     ```
     {
       "jsonrpc": "2.0",
       "result": { ... }, // Syncing details
       "id": 1
     }
     ```
   - If not syncing:
     ```
     {
       "jsonrpc": "2.0",
       "result": false,
       "id": 1
     }
     ```

---

## **Error Handling**
All errors follow JSON-RPC conventions with an error object in the response.

### Example Error Response:
```
{
   "jsonrpc":"2.0",
   "error":{
      "code": -32601,
      "message":"Method not found"
   },
   "id":1
}
```

### Common Error Codes:
| Code   | Message               | Description                          |
|--------|-----------------------|--------------------------------------|
| -32600 | Invalid Request       | JSON is not a valid request object. |
| -32601 | Method Not Found      | The method does not exist/is invalid.|
| -32602 | Invalid Params        | Parameters are invalid or missing.   |
| -32603 | Internal Error        | An internal JSON-RPC error occurred.|

---

## Additional Resources
For more information on using these methods effectively, refer to:
- [Batch Requests Documentation](./batch_requests_support.md)
- [WebSocket Subscriptions](./websocket_subscriptions.md)
