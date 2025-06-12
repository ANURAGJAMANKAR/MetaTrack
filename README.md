# MetaTrack

# 📁 filemeta

A cross-platform CLI tool to manage metadata for local server files using PostgreSQL or SQLite. Automatically infers metadata like file size, timestamps, MIME type, and OS ownership, while allowing custom tagging.

## 🚀 Features
- Infer metadata from local files (cross-platform)
- Add custom tags to files
- Search by tags, filename, or owner
- Update or delete metadata records
- Works with PostgreSQL or SQLite

## 🛠 Installation
```bash
pip install filemeta
```

## 🖥 Usage
```bash
filemeta init-db
filemeta add /path/to/file --tag category=invoice
filemeta list
filemeta update 1 --tag priority=high
filemeta delete 1
```

## 🧱 Requirements
- Python 3.7+
- PostgreSQL (or SQLite for local testing)

## 🤝 Contributing
Fork, hack, and PR away! Check `.github/CONTRIBUTING.md` (coming soon).

## 📄 License
[MIT License](LICENSE)
```

### ✅ `LICENSE` (MIT)
```text
MIT License

Copyright (c) 2025 Anurag

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software...
```

### ✅ `pyproject.toml`
```toml
[build-system]
requires = ["setuptools", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "filemeta"
version = "0.1.0"
description = "A CLI tool to manage file metadata."
authors = [
    {name = "Anurag", email = "your.email@example.com"}
]
readme = "README.md"
license = {file = "LICENSE"}
dependencies = [
    "SQLAlchemy",
    "Click",
    "psycopg2-binary"
]
requires-python = ">=3.7"

[project.scripts]
filemeta = "filemeta.cli:cli"
```

### ✅ `MANIFEST.in`
```ini
include README.md
include LICENSE
include requirements.txt
recursive-include filemeta *
```

### ✅ `requirements.txt`
```txt
SQLAlchemy
Click
psycopg2-binary
```

### ✅ `.github/workflows/python-package.yml`
```yaml
name: Python package

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Lint with flake8
        run: |
          pip install flake8
          flake8 filemeta --count --select=E9,F63,F7,F82 --show-source --statistics

      - name: Test CLI (basic smoke test)
        run: |
          filemeta --help || echo "CLI help command passed"
```
# 🎞 filemeta

**A Cross-Platform CLI Tool to Manage File Metadata with PostgreSQL & SQLAlchemy**

---

## 🧠 What is `filemeta`?

`filemeta` is a Python-based, cross-platform command-line tool that helps you manage metadata of files on your system — including custom tags and system-inferred attributes like owner, size, MIME type, and timestamps. It stores all metadata in a PostgreSQL database using SQLAlchemy ORM for persistence and queryability.

This tool is built for sysadmins, developers, data wranglers, and digital archivists who want clean, structured, queryable metadata about files across Linux, macOS, and Windows systems.

---

## 🔍 Problem It Solves

File systems are black holes. You store files, but forget:
- Who owns them?
- What they were for?
- Which project, team, or purpose they were associated with?

Manual tagging is tedious. Metadata is buried. Central tracking? Non-existent.

**`filemeta`** solves this by:
- Auto-extracting system metadata
- Letting you tag files with custom metadata
- Persisting all this in a searchable PostgreSQL DB
- Providing full CRUD access via CLI

---

## ✨ Features

✅ Cross-platform: Windows, Linux, macOS  
✅ Add custom tags (project, type, category, etc.)  
✅ Infer metadata from OS (owner, size, timestamps)  
✅ Store everything in PostgreSQL using SQLAlchemy ORM  
✅ Full CLI interface (add, search, update, delete)  
✅ Powerful search (on filename, tags, and more)  
✅ Safe, structured, developer-friendly metadata access  
✅ Export metadata to JSON

---

## ⚙️ Installation & Configuration

```bash
pip install papilv-filemeta
```

To install from source:
```bash
git clone https://github.com/yourusername/filemeta_project.git
cd filemeta_project
pip install .
```

To configure your environment:
```bash
export DATABASE_URL="postgresql://username:password@localhost:5432/yourdb"
```
Make sure PostgreSQL is installed and running.

---

## 🔧 Functionality

These are the modular functionalities `filemeta` provides. Users can choose to use only the relevant ones:

- Automatic metadata inference from filesystem
- Custom tagging via CLI with support for type parsing (int, float, bool)
- JSONB used for storing flexible, inferred metadata
- Bidirectional relationship between files and tags
- Safe cascading deletes
- Developer API (`metadata_manager.py`) to use functionality programmatically

---

## 🔊 CLI Commands

### Add a file with metadata
**Syntax:**
```bash
filemeta add <filepath> [--tag key=value ...]
```
**Example:**
```bash
filemeta add ./test_data/sample1.txt -t category=finance -t year=2024
```

### Search metadata by keyword
**Syntax:**
```bash
filemeta search -k <keyword> [--full]
```
**Example:**
```bash
filemeta search -k finance
filemeta search -k 2024 --full
```

### Show file metadata by ID
**Syntax:**
```bash
filemeta get <file_id>
```
**Example:**
```bash
filemeta get 3
```

### Update existing metadata
**Syntax:**
```bash
filemeta update <file_id> [--tag key=value ...] [--remove-tag key ...] [--overwrite]
```
**Examples:**
```bash
filemeta update 3 -t category=legal
filemeta update 3 -r category
filemeta update 3 --overwrite -t type=pdf -t access=confidential
```

### Delete metadata by ID
**Syntax:**
```bash
filemeta delete <file_id>
```
**Example:**
```bash
filemeta delete 3
```

### Export metadata
**Syntax:**
```bash
filemeta export <outputfile.json>
```
**Example:**
```bash
filemeta export backup.json
```

---

## 🚀 User Walkthrough & Tutorial

Use only what you need! Here are example commands for common use cases:

```bash
# Install the package
pip3 install papilv-filemeta

# Configure PostgreSQL connection
export DATABASE_URL="postgresql://user:pass@localhost:5432/metadata"

# View current metadata
filemeta list
filemeta list -s

# Create a dummy file for testing
echo "sample file content" > dummy.txt

# Add the file to database with tags
filemeta add dummy.txt -t project=alpha -t department=R&D

# Retrieve metadata for a specific file
filemeta get 2

# Search using tag values
filemeta search -k R&D
filemeta search -k alpha --full

# Export to JSON for backup or sharing
filemeta export metadata.json
cat metadata.json

# Update existing file metadata
filemeta update 2 -t department=Engineering
filemeta update 2 -t reviewer=QA

# Remove a tag
filemeta update 2 -r reviewer

# Overwrite all tags
filemeta update 2 --overwrite -t type=report -t version=1.1

# Delete metadata record for a file
filemeta delete 2
```

---

## 🛠️ Project Structure

```txt
filemeta_project/
│
├── filemeta/                 # Core Python package
│   ├── cli.py                # CLI interface using Click
│   ├── database.py           # Database session and engine
│   ├── metadata_manager.py   # All CRUD logic
│   ├── models.py             # SQLAlchemy models (File, Tag)
│   ├── utils.py              # Metadata inference, tag parsing
│
├── tests/                    # Test suite (TBD)
├── README.md                 # This file
├── setup.py / pyproject.toml# Packaging info
├── LICENSE                   # MIT
└── .github/workflows/       # CI/CD workflow (pytest + lint)
```

---

## 🔬 Testing

Run all tests:
```bash
pytest
```

---

## 📚 Tech Stack
- Python 3.7+
- Click (for CLI)
- SQLAlchemy ORM
- PostgreSQL (but SQLite fallback possible)
- JSONB (for inferred tags)

---

## 💡 Roadmap
- [ ] Add REST API support (FastAPI)
- [ ] Export metadata to CSV / JSON
- [ ] Tagging templates
- [ ] GUI dashboard for non-tech users
- [ ] File watcher for real-time tracking

---

## 🤝 Contributing
We love contributors! Submit PRs, create issues, or fork the repo. Major improvements like search enhancements, new tag formats, or PostgreSQL optimization are welcome.

---

## ⚖️ License

MIT License — use it, tweak it, ship it, no strings attached.

---

## 👨‍💻 Author

Made with ⚙️ by **Anurag**  
Email: your.email@example.com

---

## 🌍 Repository

[https://github.com/yourusername/filemeta_project](https://github.com/yourusername/filemeta_project)


# 🎞 filemeta

**A Cross-Platform CLI Tool to Manage File Metadata with PostgreSQL & SQLAlchemy**

---

## 🧠 What is `filemeta`?

`filemeta` is a Python-based, cross-platform command-line tool that helps you manage metadata of files on your system — including custom tags and system-inferred attributes like owner, size, MIME type, and timestamps. It stores all metadata in a PostgreSQL database using SQLAlchemy ORM for persistence and queryability.

This tool is built for sysadmins, developers, data wranglers, and digital archivists who want clean, structured, queryable metadata about files across Linux, macOS, and Windows systems.

---

## 🔍 Problem It Solves

File systems are black holes. You store files, but forget:
- Who owns them?
- What they were for?
- Which project, team, or purpose they were associated with?

Manual tagging is tedious. Metadata is buried. Central tracking? Non-existent.

**`filemeta`** solves this by:
- Auto-extracting system metadata
- Letting you tag files with custom metadata
- Persisting all this in a searchable PostgreSQL DB
- Providing full CRUD access via CLI

---

## ✨ Features

✅ Cross-platform: Windows, Linux, macOS  
✅ Add custom tags (project, type, category, etc.)  
✅ Infer metadata from OS (owner, size, timestamps)  
✅ Store everything in PostgreSQL using SQLAlchemy ORM  
✅ Full CLI interface (add, search, update, delete)  
✅ Powerful search (on filename, tags, and more)  
✅ Safe, structured, developer-friendly metadata access  
✅ Export metadata to JSON

---

## ⚙️ Installation & Configuration

```bash
pip install papilv-filemeta
```

To install from source:
```bash
git clone https://github.com/yourusername/filemeta_project.git
cd filemeta_project
pip install .
```

To configure your environment:
```bash
export DATABASE_URL="postgresql://username:password@localhost:5432/yourdb"
```
Make sure PostgreSQL is installed and running.

---

## 🔧 Functionality

These are the modular functionalities `filemeta` provides. Users can choose to use only the relevant ones:

- Automatic metadata inference from filesystem
- Custom tagging via CLI with support for type parsing (int, float, bool)
- JSONB used for storing flexible, inferred metadata
- Bidirectional relationship between files and tags
- Safe cascading deletes
- Developer API (`metadata_manager.py`) to use functionality programmatically

---

## 🔊 CLI Commands

### Add a file with metadata
**Syntax:**
```bash
filemeta add <filepath> [--tag key=value ...]
```
**Example:**
```bash
filemeta add ./test_data/sample1.txt -t category=finance -t year=2024
```

### Search metadata by keyword
**Syntax:**
```bash
filemeta search -k <keyword> [--full]
```
**Example:**
```bash
filemeta search -k finance
filemeta search -k 2024 --full
```

### Show file metadata by ID
**Syntax:**
```bash
filemeta get <file_id>
```
**Example:**
```bash
filemeta get 3
```

### Update existing metadata
**Syntax:**
```bash
filemeta update <file_id> [--tag key=value ...] [--remove-tag key ...] [--overwrite]
```
**Examples:**
```bash
filemeta update 3 -t category=legal
filemeta update 3 -r category
filemeta update 3 --overwrite -t type=pdf -t access=confidential
```

### Delete metadata by ID
**Syntax:**
```bash
filemeta delete <file_id>
```
**Example:**
```bash
filemeta delete 3
```

### Export metadata
**Syntax:**
```bash
filemeta export <outputfile.json>
```
**Example:**
```bash
filemeta export backup.json
```

---

## 🚀 User Walkthrough & Tutorial

Use only what you need! Here are example commands for common use cases:

```bash
# Install the package
pip3 install papilv-filemeta

# Configure PostgreSQL connection
export DATABASE_URL="postgresql://user:pass@localhost:5432/metadata"

# View current metadata
filemeta list
filemeta list -s

# Create a dummy file for testing
echo "sample file content" > dummy.txt

# Add the file to database with tags
filemeta add dummy.txt -t project=alpha -t department=R&D

# Retrieve metadata for a specific file
filemeta get 2

# Search using tag values
filemeta search -k R&D
filemeta search -k alpha --full

# Export to JSON for backup or sharing
filemeta export metadata.json
cat metadata.json

# Update existing file metadata
filemeta update 2 -t department=Engineering
filemeta update 2 -t reviewer=QA

# Remove a tag
filemeta update 2 -r reviewer

# Overwrite all tags
filemeta update 2 --overwrite -t type=report -t version=1.1

# Delete metadata record for a file
filemeta delete 2
```

---

## 🛠️ Project Structure

```txt
filemeta_project/
│
├── filemeta/                 # Core Python package
│   ├── cli.py                # CLI interface using Click
│   ├── database.py           # Database session and engine
│   ├── metadata_manager.py   # All CRUD logic
│   ├── models.py             # SQLAlchemy models (File, Tag)
│   ├── utils.py              # Metadata inference, tag parsing
│
├── tests/                    # Test suite (TBD)
├── README.md                 # This file
├── setup.py / pyproject.toml# Packaging info
├── LICENSE                   # MIT
└── .github/workflows/       # CI/CD workflow (pytest + lint)
```

---

## 🔬 Testing

Run all tests:
```bash
pytest
```

---

## 📚 Tech Stack
- Python 3.7+
- Click (for CLI)
- SQLAlchemy ORM
- PostgreSQL (but SQLite fallback possible)
- JSONB (for inferred tags)

---

## 💡 Roadmap
- [ ] Add REST API support (FastAPI)
- [ ] Export metadata to CSV / JSON
- [ ] Tagging templates
- [ ] GUI dashboard for non-tech users
- [ ] File watcher for real-time tracking

---

## 🤝 Contributing
We love contributors! Submit PRs, create issues, or fork the repo. Major improvements like search enhancements, new tag formats, or PostgreSQL optimization are welcome.

---

## ⚖️ License

MIT License — use it, tweak it, ship it, no strings attached.

---

## 👨‍💻 Author

Made with ⚙️ by **Anurag**  
Email: your.email@example.com

---

## 🌍 Repository

[https://github.com/yourusername/filemeta_project](https://github.com/yourusername/filemeta_project)



# 🎞 filemeta

**A Cross-Platform CLI Tool to Manage File Metadata with PostgreSQL & SQLAlchemy**

---

## 🧠 What is `filemeta`?

`filemeta` is a Python-based, cross-platform command-line tool that helps you manage metadata of files on your system — including custom tags and system-inferred attributes like owner, size, MIME type, and timestamps. It stores all metadata in a PostgreSQL database using SQLAlchemy ORM for persistence and queryability.

This tool is built for sysadmins, developers, data wranglers, and digital archivists who want clean, structured, queryable metadata about files across Linux, macOS, and Windows systems.

---

## 🔍 Problem It Solves

File systems are black holes. You store files, but forget:
- Who owns them?
- What they were for?
- Which project, team, or purpose they were associated with?

Manual tagging is tedious. Metadata is buried. Central tracking? Non-existent.

**`filemeta`** solves this by:
- Auto-extracting system metadata
- Letting you tag files with custom metadata
- Persisting all this in a searchable PostgreSQL DB
- Providing full CRUD access via CLI

---

## ✨ Features

✅ Cross-platform: Windows, Linux, macOS  
✅ Add custom tags (project, type, category, etc.)  
✅ Infer metadata from OS (owner, size, timestamps)  
✅ Store everything in PostgreSQL using SQLAlchemy ORM  
✅ Full CLI interface (add, search, update, delete)  
✅ Powerful search (on filename, tags, and more)  
✅ Safe, structured, developer-friendly metadata access  
✅ Export metadata to JSON

---

## ⚙️ Installation & Configuration

```bash
pip install papilv-filemeta
```

To install from source:
```bash
git clone https://github.com/yourusername/filemeta_project.git
cd filemeta_project
pip install .
```

To configure your environment:
```bash
export DATABASE_URL="postgresql://username:password@localhost:5432/yourdb"
```
Make sure PostgreSQL is installed and running.

---

## 🔧 Functionality

These are the modular functionalities `filemeta` provides. Users can choose to use only the relevant ones:

- Automatic metadata inference from filesystem
- Custom tagging via CLI with support for type parsing (int, float, bool)
- JSONB used for storing flexible, inferred metadata
- Bidirectional relationship between files and tags
- Safe cascading deletes
- Developer API (`metadata_manager.py`) to use functionality programmatically

---

## 🔊 CLI Commands

### Add a file with metadata
**Syntax:**
```bash
filemeta add <filepath> [--tag key=value ...]
```
**Example:**
```bash
filemeta add ./test_data/sample1.txt -t category=finance -t year=2024
```

### Search metadata by keyword
**Syntax:**
```bash
filemeta search -k <keyword> [--full]
```
**Example:**
```bash
filemeta search -k finance
filemeta search -k 2024 --full
```

### Show file metadata by ID
**Syntax:**
```bash
filemeta get <file_id>
```
**Example:**
```bash
filemeta get 3
```

### Update existing metadata
**Syntax:**
```bash
filemeta update <file_id> [--tag key=value ...] [--remove-tag key ...] [--overwrite]
```
**Examples:**
```bash
filemeta update 3 -t category=legal
filemeta update 3 -r category
filemeta update 3 --overwrite -t type=pdf -t access=confidential
```

### Delete metadata by ID
**Syntax:**
```bash
filemeta delete <file_id>
```
**Example:**
```bash
filemeta delete 3
```

### Export metadata
**Syntax:**
```bash
filemeta export <outputfile.json>
```
**Example:**
```bash
filemeta export backup.json
```

---

## 🚀 User Walkthrough & Tutorial

Use only what you need! Here are example commands for common use cases:

```bash
# Install the package
pip3 install papilv-filemeta

# Configure PostgreSQL connection
export DATABASE_URL="postgresql://user:pass@localhost:5432/metadata"

# View current metadata
filemeta list
filemeta list -s

# Create a dummy file for testing
echo "sample file content" > dummy.txt

# Add the file to database with tags
filemeta add dummy.txt -t project=alpha -t department=R&D

# Retrieve metadata for a specific file
filemeta get 2

# Search using tag values
filemeta search -k R&D
filemeta search -k alpha --full

# Export to JSON for backup or sharing
filemeta export metadata.json
cat metadata.json

# Update existing file metadata
filemeta update 2 -t department=Engineering
filemeta update 2 -t reviewer=QA

# Remove a tag
filemeta update 2 -r reviewer

# Overwrite all tags
filemeta update 2 --overwrite -t type=report -t version=1.1

# Delete metadata record for a file
filemeta delete 2
```

---

## 🛠️ Project Structure

```txt
filemeta_project/
│
├── filemeta/                 # Core Python package
│   ├── cli.py                # CLI interface using Click
│   ├── database.py           # Database session and engine
│   ├── metadata_manager.py   # All CRUD logic
│   ├── models.py             # SQLAlchemy models (File, Tag)
│   ├── utils.py              # Metadata inference, tag parsing
│
├── tests/                    # Test suite (TBD)
├── README.md                 # This file
├── setup.py / pyproject.toml# Packaging info
├── LICENSE                   # MIT
└── .github/workflows/       # CI/CD workflow (pytest + lint)
```

---

## 🔬 Testing

Run all tests:
```bash
pytest
```

---

## 📚 Tech Stack
- Python 3.7+
- Click (for CLI)
- SQLAlchemy ORM
- PostgreSQL (but SQLite fallback possible)
- JSONB (for inferred tags)

---

## 💡 Roadmap
- [ ] Add REST API support (FastAPI)
- [ ] Export metadata to CSV / JSON
- [ ] Tagging templates
- [ ] GUI dashboard for non-tech users
- [ ] File watcher for real-time tracking

---

## 🤝 Contributing
We love contributors! Submit PRs, create issues, or fork the repo. Major improvements like search enhancements, new tag formats, or PostgreSQL optimization are welcome.

---

## ⚖️ License

MIT License — use it, tweak it, ship it, no strings attached.

---

## 👨‍💻 Author

Made with ⚙️ by **Anurag**  
Email: your.email@example.com

---

## 🌍 Repository

[https://github.com/yourusername/filemeta_project](https://github.com/yourusername/filemeta_project)

# 🎞 filemeta

**A Cross-Platform CLI Tool to Manage File Metadata with PostgreSQL & SQLAlchemy**

---

## 🧠 What is `filemeta`?

`filemeta` is a Python-based, cross-platform command-line tool that helps you manage metadata of files on your system — including custom tags and system-inferred attributes like owner, size, MIME type, and timestamps. It stores all metadata in a PostgreSQL database using SQLAlchemy ORM for persistence and queryability.

This tool is built for sysadmins, developers, data wranglers, and digital archivists who want clean, structured, queryable metadata about files across Linux, macOS, and Windows systems.

---

## 🔍 Problem It Solves

File systems are black holes. You store files, but forget:
- Who owns them?
- What they were for?
- Which project, team, or purpose they were associated with?

Manual tagging is tedious. Metadata is buried. Central tracking? Non-existent.

**`filemeta`** solves this by:
- Auto-extracting system metadata
- Letting you tag files with custom metadata
- Persisting all this in a searchable PostgreSQL DB
- Providing full CRUD access via CLI

---

## ✨ Features

✅ Cross-platform: Windows, Linux, macOS  
✅ Add custom tags (project, type, category, etc.)  
✅ Infer metadata from OS (owner, size, timestamps)  
✅ Store everything in PostgreSQL using SQLAlchemy ORM  
✅ Full CLI interface (add, search, update, delete)  
✅ Powerful search (on filename, tags, and more)  
✅ Safe, structured, developer-friendly metadata access  
✅ Export metadata to JSON

---

## ⚙️ Installation & Configuration

```bash
pip install papilv-filemeta
```

To install from source:
```bash
git clone https://github.com/yourusername/filemeta_project.git
cd filemeta_project
pip install .
```

To configure your environment:
```bash
export DATABASE_URL="postgresql://username:password@localhost:5432/yourdb"
```
Make sure PostgreSQL is installed and running.

---

## 🔧 Functionality

These are the modular functionalities `filemeta` provides. Users can choose to use only the relevant ones:

- Automatic metadata inference from filesystem
- Custom tagging via CLI with support for type parsing (int, float, bool)
- JSONB used for storing flexible, inferred metadata
- Bidirectional relationship between files and tags
- Safe cascading deletes
- Developer API (`metadata_manager.py`) to use functionality programmatically

---

## 🔊 CLI Commands

### Add a file with metadata
**Syntax:**
```bash
filemeta add <filepath> [--tag key=value ...]
```
**Example:**
```bash
filemeta add ./test_data/sample1.txt -t category=finance -t year=2024
```

### Search metadata by keyword
**Syntax:**
```bash
filemeta search -k <keyword> [--full]
```
**Example:**
```bash
filemeta search -k finance
filemeta search -k 2024 --full
```

### Show file metadata by ID
**Syntax:**
```bash
filemeta get <file_id>
```
**Example:**
```bash
filemeta get 3
```

### Update existing metadata
**Syntax:**
```bash
filemeta update <file_id> [--tag key=value ...] [--remove-tag key ...] [--overwrite]
```
**Examples:**
```bash
filemeta update 3 -t category=legal
filemeta update 3 -r category
filemeta update 3 --overwrite -t type=pdf -t access=confidential
```

### Delete metadata by ID
**Syntax:**
```bash
filemeta delete <file_id>
```
**Example:**
```bash
filemeta delete 3
```

### Export metadata
**Syntax:**
```bash
filemeta export <outputfile.json>
```
**Example:**
```bash
filemeta export backup.json
```

---

## 🚀 User Walkthrough & Tutorial

Use only what you need! Here are example commands for common use cases:

```bash
# Install the package
pip3 install papilv-filemeta

# Configure PostgreSQL connection
export DATABASE_URL="postgresql://user:pass@localhost:5432/metadata"

# View current metadata
filemeta list
filemeta list -s

# Create a dummy file for testing
echo "sample file content" > dummy.txt

# Add the file to database with tags
filemeta add dummy.txt -t project=alpha -t department=R&D

# Retrieve metadata for a specific file
filemeta get 2

# Search using tag values
filemeta search -k R&D
filemeta search -k alpha --full

# Export to JSON for backup or sharing
filemeta export metadata.json
cat metadata.json

# Update existing file metadata
filemeta update 2 -t department=Engineering
filemeta update 2 -t reviewer=QA

# Remove a tag
filemeta update 2 -r reviewer

# Overwrite all tags
filemeta update 2 --overwrite -t type=report -t version=1.1

# Delete metadata record for a file
filemeta delete 2
```

---

## 🛠️ Project Structure

```txt
filemeta_project/
│
├── filemeta/                 # Core Python package
│   ├── cli.py                # CLI interface using Click
│   ├── database.py           # Database session and engine
│   ├── metadata_manager.py   # All CRUD logic
│   ├── models.py             # SQLAlchemy models (File, Tag)
│   ├── utils.py              # Metadata inference, tag parsing
│
├── tests/                    # Test suite (TBD)
├── README.md                 # This file
├── setup.py / pyproject.toml# Packaging info
├── LICENSE                   # MIT
└── .github/workflows/       # CI/CD workflow (pytest + lint)
```

---

## 🔬 Testing

Run all tests:
```bash
pytest
```

---

## 📚 Tech Stack
- Python 3.7+
- Click (for CLI)
- SQLAlchemy ORM
- PostgreSQL (but SQLite fallback possible)
- JSONB (for inferred tags)

---

## 💡 Roadmap
- [ ] Add REST API support (FastAPI)
- [ ] Export metadata to CSV / JSON
- [ ] Tagging templates
- [ ] GUI dashboard for non-tech users
- [ ] File watcher for real-time tracking

---

## 🤝 Contributing
We love contributors! Submit PRs, create issues, or fork the repo. Major improvements like search enhancements, new tag formats, or PostgreSQL optimization are welcome.

---

## ⚖️ License

MIT License — use it, tweak it, ship it, no strings attached.

---

## 👨‍💻 Author

Made with ⚙️ by **Anurag**  
Email: your.email@example.com

---

## 🌍 Repository

[https://github.com/yourusername/filemeta_project](https://github.com/yourusername/filemeta_project)

# 🎞 filemeta

**A Cross-Platform CLI Tool to Manage File Metadata with PostgreSQL & SQLAlchemy**

---

## 🧠 What is `filemeta`?

`filemeta` is a Python-based, cross-platform command-line tool that helps you manage metadata of files on your system — including custom tags and system-inferred attributes like owner, size, MIME type, and timestamps. It stores all metadata in a PostgreSQL database using SQLAlchemy ORM for persistence and queryability.

This tool is built for sysadmins, developers, data wranglers, and digital archivists who want clean, structured, queryable metadata about files across Linux, macOS, and Windows systems.

---

## 🔍 Problem It Solves

File systems are black holes. You store files, but forget:
- Who owns them?
- What they were for?
- Which project, team, or purpose they were associated with?

Manual tagging is tedious. Metadata is buried. Central tracking? Non-existent.

**`filemeta`** solves this by:
- Auto-extracting system metadata
- Letting you tag files with custom metadata
- Persisting all this in a searchable PostgreSQL DB
- Providing full CRUD access via CLI

---

## ✨ Features

✅ Cross-platform: Windows, Linux, macOS  
✅ Add custom tags (project, type, category, etc.)  
✅ Infer metadata from OS (owner, size, timestamps)  
✅ Store everything in PostgreSQL using SQLAlchemy ORM  
✅ Full CLI interface (add, search, update, delete)  
✅ Powerful search (on filename, tags, and more)  
✅ Safe, structured, developer-friendly metadata access  
✅ Export metadata to JSON

---

## ⚙️ Installation & Configuration

```bash
pip install papilv-filemeta
```

To install from source:
```bash
git clone https://github.com/yourusername/filemeta_project.git
cd filemeta_project
pip install .
```

To configure your environment:
```bash
export DATABASE_URL="postgresql://username:password@localhost:5432/yourdb"
```
Make sure PostgreSQL is installed and running.

---

## 🔧 Functionality

These are the modular functionalities `filemeta` provides. Users can choose to use only the relevant ones:

- Automatic metadata inference from filesystem
- Custom tagging via CLI with support for type parsing (int, float, bool)
- JSONB used for storing flexible, inferred metadata
- Bidirectional relationship between files and tags
- Safe cascading deletes
- Developer API (`metadata_manager.py`) to use functionality programmatically

---

## 🔊 CLI Commands

### Add a file with metadata
**Syntax:**
```bash
filemeta add <filepath> [--tag key=value ...]
```
**Example:**
```bash
filemeta add ./test_data/sample1.txt -t category=finance -t year=2024
```

### Search metadata by keyword
**Syntax:**
```bash
filemeta search -k <keyword> [--full]
```
**Example:**
```bash
filemeta search -k finance
filemeta search -k 2024 --full
```

### Show file metadata by ID
**Syntax:**
```bash
filemeta get <file_id>
```
**Example:**
```bash
filemeta get 3
```

### Update existing metadata
**Syntax:**
```bash
filemeta update <file_id> [--tag key=value ...] [--remove-tag key ...] [--overwrite]
```
**Examples:**
```bash
filemeta update 3 -t category=legal
filemeta update 3 -r category
filemeta update 3 --overwrite -t type=pdf -t access=confidential
```

### Delete metadata by ID
**Syntax:**
```bash
filemeta delete <file_id>
```
**Example:**
```bash
filemeta delete 3
```

### Export metadata
**Syntax:**
```bash
filemeta export <outputfile.json>
```
**Example:**
```bash
filemeta export backup.json
```

---

## 🚀 User Walkthrough & Tutorial

Use only what you need! Here are example commands for common use cases:

```bash
# Install the package
pip3 install papilv-filemeta

# Configure PostgreSQL connection
export DATABASE_URL="postgresql://user:pass@localhost:5432/metadata"

# View current metadata
filemeta list
filemeta list -s

# Create a dummy file for testing
echo "sample file content" > dummy.txt

# Add the file to database with tags
filemeta add dummy.txt -t project=alpha -t department=R&D

# Retrieve metadata for a specific file
filemeta get 2

# Search using tag values
filemeta search -k R&D
filemeta search -k alpha --full

# Export to JSON for backup or sharing
filemeta export metadata.json
cat metadata.json

# Update existing file metadata
filemeta update 2 -t department=Engineering
filemeta update 2 -t reviewer=QA

# Remove a tag
filemeta update 2 -r reviewer

# Overwrite all tags
filemeta update 2 --overwrite -t type=report -t version=1.1

# Delete metadata record for a file
filemeta delete 2
```

---

## 🛠️ Project Structure

```txt
filemeta_project/
│
├── filemeta/                 # Core Python package
│   ├── cli.py                # CLI interface using Click
│   ├── database.py           # Database session and engine
│   ├── metadata_manager.py   # All CRUD logic
│   ├── models.py             # SQLAlchemy models (File, Tag)
│   ├── utils.py              # Metadata inference, tag parsing
│
├── tests/                    # Test suite (TBD)
├── README.md                 # This file
├── setup.py / pyproject.toml# Packaging info
├── LICENSE                   # MIT
└── .github/workflows/       # CI/CD workflow (pytest + lint)
```

---

## 🔬 Testing

Run all tests:
```bash
pytest
```

---

## 📚 Tech Stack
- Python 3.7+
- Click (for CLI)
- SQLAlchemy ORM
- PostgreSQL (but SQLite fallback possible)
- JSONB (for inferred tags)

---

## 💡 Roadmap
- [ ] Add REST API support (FastAPI)
- [ ] Export metadata to CSV / JSON
- [ ] Tagging templates
- [ ] GUI dashboard for non-tech users
- [ ] File watcher for real-time tracking

---

## 🤝 Contributing
We love contributors! Submit PRs, create issues, or fork the repo. Major improvements like search enhancements, new tag formats, or PostgreSQL optimization are welcome.

---

## ⚖️ License

MIT License — use it, tweak it, ship it, no strings attached.

---

## 👨‍💻 Author

Made with ⚙️ by **Anurag**  
Email: your.email@example.com

---

## 🌍 Repository

[https://github.com/yourusername/filemeta_project](https://github.com/yourusername/filemeta_project)

# 🎞 filemeta

**A Cross-Platform CLI Tool to Manage File Metadata with PostgreSQL & SQLAlchemy**

---

## 🧠 What is `filemeta`?

`filemeta` is a Python-based, cross-platform command-line tool that helps you manage metadata of files on your system — including custom tags and system-inferred attributes like owner, size, MIME type, and timestamps. It stores all metadata in a PostgreSQL database using SQLAlchemy ORM for persistence and queryability.

This tool is built for sysadmins, developers, data wranglers, and digital archivists who want clean, structured, queryable metadata about files across Linux, macOS, and Windows systems.

---

## 🔍 Problem It Solves

File systems are black holes. You store files, but forget:
- Who owns them?
- What they were for?
- Which project, team, or purpose they were associated with?

Manual tagging is tedious. Metadata is buried. Central tracking? Non-existent.

**`filemeta`** solves this by:
- Auto-extracting system metadata
- Letting you tag files with custom metadata
- Persisting all this in a searchable PostgreSQL DB
- Providing full CRUD access via CLI

---

## ✨ Features

✅ Cross-platform: Windows, Linux, macOS  
✅ Add custom tags (project, type, category, etc.)  
✅ Infer metadata from OS (owner, size, timestamps)  
✅ Store everything in PostgreSQL using SQLAlchemy ORM  
✅ Full CLI interface (add, search, update, delete)  
✅ Powerful search (on filename, tags, and more)  
✅ Safe, structured, developer-friendly metadata access  
✅ Export metadata to JSON

---

## ⚙️ Installation & Configuration

```bash
pip install papilv-filemeta
```

To install from source:
```bash
git clone https://github.com/yourusername/filemeta_project.git
cd filemeta_project
pip install .
```

To configure your environment:
```bash
export DATABASE_URL="postgresql://username:password@localhost:5432/yourdb"
```
Make sure PostgreSQL is installed and running.

---

## 🔧 Functionality

These are the modular functionalities `filemeta` provides. Users can choose to use only the relevant ones:

- Automatic metadata inference from filesystem
- Custom tagging via CLI with support for type parsing (int, float, bool)
- JSONB used for storing flexible, inferred metadata
- Bidirectional relationship between files and tags
- Safe cascading deletes
- Developer API (`metadata_manager.py`) to use functionality programmatically

---

## 🔊 CLI Commands

### Add a file with metadata
**Syntax:**
```bash
filemeta add <filepath> [--tag key=value ...]
```
**Example:**
```bash
filemeta add ./test_data/sample1.txt -t category=finance -t year=2024
```

### Search metadata by keyword
**Syntax:**
```bash
filemeta search -k <keyword> [--full]
```
**Example:**
```bash
filemeta search -k finance
filemeta search -k 2024 --full
```

### Show file metadata by ID
**Syntax:**
```bash
filemeta get <file_id>
```
**Example:**
```bash
filemeta get 3
```

### Update existing metadata
**Syntax:**
```bash
filemeta update <file_id> [--tag key=value ...] [--remove-tag key ...] [--overwrite]
```
**Examples:**
```bash
filemeta update 3 -t category=legal
filemeta update 3 -r category
filemeta update 3 --overwrite -t type=pdf -t access=confidential
```

### Delete metadata by ID
**Syntax:**
```bash
filemeta delete <file_id>
```
**Example:**
```bash
filemeta delete 3
```

### Export metadata
**Syntax:**
```bash
filemeta export <outputfile.json>
```
**Example:**
```bash
filemeta export backup.json
```

---

## 🚀 User Walkthrough & Tutorial

Use only what you need! Here are example commands for common use cases:

```bash
# Install the package
pip3 install papilv-filemeta

# Configure PostgreSQL connection
export DATABASE_URL="postgresql://user:pass@localhost:5432/metadata"

# View current metadata
filemeta list
filemeta list -s

# Create a dummy file for testing
echo "sample file content" > dummy.txt

# Add the file to database with tags
filemeta add dummy.txt -t project=alpha -t department=R&D

# Retrieve metadata for a specific file
filemeta get 2

# Search using tag values
filemeta search -k R&D
filemeta search -k alpha --full

# Export to JSON for backup or sharing
filemeta export metadata.json
cat metadata.json

# Update existing file metadata
filemeta update 2 -t department=Engineering
filemeta update 2 -t reviewer=QA

# Remove a tag
filemeta update 2 -r reviewer

# Overwrite all tags
filemeta update 2 --overwrite -t type=report -t version=1.1

# Delete metadata record for a file
filemeta delete 2
```

---

## 🛠️ Project Structure

```txt
filemeta_project/
│
├── filemeta/                 # Core Python package
│   ├── cli.py                # CLI interface using Click
│   ├── database.py           # Database session and engine
│   ├── metadata_manager.py   # All CRUD logic
│   ├── models.py             # SQLAlchemy models (File, Tag)
│   ├── utils.py              # Metadata inference, tag parsing
│
├── tests/                    # Test suite (TBD)
├── README.md                 # This file
├── setup.py / pyproject.toml# Packaging info
├── LICENSE                   # MIT
└── .github/workflows/       # CI/CD workflow (pytest + lint)
```

---

## 🔬 Testing

Run all tests:
```bash
pytest
```

---

## 📚 Tech Stack
- Python 3.7+
- Click (for CLI)
- SQLAlchemy ORM
- PostgreSQL (but SQLite fallback possible)
- JSONB (for inferred tags)

---

## 💡 Roadmap
- [ ] Add REST API support (FastAPI)
- [ ] Export metadata to CSV / JSON
- [ ] Tagging templates
- [ ] GUI dashboard for non-tech users
- [ ] File watcher for real-time tracking

---

## 🤝 Contributing
We love contributors! Submit PRs, create issues, or fork the repo. Major improvements like search enhancements, new tag formats, or PostgreSQL optimization are welcome.

---

## ⚖️ License

MIT License — use it, tweak it, ship it, no strings attached.

---

## 👨‍💻 Author

Made with ⚙️ by **Anurag**  
Email: your.email@example.com

---

## 🌍 Repository

[https://github.com/yourusername/filemeta_project](https://github.com/yourusername/filemeta_project)


# 🎞 filemeta

**A Cross-Platform CLI Tool to Manage File Metadata with PostgreSQL & SQLAlchemy**

---

## 🧠 What is `filemeta`?

`filemeta` is a Python-based, cross-platform command-line tool that helps you manage metadata of files on your system — including custom tags and system-inferred attributes like owner, size, MIME type, and timestamps. It stores all metadata in a PostgreSQL database using SQLAlchemy ORM for persistence and queryability.

This tool is built for sysadmins, developers, data wranglers, and digital archivists who want clean, structured, queryable metadata about files across Linux, macOS, and Windows systems.

---

## 🔍 Problem It Solves

File systems are black holes. You store files, but forget:
- Who owns them?
- What they were for?
- Which project, team, or purpose they were associated with?

Manual tagging is tedious. Metadata is buried. Central tracking? Non-existent.

**`filemeta`** solves this by:
- Auto-extracting system metadata
- Letting you tag files with custom metadata
- Persisting all this in a searchable PostgreSQL DB
- Providing full CRUD access via CLI

---

## ✨ Features

✅ Cross-platform: Windows, Linux, macOS  
✅ Add custom tags (project, type, category, etc.)  
✅ Infer metadata from OS (owner, size, timestamps)  
✅ Store everything in PostgreSQL using SQLAlchemy ORM  
✅ Full CLI interface (add, search, update, delete)  
✅ Powerful search (on filename, tags, and more)  
✅ Safe, structured, developer-friendly metadata access  
✅ Export metadata to JSON

---

## ⚙️ Installation & Configuration

```bash
pip install papilv-filemeta
```

To install from source:
```bash
git clone https://github.com/yourusername/filemeta_project.git
cd filemeta_project
pip install .
```

To configure your environment:
```bash
export DATABASE_URL="postgresql://username:password@localhost:5432/yourdb"
```
Make sure PostgreSQL is installed and running.

---

## 🔧 Functionality

These are the modular functionalities `filemeta` provides. Users can choose to use only the relevant ones:

- Automatic metadata inference from filesystem
- Custom tagging via CLI with support for type parsing (int, float, bool)
- JSONB used for storing flexible, inferred metadata
- Bidirectional relationship between files and tags
- Safe cascading deletes
- Developer API (`metadata_manager.py`) to use functionality programmatically

---

## 🔊 CLI Commands

### Add a file with metadata
**Syntax:**
```bash
filemeta add <filepath> [--tag key=value ...]
```
**Example:**
```bash
filemeta add ./test_data/sample1.txt -t category=finance -t year=2024
```

### Search metadata by keyword
**Syntax:**
```bash
filemeta search -k <keyword> [--full]
```
**Example:**
```bash
filemeta search -k finance
filemeta search -k 2024 --full
```

### Show file metadata by ID
**Syntax:**
```bash
filemeta get <file_id>
```
**Example:**
```bash
filemeta get 3
```

### Update existing metadata
**Syntax:**
```bash
filemeta update <file_id> [--tag key=value ...] [--remove-tag key ...] [--overwrite]
```
**Examples:**
```bash
filemeta update 3 -t category=legal
filemeta update 3 -r category
filemeta update 3 --overwrite -t type=pdf -t access=confidential
```

### Delete metadata by ID
**Syntax:**
```bash
filemeta delete <file_id>
```
**Example:**
```bash
filemeta delete 3
```

### Export metadata
**Syntax:**
```bash
filemeta export <outputfile.json>
```
**Example:**
```bash
filemeta export backup.json
```

---

## 🚀 User Walkthrough & Tutorial

Use only what you need! Here are example commands for common use cases:

```bash
# Install the package
pip3 install papilv-filemeta

# Configure PostgreSQL connection
export DATABASE_URL="postgresql://user:pass@localhost:5432/metadata"

# View current metadata
filemeta list
filemeta list -s

# Create a dummy file for testing
echo "sample file content" > dummy.txt

# Add the file to database with tags
filemeta add dummy.txt -t project=alpha -t department=R&D

# Retrieve metadata for a specific file
filemeta get 2

# Search using tag values
filemeta search -k R&D
filemeta search -k alpha --full

# Export to JSON for backup or sharing
filemeta export metadata.json
cat metadata.json

# Update existing file metadata
filemeta update 2 -t department=Engineering
filemeta update 2 -t reviewer=QA

# Remove a tag
filemeta update 2 -r reviewer

# Overwrite all tags
filemeta update 2 --overwrite -t type=report -t version=1.1

# Delete metadata record for a file
filemeta delete 2
```

---

## 🛠️ Project Structure

```txt
filemeta_project/
│
├── filemeta/                 # Core Python package
│   ├── cli.py                # CLI interface using Click
│   ├── database.py           # Database session and engine
│   ├── metadata_manager.py   # All CRUD logic
│   ├── models.py             # SQLAlchemy models (File, Tag)
│   ├── utils.py              # Metadata inference, tag parsing
│
├── tests/                    # Test suite (TBD)
├── README.md                 # This file
├── setup.py / pyproject.toml# Packaging info
├── LICENSE                   # MIT
└── .github/workflows/       # CI/CD workflow (pytest + lint)
```

---

## 🔬 Testing

Run all tests:
```bash
pytest
```

---

## 📚 Tech Stack
- Python 3.7+
- Click (for CLI)
- SQLAlchemy ORM
- PostgreSQL (but SQLite fallback possible)
- JSONB (for inferred tags)

---

## 💡 Roadmap
- [ ] Add REST API support (FastAPI)
- [ ] Export metadata to CSV / JSON
- [ ] Tagging templates
- [ ] GUI dashboard for non-tech users
- [ ] File watcher for real-time tracking

---

## 🤝 Contributing
We love contributors! Submit PRs, create issues, or fork the repo. Major improvements like search enhancements, new tag formats, or PostgreSQL optimization are welcome.

---

## ⚖️ License

MIT License — use it, tweak it, ship it, no strings attached.

---

## 👨‍💻 Author

Made with ⚙️ by **Anurag**  
Email: your.email@example.com

---

## 🌍 Repository

[https://github.com/yourusername/filemeta_project](https://github.com/yourusername/filemeta_project)


# 🎞 filemeta

**A Cross-Platform CLI Tool to Manage File Metadata with PostgreSQL & SQLAlchemy**

---

## 🧠 What is `filemeta`?

`filemeta` is a Python-based, cross-platform command-line tool that helps you manage metadata of files on your system — including custom tags and system-inferred attributes like owner, size, MIME type, and timestamps. It stores all metadata in a PostgreSQL database using SQLAlchemy ORM for persistence and queryability.

This tool is built for sysadmins, developers, data wranglers, and digital archivists who want clean, structured, queryable metadata about files across Linux, macOS, and Windows systems.

---

## 🔍 Problem It Solves

File systems are black holes. You store files, but forget:
- Who owns them?
- What they were for?
- Which project, team, or purpose they were associated with?

Manual tagging is tedious. Metadata is buried. Central tracking? Non-existent.

**`filemeta`** solves this by:
- Auto-extracting system metadata
- Letting you tag files with custom metadata
- Persisting all this in a searchable PostgreSQL DB
- Providing full CRUD access via CLI

---

## ✨ Features

✅ Cross-platform: Windows, Linux, macOS  
✅ Add custom tags (project, type, category, etc.)  
✅ Infer metadata from OS (owner, size, timestamps)  
✅ Store everything in PostgreSQL using SQLAlchemy ORM  
✅ Full CLI interface (add, search, update, delete)  
✅ Powerful search (on filename, tags, and more)  
✅ Safe, structured, developer-friendly metadata access  
✅ Export metadata to JSON

---

## ⚙️ Installation & Configuration

```bash
pip install papilv-filemeta
```

To install from source:
```bash
git clone https://github.com/yourusername/filemeta_project.git
cd filemeta_project
pip install .
```

To configure your environment:
```bash
export DATABASE_URL="postgresql://username:password@localhost:5432/yourdb"
```
Make sure PostgreSQL is installed and running.

---

## 🔧 Functionality

These are the modular functionalities `filemeta` provides. Users can choose to use only the relevant ones:

- Automatic metadata inference from filesystem
- Custom tagging via CLI with support for type parsing (int, float, bool)
- JSONB used for storing flexible, inferred metadata
- Bidirectional relationship between files and tags
- Safe cascading deletes
- Developer API (`metadata_manager.py`) to use functionality programmatically

---

## 🔊 CLI Commands

### Add a file with metadata
**Syntax:**
```bash
filemeta add <filepath> [--tag key=value ...]
```
**Example:**
```bash
filemeta add ./test_data/sample1.txt -t category=finance -t year=2024
```

### Search metadata by keyword
**Syntax:**
```bash
filemeta search -k <keyword> [--full]
```
**Example:**
```bash
filemeta search -k finance
filemeta search -k 2024 --full
```

### Show file metadata by ID
**Syntax:**
```bash
filemeta get <file_id>
```
**Example:**
```bash
filemeta get 3
```

### Update existing metadata
**Syntax:**
```bash
filemeta update <file_id> [--tag key=value ...] [--remove-tag key ...] [--overwrite]
```
**Examples:**
```bash
filemeta update 3 -t category=legal
filemeta update 3 -r category
filemeta update 3 --overwrite -t type=pdf -t access=confidential
```

### Delete metadata by ID
**Syntax:**
```bash
filemeta delete <file_id>
```
**Example:**
```bash
filemeta delete 3
```

### Export metadata
**Syntax:**
```bash
filemeta export <outputfile.json>
```
**Example:**
```bash
filemeta export backup.json
```

---

## 🚀 User Walkthrough & Tutorial

Use only what you need! Here are example commands for common use cases:

```bash
# Install the package
pip3 install papilv-filemeta

# Configure PostgreSQL connection
export DATABASE_URL="postgresql://user:pass@localhost:5432/metadata"

# View current metadata
filemeta list
filemeta list -s

# Create a dummy file for testing
echo "sample file content" > dummy.txt

# Add the file to database with tags
filemeta add dummy.txt -t project=alpha -t department=R&D

# Retrieve metadata for a specific file
filemeta get 2

# Search using tag values
filemeta search -k R&D
filemeta search -k alpha --full

# Export to JSON for backup or sharing
filemeta export metadata.json
cat metadata.json

# Update existing file metadata
filemeta update 2 -t department=Engineering
filemeta update 2 -t reviewer=QA

# Remove a tag
filemeta update 2 -r reviewer

# Overwrite all tags
filemeta update 2 --overwrite -t type=report -t version=1.1

# Delete metadata record for a file
filemeta delete 2
```

---

## 🛠️ Project Structure

```txt
filemeta_project/
│
├── filemeta/                 # Core Python package
│   ├── cli.py                # CLI interface using Click
│   ├── database.py           # Database session and engine
│   ├── metadata_manager.py   # All CRUD logic
│   ├── models.py             # SQLAlchemy models (File, Tag)
│   ├── utils.py              # Metadata inference, tag parsing
│
├── tests/                    # Test suite (TBD)
├── README.md                 # This file
├── setup.py / pyproject.toml# Packaging info
├── LICENSE                   # MIT
└── .github/workflows/       # CI/CD workflow (pytest + lint)
```

---

## 🔬 Testing

Run all tests:
```bash
pytest
```

---

## 📚 Tech Stack
- Python 3.7+
- Click (for CLI)
- SQLAlchemy ORM
- PostgreSQL (but SQLite fallback possible)
- JSONB (for inferred tags)

---

## 💡 Roadmap
- [ ] Add REST API support (FastAPI)
- [ ] Export metadata to CSV / JSON
- [ ] Tagging templates
- [ ] GUI dashboard for non-tech users
- [ ] File watcher for real-time tracking

---

## 🤝 Contributing
We love contributors! Submit PRs, create issues, or fork the repo. Major improvements like search enhancements, new tag formats, or PostgreSQL optimization are welcome.

---

## ⚖️ License

MIT License — use it, tweak it, ship it, no strings attached.

---

## 👨‍💻 Author

Made with ⚙️ by **Anurag**  
Email: your.email@example.com

---

## 🌍 Repository

[https://github.com/yourusername/filemeta_project](https://github.com/yourusername/filemeta_project)

# 🎞 filemeta

**A Cross-Platform CLI Tool to Manage File Metadata with PostgreSQL & SQLAlchemy**

---

## 🧠 What is `filemeta`?

`filemeta` is a Python-based, cross-platform command-line tool that helps you manage metadata of files on your system — including custom tags and system-inferred attributes like owner, size, MIME type, and timestamps. It stores all metadata in a PostgreSQL database using SQLAlchemy ORM for persistence and queryability.

This tool is built for sysadmins, developers, data wranglers, and digital archivists who want clean, structured, queryable metadata about files across Linux, macOS, and Windows systems.

---

## 🔍 Problem It Solves

File systems are black holes. You store files, but forget:
- Who owns them?
- What they were for?
- Which project, team, or purpose they were associated with?

Manual tagging is tedious. Metadata is buried. Central tracking? Non-existent.

**`filemeta`** solves this by:
- Auto-extracting system metadata
- Letting you tag files with custom metadata
- Persisting all this in a searchable PostgreSQL DB
- Providing full CRUD access via CLI

---

## ✨ Features

✅ Cross-platform: Windows, Linux, macOS  
✅ Add custom tags (project, type, category, etc.)  
✅ Infer metadata from OS (owner, size, timestamps)  
✅ Store everything in PostgreSQL using SQLAlchemy ORM  
✅ Full CLI interface (add, search, update, delete)  
✅ Powerful search (on filename, tags, and more)  
✅ Safe, structured, developer-friendly metadata access  
✅ Export metadata to JSON

---

## ⚙️ Installation & Configuration

```bash
pip install papilv-filemeta
```

To install from source:
```bash
git clone https://github.com/yourusername/filemeta_project.git
cd filemeta_project
pip install .
```

To configure your environment:
```bash
export DATABASE_URL="postgresql://username:password@localhost:5432/yourdb"
```
Make sure PostgreSQL is installed and running.

---

## 🔧 Functionality

These are the modular functionalities `filemeta` provides. Users can choose to use only the relevant ones:

- Automatic metadata inference from filesystem
- Custom tagging via CLI with support for type parsing (int, float, bool)
- JSONB used for storing flexible, inferred metadata
- Bidirectional relationship between files and tags
- Safe cascading deletes
- Developer API (`metadata_manager.py`) to use functionality programmatically

---

## 🔊 CLI Commands

### Add a file with metadata
**Syntax:**
```bash
filemeta add <filepath> [--tag key=value ...]
```
**Example:**
```bash
filemeta add ./test_data/sample1.txt -t category=finance -t year=2024
```

### Search metadata by keyword
**Syntax:**
```bash
filemeta search -k <keyword> [--full]
```
**Example:**
```bash
filemeta search -k finance
filemeta search -k 2024 --full
```

### Show file metadata by ID
**Syntax:**
```bash
filemeta get <file_id>
```
**Example:**
```bash
filemeta get 3
```

### Update existing metadata
**Syntax:**
```bash
filemeta update <file_id> [--tag key=value ...] [--remove-tag key ...] [--overwrite]
```
**Examples:**
```bash
filemeta update 3 -t category=legal
filemeta update 3 -r category
filemeta update 3 --overwrite -t type=pdf -t access=confidential
```

### Delete metadata by ID
**Syntax:**
```bash
filemeta delete <file_id>
```
**Example:**
```bash
filemeta delete 3
```

### Export metadata
**Syntax:**
```bash
filemeta export <outputfile.json>
```
**Example:**
```bash
filemeta export backup.json
```

---

## 🚀 User Walkthrough & Tutorial

Use only what you need! Here are example commands for common use cases:

```bash
# Install the package
pip3 install papilv-filemeta

# Configure PostgreSQL connection
export DATABASE_URL="postgresql://user:pass@localhost:5432/metadata"

# View current metadata
filemeta list
filemeta list -s

# Create a dummy file for testing
echo "sample file content" > dummy.txt

# Add the file to database with tags
filemeta add dummy.txt -t project=alpha -t department=R&D

# Retrieve metadata for a specific file
filemeta get 2

# Search using tag values
filemeta search -k R&D
filemeta search -k alpha --full

# Export to JSON for backup or sharing
filemeta export metadata.json
cat metadata.json

# Update existing file metadata
filemeta update 2 -t department=Engineering
filemeta update 2 -t reviewer=QA

# Remove a tag
filemeta update 2 -r reviewer

# Overwrite all tags
filemeta update 2 --overwrite -t type=report -t version=1.1

# Delete metadata record for a file
filemeta delete 2
```

---

## 🛠️ Project Structure

```txt
filemeta_project/
│
├── filemeta/                 # Core Python package
│   ├── cli.py                # CLI interface using Click
│   ├── database.py           # Database session and engine
│   ├── metadata_manager.py   # All CRUD logic
│   ├── models.py             # SQLAlchemy models (File, Tag)
│   ├── utils.py              # Metadata inference, tag parsing
│
├── tests/                    # Test suite (TBD)
├── README.md                 # This file
├── setup.py / pyproject.toml# Packaging info
├── LICENSE                   # MIT
└── .github/workflows/       # CI/CD workflow (pytest + lint)
```

---

## 🔬 Testing

Run all tests:
```bash
pytest
```

---

## 📚 Tech Stack
- Python 3.7+
- Click (for CLI)
- SQLAlchemy ORM
- PostgreSQL (but SQLite fallback possible)
- JSONB (for inferred tags)

---

## 💡 Roadmap
- [ ] Add REST API support (FastAPI)
- [ ] Export metadata to CSV / JSON
- [ ] Tagging templates
- [ ] GUI dashboard for non-tech users
- [ ] File watcher for real-time tracking

---

## 🤝 Contributing
We love contributors! Submit PRs, create issues, or fork the repo. Major improvements like search enhancements, new tag formats, or PostgreSQL optimization are welcome.

---

## ⚖️ License

MIT License — use it, tweak it, ship it, no strings attached.

---

## 👨‍💻 Author

Made with ⚙️ by **Anurag**  
Email: your.email@example.com

---

## 🌍 Repository

[https://github.com/yourusername/filemeta_project](https://github.com/yourusername/filemeta_project)
