# Archive Node Size Requirements for LN1 Legalese Node

Provisioning an archive node is optional but can be critical for specific use cases requiring access to historical blockchain data. The size requirements for an archive node depend on several factors, including the blockchain network, the volume of data being handled, and the operational use case.

---

## **Overview of Archive Node Storage Needs**

An archive node stores the **entire history of the blockchain**, including all past states, transactions, and logs. Unlike full nodes, which prune older data to save space, archive nodes retain complete historical data for every block since the genesis block.

- **Storage Requirements**: Archive nodes require significantly more storage than full nodes.
- **Growth Over Time**: Storage needs increase as the blockchain grows, so operators must account for future scalability.

---

## **Estimated Storage Sizes**

The following table provides approximate storage requirements for archive nodes on different networks:

| **Network**       | **Estimated Size**         | **Growth Rate**           |
|--------------------|----------------------------|---------------------------|
| Ethereum Mainnet   | ~12 TB                     | ~1 TB/year                |
| OP Sepolia ([Testnet1](https://www.datahive.network/post/datahive-launches-testnet1-on-op-sepolia-facilitated-by-altlayer-advancing-integration-with-0g-aios)) | ~4 TB                      | ~0.5 TB/year              |
| Polygon Mainnet    | ~16 TB                     | ~1.5 TB/year              |
| Avalanche Mainnet  | ~3 TB                      | ~0.3 TB/year              |

**Note**: These figures are estimates and may vary based on network activity, transaction volume, and protocol upgrades.

---

## **Factors Influencing Archive Node Size**

1. **Blockchain Network**:
   - Networks with higher transaction volumes (e.g., Ethereum Mainnet) require more storage.
   - Testnets like OP Sepolia have smaller data footprints but still grow over time.

2. **Historical Data Access**:
   - Applications requiring frequent access to historical states or logs will necessitate larger storage capacities.

3. **Node Configuration**:
   - Archive nodes configured to support multiple networks (e.g., Ethereum + OP Sepolia) will require combined storage for all networks.

4. **Redundancy and Backup**:
   - Operators may allocate additional storage for backups or redundancy to ensure data availability.

---

## **Hardware Recommendations**

Based on the expected size of an archive node, here are hardware recommendations:

| **Node Tier**      | **CPU**                 | **RAM**      | **Storage**            | **Network**         |
|---------------------|-------------------------|--------------|------------------------|---------------------|
| Entry-Level         | 8-core, 3.5 GHz        | 32 GB        | 4 TB NVMe SSD          | 1 Gbps              |
| Mid-Range           | 16-core, 4.0 GHz       | 64 GB        | 8 TB NVMe SSD (RAID)   | 2.5 Gbps            |
| High-Performance    | 32-core, 4.5 GHz       | 128 GB       | 16 TB NVMe SSD (RAID)  | 10 Gbps             |

---

## **Use Cases for Archive Nodes**

Archive nodes are required in scenarios where access to historical blockchain data is essential:

1. **Historical Data Queries**:
   - Retrieve past account balances or contract states (`eth_getBalance` with historical blocks).
   - Analyze logs over a wide range of blocks (`eth_getLogs`).

2. **Transaction Tracing**:
   - Perform detailed transaction analysis using methods like `debug_traceTransaction`.

3. **Compliance and Auditing**:
   - Maintain a complete record of blockchain activity for regulatory or forensic purposes.

4. **Blockchain Analytics Platforms**:
   - Power analytics tools that provide insights into historical trends and patterns.

---

## **Best Practices for Managing Archive Node Storage**

1. **Plan for Scalability**:
   - Allocate additional storage capacity to accommodate future blockchain growth.
   - Use scalable storage solutions like RAID configurations or cloud-based options.

2. **Monitor Storage Usage**:
   - Regularly monitor disk usage to ensure sufficient free space is available.
   - Set up alerts for low disk space thresholds.

3. **Optimize Data Access**:
   - Use caching mechanisms to reduce repeated queries on historical data.
   - Implement efficient indexing strategies for faster retrieval of archived data.

4. **Backup and Redundancy**:
   - Maintain regular backups of archive node data to prevent loss in case of hardware failure.
   - Use distributed storage solutions (e.g., IPFS or Filecoin) for redundancy.

---

## Additional Resources

For more information on archive node requirements and their use cases, refer to:
- [Archive Node Requirement](./archive_node_requirement.md)
- [Resource-Intensive RPC Methods](/api/resource_intensive_rpc_methods.md)
- [Node Health and Block Sync Documentation](/api/node_health_and_block_sync.md)
