
# DataHive LN1 Node Development Environment

This guide provides a complete development environment setup for the DataHive LN1 Node, covering infrastructure, protocol, AI components, and blockchain requirements. It includes details on system requirements, environment setup, dependency management, testing, and troubleshooting. For a deeper understanding of the system architecture, refer to the [ARCHITECTURE.md](./docs/architecture/system-overview.md) file.

## Table of Contents

1. [System Requirements](#system-requirements)
2. [Core Development Stack](#core-development-stack)
3. [Environment Setup](#environment-setup)
4. [Running the Development Environment](#running-the-development-environment)
5. [Testing and Quality Assurance](#testing-and-quality-assurance)
6. [Troubleshooting and Optimization](#troubleshooting-and-optimization)
7. [Contributing](#contributing)
8. [Additional Resources](#additional-resources)
9. [Support Channels](#support-channels)

## System Requirements

### Hardware Specifications
- **CPU**: 8+ cores (recommended)
- **RAM**: 32GB minimum, 64GB recommended
- **Storage**: 500GB NVMe SSD minimum
- **GPU**: NVIDIA GPU with 8GB+ VRAM for AI model training (optional)
- **Network**: High-speed internet connection

### Supported Operating Systems
- **Ubuntu 22.04 LTS** (primary recommended) - [Installation Guide](https://ubuntu.com/tutorials/install-ubuntu-desktop)
- **macOS 12+ Monterey or later** (supported) - [Support](https://support.apple.com/macos)
- **Windows 11 with WSL2** (supported) - [WSL2 Setup Guide](https://learn.microsoft.com/en-us/windows/wsl/install)

## Core Development Stack

### Language Runtimes and Package Managers

1. **Python Environment**:
    ```bash
    python3.11
    pip
    virtualenv
    ```

2. **Node.js Environment**:
    ```bash
    nvm install 18
    npm install -g pnpm
    ```

3. **Rust Toolchain**:
    ```bash
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    rustup default stable
    rustup component add rustfmt clippy
    ```

4. **Go Installation**:
    ```bash
    wget https://go.dev/dl/go1.21.1.linux-amd64.tar.gz
    sudo tar -C /usr/local -xzf go1.21.1.linux-amd64.tar.gz
    ```

### Blockchain Development Tools

- **Layer 2 Development**:
    ```bash
    npm install -g @eth-optimism/sdk @arbitrum/sdk @0glabs/0g-ts-sdk
    ```

- **Smart Contract Development**:
    ```bash
    npm install -g hardhat truffle
    cargo install foundry-rs
    ```

- **Testing Frameworks**:
    ```bash
    npm install -g ganache
    ```

### AI & Machine Learning Libraries

```bash
pip install torch torchvision torchaudio tensorflow transformers sentence-transformers spacy lexnlp
python -m spacy download en_legal_ner
```

### Database & Storage Tools

- **PostgreSQL**:
    ```bash
    sudo apt install postgresql postgresql-contrib
    ```

- **Redis**:
    ```bash
    sudo apt install redis-server
    ```

- **IPFS**:
    ```bash
    wget https://dist.ipfs.tech/kubo/v0.20.0/kubo_v0.20.0_linux-amd64.tar.gz
    tar -xvzf kubo_v0.20.0_linux-amd64.tar.gz
    ```

---

## Environment Setup

### 1. Clone the Repository

```bash
git clone https://github.com/datahiv3/Legalese-Node-LN1.git
cd Legalese-Node-LN1
```

### 2. Configure Environment Variables

1. Copy the `.env.example` file to `.env`:
    ```bash
    cp .env.example .env
    ```

2. Update `.env` with your local settings:
    - **DATABASE_URL**: PostgreSQL database URL.
    - **REDIS_URL**: Redis server URL.
    - **IPFS_URL**: IPFS server URL.
    - **BLOCKCHAIN_PROVIDER_URL**: URL for connecting to OP Sepolia testnet.

    Refer to [ENVIRONMENT.md](./docs/setup/ENVIRONMENT.md) for more detailed configurations.

### 3. Install Dependencies

1. **Python Dependencies**:
    ```bash
    python -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
    pip install -r requirements-dev.txt
    ```

2. **Node.js Dependencies**:
    ```bash
    pnpm install
    ```

3. **Pre-Commit Hooks**:
    ```bash
    pre-commit install
    ```

### 4. Docker Setup

For containerized environments:

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
    environment:
      - NODE_ENV=development
      - ENABLE_TESTNET=true
  postgres:
    image: postgres:13
    ports:
      - "5432:5432"
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
```

---

## Running the Development Environment

### Start Docker Environment

```bash
docker-compose up -d
```

### Run Development Server

```bash
python manage.py runserver
```

Access the API documentation at [http://localhost:3000/docs](http://localhost:3000/docs).

---

## Testing and Quality Assurance

### Run Tests

1. **Complete Test Suite**:
    ```bash
    pytest
    ```

2. **Specific Component Tests**:
    ```bash
    pytest tests/protocol/
    pytest tests/ai/
    pytest tests/storage/
    ```

3. **Generate Coverage Report**:
    ```bash
    pytest --cov=app --cov-report=html
    ```

### Linting and Code Formatting

1. **Python Formatting**:
    ```bash
    black .
    ```

2. **Rust Formatting**:
    ```bash
    cargo fmt
    cargo clippy
    ```

## Troubleshooting and Optimization

- **Docker-WSL2 Performance**:
    - Allocate more memory and CPU in Docker settings for better performance.
    - Check integration with WSL2 if running on Windows.

- **Database Connectivity**:
    - Verify `.env` settings for `DATABASE_URL` and ensure PostgreSQL is running.
    - Check Docker logs:
      ```bash
      docker-compose logs -f postgres
      ```

- **Blockchain Testnet**:
    - Ensure access to the OP Sepolia testnet and add any required API keys to the `.env`.

## Contributing

Please refer to the [CONTRIBUTING.md](./docs/CONTRIBUTING.md) file for guidelines on contributing to this project, including coding standards, commit message format, and code review process.

## Additional Resources

- [API Documentation](./docs/api/API.md)
- [Protocol Specification](./docs/protocol/SPEC.md)
- [Security Guidelines](./docs/security/SECURITY.md)

## Support Channels

- [GitHub Issues](https://github.com/datahiv3/Legalese-Node-LN1/issues) - Report bugs or request features
- [Development Discussions](https://github.com/datahiv3/Legalese-Node-LN1/discussions) - Community and technical discussions
- [Technical Documentation](./docs/README.md) - Complete development documentation
