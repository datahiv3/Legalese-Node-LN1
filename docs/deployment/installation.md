# LN1 Node Installation Guide

## Prerequisites

### System Requirements

- **Hardware**
  - CPU: 4+ cores
  - RAM: 16GB minimum
  - Storage: 500GB SSD
  - Network: 100Mbps dedicated connection

- **Software**
  - Ubuntu 20.04 LTS or later
  - Docker 20.10+
  - Node.js 16+
  - Python 3.9+

### Network Requirements

```bash
# Required open ports
- 30303 (P2P)
- 8545 (RPC)
- 8546 (WebSocket)
- 9090 (Metrics)
```

## Installation Steps

### 1. System Preparation

```bash
# Update system packages
sudo apt-get update
sudo apt-get upgrade -y

# Install system dependencies
sudo apt-get install -y \
    build-essential \
    curl \
    git \
    python3-pip \
    nodejs \
    npm
```

### 2. Docker Installation

```bash
# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Add user to docker group
sudo usermod -aG docker $USER

# Start Docker service
sudo systemctl enable docker
sudo systemctl start docker
```

### 3. Node Setup

```bash
# Clone repository
git clone https://github.com/datahiv3/Legalese-Node-LN1.git
cd Legalese-Node-LN1

# Install dependencies
pip install -r requirements.txt
npm install
```

### 4. Configuration

```bash
# Copy example configuration
cp config/example.env .env

# Edit configuration file
nano .env

# Configuration parameters
NODE_ID=unique_node_id
NETWORK=testnet
RPC_ENDPOINT=https://sepolia.optimism.io
API_KEY=your_api_key
```

## Network Configuration

### OP Sepolia Setup

```python
class NetworkConfig:
    def __init__(self):
        self.chain_id = 11155420
        self.network = "testnet"
        self.rpc_url = "https://sepolia.optimism.io"
```

### 0G Network Integration

```bash
# Install 0G client
npm install @0g/client

# Configure 0G connection
cp config/0g-config.example.json config/0g-config.json
nano config/0g-config.json
```

## Security Setup

### SSL/TLS Configuration

```bash
# Generate SSL certificate
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout config/private.key \
    -out config/certificate.crt
```

### Firewall Configuration

```bash
# Configure UFW
sudo ufw allow 30303/tcp
sudo ufw allow 8545/tcp
sudo ufw allow 8546/tcp
sudo ufw allow 9090/tcp
sudo ufw enable
```

## Node Initialization

### Start Node

```bash
# Build Docker containers
docker-compose build

# Start services
docker-compose up -d
```

### Verify Installation

```bash
# Check node status
curl http://localhost:8545/status

# Check logs
docker-compose logs -f
```

## Post-Installation

### Health Check

```python
class HealthCheck:
    def verify_installation(self):
        return {
            'node_status': self.check_node_status(),
            'network_connection': self.verify_network(),
            'storage_access': self.check_storage(),
            'api_availability': self.verify_api()
        }
```

### Monitor Setup

```bash
# Install monitoring tools
docker-compose -f docker-compose.monitoring.yml up -d

# Access dashboard
# Navigate to http://localhost:3000
```

## Troubleshooting

### Common Issues

1. **Connection Issues**
   - Verify network configuration
   - Check firewall settings
   - Validate RPC endpoint

2. **Storage Problems**
   - Check disk space
   - Verify permissions
   - Validate mount points

### Logging

```bash
# View real-time logs
docker-compose logs -f

# Check specific service
docker-compose logs -f node

# Export logs
docker-compose logs > node_logs.txt
```

## Maintenance

### Backup Procedures

```bash
# Backup configuration
./scripts/backup-config.sh

# Backup data
./scripts/backup-data.sh
```

### Update Procedures

```bash
# Update node software
git pull
docker-compose build
docker-compose up -d

# Update dependencies
pip install -r requirements.txt --upgrade
npm update
```

## Additional Resources

- [Technical Documentation](/docs/technical/ARCHITECTURE.md)
- [API Documentation](/docs/api/ENDPOINTS.md)
- [Security Guidelines](/docs/infrastructure/SECURITY.md)
- [Node Operations](/docs/deployment/NODE_OPERATIONS.md)