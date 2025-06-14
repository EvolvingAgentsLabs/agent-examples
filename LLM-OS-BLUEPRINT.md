# LLM-OS: Claude Code Runtime Architecture

## Overview

LLM-OS uses Claude Code as its runtime engine. Instead of simulation, it performs real operations using Claude Code's native tools while maintaining the document-centric agent framework approach.

## Architecture

### Core Concept: Dual-Mode Operation

LLM-OS operates in two modes seamlessly:

1. **Training Data Generation Mode**: Pure document simulation for creating fine-tuning datasets
2. **Execution Mode**: Real tool execution through Claude Code's native capabilities

### Key Components

#### 1. State Machine Engine (`workspace/execution_state.md`)
- Tracks current execution state, step, and variables
- Records tool call results and state transitions  
- Enables pausable, resumable execution
- Provides atomic state transitions

#### 2. Enhanced SystemAgent (`system/SystemAgent.md`)
- Orchestrates execution using Claude Code tools
- Manages state transitions
- Handles error recovery and adaptation
- Supports both simulation and real execution modes

#### 3. Real Tool Mapping (`system/ClaudeCodeToolMap.md`)
- Maps abstract framework tools to Claude Code native tools
- Defines cost, latency, and side-effect metadata
- Enables intelligent tool selection

#### 4. Training Data Generator (`system/TrainingDataCollector.md`)
- Captures execution traces for fine-tuning
- Records state transitions and tool results
- Generates structured datasets

## Tool Integration Strategy

### Native Claude Code Tools Available:
- **WebFetch**: Real web content retrieval
- **Read/Write**: File system operations  
- **Bash**: System command execution
- **Grep/Glob**: Code search and file discovery
- **Task**: Automated sub-task execution

### Framework Tool Mapping:
```markdown
WebFetcherTool → WebFetch tool
FileWriterTool → Write tool  
FileReaderTool → Read tool
SearchTool → Grep/Glob tools
SystemTool → Bash tool
SubTaskTool → Task tool
```

## Execution Flow

1. **Goal Input**: User provides high-level goal
2. **State Initialization**: Create `workspace/execution_state.md` 
3. **Planning Phase**: SystemAgent reads memory/library, creates execution plan
4. **State Machine Loop**:
   - Read current state from `execution_state.md`
   - Execute next planned step using real Claude Code tools
   - Update state with results
   - Continue until goal achieved
5. **Memory Update**: Record experience in SmartMemory
6. **Training Data Export**: Save execution trace for fine-tuning

## Key Innovations

### 1. Grounded Tool Metadata
Components now include real-world characteristics:
- `cost`: Token/API cost estimates
- `latency`: Expected execution time
- `side_effects`: System state changes
- `error_modes`: Common failure patterns

### 2. Error Recovery & Adaptation
- Real error handling from actual tool failures
- Network timeouts, file system errors, API limits
- Dynamic plan adjustment based on actual results

### 3. Human-in-the-Loop Integration
- Pause execution for human input/approval
- Capture human feedback for training data
- Interactive debugging and guidance

### 4. Multi-Modal Capability  
- Image processing through Claude Code's vision
- File type detection and appropriate handling
- Structured data manipulation (JSON, CSV, etc.)

## Training Data Generation

Every execution generates a complete training example:

```json
{
  "execution_id": "exec_001",
  "goal": "Get weather for London and save to file",
  "initial_state": { ... },
  "transitions": [
    {
      "step": 1,
      "tool": "WebFetch",
      "inputs": { "url": "weather-api.com/london" },
      "outputs": { "content": "London: 15°C, cloudy" },
      "state_after": { ... }
    }
  ],
  "final_outcome": "success",
  "total_cost": "$0.0023",
  "execution_time": "4.2s"
}
```

## Benefits Over Previous Approach

1. **Real Execution**: Actual tool calls with real results
2. **Cost Awareness**: Learns actual costs and trade-offs
3. **Error Resilience**: Handles real-world failures
4. **Performance Optimization**: Optimizes for actual latency/cost
5. **Human Collaboration**: Natural human-AI interaction
6. **Rich Training Data**: Captures real execution complexity

## Implementation Plan

1. Create execution state management system
2. Update SystemAgent for Claude Code tool integration  
3. Build tool mapping and metadata system
4. Implement training data collection
5. Create demonstration scenarios
6. Test end-to-end execution and data generation

This architecture transforms AGI-DAF from a simulation into a practical, production-ready agent framework that generates its own training data through real-world execution.