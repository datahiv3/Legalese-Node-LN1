# WebSocket Subscriptions in LN1 Legalese Node

The LN1 Legalese Node supports WebSocket (WS) connections, allowing clients to subscribe to real-time updates and notifications for various blockchain events. This document outlines the available WebSocket subscriptions, their usage, and best practices for implementation.

---

## **Overview of WebSocket Connections**

WebSocket connections enable persistent, full-duplex communication channels between clients and the LN1 node. This allows for efficient data transfer and real-time updates without the need for constant polling.

### **Benefits of Using WebSocket Subscriptions**
- **Real-Time Data**: Receive immediate notifications for events such as new blocks or pending transactions.
- **Reduced Latency**: Minimize delays associated with traditional HTTP requests.
- **Efficient Resource Use**: Decrease network overhead by avoiding repetitive requests.

---

## **Available WebSocket Subscriptions**

### 1. **New Block Headers (`newHeads`)**
- **Description**: Subscribe to notifications for new block headers added to the blockchain.
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
    "result": "0xSubscriptionId", // Unique subscription ID
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
      "result": {
        // New block header details
      }
    }
  }
  ```

### 2. **Pending Transactions (`newPendingTransactions`)**
- **Description**: Subscribe to notifications for new transactions that are pending in the mempool.
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
    "result": "0xSubscriptionId", // Unique subscription ID
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
      "result": {
        // Transaction hash or details
      }
    }
  }
  ```

### 3. **Logs (`logs`)**
- **Description**: Subscribe to logs emitted by smart contracts that match specified filter criteria.
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
    "result": "0xSubscriptionId", // Unique subscription ID
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
      "result": {
        // Log details
      }
    }
  }
  ```

---

## **Unsubscribing from Subscriptions**

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

## **Best Practices for Using WebSocket Subscriptions**

1. **Connection Management**:
   - Maintain a persistent WebSocket connection for real-time updates.
   - Implement automatic reconnection logic in case of disconnection.

2. **Efficient Subscription Usage**:
   - Subscribe only to the events necessary for your application to minimize resource usage.
   - Use filters (e.g., topics, addresses) when subscribing to logs to reduce unnecessary data transfer.

3. **Error Handling**:
   - Implement robust error handling for invalid subscription requests or unexpected connection drops.
   - Monitor and log WebSocket errors for debugging purposes.

4. **Rate Limiting Awareness**:
   - Be mindful of rate limits imposed by the node operator to avoid throttling or disconnection.

---

## Additional Resources

For more information on JSON-RPC methods and general API usage, refer to:
- [API Overview](./api_overview.md)
- [Batch Requests Support](./batch_requests_support.md)
