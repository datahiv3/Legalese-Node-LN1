I'll help update the README.md with appropriate internal folder and file links based on the folder structure we established. Here's the updated version:

# LN1 Legalese Node - Public Repository

Welcome to the public repository for DataHive's LN1 Legalese Node. This repo contains open-source components and documentation for the legal data indexing and curation system powering the DataHive network.

## About LN1 Legalese Node

The LN1 Legalese Node is a crucial component of the DataHive ecosystem, designed to index, curate, and process legal data in a decentralized manner. It plays a key role in building and maintaining the Legal Intelligence Layer of the DataHive network.

## Technical Specifications

The LN1 Legalese Node employs a modular, microservices-based architecture with the following core components:

* Universal Core Processing Unit (UCPU) - [`/src/core/processing-unit`](/src/core/processing-unit)
* Legal Data Indexer - [`/src/core/legal-indexer`](/src/core/legal-indexer)
* Compliance Engine - [`/src/core/compliance-engine`](/src/core/compliance-engine)
* Blockchain Interface - [`/src/core/blockchain-interface`](/src/core/blockchain-interface)
* Storage Layer - [`/src/storage`](/src/storage)
* API Gateway - [`/src/api/gateway`](/src/api/gateway)

For detailed documentation, please refer to:
* [Architecture Overview](/docs/architecture/system-overview.md)
* [API Documentation](/docs/api/rest-api.md)
* [Deployment Guide](/docs/deployment/installation.md)

## Guide for Node Operators

### For Windows and Linux Users:
1. Download the appropriate installer from our [releases page](https://github.com/datahiv3/ln1-public/releases)
2. Run the installer and follow the on-screen instructions
3. For detailed setup instructions, see our [Installation Guide](/docs/deployment/installation.md)

### For Advanced Users:
1. Ensure Git is installed on your system
2. Open your terminal or command prompt
3. Clone the repository:
```bash
git clone https://github.com/datahiv3/ln1-public.git
```
4. Follow the manual setup instructions in [`/docs/deployment/installation.md`](/docs/deployment/installation.md)

## Smart Contracts

Our core smart contracts can be found in the [`/contracts`](/contracts) directory:
* Node Registry - [`/contracts/core/NodeRegistry.sol`](/contracts/core/NodeRegistry.sol)
* Staking Contract - [`/contracts/core/StakingContract.sol`](/contracts/core/StakingContract.sol)
* Governance Controller - [`/contracts/governance/GovernanceController.sol`](/contracts/governance/GovernanceController.sol)

## Development

* [Development Guide](/docs/guides/node-operators.md)
* [API Documentation](/docs/api/rest-api.md)
* [Testing Guidelines](/test/README.md)
* [Docker Setup](/docker/README.md)

## Contributing

We welcome contributions from the community! Please read our [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on:
* Code Style Guidelines
* Pull Request Process
* Development Setup
* Testing Requirements

## Support

If you encounter any issues:
* Check our [Troubleshooting Guide](/docs/guides/troubleshooting.md)
* Open an issue in this repository
* Review existing [documentation](/docs)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Stay Connected

* Follow us on Twitter: [@GetDataHive](https://x.com/getdatahive)
* Join our Telegram community: [DataHive Official](https://t.me/datahiveofficial)
* View our [Security Audits](/docs/security/audits.md)
* Check our [Development Roadmap](/docs/roadmap.md)

Thank you for your interest in the LN1 Legalese Node project. Together, we're shaping the future of decentralized legal intelligence!