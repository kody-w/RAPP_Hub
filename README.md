# RAPP Hub

**Central Registry for Complete RAPP AI Implementations**

Discover, share, and deploy production-ready AI solutions. RAPP Hub is to AI implementations what GitHub is to code repositories - a central place to find and share complete, working RAPP-based AI systems.

## How It Works

```
┌─────────────────────────────────────────────────────────────────┐
│                         RAPP Hub                                 │
│         (Complete AI Implementations)                            │
│                                                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │   Copilot    │  │   Document   │  │    Email     │          │
│  │   Entra      │  │ Intelligence │  │  Automation  │          │
│  │   Agent      │  │     Hub      │  │    Suite     │          │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘          │
│         │                 │                 │                   │
│         └────────────────┼─────────────────┘                   │
│                          │                                      │
│                          ▼                                      │
│              ┌─────────────────────┐                           │
│              │   RAPP Store        │                           │
│              │  (Agent Registry)   │                           │
│              │                     │                           │
│              │  ├─ pdf_processor   │                           │
│              │  ├─ email_assistant │                           │
│              │  ├─ data_analyst    │                           │
│              │  └─ ...             │                           │
│              └─────────────────────┘                           │
└─────────────────────────────────────────────────────────────────┘
```

**RAPP Hub** = Complete implementations (like full applications)
**RAPP Store** = Individual agents/skills (like npm packages)

Implementations in RAPP Hub can declare dependencies on RAPP Store agents, which are automatically resolved and installed.

## Quick Start

### Browse Implementations

Visit the web UI: **https://kody-w.github.io/RAPP_Hub/**

Or use the CLI:

```bash
# Install RAPP Hub CLI
pip install rapp-hub

# Browse available implementations
rapp-hub browse

# Search for specific solutions
rapp-hub search "copilot"

# Get details about an implementation
rapp-hub info copilot-entra-agent
```

### Install an Implementation

```bash
# Clone and set up an implementation with all dependencies
rapp-hub install copilot-entra-agent

# This will:
# 1. Clone the repository
# 2. Install RAPP Store agent dependencies
# 3. Install Python dependencies
# 4. Set up the project structure
```

### Manual Installation

```bash
# 1. Clone the implementation
git clone https://github.com/kody-w/AI-Agent-Templates.git
cd AI-Agent-Templates/CommunityRAPP

# 2. Install RAPP Store dependencies
rapp-hub deps install

# 3. Install Python dependencies
pip install -r requirements.txt

# 4. Run the implementation
./run.sh
```

## Dependency Management

### rapp.json

Each RAPP Hub implementation includes a `rapp.json` file that declares dependencies:

```json
{
  "name": "my-rapp-implementation",
  "version": "1.0.0",
  "description": "My awesome AI implementation",
  "dependencies": {
    "rapp_store": {
      "agents": [
        "pdf_processor_agent@^1.0.0",
        "email_assistant_agent@^1.0.0"
      ],
      "skills": [
        "algorithmic-art@latest"
      ]
    },
    "python": [
      "openai>=1.0.0",
      "pandas>=2.0.0"
    ]
  }
}
```

### Installing Dependencies

```bash
# Install all dependencies from rapp.json
rapp-hub deps install

# Install specific agent from RAPP Store
rapp-hub deps add pdf_processor_agent

# Install specific skill
rapp-hub deps add algorithmic-art --type skill

# Update all dependencies
rapp-hub deps update
```

### How Dependencies Work

1. **RAPP Store agents** are downloaded to `./agents/` folder
2. **RAPP Store skills** are downloaded to `./skills/` folder
3. **Python packages** are installed via pip
4. Version resolution follows semver (^1.0.0, ~1.0.0, latest)

## Publishing Your Implementation

### 1. Prepare Your Repository

Ensure your repo follows the RAPP Hub protocol:

```
your-implementation/
├── rapp.json           # Required: Dependencies and metadata
├── README.md           # Required: Documentation
├── main.py             # Entry point
├── agents/             # Local agents + RAPP Store agents
│   ├── basic_agent.py  # Base class
│   └── your_agent.py   # Custom agents
├── requirements.txt    # Python dependencies
└── ...
```

### 2. Create rapp.json

```json
{
  "name": "your-implementation",
  "version": "1.0.0",
  "description": "What your implementation does",
  "author": "Your Name",
  "license": "Apache-2.0",
  "repository": "https://github.com/you/your-repo",
  "category": "enterprise",
  "tags": ["tag1", "tag2"],
  "features": [
    "Feature 1",
    "Feature 2"
  ],
  "stack": {
    "runtime": "python",
    "version": "3.11",
    "platform": "azure-functions",
    "ai": "azure-openai"
  },
  "dependencies": {
    "rapp_store": {
      "agents": ["agent_id@version"],
      "skills": ["skill-id@version"]
    },
    "python": ["package>=version"]
  },
  "scripts": {
    "setup": "pip install -r requirements.txt",
    "start": "python main.py",
    "test": "pytest"
  }
}
```

### 3. Submit to RAPP Hub

Option A: **Pull Request**
```bash
# Fork RAPP_Hub
# Add your implementation to manifest.json
# Submit PR
```

Option B: **Self-Hosted**
```bash
# Add your repo URL to any RAPP Hub instance
rapp-hub registry add https://github.com/you/your-repo
```

## Protocol Specification

### Implementation Entry Format

```json
{
  "id": "unique-id",
  "name": "Human Readable Name",
  "description": "What this implementation does",
  "version": "1.0.0",
  "category": "category-id",
  "author": "Author Name",
  "license": "Apache-2.0",
  "repo": "https://github.com/owner/repo",
  "path": "path/within/repo",
  "branch": "main",
  "icon": "🤖",
  "tags": ["tag1", "tag2"],
  "features": ["Feature 1", "Feature 2"],
  "stack": {
    "runtime": "python",
    "version": "3.11",
    "platform": "azure-functions",
    "ai": "azure-openai"
  },
  "dependencies": {
    "rapp_store": {
      "agents": ["agent_id@version"],
      "skills": ["skill-id@version"]
    },
    "python": ["package"]
  },
  "quickstart": {
    "clone": "git clone command",
    "setup": "setup command",
    "run": "run command"
  }
}
```

### Dependency Resolution

```
rapp_store.agents: ["pdf_processor_agent@^1.0.0"]
                          │           │
                          │           └── Version constraint (semver)
                          └── Agent ID from RAPP Store
```

**Version Constraints:**
- `^1.0.0` - Compatible with 1.x.x (>=1.0.0 <2.0.0)
- `~1.0.0` - Patch-level changes (~=1.0.0, >=1.0.0 <1.1.0)
- `1.0.0` - Exact version
- `latest` - Always get latest version
- `*` - Any version

## Categories

| ID | Name | Description |
|----|------|-------------|
| `enterprise` | Enterprise Solutions | Production-ready enterprise AI |
| `copilot` | Copilot Integrations | M365 Copilot and Teams |
| `automation` | Workflow Automation | Business process automation |
| `analytics` | Analytics & Insights | Data analysis and BI |
| `customer-service` | Customer Service | Support and service desk |
| `developer-tools` | Developer Tools | Dev and DevOps tooling |
| `starter` | Starter Templates | Boilerplate templates |

## Featured Implementations

### 🤖 Copilot Entra Agent
Enterprise AI assistant with Azure Functions, GPT-4, persistent memory, and full Microsoft 365 integration.

### 📄 Document Intelligence Hub
AI-powered document processing with PDF extraction, analysis, and automated workflows.

### 🚀 RAPP Starter Template
Minimal boilerplate to start a new RAPP implementation with best practices.

## Contributing

See [CONTRIBUTING.md](docs/CONTRIBUTING.md) for guidelines on:
- Submitting new implementations
- Improving existing implementations
- Protocol enhancements

## License

Apache 2.0 - See [LICENSE](LICENSE) for details.

## Links

- **RAPP Hub**: https://github.com/kody-w/RAPP_Hub
- **RAPP Store**: https://github.com/kody-w/RAPP_Store
- **Web UI**: https://kody-w.github.io/RAPP_Hub/
- **Documentation**: [docs/](docs/)
