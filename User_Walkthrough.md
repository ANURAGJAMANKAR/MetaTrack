# PAP-filemeta

A comprehensive file metadata management system with tagging, search, and validation capabilities. PAP-filemeta provides a powerful CLI interface, FastAPI backend, and Python package for managing file metadata with advanced tagging and search functionality.

## 🚀 Features

- **File Metadata Management**: Add, update, delete, and retrieve file metadata
- **Advanced Tagging System**: Flexible tag management with key-value pairs
- **Powerful Search**: Search files by tags, metadata, and content
- **Data Validation**: Validate file integrity and metadata consistency
- **Export/Import**: Backup and restore metadata in JSON format
- **Multiple Interfaces**: CLI, FastAPI REST API, and Python package
- **Database Support**: Configurable database backend for metadata storage

## 📦 Installation

### From PyPI

```bash
pip3 install PAP-filemeta
```

### From Source

```bash
git clone https://github.com/your-org/PAP-filemeta.git
cd PAP-filemeta
pip3 install -e .
```

## 🔧 Configuration

### Database Setup

Before using PAP-filemeta, configure your database connection:

```bash
# Set database URL (required)
export DATABASE_URL="sqlite:///filemeta.db"
# or for PostgreSQL
export DATABASE_URL="postgresql://user:password@localhost/filemeta"
# or for MySQL
export DATABASE_URL="mysql://user:password@localhost/filemeta"
```

### Initialize Database

```bash
filemeta init
```

## 🖥️ CLI Usage

### Basic Commands

#### List Files

```bash
# List all files with metadata
filemeta list

# List files with summary view
filemeta list -s
```

#### Add Files

```bash
# Create a test file
echo "test file content" > test.txt

# Add file with tags
filemeta add test.txt -t tag1=papil -t tag2=papil2

# Add file with multiple tags and metadata
filemeta add document.pdf -t category=work -t priority=high -t author="John Doe"
```

#### Retrieve Files

```bash
# Get file by ID
filemeta get 17

# Get file with detailed metadata
filemeta get 17 --verbose
```

#### Search Files

```bash
# Search by tag value
filemeta search -k papil2

# Search with full details
filemeta search -k papil2 --full

# Search by multiple criteria
filemeta search -k category=work -k priority=high

# Search with wildcards
filemeta search -k "author=John*"
```

#### Update Files

```bash
# Update specific tag
filemeta update 17 -t tag1=papil123

# Remove a tag
filemeta update 17 -r tag1

# Overwrite all tags
filemeta update 17 --overwrite -t tag1=papil12345 -t tag2=Verma

# Add new tag to existing ones
filemeta update 17 -t tag3=verma584
```

#### Delete Files

```bash
# Delete file metadata
filemeta delete 17

# Delete multiple files
filemeta delete 17 18 19

# Force delete (skip confirmation)
filemeta delete 17 --force
```

#### Rename Files

```bash
# Rename file
filemeta rename 17 new_file_name.txt

# Rename with path update
filemeta rename 17 /new/path/new_file_name.txt
```

### Tag Management

```bash
# List all tags
filemeta tags list

# List unique tags only
filemeta tags list --unique

# List unique tags with sorting
filemeta tags list --unique --sort key --order asc --limit 10
filemeta tags list --unique --sort key --order desc --limit 10

# List tags with value sorting
filemeta tags list --unique --sort value --order asc --limit 20

# Filter tags by pattern
filemeta tags list --pattern "category=*"
```

### Data Export/Import

```bash
# Export metadata to JSON
filemeta export metadata_backup.json

# View exported data
cat metadata_backup.json

# Import metadata from JSON
filemeta import metadata_backup.json

# Import with merge strategy
filemeta import metadata_backup.json --merge
```

### Validation

```bash
# Validate all files
filemeta validate --all

# Validate specific file by ID
filemeta validate --id 4

# Validate by filename
filemeta validate --filename "document.pdf"

# Validate with auto-fix
filemeta validate --all --fix

# Validate and show detailed report
filemeta validate --all --verbose
```

### Advanced Features

```bash
# Statistics
filemeta stats

# Clean orphaned metadata
filemeta clean --orphaned

# Rebuild search index
filemeta reindex

# Show configuration
filemeta config show

# Set configuration
filemeta config set --max-file-size 100MB
```

## 🐍 Python Package Usage

### Basic Usage

```python
from pap_filemeta import FileMetaManager

# Initialize manager
manager = FileMetaManager(database_url="sqlite:///filemeta.db")

# Add file with tags
file_id = manager.add_file(
    "document.pdf",
    tags={"category": "work", "priority": "high"},
    metadata={"author": "John Doe", "created": "2024-01-01"}
)

# Get file metadata
file_info = manager.get_file(file_id)
print(f"File: {file_info.filename}")
print(f"Tags: {file_info.tags}")

# Search files
results = manager.search_files(tags={"category": "work"})
for result in results:
    print(f"Found: {result.filename}")

# Update file tags
manager.update_file(file_id, tags={"category": "personal"})

# Delete file
manager.delete_file(file_id)
```

### Advanced Usage

```python
from pap_filemeta import FileMetaManager, SearchQuery, ValidationReport

# Initialize with custom configuration
manager = FileMetaManager(
    database_url="postgresql://user:pass@localhost/filemeta",
    cache_size=1000,
    auto_validate=True
)

# Complex search
query = SearchQuery()
query.add_tag_filter("category", "work")
query.add_tag_filter("priority", "high")
query.add_filename_pattern("*.pdf")
query.set_date_range("2024-01-01", "2024-12-31")

results = manager.search(query)

# Batch operations
files_to_add = [
    {"filename": "doc1.pdf", "tags": {"type": "document"}},
    {"filename": "img1.jpg", "tags": {"type": "image"}},
]

file_ids = manager.add_files_batch(files_to_add)

# Validation
validation_report = manager.validate_all()
if validation_report.has_errors():
    for error in validation_report.errors:
        print(f"Error: {error}")

# Export/Import
manager.export_metadata("backup.json")
manager.import_metadata("backup.json", merge=True)
```

### Context Manager

```python
from pap_filemeta import FileMetaManager

# Use as context manager for automatic cleanup
with FileMetaManager("sqlite:///filemeta.db") as manager:
    file_id = manager.add_file("test.txt", tags={"temp": "true"})
    file_info = manager.get_file(file_id)
    print(f"Added: {file_info.filename}")
    # Database connection automatically closed
```

## 🌐 FastAPI Integration

### Basic FastAPI App

```python
from fastapi import FastAPI
from pap_filemeta.api import create_filemeta_router
from pap_filemeta import FileMetaManager

app = FastAPI(title="File Metadata API")

# Initialize manager
manager = FileMetaManager("sqlite:///filemeta.db")

# Add filemeta routes
filemeta_router = create_filemeta_router(manager)
app.include_router(filemeta_router, prefix="/api/v1/filemeta")

# Run with: uvicorn main:app --reload
```

### Custom FastAPI Integration

```python
from fastapi import FastAPI, HTTPException, Depends
from pap_filemeta import FileMetaManager
from typing import List, Dict, Any

app = FastAPI()
manager = FileMetaManager("sqlite:///filemeta.db")

@app.post("/files/")
async def add_file(
    filename: str,
    tags: Dict[str, str] = None,
    metadata: Dict[str, Any] = None
):
    try:
        file_id = manager.add_file(filename, tags=tags, metadata=metadata)
        return {"file_id": file_id, "status": "success"}
    except Exception as e:
        raise HTTPException(status_code=400, detail=str(e))

@app.get("/files/{file_id}")
async def get_file(file_id: int):
    file_info = manager.get_file(file_id)
    if not file_info:
        raise HTTPException(status_code=404, detail="File not found")
    return file_info.to_dict()

@app.get("/search/")
async def search_files(
    tags: str = None,
    filename: str = None,
    limit: int = 100
):
    results = manager.search_files(
        tags=parse_tags(tags) if tags else None,
        filename_pattern=filename,
        limit=limit
    )
    return [result.to_dict() for result in results]

def parse_tags(tags_str: str) -> Dict[str, str]:
    """Parse tags from query string format: key1=value1,key2=value2"""
    tags = {}
    for tag in tags_str.split(','):
        if '=' in tag:
            key, value = tag.split('=', 1)
            tags[key.strip()] = value.strip()
    return tags
```

## 📊 API Endpoints

When using the built-in FastAPI router, the following endpoints are available:

### Files
- `GET /files/` - List all files
- `POST /files/` - Add new file
- `GET /files/{file_id}` - Get file by ID
- `PUT /files/{file_id}` - Update file
- `DELETE /files/{file_id}` - Delete file
- `POST /files/{file_id}/rename` - Rename file

### Search
- `GET /search/` - Search files
- `POST /search/advanced` - Advanced search with complex queries

### Tags
- `GET /tags/` - List all tags
- `GET /tags/unique` - List unique tags
- `GET /tags/stats` - Tag statistics

### Validation
- `POST /validate/` - Validate files
- `GET /validate/{file_id}` - Validate specific file

### Export/Import
- `GET /export/` - Export metadata
- `POST /import/` - Import metadata

## 🔧 Configuration Options

### Environment Variables

```bash
# Database configuration
export DATABASE_URL="sqlite:///filemeta.db"
export DATABASE_POOL_SIZE=20
export DATABASE_TIMEOUT=30

# Cache configuration
export CACHE_SIZE=1000
export CACHE_TTL=3600

# File handling
export MAX_FILE_SIZE="100MB"
export ALLOWED_EXTENSIONS=".pdf,.doc,.txt,.jpg,.png"

# Search configuration
export SEARCH_INDEX_PATH="/tmp/filemeta_index"
export SEARCH_MAX_RESULTS=1000

# Logging
export LOG_LEVEL="INFO"
export LOG_FILE="/var/log/filemeta.log"
```

### Configuration File

Create `~/.filemeta/config.yaml`:

```yaml
database:
  url: "sqlite:///filemeta.db"
  pool_size: 20
  timeout: 30

cache:
  size: 1000
  ttl: 3600

files:
  max_size: "100MB"
  allowed_extensions:
    - ".pdf"
    - ".doc"
    - ".txt"
    - ".jpg"
    - ".png"

search:
  index_path: "/tmp/filemeta_index"
  max_results: 1000

logging:
  level: "INFO"
  file: "/var/log/filemeta.log"
```

## 🧪 Testing

### Unit Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=pap_filemeta

# Run specific test file
pytest tests/test_cli.py

# Run with verbose output
pytest -v
```

### Integration Tests

```bash
# Test CLI commands
pytest tests/integration/test_cli_integration.py

# Test API endpoints
pytest tests/integration/test_api_integration.py

# Test database operations
pytest tests/integration/test_database_integration.py
```

## 📈 Performance Tips

### Database Optimization

```python
# Use connection pooling for better performance
manager = FileMetaManager(
    database_url="postgresql://user:pass@localhost/filemeta",
    pool_size=20,
    pool_pre_ping=True
)

# Enable query optimization
manager.enable_query_cache(size=1000)

# Use batch operations for multiple files
manager.add_files_batch(files_data)
```

### Search Optimization

```python
# Create search indexes for better performance
manager.create_search_index()

# Use specific tag filters instead of wildcards
manager.search_files(tags={"category": "work"})  # Fast
manager.search_files(tags={"category": "*work*"})  # Slower
```

## 🐛 Troubleshooting

### Common Issues

1. **Database Connection Errors**
   ```bash
   # Check database URL
   echo $DATABASE_URL
   
   # Test connection
   filemeta config test-db
   ```

2. **File Not Found Errors**
   ```bash
   # Validate file existence
   filemeta validate --filename "missing_file.txt"
   
   # Clean orphaned metadata
   filemeta clean --orphaned
   ```

3. **Search Performance Issues**
   ```bash
   # Rebuild search index
   filemeta reindex
   
   # Check database statistics
   filemeta stats
   ```

### Debug Mode

```bash
# Enable debug logging
export LOG_LEVEL=DEBUG

# Run with verbose output
filemeta --verbose list

# Check configuration
filemeta config show
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and add tests
4. Run tests: `pytest`
5. Submit a pull request

### Development Setup

```bash
# Clone repository
git clone https://github.com/your-org/PAP-filemeta.git
cd PAP-filemeta

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install in development mode
pip install -e ".[dev]"

# Install pre-commit hooks
pre-commit install

# Run tests
pytest
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [Click](https://click.palletsprojects.com/) for CLI interface
- [FastAPI](https://fastapi.tiangolo.com/) for REST API
- [SQLAlchemy](https://www.sqlalchemy.org/) for database operations
- [Pydantic](https://pydantic-docs.helpmanual.io/) for data validation

## 📞 Support

- 📧 Email: support@pap-filemeta.com
- 🐛 Issues: [GitHub Issues](https://github.com/your-org/PAP-filemeta/issues)
- 📚 Documentation: [Read the Docs](https://pap-filemeta.readthedocs.io/)
- 💬 Community: [Discord](https://discord.gg/pap-filemeta)
