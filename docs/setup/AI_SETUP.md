# AI Setup Documentation

## Overview

This guide provides step-by-step instructions for setting up the AI components of the LN1 system. It covers the installation and configuration of necessary tools and libraries to ensure a seamless integration of AI capabilities within the DataHive ecosystem.

## Prerequisites

Before setting up the AI components, ensure you have the following:

- **Python 3.8+**: Required for running AI scripts and models.
- **Node.js 16+**: For managing dependencies and running supporting scripts.
- **Docker**: To containerize and manage AI services.
- **Git**: For version control and repository management.

## Installation Steps

### 1. Clone the Repository

Start by cloning the LN1 repository to your local machine:

```bash
git clone https://github.com/datahiv3/ln1-public.git
cd ln1-public
```

### 2. Set Up Python Environment

Create a virtual environment and install Python dependencies:

```bash
python -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`
pip install -r requirements.txt
```

### 3. Install Node.js Dependencies

Navigate to the project directory and install Node.js dependencies:

```bash
npm install
```

### 4. Configure Docker

Ensure Docker is running and build the necessary containers:

```bash
docker-compose up --build
```

### 5. Environment Configuration

Copy the example environment file and configure it as needed:

```bash
cp .env.example .env
# Edit .env with your preferred settings
```

## Running AI Services

Once everything is set up, you can start the AI services using Docker:

```bash
docker-compose up ai-services
```

This command will launch all AI-related services, including model training, inference, and data processing components.

## Verification

To verify that the setup is successful, run the test suite to ensure all components are functioning correctly:

```bash
npm run test
```

## Troubleshooting

- **Docker Issues**: Ensure Docker is installed correctly and has sufficient resources allocated.
- **Dependency Errors**: Double-check that all dependencies are installed with compatible versions.
- **Environment Variables**: Ensure all required environment variables are set in your `.env` file.

