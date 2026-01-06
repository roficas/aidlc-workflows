# AI-DLC for GitHub Copilot

AI-DLC is an intelligent software development workflow that adapts to your needs, maintains quality standards, and keeps you in control of the process. This guide shows how to set up AI-DLC with GitHub Copilot in VS Code.

## Prerequisites

- [GitHub Copilot VS Code Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)
- [GitHub Copilot Chat VS Code Extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat)
- VS Code (version 1.84 or later recommended)
- GitHub account with active Copilot subscription

## Quick Start

Clone this repo:
```bash
git clone <this-repo>
```

Create a new project folder:

**Unix/Linux/macOS:**
```bash
mkdir <my-project>
cd <my-project>
```

**Windows PowerShell:**
```powershell
New-Item -ItemType Directory -Name "<my-project>"
Set-Location "<my-project>"
```

**Windows CMD:**
```cmd
mkdir <my-project>
cd <my-project>
```

### GitHub Copilot Setup

AI-DLC uses project context files and Copilot's Chat capabilities to implement its intelligent workflow. Copilot will reference these files to understand the AI-DLC methodology and guide your development process.

#### Setting Up AI-DLC Rules

Copy the AI-DLC workflow to your project's workspace:

**Unix/Linux/macOS:**
```bash
# Copy core workflow to .copilot/instructions.md
mkdir -p .copilot
cp ../aidlc-workflows/aidlc-rules/aws-aidlc-rules/core-workflow.md .copilot/instructions.md

# Copy rule details to .aidlc-rule-details (loaded on-demand by the workflow)
mkdir -p .aidlc-rule-details
cp -R ../aidlc-workflows/aidlc-rules/aws-aidlc-rule-details/* .aidlc-rule-details/
```

**Windows PowerShell:**
```powershell
# Copy core workflow to .copilot/instructions.md
New-Item -ItemType Directory -Force -Path ".copilot"
Copy-Item "..\aidlc-workflows\aidlc-rules\aws-aidlc-rules\core-workflow.md" ".copilot\instructions.md"

# Copy rule details to .aidlc-rule-details (loaded on-demand by the workflow)
New-Item -ItemType Directory -Force -Path ".aidlc-rule-details"
Copy-Item "..\aidlc-workflows\aidlc-rules\aws-aidlc-rule-details\*" ".aidlc-rule-details\" -Recurse
```

**Windows CMD:**
```cmd
REM Copy core workflow to .copilot/instructions.md
mkdir .copilot
copy "..\aidlc-workflows\aidlc-rules\aws-aidlc-rules\core-workflow.md" ".copilot\instructions.md"

REM Copy rule details to .aidlc-rule-details (loaded on-demand by the workflow)
mkdir .aidlc-rule-details
xcopy "..\aidlc-workflows\aidlc-rules\aws-aidlc-rule-details" ".aidlc-rule-details\" /E /I
```

#### Alternative Setup: Project Root COPILOT.md

You can also place instructions in the project root for easier access:

**Unix/Linux/macOS:**
```bash
# Copy core workflow to COPILOT.md in project root
cp ../aidlc-workflows/aidlc-rules/aws-aidlc-rules/core-workflow.md ./COPILOT.md

# Copy rule details to .aidlc-rule-details (loaded on-demand by the workflow)
mkdir -p .aidlc-rule-details
cp -R ../aidlc-workflows/aidlc-rules/aws-aidlc-rule-details/* .aidlc-rule-details/
```

**Windows PowerShell:**
```powershell
# Copy core workflow to COPILOT.md in project root
Copy-Item "..\aidlc-workflows\aidlc-rules\aws-aidlc-rules\core-workflow.md" ".\COPILOT.md"

# Copy rule details to .aidlc-rule-details (loaded on-demand by the workflow)
New-Item -ItemType Directory -Force -Path ".aidlc-rule-details"
Copy-Item "..\aidlc-workflows\aidlc-rules\aws-aidlc-rule-details\*" ".aidlc-rule-details\" -Recurse
```

**Windows CMD:**
```cmd
REM Copy core workflow to COPILOT.md in project root
copy "..\aidlc-workflows\aidlc-rules\aws-aidlc-rules\core-workflow.md" ".\COPILOT.md"

REM Copy rule details to .aidlc-rule-details (loaded on-demand by the workflow)
mkdir .aidlc-rule-details
xcopy "..\aidlc-workflows\aidlc-rules\aws-aidlc-rule-details" ".aidlc-rule-details\" /E /I
```

### Understanding the Configuration

**Instructions File Options:**
- **`.copilot/instructions.md`**: Structured directory approach, recommended for larger projects
- **`COPILOT.md`**: Simple root-level approach, recommended for smaller projects or quick setup

**Directory Structure After Setup (Option 1 - .copilot Directory):**
```
<my-project>/
├── .copilot/
│   └── instructions.md                   # Core AI-DLC workflow
└── .aidlc-rule-details/                  # Detailed rules (loaded on-demand)
    ├── common/                           # Common rules and standards
    ├── inception/                        # Inception phase rules
    ├── construction/                     # Construction phase rules
    └── operations/                       # Operations phase rules
```

**Directory Structure After Setup (Option 2 - Project Root):**
```
<my-project>/
├── COPILOT.md                            # Core AI-DLC workflow
└── .aidlc-rule-details/                  # Detailed rules (loaded on-demand)
    ├── common/                           # Common rules and standards
    ├── inception/                        # Inception phase rules
    ├── construction/                     # Construction phase rules
    └── operations/                       # Operations phase rules
```

### Verifying Setup

To confirm that the AI-DLC rules are correctly set up:

1. **Check file structure:**
   - `COPILOT.md` should exist in your project root OR `.copilot/instructions.md` should exist
   - `.aidlc-rule-details/` should contain subdirectories with detailed rule files

2. **Verify in VS Code:**
   - Open VS Code with your project folder
   - Open the Copilot Chat panel (Cmd/Ctrl+Shift+I or use the Chat icon)
   - Ask Copilot: "What project instructions are currently active?"
   - Copilot should acknowledge the AI-DLC workflow
   - You can reference the instructions by typing `#file .copilot/instructions.md` or `#file COPILOT.md` in the chat

3. **Test the workflow:**
   - Open Copilot Chat
   - Start a conversation: "Using AI-DLC, create a simple hello world application"
   - The AI-DLC workflow should activate and guide you through the process

**Why this separation?**
- **Core Workflow** (`COPILOT.md` or `.copilot/instructions.md`): Main workflow logic referenced by Copilot
- **Rule Details** (`.aidlc-rule-details/`): Detailed stage-specific instructions loaded on-demand by the workflow
- This keeps project structure organized while providing full functionality when needed

**Benefits:**
- **Project-specific**: Each project can have its own AI-DLC configuration
- **Version controlled**: Instructions are part of your repository
- **Simple**: Plain markdown files, no complex configuration needed
- **On-demand loading**: Detailed rules are only loaded when needed, saving context
- **Flexible**: Use Copilot Chat's `#file` references to include instructions as needed

## Best Practices for GitHub Copilot with AI-DLC

### 1. Reference Instructions Explicitly

When starting AI-DLC workflows, reference the instructions file:

**Option A - Using File Reference:**
```
#file COPILOT.md

Using AI-DLC, create a new feature for user authentication
```

**Option B - Pasting Key Instructions:**
- Copy the relevant section from your instructions file
- Paste it into the chat to ensure Copilot uses the current version

### 2. Keep Instructions Focused and Actionable

- Keep instructions concise and clear
- Use concrete examples and expected outcomes
- Provide file structure templates
- Avoid vague guidance - be specific about workflows

### 3. Maintain Up-to-Date Documentation

- Regularly update `COPILOT.md` or `.copilot/instructions.md` to reflect current project decisions
- Document architectural decisions and their rationale
- Keep instructions synchronized with your team's practices

### 4. Use Chat Context Effectively

Copilot's Chat has context limitations. For lengthy workflows:
- Start with a high-level summary of AI-DLC
- Reference `.aidlc-rule-details/` files for detailed rules
- Use `#file <filename>` syntax to include specific files
- Ask Copilot to load relevant rule details when needed

Example:
```
#file .aidlc-rule-details/inception/requirements-analysis.md

Now analyze requirements for the user authentication feature
```

### 5. Leverage Copilot Chat Features

**Using File References:**
```
#file <path/to/file.md>      # Include file content in chat
@<mention-symbol>            # Reference variables or symbols
```

**Asking Copilot to Read Files:**
- "Read the requirements from `.aidlc-rule-details/inception/requirements-analysis.md`"
- "Summarize the workflow from `COPILOT.md`"
- "What does `.aidlc-rule-details/construction/code-generation.md` specify?"

### 6. Version Control Considerations

**Commit to repository:**
```gitignore
# These should be version controlled
COPILOT.md
.copilot/instructions.md
.aidlc-rule-details/
```

**Optional - Add to `.gitignore` (if needed):**
```gitignore
# If you have local-only Copilot settings
.copilot/settings.local.json
.copilot/context/
```

## Managing Instructions

### Editing Instructions

1. Edit the instruction file directly:
   ```bash
   # Unix/Linux/macOS
   vim COPILOT.md
   # or
   vim .copilot/instructions.md

   # Windows
   notepad COPILOT.md
   # or
   notepad .copilot\instructions.md
   ```

2. Changes take effect immediately in new Copilot Chat sessions
3. For existing chat sessions, you may need to restart the chat to load updated instructions

### Adding Project-Specific Guidelines

Enhance your instructions with project-specific guidance:

```markdown
# AI-DLC Workflow

[Main workflow content here...]

## Project-Specific Guidelines

### Frontend Development
For frontend development, follow guidelines in: `.aidlc-rule-details/inception/application-design.md`

### Backend Development
For backend development, follow guidelines in: `.aidlc-rule-details/construction/functional-design.md`

### Architecture Decision
The project uses [your architecture pattern]. All new components should follow this pattern.
```

### Referencing Additional Files

You can extend your instructions by referencing other files:

```markdown
## Detailed Rules

- **Requirements Analysis**: See `.aidlc-rule-details/inception/requirements-analysis.md`
- **Code Generation**: See `.aidlc-rule-details/construction/code-generation.md`
- **Content Validation**: See `.aidlc-rule-details/common/content-validation.md`
```

## Usage

1. Start any software development project by stating your intent starting with the phrase "Using AI-DLC, ..." in the Copilot Chat
2. AI-DLC workflow automatically activates and guides you from there
3. Answer structured questions that Copilot asks you
4. Carefully review every plan that Copilot generates. Provide your oversight and validation
5. Review the execution plan to see which stages will run
6. Carefully review the artifacts and approve each stage to maintain control
7. All the artifacts will be generated in the `aidlc-docs/` directory

## Three-Phase Adaptive Workflow

AI-DLC follows a structured three-phase approach that adapts to your project's complexity:

- **🔵 INCEPTION PHASE**: Determines **WHAT** to build and **WHY**
  - Requirements analysis and validation
  - User story creation (when applicable)
  - Application Design and creating units of work for parallel development
  - Risk assessment and complexity evaluation

- **🟢 CONSTRUCTION PHASE**: Determines **HOW** to build it
  - Detailed component design
  - Code generation and implementation
  - Build configuration and testing strategies
  - Quality assurance and validation

- **🟡 OPERATIONS PHASE**: Deployment and monitoring (future)
  - Deployment automation and infrastructure
  - Monitoring and observability setup
  - Production readiness validation

## Key Features

- **Adaptive Intelligence**: Only executes stages that add value to your specific request
- **Context-Aware**: Analyzes existing codebase and complexity requirements
- **Risk-Based**: Complex changes get comprehensive treatment, simple changes stay efficient
- **Question-Driven**: Structured multiple-choice questions in files, not chat
- **Always in Control**: Review execution plans and approve each phase

## Troubleshooting

### Instructions Not Being Applied

1. **Check file exists**: Verify `COPILOT.md` or `.copilot/instructions.md` exists in project root
2. **Check file content**: Ensure the file contains the AI-DLC workflow content
3. **Ask Copilot**: Use the `#file COPILOT.md` or `#file .copilot/instructions.md` reference in chat
4. **Verify file encoding**: Ensure the file is UTF-8 encoded
5. **Start new chat session**: Instructions may be cached; start a new Copilot Chat session

### Chat Context Limitations

1. **Large instructions**: If instructions are too large, Copilot may trim them
   - Solution: Reference specific rule detail files instead of pasting everything
2. **Context overflow**: If chat context is full, add file references strategically
   - Solution: Use `#file .aidlc-rule-details/[phase]/[stage].md` to load only needed sections
3. **Token limits**: Copilot has token limits for Chat responses
   - Solution: Ask Copilot to summarize or focus on specific stages

### Rule Details Not Loading

1. **Verify directory structure**: Ensure `.aidlc-rule-details/` exists with subdirectories
2. **Check file permissions**: Ensure VS Code can read the rule detail files
3. **Reference files explicitly**: Ask Copilot to read specific files using `#file` syntax
4. **Test manually**: Try asking Copilot to read a specific rule detail file

### File Path Issues on Windows

- Use forward slashes `/` in file paths within instructions:
  ```markdown
  Read the detailed requirements from: `.aidlc-rule-details/inception/requirements-analysis.md`
  ```
- Windows paths with backslashes may not work correctly in markdown

## Integration with VS Code

### Opening Your Project

1. **Open your project in VS Code**
   - File → Open Folder → Select `<my-project>`
   - Or: `code .` in terminal

2. **Verify Copilot Extensions**
   - Check Extensions panel (Ctrl+Shift+X)
   - Ensure "GitHub Copilot" and "GitHub Copilot Chat" are installed and enabled
   - Sign in with your GitHub account if needed

3. **Open Copilot Chat**
   - Use keyboard: Cmd/Ctrl+Shift+I
   - Or click Chat icon in sidebar
   - Instructions will be available for reference

### Checking if Instructions are Loaded

In the Copilot Chat:

1. Type: `#file COPILOT.md` (or `.copilot/instructions.md`)
2. Ask: "What instructions does this file contain?"
3. Copilot will confirm it can access the file

Alternatively:
1. Ask: "What project instructions are currently active?"
2. Copilot should acknowledge the AI-DLC workflow and rules

## Advanced Configuration

### Multi-Project Workspaces

For VS Code multi-root workspaces, place instructions in each workspace folder:

```
workspace/
├── project-a/
│   ├── COPILOT.md
│   └── .aidlc-rule-details/
├── project-b/
│   ├── COPILOT.md
│   └── .aidlc-rule-details/
```

VS Code will use the instructions from the active project folder.

### Custom Project Settings

Create a `.copilot-settings.json` file for project-specific configuration:

```json
{
  "model": "gpt-4-turbo",
  "temperature": 0.7,
  "workflowPhases": ["inception", "construction"],
  "defaultStages": ["requirements-analysis", "code-generation"]
}
```

### Integration with VS Code Settings

Add Copilot-specific settings to `.vscode/settings.json`:

```json
{
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": true
  },
  "github.copilot.advanced": {
    "debug.overrideChatModel": "gpt-4-turbo",
    "debug.testOverrideProxyUrl": ""
  }
}
```

## Additional Resources

- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [GitHub Copilot Chat Documentation](https://docs.github.com/en/copilot/github-copilot-chat)
- [Copilot Chat Tips and Tricks](https://github.com/features/copilot)
- [AI-DLC Methodology Blog](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/)
- [AI-DLC Method Definition Paper](https://prod.d13rzhkk8cj2z0.amplifyapp.com/)

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
