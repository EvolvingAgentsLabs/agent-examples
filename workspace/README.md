# Workspace Directory

## Overview
The workspace directory serves as the primary working area for LLMunix executions, containing all input files, intermediate results, outputs, and execution state.

## Directory Structure

```
workspace/
├── README.md              # This file
├── execution_state.md     # Current execution state (created during runs)
├── data/                  # Input data and source files
├── results/               # Final outputs and reports
├── logs/                  # Execution logs and debug information
├── cache/                 # Cached web content and tool results
└── temp/                  # Temporary files and intermediate processing
```

## Directory Descriptions

### data/
Contains input files and source data for processing:
- Document files to be analyzed
- Configuration files
- Reference data and templates
- User-provided inputs

### results/
Final outputs from completed executions:
- Generated reports and analysis
- Processed data files
- Summary documents
- Deliverable assets

### logs/
Execution logging and debugging information:
- Agent execution logs
- Tool invocation records
- Error logs and debugging traces
- Performance metrics

### cache/
Cached data to improve performance:
- Web content cache (15-minute default)
- Tool result cache
- Processed data cache
- External API responses

### temp/
Temporary files during processing:
- Intermediate processing results
- Partial outputs
- Working files
- Cleanup candidates

## File Naming Conventions

### Timestamps
Use ISO 8601 format for timestamps in filenames:
- `analysis_2024-01-15T10-30-00Z.md`
- `report_20240115_103000.json`

### Execution IDs
Include execution ID in generated files:
- `exec_001_research_report.md`
- `campaign_gen_002_content.json`

### Component Names
Include generating component in filename:
- `summarization_agent_output.md`
- `web_fetch_cache_001.json`

## File Management

### Automatic Cleanup
- Temp files: Cleaned after successful execution
- Old cache files: Removed after expiration
- Log rotation: Keep last 30 days by default

### Backup Strategy
- Critical state files backed up automatically
- User can manually backup workspace contents
- Version control recommended for important projects

### Security
- Workspace isolated from system directories
- No access outside workspace tree
- Sensitive data handling per GDPR/privacy requirements

## Usage Examples

### Basic Execution
```bash
# LLMunix automatically creates and manages workspace structure
# Users typically only need to place input files in data/
cp my_document.pdf workspace/data/
```

### Manual File Organization
```bash
# Organize input data
mkdir -p workspace/data/contracts
cp *.pdf workspace/data/contracts/

# Check execution results
ls workspace/results/
```

### Workspace Cleanup
```bash
# Clean temporary files
rm -rf workspace/temp/*

# Clear old cache (optional)
rm -rf workspace/cache/*
```

## Integration with LLMunix

### State Management
- `execution_state.md` created automatically during runs
- State persisted across pauses and resumes
- Recovery possible from last checkpoint

### Tool Integration
- All tools operate within workspace boundaries
- File paths automatically prefixed with workspace/
- Security sandbox prevents external access

### Data Flow
1. Input data placed in `data/` directory
2. Tools process data within workspace
3. Intermediate results stored in `temp/`
4. Final outputs saved to `results/`
5. Execution state tracked in root

## Best Practices

### Organization
- Use descriptive directory names for complex projects
- Group related files together
- Include documentation with data files

### Performance
- Clean temp files regularly
- Monitor cache size and effectiveness
- Use workspace for all file operations

### Security
- Never store credentials in workspace
- Review generated files before sharing
- Use appropriate file permissions

### Collaboration
- Document file purposes and formats
- Use version control for shared workspaces
- Include metadata with important files

This workspace structure ensures organized, secure, and efficient execution of LLMunix workflows while maintaining clear separation between inputs, processing, and outputs.