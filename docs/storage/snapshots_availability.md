# Snapshots Availability in LN1 Legalese Node

Snapshots are available for both full and archive nodes in the LN1 Legalese Node. These snapshots facilitate easier recovery, faster synchronization, and efficient data management, making them a critical feature for node operators.

---

## **What Are Snapshots?**

A snapshot is a point-in-time copy of a node's blockchain data. It captures the current state of the blockchain, allowing operators to:
- Quickly restore a node to a specific state without re-syncing from scratch.
- Reduce downtime during maintenance or disaster recovery.
- Share pre-synced node states for faster deployment.

---

## **Snapshot Support**

### 1. **Full Nodes**
- **Purpose**: Full nodes store only the latest blockchain state and prune older data.
- **Snapshot Benefits**:
  - Faster recovery after hardware failures.
  - Efficient deployment of additional full nodes using pre-synced snapshots.

### 2. **Archive Nodes**
- **Purpose**: Archive nodes store the entire blockchain history, including all historical states.
- **Snapshot Benefits**:
  - Simplifies recovery while preserving complete historical data.
  - Reduces the time required to set up new archive nodes.

---

## **How to Use Snapshots**

### 1. **Downloading Snapshots**
Snapshots can be downloaded from trusted sources or generated manually. Ensure that:
- The snapshot corresponds to your desired network (e.g., Ethereum Mainnet, OP Sepolia).
- The snapshot is up-to-date and verified for integrity.

### 2. **Restoring from Snapshots**
To restore a node using a snapshot:
1. Stop the node if it is currently running.
2. Replace the existing blockchain data directory with the snapshot files.
3. Start the node and allow it to sync any remaining blocks from the network.

#### Example Command (Geth):
```
geth --datadir /path/to/snapshot
```

### 3. **Generating Snapshots**
Operators can create their own snapshots by copying the node's data directory at a specific block height.

#### Steps:
1. Stop the node to ensure data consistency.
2. Compress the data directory into an archive file (e.g., `.tar.gz`).
3. Store or share the snapshot securely.

---

## **Best Practices for Using Snapshots**

1. **Verify Snapshot Integrity**:
   - Always verify downloaded snapshots using checksums (e.g., SHA256) to ensure they have not been tampered with.

2. **Keep Snapshots Updated**:
   - Regularly create new snapshots to minimize synchronization time during recovery.

3. **Secure Storage**:
   - Store snapshots in secure locations (e.g., cloud storage or encrypted drives) to prevent unauthorized access.

4. **Use Trusted Sources**:
   - Only download snapshots from trusted providers or generate them manually to avoid malicious data.

5. **Monitor Disk Space**:
   - Ensure sufficient storage is available before restoring or generating snapshots, especially for archive nodes.

---

## **Advantages of Using Snapshots**

1. **Faster Node Deployment**:
   - Deploy new nodes quickly without syncing from genesis.

2. **Disaster Recovery**:
   - Minimize downtime by restoring nodes rapidly after failures.

3. **Efficient Data Sharing**:
   - Share pre-synced states with other operators or teams for collaborative projects.

4. **Reduced Network Load**:
   - Avoid downloading large amounts of blockchain data repeatedly during setup.

---

## Additional Resources

For more details on managing node storage and recovery, refer to:
- [Archive Node Size Requirements](/docs/technical/archive_node_size.md)
- [Node Health and Block Sync Documentation](/api/node_health_and_block_sync.md)
