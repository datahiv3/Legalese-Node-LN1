# WebSocket Connections in LN1 Legalese Node

The LN1 Legalese Node supports WebSocket (WS) connections, enabling real-time communication and subscriptions for blockchain events. This feature is ideal for applications requiring low-latency updates, such as monitoring new blocks, pending transactions, or contract events.

---

## **Key Features**
- **Real-Time Updates**: WebSocket connections provide push-based notifications for blockchain events without requiring repeated polling.
- **JSON-RPC 2.0 Compatibility**: WebSocket communication adheres to the JSON-RPC 2.0 specification.
- **Subscriptions**: Developers can subscribe to specific events like new blocks or pending transactions.

---

## **WebSocket Endpoint**
- **URL**: `ws://<node-address>:<port>`
- Replace `<node-address>` and `<port>` with the appropriate values for your LN1 Legalese Node instance.

---

## **Supported Subscriptions**

### 1. **New Block Headers (`newHeads`)**
- **Description**: Subscribes to notifications for new block headers.
- **Request Example**:
  ```
  {
    "jsonrpc": "2.0",
    "method": "eth_subscribe",
    "params": ["newHeads"],
    "id": 1
  }
  ```
- **Response Example**:
  ```
  {
    "jsonrpc": "2.0",
    "result": "0xSubscriptionId", // Subscription ID
    "id": 1
  }
  ```

- **Push Notification Example**:
  ```
  {
    "jsonrpc": "2.0",
    "method": "eth_subscription",
    "params": {
      "subscription": "0xSubscriptionId",
      "result": { ... } // New block header details
    }
  }
  ```

---

### 2. **Pending Transactions (`newPendingTransactions`)**
- **Description**: Subscribes to notifications for new pending transactions.
- **Request Example**:
  ```
  {
    "jsonrpc": "2.0",
    "method": "eth_subscribe",
    "params": ["newPendingTransactions"],
    "id": 2
  }
  ```
- **Response Example**:
  ```
  {
    "jsonrpc": "2.0",
    "result": "0xSubscriptionId", // Subscription ID
    "id": 2
  }
  ```

- **Push Notification Example**:
  ```
  {
    "jsonrpc": "2.0",
    "method": "eth_subscription",
    "params": {
      "subscription": "0xSubscriptionId",
      "result": { ... } // Transaction hash or details
    }
  }
  ```

---

### 3. **Logs (`logs`)**
- **Description**: Subscribes to logs emitted by smart contracts that match specified filter criteria.
- **Parameters**:
  - `filterObject`: Includes options like `address`, `topics`, etc.
- **Request Example**:
  ```
  {
    "jsonrpc": "2.0",
    "method": "eth_subscribe",
    "params": ["logs", {
      "address": ["0xContractAddress"],
      "topics": ["0xTopicHash"]
    }],
    "id": 3
  }
  ```
- **Response Example**:
  ```
  {
    "jsonrpc": "2.0",
    "result": "0xSubscriptionId", // Subscription ID
    "id": 3
  }
  ```

- **Push Notification Example**:
  ```
  {
    "jsonrpc": "2.0",
    "method": "eth_subscription",
    "params": {
      "subscription": "0xSubscriptionId",
      "result": { ... } // Log details
    }
  }
  ```

---

## **Unsubscribing**
To terminate a subscription, use the `eth_unsubscribe` method.

### Request Example:
```
{
   "jsonrpc":"2.0",
   "method":"eth_unsubscribe",
   "params":["0xSubscriptionId"],
   "id":4
}
```

### Response Example:
```
{
   "jsonrpc":"2.0",
   "result":true,
   "id":4
}
```

---

## **Best Practices**
1. **Connection Management**:
   - Maintain a persistent WebSocket connection for real-time updates.
   - Reconnect automatically in case of disconnection.

2. **Efficient Subscriptions**:
   - Subscribe only to the events your application requires to minimize network overhead.
   - Use filters (e.g., `topics`, `address`) when subscribing to logs.

3. **Error Handling**:
   - Handle errors gracefully, such as invalid subscription requests or connection drops.
   - Monitor and log WebSocket errors for debugging purposes.

4. **Rate Limiting Awareness**:
   - Be mindful of rate limits imposed by the node operator to avoid throttling or disconnection.

---

## Additional Resources
For more information on JSON-RPC methods and batch requests, refer to:
- [API Overview](./api_overview.md)
- [Batch Requests Support](./batch_requests_support.md)
