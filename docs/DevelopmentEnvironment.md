# DataHive LN1 Node Development Environment

Complete development environment setup for the DataHive LN1 Node, covering infrastructure, protocol, and AI components. For detailed system architecture, see [ARCHITECTURE.md](./docs/architecture/system-overview.md).

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

#### Installation Guides
- [Ubuntu 22.04 LTS Installation Guide](https://ubuntu.com/tutorials/install-ubuntu-desktop)
- [WSL2 Setup Guide](https://learn.microsoft.com/en-us/windows/wsl/install)

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

For detailed language-specific setup, see [LANGUAGES.md](./docs/setup/LANGUAGES.md)

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

For blockchain configuration details, see [BLOCKCHAIN.md](./docs/setup/BLOCKCHAIN.md)

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

For AI model setup details, see [AI_SETUP.md](./docs/setup/AI_SETUP.md)

### Database & Storage
```bash
# Core Database
sudo apt install postgresql postgresql-contrib
sudo apt install redis-server

# IPFS & Storage
wget https://dist.ipfs.tech/kubo/v0.20.0/kubo_v0.20.0_linux-amd64.tar.gz
tar -xvzf kubo_v0.20.0_linux-amd64.tar.gz
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

### 4. IDE Configuration

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

For detailed IDE setup, see [IDE_SETUP.md](./docs/setup/IDE_SETUP.md)

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

## Additional Resources

### Documentation
- [API Documentation](./docs/api/API.md)
- [Protocol Specification](./docs/protocol/SPEC.md)
- [Security Guidelines](./docs/security/SECURITY.md)
- [Contributing Guide](./docs/CONTRIBUTING.md)

## Support Channels
- [GitHub Issues](https://github.com/datahiv3/Legalese-Node-LN1/issues) - Bug reports and feature requests
- [Development Discussions](https://github.com/datahiv3/Legalese-Node-LN1/discussions) - Technical discussions and community chat
- [Technical Documentation](./docs/README.md) - Comprehensive development guides

## Related Components
- [Core Protocol Architecture](./docs/architecture/PROTOCOL.md)
- [Legal Intelligence Model](./docs/ai/LEGAL_AI.md)
- [Storage System](./docs/storage/STORAGE.md)
- [Node Operations](./docs/deployment/NODE_OPERATIONS.md)
