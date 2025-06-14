# LLMUNIX Agentic Examples

Welcome to the official examples repository for **LLMUNIX**, the document-centric operating system powered by the [Evolving Agents Labs Framework Core](https://github.com/EvolvingAgentsLabs/framework-core).

This repository contains a curated collection of high-impact examples demonstrating the core power of the framework: **providing a simple, natural language goal and watching the OS autonomously create the entire agent and tool toolchain needed to accomplish it.**

## How to Run These Examples

This repository is designed to be run using **Claude Code**, which acts as the runtime engine for the LLMUNIX operating system.

### Prerequisites

**Install and Start Claude Code:**
1. First, ensure you have Claude Code installed on your system
2. Open your terminal/command prompt
3. Start Claude Code by running:
   ```bash
   claude
   ```
4. This will open the Claude Code console interface

### Step 1: Load the LLMUNIX Framework

Once you're in the Claude Code console, you need to load the LLMUNIX operating system framework.

**Action:**
1. Copy the **entire contents** of the `CLAUDE.md` file from this repository
2. Paste it directly into the Claude Code console as your first command
3. Press Enter to execute

Claude Code will acknowledge that it has loaded the LLMUNIX project and is ready to act as the operating system runtime.

### Step 2: Choose and Run a Scenario

Each example in the `examples/` directory contains a `scenario.md` file with a specific user goal to demonstrate LLMUNIX capabilities.

**Action:**
1. Choose an example, for instance, `01_Legal_Contract_Analysis`
2. Open the `examples/01_Legal_Contract_Analysis/scenario.md` file
3. Copy the user goal from that file
4. In the Claude Code console, paste the goal prefixed with the `llmunix>` prompt

**Example Command:**
```
llmunix> I have a new service agreement from a vendor. Please act as a paralegal, review the attached contract, and give me a summary of the key terms, including the parties involved, the effective date, the term length, payment details, and any potential risks or non-standard clauses I should be aware of. The contract text is: """SERVICE AGREEMENT This Agreement is made effective as of January 1, 2025..."""
```

### Step 3: Observe the Autonomous Workflow

Claude Code, running LLMUNIX, will now perform the entire task autonomously. You will observe it:

1. **Analyze the Goal:** Parse and understand the specific requirements (legal analysis in this case)
2. **Consult Smart Memory:** Check for relevant past experiences and learned patterns
3. **Consult the Library:** Review `system/SmartLibrary.md` to find available components
4. **Create Missing Components:** If needed tools don't exist, autonomously generate them:
   - Announce capability gaps (e.g., "No legal analysis tools found")
   - Generate complete markdown definitions for new components (e.g., `ContractAnalysisAgent`, `RiskDetectionTool`)
   - Update the SmartLibrary registry with new components
5. **Plan Execution:** Create a detailed step-by-step execution plan in `execution_state.md`
6. **Execute State Machine:** Use real Claude Code tools (WebFetch, Read, Write, etc.) to complete each step
7. **Generate Results:** Create deliverable files in the workspace directory
8. **Update Memory:** Record the experience for future learning

### Working with Claude Code Console

**Key Commands:**
```bash
# View current directory and files
ls

# Read scenario files
cat examples/01_Legal_Contract_Analysis/scenario.md

# Monitor execution progress
cat workspace/execution_state.md

# View generated results
ls workspace/
```

**Tips for Claude Code Usage:**
- Use `ls` to explore the directory structure
- Use `cat` to read file contents  
- The `workspace/` directory will contain all generated outputs
- LLMUNIX uses real Claude Code tools for actual file operations
- All tool executions are logged for transparency

## Available Examples

-   **[01_Legal_Contract_Analysis](./examples/01_Legal_Contract_Analysis/):** An agent that acts as a paralegal, analyzing a service agreement to extract key terms, dates, and potential risks.
-   **[02_Marketing_Campaign_Generator](./examples/02_Marketing_Campaign_Generator/):** An agent that acts as a marketing assistant, creating a complete multi-channel marketing campaign from a simple product description.
-   **[03_Healthcare_Patient_Onboarding](./examples/03_Healthcare_Patient_Onboarding/):** An agent that simulates a HIPAA-compliant patient intake process, generating forms and summarizing patient information.

## Key Features Demonstrated

### Zero-to-Tool Capability
Watch LLMUNIX autonomously generate specialized tools on-demand:
- **Legal Analysis Tools** for contract review and risk assessment
- **Marketing Tools** for campaign generation and content creation  
- **Healthcare Tools** for HIPAA-compliant patient processing
- **Custom Tools** tailored to your specific domain requirements

### Zero-to-Agent Capability  
Observe intelligent agents being created dynamically:
- **Decision-making agents** that understand domain-specific requirements
- **Multi-step workflow agents** that coordinate complex processes
- **Learning agents** that improve performance based on outcomes
- **Specialized agents** for legal, marketing, healthcare, and other domains

### Real Claude Code Integration
All examples use actual Claude Code tools for:
- **Live web fetching** with real HTTP requests and error handling
- **Real file operations** creating actual deliverable files
- **State management** with persistent execution tracking
- **Training data generation** from real execution traces

## Advanced Usage

### Custom Scenarios
You can create your own scenarios by:
1. Creating a new directory in `examples/`
2. Adding a `README.md` with the goal description
3. Adding a `scenario.md` with the specific user goal
4. Running the scenario through LLMUNIX

### Extending the Framework
LLMUNIX learns and evolves:
- New tools and agents are automatically registered
- The SmartMemory system captures execution patterns
- Future runs leverage learned optimizations
- Training data improves autonomous capabilities

## Contributing

We welcome contributions to expand the LLMUNIX examples! Here's how you can contribute:

### Adding New Examples

1. **Fork the Repository**
   ```bash
   git fork https://github.com/EvolvingAgentsLabs/agent-examples
   cd agent-examples
   ```

2. **Create a New Example**
   ```bash
   mkdir examples/04_Your_Example_Name
   cd examples/04_Your_Example_Name
   ```

3. **Create Required Files**
   - `README.md`: Describe the example's purpose and what it demonstrates
   - `scenario.md`: Contains the specific user goal and any test data

4. **Example Structure**
   ```markdown
   # README.md
   # Your Example Name
   
   **Goal:** [Brief description of what this example does]
   
   **Demonstrates:** [Key capabilities showcased, e.g., "Real-time data processing, API integration, and automated reporting"]
   
   # scenario.md  
   ### User Goal
   [The specific natural language goal that users will paste into LLMUNIX]
   ```

5. **Test Your Example**
   - Load LLMUNIX in Claude Code using the `CLAUDE.md` file
   - Run your scenario to ensure it works correctly
   - Verify that LLMUNIX creates appropriate tools and agents
   - Check that deliverable files are generated in `workspace/`

6. **Submit a Pull Request**
   - Commit your changes with a descriptive message
   - Push to your fork and create a pull request
   - Include a description of what your example demonstrates

### Example Categories We're Looking For

- **Business Intelligence:** Data analysis, reporting, dashboard generation
- **Content Creation:** Writing, editing, multimedia content generation  
- **Software Development:** Code analysis, documentation, testing automation
- **Research & Analysis:** Literature review, data mining, trend analysis
- **Education & Training:** Curriculum development, assessment creation
- **Finance & Accounting:** Financial analysis, compliance checking, reporting
- **HR & Recruitment:** Resume analysis, interview scheduling, onboarding
- **Customer Service:** Ticket analysis, response generation, workflow automation

### Quality Guidelines

**Good Examples Should:**
- Demonstrate real-world, practical use cases
- Require LLMUNIX to create multiple tools/agents
- Show complex multi-step workflows
- Include realistic test data or scenarios
- Generate meaningful deliverable outputs

**Technical Requirements:**
- Include comprehensive `README.md` documentation
- Provide clear, specific goals in `scenario.md`
- Test successfully with Claude Code runtime
- Follow existing naming conventions
- Include realistic complexity requiring tool generation

### Getting Help

- **Questions:** Open a discussion in the repository
- **Bug Reports:** Create an issue with reproduction steps  
- **Feature Requests:** Describe your use case and desired capabilities
- **Documentation:** Help improve setup instructions and examples

### Recognition

Contributors will be:
- Listed in project acknowledgments
- Credited in example documentation
- Invited to collaborate on future developments
- Recognized for expanding LLMUNIX capabilities

## Acknowledgements

*   Original Concept Contributors: [Matias Molinas](https://github.com/matiasmolinas) and [Ismael Faro](https://github.com/ismaelfaro).

*LLMUNIX: Where simulation meets reality, and training data drives the future of autonomous AI.*