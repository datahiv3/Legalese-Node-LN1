# LN1 Infrastructure Setup Guide

## System Requirements

### Hardware Requirements

```python
class NodeRequirements:
    MINIMUM_SPECS = {
        "cpu": {
            "cores": 4,
            "architecture": "x86_64",
            "speed": "2.5GHz"
        },
        "memory": {
            "ram": "16GB",
            "type": "DDR4"
        },
        "storage": {
            "capacity": "500GB",
            "type": "SSD",
            "iops": 3000
        },
        "network": {
            "bandwidth": "100Mbps",
            "type": "dedicated"
        }
    }
```

### Network Requirements

- Public IPv4 address
- Open ports:
  - 30303 (P2P)
  - 8545 (RPC)
  - 8546 (WebSocket)
  - 9090 (Metrics)

## Installation Steps

### 1. Base System Setup

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install dependencies
sudo apt install -y \
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

# Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.0.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### 3. Node Setup

```bash
# Clone repository
git clone https://github.com/datahiv3/Legalese-Node-LN1.git
cd Legalese-Node-LN1

# Create directories
mkdir -p data/{storage,logs,config}

# Set permissions
sudo chown -R $USER:$USER data/
```

## Configuration

### Environment Setup

```bash
# Copy example configuration
cp config/example.env .env

# Edit configuration
nano .env

# Required variables
NODE_ID=your_node_id
NETWORK=testnet
RPC_ENDPOINT=https://sepolia.optimism.io
API_KEY=your_api_key
```

### Network Configuration

```python
class NetworkConfig:
    def __init__(self):
        self.network_params = {
            'chain_id': 11155420,  # OP Sepolia
            'p2p_port': 30303,
            'rpc_port': 8545,
            'ws_port': 8546,
            'metrics_port': 9090
        }
```

## Security Setup

### SSL/TLS Configuration

```bash
# Generate SSL certificate
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout config/ssl/private.key \
    -out config/ssl/certificate.crt
```

### Firewall Setup

```bash
# Configure UFW
sudo ufw allow 30303/tcp
sudo ufw allow 8545/tcp
sudo ufw allow 8546/tcp
sudo ufw allow 9090/tcp
sudo ufw enable
```

## Container Deployment

### Docker Compose Configuration

```yaml
version: '3.8'
services:
  ln1_node:
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - ./data:/data
      - ./config:/config
    ports:
      - "8545:8545"
      - "8546:8546"
      - "30303:30303"
      - "9090:9090"
    environment:
      - NODE_ENV=production
    restart: unless-stopped
```

### Start Services

```bash
# Build and start containers
docker-compose up -d

# Check logs
docker-compose logs -f
```

## Monitoring Setup

### Prometheus Configuration

```yaml
# prometheus.yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'ln1_node'
    static_configs:
      - targets: ['localhost:9090']
```

### Grafana Setup

```bash
docker run -d \
  -p 3000:3000 \
  --name grafana \
  grafana/grafana
```

## Post-Installation

### Health Check

```python
class HealthChecker:
    async def verify_installation(self):
        return {
            'node_status': self.check_node_status(),
            'network_connection': self.verify_network(),
            'storage_access': self.check_storage(),
            'api_availability': self.verify_api()
        }
```

### Backup Configuration

```bash
# Create backup script
cat > backup.sh << 'EOF'
#!/bin/bash
backup_dir="/backup/ln1"
mkdir -p $backup_dir
tar -czf $backup_dir/config-$(date +%Y%m%d).tar.gz config/
tar -czf $backup_dir/data-$(date +%Y%m%d).tar.gz data/
EOF

chmod +x backup.sh
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
# View logs
docker-compose logs -f

# Export logs
docker-compose logs > node_logs.txt
```

## Maintenance

### Regular Tasks

- Monitor system resources
- Check log files
- Update security patches
- Backup configuration
- Verify node status

### Update Procedure

```bash
# Update repository
git pull

# Rebuild containers
docker-compose build
docker-compose up -d