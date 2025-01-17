# Environment Setup Guide

Setting up the correct environment is essential for running and maintaining a node in the DataHive network. This guide provides step-by-step instructions to configure your local environment for optimal performance and compatibility.

---

## Prerequisites

### 1. **Operating System**
- Recommended:
  - Ubuntu 20.04 or later
  - Windows 10/11 Pro
  - macOS Big Sur or later

### 2. **Hardware Requirements**
- Refer to the [hardware guide](/docs/onboarding/hardware.md) for detailed specifications.

### 3. **Dependencies**
- Ensure the following software is installed:
  - Docker (latest version)
  - Node.js (v16 or higher)
  - Go (v1.19 or higher)
  - Rust (latest stable version)
  - Python (v3.9 or higher)

---

## Step-by-Step Environment Configuration

### 1. Install Essential Tools

#### For Linux:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y docker.io nodejs npm golang rustc python3 python3-pip
```

#### For macOS:
```bash
brew update
brew install docker node go rust python
```

#### For Windows:
1. Install [Docker Desktop](https://www.docker.com/products/docker-desktop/).
2. Download and install Node.js from [nodejs.org](https://nodejs.org/).
3. Install Go from [golang.org](https://golang.org/).
4. Install Rust using [rustup](https://rustup.rs/).
5. Ensure Python is installed via the Microsoft Store or [python.org](https://www.python.org/).

---

### 2. Configure Environment Variables

Create a `.env` file in your project directory with the following:
```env
NODE_ENV=production
PORT=3000
DATA_DIR=/path/to/data-directory
WALLET_ADDRESS=0xYourWalletAddress
RPC_URL=https://mainnet.infura.io/v3/your_project_id
```

Export the variables:
#### Linux/MacOS:
```bash
export $(cat .env | xargs)
```
#### Windows (PowerShell):
```powershell
Get-Content .env | ForEach-Object { Set-Content -Path env:\$($_ -split "=")[0] -Value (\$_ -split "=")[1] }
```

---

### 3. Set Up File Permissions

1. Ensure your node’s data directory is accessible:
```bash
sudo chmod -R 755 /path/to/data-directory
```

2. Verify Docker permissions:
```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

### 4. Install DataHive Node Software

Clone the DataHive repository:
```bash
git clone https://github.com/datahiv3/Legalese-Node-LN1.git
cd Legalese-Node-LN1
```

Install dependencies:
```bash
npm install
```

Run setup scripts:
```bash
npm run setup
```

---

## Testing the Environment

1. **Verify Docker Installation**:
```bash
docker --version
```

2. **Check Node.js Version**:
```bash
node -v
```

3. **Confirm Python Installation**:
```bash
python3 --version
```

4. **Run Node Diagnostics**:
```bash
npm run test
```

---

## Best Practices for Environment Maintenance

1. **Regular Updates**:
   - Keep your OS and software dependencies up to date.
   - Use `apt update && apt upgrade` (Linux) or `brew upgrade` (macOS) to update tools.

2. **Resource Monitoring**:
   - Use tools like `htop` or `Activity Monitor` to monitor CPU and memory usage.

3. **Backup Configurations**:
   - Periodically backup your `.env` file and configuration settings.

4. **Secure Your Environment**:
   - Use firewalls and anti-malware tools to protect your system.

---

## Troubleshooting

| **Issue**                 | **Solution**                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| Docker not running        | Ensure the Docker service is started: `sudo systemctl start docker`.       |
| Missing dependencies      | Reinstall using package managers like `apt`, `brew`, or manual downloads.  |
| Environment variable errors | Verify `.env` file paths and syntax.                                      |

---

## Support and Resources

- **Documentation**:
  - Access additional setup resources in the [onboarding documentation](/docs/onboarding/overview.md).
- **Community Forums**:
  - Engage with other operators in the [community forums](/docs/onboarding/community/forums.md).
- **Technical Support**:
  - Submit tickets for assistance through the [support portal](/docs/onboarding/support/tickets.md).

---

Setting up your environment is the first step toward successfully running a DataHive node. For additional guidance, visit the [DataHive Node Registration Portal](https://www.datahive.network/nodes).
