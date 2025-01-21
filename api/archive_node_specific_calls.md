# Archive Node-Specific RPC Calls in LN1 Legalese Node

Certain RPC methods in the LN1 Legalese Node are designated specifically for archive nodes. These methods provide access to historical blockchain data that is unavailable through standard full nodes. This document outlines these methods, their use cases, and recommendations for efficient usage.

## **What Are Archive Node-Specific Calls?**

Archive node-specific calls enable access to:
- **Historical States**: Query blockchain data at specific block heights.
- **Detailed Transaction Tracing**: Analyze the execution of past transactions.
- **Historical Logs**: Retrieve logs emitted by smart contracts over a wide range of blocks.

These operations require the complete historical state stored by archive nodes, which is not available in pruned full nodes.

## **List of Archive Node-Specific RPC Methods**

### 1. **`eth_getBalance` (for Historical Blocks)**
- **Description**: Retrieves the balance of an account at a specific block height.
- **Use Case**: Querying account balances at any historical block.
- **Example Request**:
  ```
  {
    "jsonrpc": "2.0",
    "method": "eth_getBalance",
    "params": ["0xAccountAddress", "0xBlockNumber"],
    "id": 1
  }
  ```
- **Example Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": "0x0234c8a3397aab58", // Balance in wei
    "id": 1
  }
  ```

---

### 2. **`debug_traceTransaction`**
- **Description**: Traces the execution of a transaction, providing detailed information about its operations.
- **Use Case**: Debugging smart contract execution or analyzing transaction behavior.
- **Example Request**:
  ```
  {
    "jsonrpc": "2.0",
    "method": "debug_traceTransaction",
    "params": ["0xTransactionHash"],
    "id": 2
  }
  ```
- **Example Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": { ... } // Detailed trace data
    "id": 2
  }
  ```

---

### 3. **`eth_getLogs`**
- **Description**: Retrieves logs emitted by smart contracts within a specified block range.
- **Use Case**: Querying historical events or contract activity over a wide range of blocks.
- **Example Request**:
  ```
  {
    "jsonrpc": "2.0",
    "method": "eth_getLogs",
    "params": [{
      "fromBlock": "0xBlockStart",
      "toBlock": "0xBlockEnd",
      "address": ["0xContractAddress"],
      "topics": ["0xTopicHash"]
    }],
    "id": 3
  }
  ```
- **Example Response**:
  ```
  {
    "jsonrpc": "2.0",
    "result": [ ... ] // Array of log objects
    "id": 3
  }
  ```

## **When to Use Archive Node-Specific Calls**

1. **Historical Analysis**:
   - Retrieve account balances or contract states at specific points in time.
   - Analyze past events or transaction behavior for auditing or debugging purposes.

2. **Compliance and Auditing**:
   - Access complete historical data for regulatory compliance or forensic investigations.

3. **Blockchain Analytics Platforms**:
   - Power analytics tools requiring access to historical trends and patterns.

## **Best Practices for Using Archive Node-Specific Calls**

1. **Optimize Queries**:
   - Narrow block ranges and use filters (e.g., topics, addresses) to reduce the amount of data processed.

2. **Leverage Caching**:
   - Cache frequently accessed historical data to minimize repeated queries.

3. **Monitor Resource Usage**:
   - Be mindful of the high computational and storage requirements of archive node calls.

4. **Rate Limit Requests**:
   - Avoid overwhelming the node with excessive concurrent requests.

5. **Use Only When Necessary**:
   - Prefer full node calls for real-time data whenever possible to conserve resources.


## Additional Resources

For more information on archive nodes and their capabilities, refer to:
- [Archive Node Requirement](/docs/technical/archive_node_requirement.md)
- [Resource-Intensive RPC Methods](/api/resource_intensive_rpc_methods.md)
