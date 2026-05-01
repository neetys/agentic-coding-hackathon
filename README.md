# Energize Your Code - Hackathon

![Energize Your Code Banner](docs/images/hackathon-logo.png)

> **Build Your Own AI-Powered Workflow with GitHub Copilot**
>
> Choose a use case. Design your own agents, prompts, skills, and MCP server configuration. Execute your workflow and deliver results.

---

## The Challenge

Your team will **build a custom agentic workflow from scratch** using GitHub Copilot's extensibility features:

- **Custom Agents** (`.github/agents/`) — specialized AI roles with specific tools and handoffs
- **Reusable Prompts** (`.github/prompts/`) — sequential workflow steps your agents execute
- **Skills** (`.github/skills/`) — domain knowledge packages for your agents
- **MCP Servers** (`.vscode/mcp.json`) — tool integrations (Azure, Playwright, docs, etc.)

You decide what agents you need, what each one does, how they hand off to each other, and what prompts drive the workflow. Then you execute it and deliver the output.

---

## Choose Your Use Case

| | Use Case 1: IaC | Use Case 2: Discovery | Use Case 3: Spec-Driven |
|---|---|---|---|
| **Type** | Greenfield IaC | Brownfield Assessment | Greenfield Application |
| **Goal** | Deploy Azure infrastructure from scratch | Discover & assess a live Azure environment | Build a web app from specifications |
| **You Build** | Agents + prompts for an IaC pipeline | Agents + prompts for a discovery pipeline | A spec-driven app workflow using Spec Kit or OpenSpec |
| **Output** | Bicep modules + deployed resources | Assessment reports + Mermaid diagrams | Working app + Playwright tests |
| **Guide** | [Use Case 1 Guide](docs/use-case-iac.md) | [Use Case 2 Guide](docs/use-case-discovery.md) | [Use Case 3 Guide](docs/use-case-spec-driven.md) |
| **Sample** | [IaC Walkthrough](docs/sample/sample-iac.md) | [Discovery Walkthrough](docs/sample/sample-discovery.md) | [Spec-Driven Walkthrough](docs/sample/sample-spec-driven.md) |

---

## Prerequisites

- **Azure Subscription** with Contributor access
- **GitHub Copilot** license (Business or Enterprise recommended)
- **VS Code** (or Codespaces) with GitHub Copilot & Copilot Chat
- **For Use Case 3 (Spec-Driven)**: install `alfredoperez.speckit-companion` and `atman-dev.openspec-for-copilot`
- **Azure CLI** with Bicep installed

> **Tip**: Open this repo in **GitHub Codespaces** — the devcontainer pre-installs all tools automatically!

### Azure Login (Required Before Exercises)

Before starting any exercise, log in to Azure using the credentials provided by the hackathon coaches:

```bash
az login
```

After logging in, verify you are on the correct subscription:

```bash
az account show --query "{name:name, id:id, tenantId:tenantId}" -o table
```

> **Important**: Confirm with the hackathon coaches that the displayed subscription and tenant are correct before proceeding.

---

## Quick Start

### 1. Clone and Open

```bash
git clone https://github.com/pascalvanderheiden/energize-your-code-hackathon.git
cd energize-your-code-hackathon
```

Open in VS Code or Codespaces. The devcontainer will install all required tools.

### 2. Choose Your Path

There are two good ways through the hackathon:

**Recommended first: follow a sample walkthrough.**

The samples are the fastest way to understand the concept, see the agentic workflow in action, and learn how agents, prompts, skills, and MCP servers work together:

- [Sample Walkthrough: IaC](docs/sample/sample-iac.md)
- [Sample Walkthrough: Discovery](docs/sample/sample-discovery.md)
- [Sample Walkthrough: Spec-Driven](docs/sample/sample-spec-driven.md)

**Then: build your own workflow with a use case.**

The use case guides are ideal when you want to create your own agentic template during the hackathon, or continue exploring after the hack. Pick one guide:

- [Use Case 1: Infrastructure as Code](docs/use-case-iac.md) — Build Azure infra with Bicep
- [Use Case 2: Agentic Discovery](docs/use-case-discovery.md) — Discover & assess a live Azure environment
- [Use Case 3: Spec-Driven Development](docs/use-case-spec-driven.md) — Build a web app from specs

When you follow a use case guide, it walks you through the things to think about while designing your workflow:

1. **Define your goal** — What exactly are you building or discovering?
2. **Choose your tools** — Which MCP servers, skills, and extensions do you need?
3. **Design your agents** — What roles do you need? How do they hand off?
4. **Write your prompts** — One prompt per workflow step, executed in order
5. **Execute & iterate** — Run your prompts, verify output, refine
6. **Verify & present** — Demo your workflow and results

### 3. Get Unstuck

If you're building your own template and get stuck, this repo includes **reference examples** — agents, prompts, skills, and MCP configuration. Browse them for inspiration, but build your own!

---

## Available MCP Servers

These MCP servers are pre-configured in `.vscode/mcp.json` and ready to use in your agents:

| Server | Purpose | Useful For |
|---|---|---|
| **Azure MCP** | Azure resource management, discovery, deployment | All use cases |
| **Learn MCP** (`mcp_microsoftdocs`) | Microsoft documentation, WAF/CAF references | Use Cases 1 & 2 |
| **Playwright MCP** | Browser automation and E2E testing | Use Case 3 |

> The **Bicep MCP** is auto-enabled by the `ms-azuretools.vscode-bicep` extension — no manual configuration needed.

You can add more MCP servers to `.vscode/mcp.json` as needed for your workflow.

---

## Reference Examples

This repo includes a complete set of example agents, prompts, and skills that demonstrate one way to solve each use case. **These are NOT mandatory** — they exist so you can peek at them when stuck.

### Example Agents (`.github/agents/`)

| Agent | Role | Use Case |
|---|---|---|
| `architect` | Architecture designer | IaC |
| `reviewer` | WAF/CAF reviewer & assessor | IaC, Discovery |
| `planner` | Development task planner | IaC |
| `implementer` | Bicep code writer | IaC |
| `tester` | Infrastructure validator | IaC |
| `documenter` | Documentation generator | IaC |
| `deployer` | Azure deployer | IaC, Spec-Driven |
| `discoverer` | Azure environment scanner | Discovery |
| `reporter` | Report & diagram writer | Discovery |
| `migration-planner` | PaaS migration planner | Discovery |

### Example Prompts (`.github/prompts/`)

| Workflow | Prompts |
|---|---|
| **IaC** | `iac-1-architect` → `iac-2-review` → `iac-3-plan` → `iac-4-implement` → `iac-5-test` → `iac-6-document` → `iac-7-deploy` |
| **Discovery** | `disc-1-discover` → `disc-2-assess` → `disc-3-report` → `disc-4-migration` → `disc-5-full-pipeline` |
| **Spec-Driven** | Use the participant guide flow with Spec Kit/OpenSpec slash commands (no dedicated `spec-*` prompt files) |

### Copilot Instruction Files (`.github/instructions/`)

These instruction files **auto-activate** when you create or edit agents, prompts, skills, or instructions — giving Copilot real-time guidance on how to write them correctly:

| File | Auto-Activates On | What It Does |
|---|---|---|
| `agents.instructions.md` | `**/*.agent.md` | Guides you through agent frontmatter, tools, handoffs, and best practices |
| `prompt.instructions.md` | `**/*.prompt.md` | Guides you through prompt structure, frontmatter, inputs, and output definitions |
| `agent-skills.instructions.md` | `**/.github/skills/**/SKILL.md` | Guides you through skill creation, descriptions, and resource bundling |
| `instructions.instructions.md` | `**/*.instructions.md` | Guides you through writing custom instruction files |

> **Pro tip**: Just start creating a file (e.g., `.github/agents/my-agent.agent.md`) and Copilot will automatically load the matching guidelines!

### Example Skills (`.github/skills/`)

| Skill | Purpose |
|---|---|
| `find-skills` | Discover and install additional skills |
| `update-avm-modules-in-bicep` | Keep AVM module versions current |
| `terraform-style-guide` | Terraform HCL standards |

### Azure Skills Added To This Project

This project now also includes a curated set of Azure skills sourced from the MicrosoftDocs Azure Agent Skills repository:

- Repository: [MicrosoftDocs/agent-skills](https://github.com/MicrosoftDocs/agent-skills)
- Browse more Azure skills: [MicrosoftDocs/agent-skills/skills](https://github.com/MicrosoftDocs/agent-skills/tree/main/skills)

The scenario-specific skill guidance lives in the custom agents, so participant prompts can stay small. These skills are installed locally under `.github/skills/` and can be used directly in this repository. If you want to expand beyond this curated set, the MicrosoftDocs repository above has a much broader catalog of Azure service skills.

### Sample Walkthroughs ([docs/sample/](docs/sample/))

Step-by-step guides that execute the pre-built agentic template — for teams who want to follow along rather than build from scratch:

| Walkthrough | Use Case | What You'll Do |
|---|---|---|
| [IaC Walkthrough](docs/sample/sample-iac.md) | Use Case 1 | Run all 9 IaC prompts end-to-end: architect → review → plan → implement → test → document → deploy |
| [Discovery Walkthrough](docs/sample/sample-discovery.md) | Use Case 2 | Run all 5 discovery prompts: discover → assess → report → migration plan |
| [Spec-Driven Walkthrough](docs/sample/sample-spec-driven.md) | Use Case 3 | Follow the full spec-driven lifecycle: brainstorm → specify → implement (apply proposals separately for OpenSpec) → test → deploy |

---

## Project Structure

```
.
├── .devcontainer/
│   └── devcontainer.json               # Dev environment (Codespaces-ready)
├── .github/
│   ├── agents/                          # 📖 Example agents (reference)
│   ├── instructions/                    # 🤖 Auto-activating Copilot guidelines
│   ├── skills/                          # 📖 Example skills (reference)
│   ├── prompts/                         # 📖 Example prompts (reference)
│   └── copilot-instructions.md         # Workspace-wide Copilot context
├── .vscode/
│   └── mcp.json                         # MCP server configuration
├── docs/
│   ├── use-case-iac.md                  # Use Case 1 participant guide
│   ├── use-case-discovery.md            # Use Case 2 participant guide
│   ├── use-case-spec-driven.md          # Use Case 3 participant guide
│   ├── images/
│   └── sample/                          # 📖 Step-by-step walkthroughs & examples
├── LICENSE
└── README.md
```

---

## Tips for Hackathon Teams

1. **Pick ONE use case** — Focus your team's energy on one path
2. **Build your own agents** — Don't just use the examples; create agents tailored to your workflow
3. **Start simple** — One agent, one prompt, get it working, then expand
4. **Number your prompts** — Sequential numbering makes the workflow easy to follow
5. **Use Codespaces** — Everything is pre-configured, no local setup needed
6. **Test each step** — Verify agent output before moving to the next prompt
7. **Peek at examples when stuck** — The reference agents, prompts, and samples are there to help
8. **Be creative** — There's no single right answer; design the workflow your way

---

## License

[MIT](LICENSE)

---

*Built for the Energize Your Code Hackathon*
