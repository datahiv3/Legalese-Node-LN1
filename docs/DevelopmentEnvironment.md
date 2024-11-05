# LN1 Development Environment

Complete development environment setup for the DataHive LN1 Node, covering infrastructure, protocol, and AI components. For detailed system architecture, see [system-overview.md](./docs/architecture/system-overview.md).

## System Requirements

### Hardware Specifications
- CPU: 8+ cores recommended
- RAM: 32GB minimum (64GB recommended)
- Storage: 500GB NVMe SSD minimum
- GPU: NVIDIA GPU with 8GB+ VRAM for AI training (optional)
- Network: High-speed internet connection

### Operating System
- [Ubuntu 22.04 LTS](https://ubuntu.com/download/desktop) (primary recommended)
- [macOS 12+ Monterey or later](https://support.apple.com/macos) (supported)
- [Windows 11 with WSL2](https://learn.microsoft.com/en-us/windows/wsl/install) (supported)

## Core Development Stack

### Language Runtimes
```bash
# Python Environment
python3.11
pip
virtualenv

# Node.js Environment
nvm install 18
npm install -g pnpm

# Rust Toolchain
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
rustup default stable
rustup component add rustfmt clippy

# Go Installation
wget https://go.dev/dl/go1.21.1.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.21.1.linux-amd64.tar.gz
```

For detailed language-specific setup, see [LANGUAGES.md](./docs/architecture/setup/LANGUAGES.md)

### Blockchain Development Tools
```bash
# Layer 2 Development
npm install -g @eth-optimism/sdk
npm install -g @arbitrum/sdk
npm install -g @0glabs/0g-ts-sdk

# Smart Contract Development
npm install -g hardhat
npm install -g truffle
cargo install foundry-rs

# Testing Frameworks
npm install -g ganache
```

For blockchain configuration details, see [BLOCKCHAIN.md](./docs/architecture/setup/BLOCKCHAIN.md)

### AI & Machine Learning Stack
```bash
# Core ML Libraries
pip install torch torchvision torchaudio
pip install tensorflow
pip install transformers
pip install sentence-transformers

# Legal AI Specific
pip install spacy
python -m spacy download en_legal_ner
pip install lexnlp
```

For AI model setup details, see [AI_SETUP.md](./docs/architecture/setup/AI_SETUP.md)

### Storage & Database
```bash
# Core Database
sudo apt install postgresql postgresql-contrib
sudo apt install redis-server

# IPFS & Storage
wget https://dist.ipfs.tech/kubo/v0.20.0/kubo_v0.20.0_linux-amd64.tar.gz
tar -xvzf kubo_v0.20.0_linux-amd64.tar.gz

# 0G Storage Integration
npm install @0glabs/0g-storage-client
```

## Development Environment Setup

### 1. Repository Setup
```bash
git clone https://github.com/datahiv3/Legalese-Node-LN1.git
cd Legalese-Node-LN1
```

### 2. Environment Configuration
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
pip install -r requirements-dev.txt

# Install pre-commit hooks
pre-commit install
```

### 3. Docker Environment
```yaml
version: '3.8'
services:
  ln1-node:
    build:
      context: .
      dockerfile: Dockerfile.dev
    ports:
      - "3000:3000"
      - "8545:8545"
    volumes:
      - .:/app
    environment:
      - NODE_ENV=development
      - ENABLE_TESTNET=true

  postgres:
    image: postgres:13
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:alpine
    ports:
      - "6379:6379"

  ipfs:
    image: ipfs/kubo:latest
    ports:
      - "4001:4001"
      - "8080:8080"
      - "5001:5001"

volumes:
  postgres_data:
```

### 4. Network Configuration

#### OP Sepolia Setup
```yaml
networks:
  op_sepolia:
    rpc_url: "https://sepolia-sequencer.optimism.io"
    chain_id: 11155420
    explorer: "https://sepolia-optimism.etherscan.io"
```

#### AltLayer Configuration
```yaml
networks:
  altlayer:
    rpc_url: "${ALTLAYER_RPC_URL}"
    chain_id: "${ALTLAYER_CHAIN_ID}"
```

### 5. IDE Configuration

#### VS Code Setup
```json
{
    "editor.formatOnSave": true,
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "rust-analyzer.checkOnSave.command": "clippy",
    "[python]": {
        "editor.defaultFormatter": "ms-python.black-formatter"
    },
    "[rust]": {
        "editor.defaultFormatter": "rust-lang.rust-analyzer"
    }
}
```

For detailed IDE setup, see [SETUP.md](./docs/guidelines/infrastructure/SETUP.md)

## Development Workflow

### Local Development
```bash
# Start development environment
docker-compose up -d

# Run development server
python manage.py runserver

# Access API documentation
open http://localhost:3000/docs
```

### Testing
```bash
# Run test suite
pytest

# Run specific components
pytest tests/protocol/
pytest tests/ai/
pytest tests/storage/

# Generate coverage report
pytest --cov=app --cov-report=html
```

## Documentation Resources

### Core Documentation
- [API Documentation](./docs/api/API.md)
- [Protocol Specification](./docs/api/SPEC.md)
- [Security Guidelines](./docs/guidelines/infrastructure/SECURITY.md)
- [Contributing Guide](./docs/guidelines/CONTRIBUTING.md)

### Component Documentation
- [Core Protocol Architecture](./docs/architecture/DEVELOPMENT.md)
- [Legal Intelligence Model](./docs/components/CURATOR.md)
- [Storage System](./docs/0g/STORAGE.md)
- [Node Operations](./docs/deployment/NODE_OPERATIONS.md)

## Support & Community
- [GitHub Issues](https://github.com/datahiv3/Legalese-Node-LN1/issues)
- [Development Discussions](https://github.com/datahiv3/Legalese-Node-LN1/discussions)
- [Technical Documentation](./docs/README.md)
