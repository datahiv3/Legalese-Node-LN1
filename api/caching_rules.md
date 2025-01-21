# Caching Rules for RPC Methods in LN1 Legalese Node

Caching is an essential strategy for optimizing performance and reducing redundant requests when interacting with the LN1 Legalese Node. This document outlines suggested caching rules for various RPC methods and provides best practices for implementing an efficient caching mechanism.

---

## **Why Use Caching?**

Caching helps to:
- **Reduce Latency**: Minimize response times by serving frequently requested data from cache.
- **Optimize Resource Usage**: Lower the load on the node by avoiding repeated processing of identical requests.
- **Improve Scalability**: Handle more requests efficiently by reducing backend computation.

---

## **Recommended Caching Strategy**

The **Least Recently Used (LRU)** cache strategy is recommended for LN1 Legalese Node:
- **How It Works**: LRU evicts the least recently accessed items when the cache reaches its capacity, ensuring that frequently used data remains readily available.
- **Implementation**: Use LRU caching libraries or frameworks available in your programming language (e.g., `lru-cache` in JavaScript, `functools.lru_cache` in Python).

---

## **Suggested Caching Rules by RPC Method**

### 1. **Blockchain Data Retrieval**
These methods often involve static or infrequently changing data, making them ideal candidates for caching.

| Method                  | Cache Duration | Notes                                                                 |
|-------------------------|----------------|----------------------------------------------------------------------|
| `eth_blockNumber`       | 5 seconds      | Cache the latest block number to reduce redundant queries.           |
| `eth_getBlockByNumber`  | 10 seconds     | Cache block details unless querying `latest`.                        |
| `eth_getTransactionByHash` | 30 seconds   | Cache transaction details as they rarely change after confirmation. |

---

### 2. **Account and State Queries**
These methods involve dynamic data but can still benefit from short-term caching.

| Method                  | Cache Duration | Notes                                                                 |
|-------------------------|----------------|----------------------------------------------------------------------|
| `eth_getBalance`        | 5-10 seconds   | Cache balances to reduce load during frequent polling.               |
| `eth_call`              | No caching     | Avoid caching as results depend on contract state and input params.  |

---

### 3. **Historical Data Queries**
These methods often involve static historical data, making them highly cacheable.

| Method                  | Cache Duration | Notes                                                                 |
|-------------------------|----------------|----------------------------------------------------------------------|
| `eth_getLogs`           | 1 minute       | Cache logs based on filter criteria to improve performance.          |
| `debug_traceTransaction`| 5 minutes      | Cache trace results as they are computationally expensive to generate.|

---

### 4. **Node Health and Metrics**
These methods provide real-time information about node status and should not be cached.

| Method                  | Cache Duration | Notes                                                                 |
|-------------------------|----------------|----------------------------------------------------------------------|
| `net_version`           | No caching     | Always fetch the latest network ID.                                  |
| `eth_syncing`           | No caching     | Real-time sync status requires fresh data.                           |

---

## **Best Practices for Caching**

1. **Set Appropriate Expiry Times**:
   - Use shorter durations for dynamic data (e.g., block number, balances).
   - Use longer durations for static or historical data (e.g., logs, traces).

2. **Invalidate Stale Data**:
   - Automatically invalidate cached data when new blocks are detected.
   - Implement logic to refresh cache on significant state changes.

3. **Use Parameter-Based Keys**:
   - Include method parameters (e.g., block number, address) in cache keys to avoid collisions.

4. **Monitor Cache Performance**:
   - Track cache hit/miss ratios to optimize configuration.
   - Adjust cache size and eviction policies based on usage patterns.

5. **Secure Cached Data**:
   - Encrypt sensitive data in cache (e.g., account balances).
   - Restrict access to cached data using appropriate permissions.

---

## Additional Resources
For more information on RPC methods and their usage, refer to:
- [RPC Methods Documentation](./rpc_methods.md)
- [Node Server Paths](./node_server_paths.md)
