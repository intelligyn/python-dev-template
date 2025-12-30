# Developer Setup Development Environment Instruction

**Regulatory Context:** **{Add your regulatory context if applicable, e.g., EU MDR / IEC 62304}**
**Applicable System:** **{Your system/project name}**

## 1. Purpose

This instruction describes how a developer must install Git, Docker, and UV to ensure a controlled, consistent, and compliant development environment.

## 2. Scope

Applies to:

- All **{Project name}** software developers
- macOS, Linux, and Windows with wsl development laptops

Does not apply to:

- Production systems
- **{Add project-specific exclusions}**
- Customer-operated systems

## 3. Responsibilities

| Role          | Responsibility                              |
|---------------|---------------------------------------------|
| Developer     | Install, configure, and verify environment  |
| Team Lead     | Confirm onboarding completion               |
| QA / RA       | Maintain this document under change control |
| IT / Security | Ensure IT/cybersecurity policy compliance   |

## 4. Required Software Components

- Git
- Github cli (optional but simplifies working with repos in github)
- Docker Desktop (macOS/Windows) or Docker Engine (Linux)
- uv
- VS Code (preferred code editor)
- On windows: [wsl](https://learn.microsoft.com/en-us/windows/wsl/install), [chocolatey](https://chocolatey.org/install)
- On macOS: [brew](https://brew.sh)

Environment must support:

- Source control access
- Container execution
- Automated test execution

## 5. Prerequisites

- Administrative rights on device
- Internet access
- Minimum **{20 GB}** free disk space (adjust based on project needs - Docker images, multiple projects, and build artifacts can require significant space)
- Device meets cybersecurity baseline

## 6. Software Installation Instructions

### 6.1 macOS

Install Git

1. Open Terminal
2. Run: `brew install git`
3. Verify: `git --version`

Install github-cli

1. Use instructions on <https://github.com/cli/cli/blob/trunk/docs/install_macos>
2. Verify: `gh version`

Install Docker Desktop

1. Download Docker Desktop for macOS
2. Install using default options
3. Open Docker Desktop
4. Verify: `docker info`

Install UV

1. Open terminal
2. Run: `curl -LsSf https://astral.sh/uv/install.sh | sh`
3. Verify: `uv version`

Install VS Code

1. Goto: <https://code.visualstudio.com/download>
2. Verify: `code --version`

3. Open Terminal
4. Run: `brew install make`
5. Verify: `make --version`

Install nvm and node

1. Open Terminal
2. Verify: `node -V`

### 6.2 Linux (Ubuntu / Debian / popOs)

Install Git

1. Open Terminal
2. Run: `sudo apt update`
3. Run: `sudo apt install -y git`
4. Verify: `git --version`

Install github-cli

1. Use instructions on <https://github.com/cli/cli/blob/trunk/docs/install_linux.md#debian>
2. Verify: `gh version`

Install Docker

1. Run: `sudo apt install -y docker.io`
2. Run: `sudo systemctl enable docker`
3. Run: `sudo systemctl start docker`
4. Run: `sudo usermod -aG docker $USER`
5. Re-login
6. Verify: `docker --version`

Install UV

1. Check uv website for install instructions
curl -LsSf <https://astral.sh/uv/install.sh> | sh
2. Verify: `uv version`

Install VS Code

1. Goto: <https://code.visualstudio.com/download>
2. Verify: `code --version`

Install make

1. Open terminal
2. Run: `sudo apt install make`
3. Verify: `make --version`

Install nvm and node

1. Open Terminal
2. Run: `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash`
3. Restart terminal
4. Run: `nvm install --lts`
5. Verify: `node -V`

### 6.3 Windows 11

Install Git

1. Download "Git for Windows"
2. Install with recommended defaults
3. Verify using PowerShell: `git --version`

Install github-cli

1. Use instructions on <https://github.com/cli/cli/blob/trunk/docs/install_windows>
2. Verify: `gh version`

Install Docker Desktop

1. Download Docker Desktop for Windows
2. Enable WSL2 backend
3. Launch Docker Desktop
4. Verify: `docker info`

Install UV

1. Start PowerShell terminal
2. Run: `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`
3. Verify: `uv version`

Install VS Code

1. Go to: <https://code.visualstudio.com/download>
2. Verify: `code --version`

Install nvm and node

1. Open Terminal
2. Run: `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash`
3. Restart terminal
4. Run: `nvm install --lts`
5. Verify: `node -V`

## 7. Additional configuration and setup (instruction same for Linux, macOS and Windows)

7.1 Prepare git commit

1. Open terminal
2. Run: `git config --global user.email "you@example.com"`
3. Run: `git config --global user.name "Your Name"`

Note: replace with your own GitHub email and name

7.2 With uv

1. Clone repo
2. `uv venv --python 3.12`
3. `uv sync`

7.3 VS Code extensions

1. Python (Microsoft)
2. Pylance (Microsoft)

7.4 Markdown linting

1. Open terminal
2. Run: `npm install -g markdownlint-cli`
3. Verify: `markdownlint -version`

## 8. Post-Installation Validation Checklist

| Check              | Expected Result                    |
|--------------------|------------------------------------|
| Git installed      | git --version returns version      |
| Repo clone         | developer can clone repository     |
| Docker operational | docker run hello-world succeeds    |
| UV operational     | uv version returns version         |

Developer must record validation results.

## 9. Records

- Developer name
- Installation date
- OS version
- Tool versions installed

Stored in onboarding documentation.

## 10. Constraints

- **{Add project-specific constraints}**
- Cloud sync folders must not contain source code
- Only approved versions allowed
- Device must remain security compliant

## 11. Change Management

Changes to software requirements or installation steps must follow **{your change control process, e.g., QMS change control}**.
