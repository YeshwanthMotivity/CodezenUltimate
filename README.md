# CodezenUltimate

> **AI-Powered Code Analysis and Refactoring Agent**

CodezenUltimate is an intelligent code review and refactoring tool that analyzes your codebase using LLMs (Gemini or local LM Studio), identifies issues, suggests improvements, and automatically creates Pull Requests with the fixes.

![Python](https://img.shields.io/badge/Python-3.8+-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-Backend-green)

---

## Features

- **Multi-Language Support** - Analyzes Python, JavaScript, TypeScript, and Java files
- **Intelligent Analysis** - Detects code issues, style violations, dead code, and logic bugs
- **Auto-Refactoring** - Suggests and applies code improvements automatically
- **GitHub Integration** - Creates PRs directly via GitHub App integration
- **Flexible LLM Backend** - Supports Google Gemini (cloud) or LM Studio (local)
- **CLI Tool** - Developer-friendly command-line interface

---

## Architecture

<img width="1430" height="720" alt="image" src="https://github.com/user-attachments/assets/9d32baab-ad76-4230-b23f-fca09c59155b" />

---

## Installation

### Prerequisites

- Python 3.8+
- Git
- (Optional) LM Studio or Gemini API Key

### Backend Setup

```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### CLI Installation

```bash
# Navigate to CLI directory
cd cli

# Install CLI as a package
pip install -e .

# Verify installation
codezen --help
```

---

## Configuration

### Backend Configuration

Create a `.env` file in the `backend/` directory:

```env
# ---- GITHUB APP ----
GITHUB_APP_ID=your_app_id
GITHUB_CLIENT_ID=your_client_id
GITHUB_CLIENT_SECRET=your_client_secret
GITHUB_PRIVATE_KEY_PATH=path/to/private-key.pem

# ---- BACKEND ----
CODEZEN_HOST=0.0.0.0
CODEZEN_PORT=8000
CODEZEN_PUBLIC_URL=http://localhost:8000

# ---- LLM Configuration ----
# For Gemini (Cloud)
USE_GEMINI=true
GEMINI_API_KEY=your_gemini_api_key
GEMINI_MODEL=gemini-1.5-flash-latest

# For LM Studio (Local)
USE_GEMINI=false
LMSTUDIO_API=http://localhost:1234/v1
LMSTUDIO_MODEL=qwen2.5-coder-7b-instruct
```

### CLI Configuration

```bash
# Set backend URL
codezen config --backend https://your-backend-url.com
```

---

## 🚀 Usage

### Starting the Backend

```bash
cd backend
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

### Using the CLI

```bash
# Initialize a repository
cd your-project
codezen init

# Analyze code and apply fixes
codezen analyze

# Check installation status
codezen status
```

### CLI Commands

| Command | Description |
|---------|-------------|
| `codezen init` | Initialize repository and get GitHub App install link |
| `codezen analyze` | Analyze code, review suggestions, and create PR |
| `codezen status` | Check GitHub App installation status |
| `codezen config --backend <URL>` | Set backend URL |
| `codezen version` | Show CLI version |
| `codezen help` | Display help menu |

---

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Health check |
| `/init` | POST | Initialize repository |
| `/analyze` | POST | Analyze code files |
| `/apply-fixes` | POST | Apply refactors and create PR |
| `/status` | GET | Get installation status |
| `/github/webhook` | POST | GitHub webhook handler |

---

## Project Structure

```
CodezenUltimate/
├── backend/
│   ├── main.py              # FastAPI application
│   ├── llm_client.py        # LLM integration (Gemini/LM Studio)
│   ├── github_app.py        # GitHub App authentication
│   ├── pr_manager.py        # Git operations & PR creation
│   ├── codezen_store.py     # Installation data storage
│   ├── requirements.txt     # Python dependencies
│   └── .env.example         # Environment template
│
├── cli/
│   ├── codezen_cli.py       # Command-line interface
│   ├── pyproject.toml       # CLI package configuration
│   └── README.md            # CLI documentation
│
└── README.md                # This file
```

---

## Development

### Running in Development Mode

```bash
# Backend with hot reload
cd backend
uvicorn main:app --reload --port 8000

# For external access (with ngrok)
ngrok http 8000
```

### Supported File Types

The analyzer supports:
- `.py` - Python
- `.js` - JavaScript
- `.ts` - TypeScript
- `.java` - Java

---

## How It Works

1. **Initialize** - Run `codezen init` to register your repo with the CodeZen GitHub App
2. **Analyze** - Run `codezen analyze` to scan your code for issues
3. **Review** - Review AI-generated suggestions for each file
4. **Apply** - Approve changes and let CodeZen create a PR automatically
5. **Merge** - Review and merge the PR on GitHub

---

## Security

- Private keys and credentials are stored locally in `.env`
- GitHub tokens are short-lived and refreshed automatically
- All communication uses HTTPS
- Supports local LLM deployment for sensitive codebases
---

## Authors

- **Yeshwanth Goud** - [MotivityLabs](https://motivitylabs.com)

---

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

<p align="center">
  Made with ❤️ by MotivityLabs
</p>
