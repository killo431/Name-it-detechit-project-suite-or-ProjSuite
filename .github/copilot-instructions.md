# GitHub Copilot Instructions for DeTechIT Universal Project Suite (DUPS)

## Repository Overview

The **DeTechIT Universal Project Suite (DUPS)** is a comprehensive framework for AI-assisted project development using multi-agent orchestration integrated with Linear project management. This is **not a traditional software project** - it's a documentation and template framework that provides structured workflows, AI agent configurations, and project templates for building various types of applications.

## High-Level Repository Details

- **Repository Type**: Documentation/template framework (language-agnostic)
- **Primary Purpose**: Multi-agent AI development orchestration system
- **Size**: ~50 documentation files, configuration templates, and workflow definitions
- **Languages**: Markdown (documentation), JSON (configuration), YAML (rules)
- **Target Runtime**: Framework supports Python, Node.js, and other languages via `/bin/` structure
- **Key Integration**: Linear project management platform

## Validation and Build Process

Since this is a template/framework repository, there are **no traditional build, test, or run commands**. Instead, validation focuses on:

### 1. JSON Configuration Validation
**Always validate JSON files after making changes:**
```bash
# Validate all JSON files in the repository
find . -name "*.json" -exec python3 -m json.tool {} \;
```
**Required before**: Any changes to agent configs, rule definitions, or dashboard files  
**Time required**: <5 seconds  
**Expected outcome**: All JSON files should parse without syntax errors

### 2. YAML Rules Validation
**Validate YAML syntax for rule files:**
```bash
# Check YAML syntax (requires PyYAML: pip install pyyaml)
python3 -c "import yaml; [yaml.safe_load(open(f)) for f in ['./library/rules/dynamic_rules.yaml', './etc/server_config.yaml']]"
```
**Required before**: Changes to rule definitions or server configurations

### 3. Documentation Consistency Check
**Verify required documentation structure exists:**
```bash
# Ensure core documentation files exist
ls -la IMPLEMENTATION_GUIDE.md MANIFEST.md SPECIAL_INSTRUCTIONS.md
```

### 4. Agent Configuration Integrity
**Validate agent role definitions align with system architecture:**
```bash
# Check that ai-config.json references existing files
cat agents/ai-config.json
```

## Project Layout and Architecture

### Core System Architecture
```
├── /bin/                    # CLI tools (python, node, npm placeholders)
├── /lib/                    # AI/system libraries 
├── /etc/                    # Configuration files (envs, keys)
├── /var/                    # Logs and runtime data
├── /opt/                    # LLMs, embeddings, weights
├── /home/builder/project/   # Runtime sandbox per project
│   ├── src/                 # Application source code
│   ├── config/              # Runtime configs  
│   ├── data/                # Development/test datasets
│   ├── models/              # Small fine-tuned models
│   ├── logs/                # App or agent logs
│   ├── tests/               # Unit/integration/E2E tests
│   └── docs/                # Project documentation
├── /agents/                 # AI agent configurations
│   ├── ai-config.json       # Context file references
│   ├── agents.json          # Agent role definitions
│   ├── vocab.json           # Domain terminology
│   └── context/             # Agent context files
├── /library/                # Prompt and rule libraries
│   ├── prompts/             # Prompt templates (base, dynamic, goal-mapped)
│   └── rules/               # JSON/YAML constraint rules
├── /projects/               # Project instances
├── /linear_templates/       # Linear integration templates
└── /templates/              # Various templates (docs, infra, agents)
```

### Key Configuration Files
- **agents/ai-config.json**: Defines context files for AI agents
- **agents/agents.json**: Lists agent roles and responsibilities  
- **library/rules/security.json**: Security constraint rules
- **library/rules/performance.json**: Performance optimization rules
- **library/rules/dynamic_rules.yaml**: Goal-based rules
- **SPECIAL_INSTRUCTIONS.md**: Strict implementation boundaries and rules

### Critical Validation Rules
The **SPECIAL_INSTRUCTIONS.md** file contains non-negotiable rules:
1. **File Structure**: Code goes in `/home/builder/project/src/`, configs in `/config/`, docs in `/docs/`
2. **No Scope Drift**: Only build what's defined in `goals.md` or Linear tasks
3. **Documentation**: Log all decisions in `decisions.md`
4. **Naming Conventions**: Files use `kebab-case`, variables `camelCase`, classes `PascalCase`
5. **AI Role Boundaries**: Respect agent responsibilities (DevAgent: code only, DocGen: docs only, etc.)

### AI Agent Roles and Responsibilities
- **Planner**: Converts goals to backlogs
- **Architect**: Designs systems and maintains boundaries  
- **DevAgent**: Writes modular, testable code
- **DocGen**: Creates documentation and changelogs
- **OpsAgent**: Handles CI/CD and deployment automation
- **Data Analyst**: Manages KPIs and validation
- **AI Interviewer**: Gathers stakeholder feedback

### Linear Integration Workflow
- **Projects**: 1 per live project folder
- **Milestones**: Core, Design, Validation, Deploy  
- **Labels**: phase:*, ai-agent:*, output:*
- **Issue Templates**: 4 phase-based templates with linked files

### Snapshot and Reset System
- **Reset Process**: Clears `/projects`, logs, memory (logged to `reset_log.md`)
- **Snapshots**: Saved in `/snapshot/` directory, mapped in `snapshot-index.md`

## Files in Repository Root
```
IMPLEMENTATION_GUIDE.md  # Complete framework documentation
MANIFEST.md             # File index and explanations  
SPECIAL_INSTRUCTIONS.md # Implementation rules and boundaries
agents/                 # AI agent configurations
bin/                    # CLI tool placeholders
dashboards/             # Project health and metrics
docs/                   # Workflow documentation
env-reset/              # Reset and snapshot guides
etc/                    # Configuration templates
home/                   # Project sandbox structure
lib/                    # System libraries placeholder
library/                # Prompts and rules
linear_templates/       # Linear integration templates
opt/                    # AI model placeholders
projects/               # Project instances
templates/              # Various templates
test                    # Empty test placeholder
var/                    # Runtime data placeholder
```

## Common Pitfalls to Avoid

1. **Do not treat this as a traditional software project** - there are no build scripts, package.json, or typical CI/CD
2. **Always validate JSON syntax** after editing configuration files
3. **Respect the file structure** defined in SPECIAL_INSTRUCTIONS.md
4. **Do not cross AI agent role boundaries** without explicit permission
5. **Always trace changes back to goals.md or Linear tasks** to avoid scope drift
6. **Use PromptImprovementChecklist.md** before implementing any new prompts

## Trust These Instructions

These instructions have been validated against the current repository structure. Only search for additional information if:
- The instructions are incomplete for your specific task
- You find contradictory information in the repository
- The repository structure has changed significantly since these instructions were created

Always reference SPECIAL_INSTRUCTIONS.md and IMPLEMENTATION_GUIDE.md for authoritative guidance on this framework.