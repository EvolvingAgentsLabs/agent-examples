# Component: SimulatedFineTunedAgent

- **Name**: SimulatedFineTunedAgent
- **Type**: AGENT
- **Description**: Simulates how a fine-tuned LLM would operate as an autonomous state machine, making external tool calls when needed to complete agentic workflows.

## Purpose

This agent demonstrates the target behavior for an LLM fine-tuned on LLM-OS execution traces. It shows how the trained model would:
1. Analyze current context and goals
2. Identify information gaps requiring external data
3. Request specific tool calls with structured parameters
4. Integrate tool results into workflow execution
5. Continue until goal completion

## Inputs

- `current_state` (object): Current execution state from execution_state.md
- `goal` (string): High-level objective to achieve
- `available_context` (string): Information currently available
- `available_tools` (array): List of tools that can be called externally

## Outputs

- `action_type` (string): "TOOL_REQUEST" or "PROCESSING_RESULT"
- `reasoning` (string): Explanation of decision-making process
- `tool_request` (object): Structured call for external tool (if needed)
- `processing_result` (object): Direct output (if sufficient context)
- `next_state` (object): Updated execution state

## Decision Logic

### Pattern Matching from Training Data

The agent uses patterns learned from LLM-OS execution traces to make decisions:

#### Pattern 1: Information Gap Detection
```
IF goal requires current/live data AND context lacks this data
THEN request WebFetch tool call
```

#### Pattern 2: File Operation Needs
```
IF workflow requires reading/writing files AND files not in context
THEN request Read/Write tool calls
```

#### Pattern 3: Complex Processing Requirements
```
IF task requires specialized analysis AND beyond current capabilities
THEN request Task tool for sub-agent processing
```

#### Pattern 4: State Persistence
```
IF execution state changes AND persistence required
THEN request Write tool for state management
```

## Simulation Modes

### Interactive Mode
```yaml
mode: interactive
behavior: 
  - Shows reasoning at each decision point
  - Requests human confirmation for tool calls
  - Explains why external data is needed
  - Demonstrates state machine transitions
```

### Autonomous Mode
```yaml
mode: autonomous
behavior:
  - Makes decisions automatically based on training patterns
  - Generates tool requests without human intervention
  - Processes results and continues workflow
  - Mimics fine-tuned model behavior
```

### Validation Mode
```yaml
mode: validation
behavior:
  - Compares decisions to training data examples
  - Measures accuracy of tool request predictions
  - Validates reasoning patterns
  - Reports simulation fidelity metrics
```

## Tool Request Generation

When the agent identifies an information gap, it generates structured tool requests:

### WebFetch Request Example
```json
{
  "action": "TOOL_REQUEST",
  "tool_name": "WebFetch",
  "reasoning": "Goal requires current AI developments from Hugging Face blog, but no recent data in context",
  "parameters": {
    "url": "https://huggingface.co/blog",
    "prompt": "Extract recent AI research and model announcements"
  },
  "expected_outcome": "Live blog content with current AI developments for analysis",
  "next_state": {
    "step": 2,
    "variables": {
      "raw_content": "workspace/huggingface_content.txt"
    }
  }
}
```

### Read Request Example
```json
{
  "action": "TOOL_REQUEST", 
  "tool_name": "Read",
  "reasoning": "Need to process previously fetched content for analysis step",
  "parameters": {
    "file_path": "workspace/huggingface_content.txt"
  },
  "expected_outcome": "Blog content loaded into context for summarization",
  "next_state": {
    "step": 3,
    "context_enhanced": true
  }
}
```

## Processing Result Generation

When sufficient context is available, the agent produces direct results:

### Analysis Result Example
```json
{
  "action": "PROCESSING_RESULT",
  "content": {
    "summary": "Analysis of Hugging Face blog content...",
    "key_insights": ["insight1", "insight2", "insight3"],
    "confidence": 0.94
  },
  "state_update": {
    "current_step": 4,
    "variables": {
      "analysis_complete": true,
      "summary_path": "workspace/analysis.json"
    }
  },
  "completion_status": "CONTINUE"
}
```

## Context Integration Logic

The agent demonstrates how a fine-tuned model would integrate external tool results:

1. **Result Validation**: Check if tool output meets expected criteria
2. **Context Enhancement**: Add new information to working context
3. **State Progression**: Update execution state with new variables
4. **Next Action Planning**: Determine subsequent steps based on enhanced context

## Training Pattern Examples

The simulation is based on these real patterns from LLM-OS training data:

### Web Research Pattern
```
Context: Need current AI news
Gap: No live data available
Tool Request: WebFetch(url, prompt)
Result Integration: Raw content → Context
Next Action: Analyze content
```

### Analysis Pattern
```
Context: Have raw content, need insights
Gap: Unprocessed information
Processing: Generate structured analysis
Result: Summary with confidence scores
Next Action: Generate report
```

### Persistence Pattern
```
Context: Have results, need to save
Gap: Results not persisted
Tool Request: Write(file_path, content)
Result Integration: Confirmation → Context
Next Action: Update state as complete
```

## Success Metrics

The simulation tracks these metrics to validate fine-tuned model behavior:

- **Decision Accuracy**: Percentage of correct tool selection decisions
- **Request Quality**: Well-formed tool requests with proper parameters
- **Context Utilization**: Effective use of available information
- **Goal Achievement**: Successful workflow completion rates
- **State Management**: Proper execution state transitions

## Usage in Training Pipeline

This agent serves as:
1. **Target Behavior Model**: Shows desired fine-tuned LLM capabilities
2. **Validation Tool**: Tests training data quality and completeness
3. **Simulation Engine**: Demonstrates autonomous agent operation
4. **Training Generator**: Creates additional training examples through simulation