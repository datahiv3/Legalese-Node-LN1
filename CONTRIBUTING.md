# Contributing to LN1

## Overview

Welcome to the LN1 (Legalese Node) project. This document provides guidelines for contributing to the development of our decentralized legal intelligence infrastructure.

## Development Setup

### Prerequisites

```bash
# Required Software
- Python 3.9+
- Node.js 16+
- Docker 20.10+
- Git

# Development Tools
- Visual Studio Code (recommended)
- Python virtual environment
- Docker Compose
```

### Initial Setup

```bash
# Clone repository
git clone https://github.com/datahiv3/Legalese-Node-LN1.git
cd Legalese-Node-LN1

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Unix
.\venv\Scripts\activate   # Windows

# Install dependencies
pip install -r requirements.txt
pip install -r requirements-dev.txt
```

## Code Standards

### Python Style Guide

```python
# Example of proper code style
class DocumentProcessor:
    """
    Process legal documents according to LN1 standards.
    """
    def __init__(self):
        self.validator = DocumentValidator()
        self.indexer = DocumentIndexer()

    async def process_document(self, document: Document) -> ProcessedDocument:
        """
        Process a document through the validation pipeline.
        
        Args:
            document: Input document to process
            
        Returns:
            ProcessedDocument: Validated and processed document
        """
        validated = await self.validator.validate(document)
        return await self.indexer.index(validated)
```

### Solidity Style Guide

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract LN1Validator {
    mapping(address => bool) public validators;
    
    event ValidationSubmitted(bytes32 indexed documentHash);
    
    modifier onlyValidator() {
        require(validators[msg.sender], "Not authorized");
        _;
    }
}
```

## Git Workflow

### Branch Naming

- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation updates
- `refactor/` - Code refactoring
- `test/` - Test additions or modifications

### Commit Messages

Use conventional commit format:
```bash
# Format
<type>(<scope>): <description>

# Examples
feat(indexer): add legal document parsing
fix(validator): resolve consensus deadlock
docs(api): update endpoint documentation
```

## Testing Requirements

### Unit Tests

```python
class TestDocumentProcessor(unittest.TestCase):
    def setUp(self):
        self.processor = DocumentProcessor()
        
    async def test_document_processing(self):
        document = create_test_document()
        result = await self.processor.process_document(document)
        self.assertEqual(result.status, "PROCESSED")
```

### Integration Tests

```python
@pytest.mark.integration
async def test_validation_flow():
    async with TestClient(app) as client:
        response = await client.post(
            "/validation/submit",
            json={"document_id": "test_doc"}
        )
        assert response.status_code == 200
```

## Documentation

### Code Documentation

- Use descriptive variable names
- Add comments for complex logic
- Include type hints
- Write comprehensive docstrings

### API Documentation

```python
@router.post("/documents")
async def create_document(
    document: DocumentCreate,
    current_user: User = Depends(get_current_user)
) -> DocumentResponse:
    """
    Create a new legal document.
    
    Args:
        document: Document creation model
        current_user: Authenticated user
        
    Returns:
        DocumentResponse: Created document details
    """
    pass
```

## Pull Request Process

1. Create feature branch
2. Implement changes
3. Add/update tests
4. Update documentation
5. Submit PR with detailed description

### PR Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] New feature
- [ ] Bug fix
- [ ] Documentation update
- [ ] Performance improvement

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] All tests passing

## Documentation
- [ ] Code documentation updated
- [ ] API documentation updated
- [ ] README updated if needed
```

## Security Guidelines

- Follow OWASP security guidelines
- Implement input validation
- Use secure dependencies
- Regular security audits
- Report security issues privately

## Community Guidelines

- Be respectful and inclusive
- Follow project guidelines
- Help others learn
- Provide constructive feedback
- Participate in discussions

## Getting Help

- Review existing documentation
- Check GitHub issues
- Join Discord community
- Attend community calls

## License

All contributions to LN1 are subject to the project's MIT license with additional terms for network participation.