# Component: WebFetcherTool

- **Name**: WebFetcherTool
- **Type**: TOOL
- **Description**: Legacy web content fetching tool maintained for backward compatibility with existing workflows. Provides basic web content retrieval functionality.

## Inputs

- `url` (string): The URL to fetch content from
- `prompt` (string): Optional prompt for content extraction (default: "Extract main content")

## Outputs

- `content` (string): The fetched and processed web content
- `status` (string): "success" or "error"
- `error_message` (string): Error description if fetch failed

## Tool Dependencies

- **RealWebFetchTool**: Enhanced version with advanced features
- **WebFetch**: Claude Code's native web fetching capability

## Logic

### EXECUTION MODE:

1. **Input Validation**:
   - Validate URL format
   - Apply basic security checks
   - Set default extraction prompt if not provided

2. **Content Fetching**:
   - Delegate to RealWebFetchTool for actual processing
   - Use simplified parameter mapping
   - Return basic success/error status

3. **Legacy Compatibility**:
   - Maintain original output format
   - Provide simplified error handling
   - Support existing workflow integrations

### SIMULATION MODE:
1. Simulate basic web content fetching
2. Generate simple training examples
3. Maintain compatibility with legacy simulations

## Migration Notice

**DEPRECATED**: This tool is maintained for backward compatibility only. New implementations should use **RealWebFetchTool** which provides:

- Advanced content processing options
- Comprehensive error handling
- Performance optimization features
- Caching capabilities
- Security enhancements
- Better metadata extraction

## Simplified Usage

### Basic Web Content Fetch
```
Input: {
  url: "https://example.com/article",
  prompt: "Extract the main article content"
}
Output: {
  content: "Article content in markdown format...",
  status: "success"
}
```

### Error Response
```
Input: {
  url: "https://invalid-url.com",
  prompt: "Extract content"
}
Output: {
  content: "",
  status: "error", 
  error_message: "Unable to fetch content from URL"
}
```

## Mapping to RealWebFetchTool

This tool internally maps to RealWebFetchTool with simplified parameters:

```yaml
WebFetcherTool_request → RealWebFetchTool_request
url: "{input.url}"
extraction_prompt: "{input.prompt || 'Extract main content'}"
output_format: "markdown"
follow_redirects: true
timeout: 30
cache_duration: 15
```

## Performance Characteristics

```yaml
cost: medium (same as RealWebFetchTool)
latency: medium (5-30 seconds)
side_effects: "Creates cache files through RealWebFetchTool"
error_modes: ["timeout", "connection_failed", "invalid_url"]
cache_enabled: true (through RealWebFetchTool)
```

## Legacy Support Features

### Existing Workflow Compatibility
- Maintains original function signatures
- Preserves expected output formats
- Supports legacy error handling patterns
- Compatible with existing agent definitions

### Migration Path
1. **Phase 1**: Continue using WebFetcherTool with legacy workflows
2. **Phase 2**: Update workflows to use RealWebFetchTool parameters
3. **Phase 3**: Retire WebFetcherTool and update all references

### Upgrade Benefits
Moving to RealWebFetchTool provides:
- **Enhanced Processing**: Multiple output formats and content filters
- **Better Error Handling**: Detailed error reporting and recovery
- **Performance Features**: Caching, parallel requests, optimization
- **Security Improvements**: Enhanced URL validation and content sanitization
- **Metadata Access**: Rich page metadata and analysis

## Training Data Format

```json
{
  "tool_execution": {
    "tool": "WebFetcherTool",
    "inputs": {
      "url": "https://example.com/page",
      "prompt": "Extract main content"
    },
    "internal_mapping": {
      "tool": "RealWebFetchTool",
      "mapped_inputs": {
        "url": "https://example.com/page",
        "extraction_prompt": "Extract main content",
        "output_format": "markdown"
      }
    },
    "outputs": {
      "content": "Processed content...",
      "status": "success"
    },
    "performance": {
      "execution_time": "5.2s",
      "compatibility_layer": "active"
    }
  }
}
```

## Error Handling

### Simplified Error Responses
- **Network Errors**: Generic "connection failed" message
- **Content Errors**: Basic "content unavailable" message  
- **Timeout Errors**: Simple "request timeout" message
- **URL Errors**: Basic "invalid URL" message

### Error Recovery
- Limited retry capabilities (handled by RealWebFetchTool)
- Basic timeout handling
- Simple fallback to empty content

## Usage Recommendations

### For New Projects
```markdown
❌ DON'T USE: WebFetcherTool
✅ USE INSTEAD: RealWebFetchTool
```

### For Existing Projects
```markdown
✅ CURRENT: Continue using WebFetcherTool for compatibility
🔄 MIGRATION: Plan upgrade to RealWebFetchTool
📅 TIMELINE: Migrate before next major version
```

### Migration Example
```yaml
# OLD (WebFetcherTool)
tool: WebFetcherTool
inputs:
  url: "https://example.com"
  prompt: "Extract content"

# NEW (RealWebFetchTool)  
tool: RealWebFetchTool
inputs:
  url: "https://example.com"
  extraction_prompt: "Extract content"
  output_format: "markdown"
  cache_duration: 15
```

## Maintenance Status

### Current Support Level
- **Bug Fixes**: Critical issues only
- **Features**: No new features planned
- **Updates**: Security updates through RealWebFetchTool
- **Documentation**: Maintenance mode only

### End-of-Life Planning
- **Deprecation Notice**: Already announced
- **Support Timeline**: Until migration complete
- **Removal Schedule**: TBD based on usage analytics
- **Migration Tools**: Available for automatic conversion

This tool serves as a compatibility bridge while projects migrate to the enhanced RealWebFetchTool, ensuring existing workflows continue to function while providing a clear upgrade path.