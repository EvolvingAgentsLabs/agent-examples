# Component: RealSummarizationAgent

- **Name**: RealSummarizationAgent
- **Type**: AGENT  
- **Description**: Advanced summarization agent that reads real files and generates structured summaries using Claude Code's native capabilities.

## Inputs

- `input_source` (string): Source type - "file", "url", "text"
- `input_path` (string): File path or URL to summarize
- `input_text` (string): Direct text input (if source is "text")
- `output_format` (string): "json", "markdown", "plain" (default: "json")
- `summary_length` (string): "brief", "detailed", "executive" (default: "brief")
- `focus_areas` (array): Specific aspects to emphasize

## Outputs

- `summary` (object/string): Generated summary in requested format
- `key_points` (array): Main points extracted
- `metadata` (object): Analysis metadata (word count, sentiment, etc.)
- `confidence` (number): Confidence score 0-1

## Tool Dependencies

- **RealFileSystemTool**: For reading input files
- **RealWebFetchTool**: For URL-based inputs
- Built-in LLM reasoning: For analysis and summarization

## Logic

### EXECUTION MODE:

1. **Input Processing**:
   - If input_source is "file": Use RealFileSystemTool to read content
   - If input_source is "url": Use RealWebFetchTool to fetch content  
   - If input_source is "text": Use input_text directly

2. **Content Analysis**:
   - Analyze content length and complexity
   - Identify key themes and topics
   - Extract factual information and opinions
   - Assess content structure and organization

3. **Summary Generation**:
   - Generate summary based on length preference
   - Structure output according to format specification
   - Include focus areas if specified
   - Calculate confidence score

4. **Output Formatting**:
   - Format according to output_format
   - Include metadata and analysis details
   - Validate output structure

### SIMULATION MODE:
1. Simulate content reading from various sources
2. Generate realistic summary outputs
3. Create training data for multi-modal summarization

## Output Formats

### JSON Format
```json
{
  "title": "Content Title",
  "summary": "Concise summary text...",
  "key_points": [
    "Key point 1",
    "Key point 2", 
    "Key point 3"
  ],
  "metadata": {
    "word_count": 1500,
    "reading_time": "6 min",
    "sentiment": "neutral",
    "topics": ["business", "technology"]
  },
  "confidence": 0.89
}
```

### Markdown Format
```markdown
# Content Title

## Summary
Concise summary text...

## Key Points
- Key point 1
- Key point 2
- Key point 3

## Metadata
- Word Count: 1500
- Reading Time: 6 min
- Confidence: 89%
```

### Plain Format
```
Title: Content Title

Summary: Concise summary text...

Key Points:
1. Key point 1
2. Key point 2  
3. Key point 3
```

## Usage Examples

**Summarize web article:**
```
Input: {
  input_source: "url",
  input_path: "https://example.com/article",
  output_format: "json",
  summary_length: "brief"
}
Output: {JSON summary object}
```

**Summarize local file:**
```
Input: {
  input_source: "file", 
  input_path: "workspace/document.txt",
  output_format: "markdown",
  summary_length: "detailed"
}
Output: {Markdown formatted summary}
```

## Quality Metrics

- **Completeness**: All key information captured
- **Accuracy**: Factual correctness maintained
- **Conciseness**: Appropriate length for summary_length
- **Clarity**: Clear, readable language
- **Structure**: Well-organized output

## Error Handling

- **Content Too Long**: Chunk processing for large documents
- **Content Unavailable**: Clear error with retry suggestions
- **Format Invalid**: Default to plain text with warning
- **Low Confidence**: Flag for human review

## Performance Characteristics

```yaml
cost: medium (depends on content length)
latency: medium (5-30 seconds)
side_effects: "May create intermediate analysis files"
error_modes: ["content_unavailable", "format_error", "analysis_timeout"]
quality_metrics: ["accuracy", "completeness", "clarity"]
```

## Training Data Format

```json
{
  "agent_execution": {
    "agent": "RealSummarizationAgent",
    "inputs": {...},
    "tool_calls": [
      {"tool": "Read", "file": "input.txt"},
      {"tool": "Write", "file": "summary.json"}
    ],
    "outputs": {...},
    "performance": {"quality_score": 0.89, "time": "12s"}
  }
}
```