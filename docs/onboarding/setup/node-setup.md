# Node Setup Guide

Setting up your node is a critical step in joining the DataHive network. This guide provides a step-by-step process to help you configure and activate your node for optimal performance and compliance.

---

## Prerequisites

1. **Hardware Requirements**:
   - Ensure your system meets the minimum specifications for your node tier. Refer to the [hardware guide](/docs/onboarding/hardware.md).

2. **Wallet Setup**:
   - Set up a compatible cryptocurrency wallet. See the [wallet compatibility guide](/docs/onboarding/wallets.md).

3. **KYC Verification**:
   - Complete the [KYC process](/docs/onboarding/kyc.md) to validate your identity.

4. **License Fee Payment**:
   - Pay the annual license fee to activate your node. Learn more about [license fees](/docs/onboarding/fees.md).

---

## Step-by-Step Setup

### 1. Register Your Node
- Visit the [DataHive Node Registration Portal](https://www.datahive.network/nodes).
- Connect your wallet and complete the registration form.

### 2. Install Node Software
- Download the latest node software package from the [DataHive repository](https://github.com/datahiv3/Legalese-Node-LN1).
- Follow these installation commands based on your operating system:

#### For Linux:
```bash
wget https://example.com/download/node-installer.sh
chmod +x node-installer.sh
./node-installer.sh
```

#### For Windows:
1. Download the installer from the portal.
2. Run the `.exe` file and follow the on-screen instructions.

#### For macOS:
```bash
curl -O https://example.com/download/node-installer-mac.sh
chmod +x node-installer-mac.sh
./node-installer-mac.sh
```

### 3. Configure Node Settings
- Edit the configuration file (`config.json`) to include:
  - Wallet address
  - Node name
  - Network tier
- Save and exit the file.

### 4. Run Your Node
- Start the node using the following command:
```bash
./node start
```
- Verify the node’s status by accessing the [monitoring dashboard](/docs/onboarding/monitoring.md).

### 5. Validate Node Activation
- Confirm your node’s activation by checking the [dashboard](/docs/onboarding/dashboard.md).
- Ensure it is listed as “Active” with appropriate performance metrics.

---

## Post-Setup Tasks

1. **Monitor Performance**:
   - Use the [monitoring dashboard](/docs/onboarding/monitoring.md) to track metrics like uptime, task completion, and validation accuracy.

2. **Stake Tokens**:
   - Stake the required tokens based on your tier. Refer to the [staking guide](/docs/onboarding/staking/initiation.md).

3. **Optimize Configuration**:
   - Regularly update software to the latest version.
   - Adjust configurations to improve performance and reduce latency.

4. **Participate in Governance**:
   - Join governance discussions and voting through the [governance portal](/docs/onboarding/governance/proposals.md).

---

## Troubleshooting

| **Issue**                  | **Solution**                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| Node not starting          | Check logs for errors and ensure dependencies are installed.                |
| Low performance metrics    | Optimize hardware and check network connections.                            |
| License not validated      | Confirm payment and wallet connection through the [license portal](/docs/onboarding/legal/license-nft.md). |

---

## Support and Resources

- **Documentation**:
  - Access additional setup resources via the [onboarding documentation](/docs/onboarding/overview.md).
- **Community Forums**:
  - Engage with other operators in the [community forums](/docs/onboarding/community/forums.md).
- **Technical Support**:
  - Submit tickets for assistance through the [support portal](/docs/onboarding/support/tickets.md).

---

By following this guide, you’ll successfully set up and activate your node, contributing to the efficiency and growth of the DataHive network. Begin your journey today by registering at the [DataHive Node Registration Portal](https://www.datahive.network/nodes).
