# Component: RealWebFetchTool

- **Name**: RealWebFetchTool
- **Type**: TOOL
- **Description**: Advanced web content fetching using Claude Code's WebFetch tool with intelligent content processing, caching, and extraction capabilities.

## Inputs

- `url` (string): Target URL to fetch content from
- `extraction_prompt` (string): Specific prompt for content extraction
- `output_format` (string): "raw", "markdown", "structured", "summary" (default: "markdown")
- `follow_redirects` (boolean): Follow HTTP redirects (default: true)
- `timeout` (number): Request timeout in seconds (default: 30)
- `cache_duration` (number): Cache result for N minutes (default: 15)
- `extract_links` (boolean): Extract and return links found (default: false)
- `extract_images` (boolean): Extract image information (default: false)
- `content_filter` (string): Filter content by type - "text", "data", "navigation"

## Outputs

- `success` (boolean): Whether fetch operation succeeded
- `content` (string): Processed web content
- `metadata` (object): Page metadata (title, description, etc.)
- `links` (array): Extracted links (if requested)
- `images` (array): Image information (if requested)
- `performance` (object): Fetch performance metrics
- `cache_info` (object): Cache status and timing

## Tool Dependencies

- **WebFetch**: Claude Code's native web fetching capability
- Built-in content processing and extraction logic

## Content Processing Modes

### Raw Mode
- Returns unprocessed HTML content
- Useful for custom parsing requirements
- Minimal processing overhead

### Markdown Mode (Default)
- Converts HTML to clean markdown
- Removes navigation, ads, and clutter
- Preserves content structure and formatting
- Ideal for reading and analysis

### Structured Mode
- Extracts structured data (titles, headings, lists)
- Returns JSON with organized content sections
- Useful for automated processing

### Summary Mode
- Provides concise content summary
- Extracts key points and main ideas
- Includes metadata and analysis

## Logic

### EXECUTION MODE:

1. **URL Validation**:
   - Validate URL format and accessibility
   - Check against security blacklists
   - Handle protocol variations (HTTP/HTTPS)

2. **Cache Management**:
   - Check for cached content within duration
   - Return cached result if available and fresh
   - Store new results in cache with timestamp

3. **Content Fetching**:
   - Use Claude Code WebFetch tool with extraction prompt
   - Handle redirects and timeouts
   - Manage rate limiting and retries

4. **Content Processing**:
   - Apply requested output format transformation
   - Extract additional data (links, images) if requested
   - Clean and structure content appropriately

5. **Metadata Extraction**:
   - Extract page title, description, keywords
   - Identify content type and language
   - Analyze page structure and quality

### SIMULATION MODE:
1. Simulate web requests and responses
2. Generate realistic web content and metadata
3. Create training data for web scraping workflows

## Content Extraction Patterns

### News Articles
```yaml
extraction_focus: "main article content, author, publication date"
content_cleaning: "remove ads, navigation, comments"
structured_output: "headline, byline, body, metadata"
```

### Technical Documentation
```yaml
extraction_focus: "code examples, API references, procedures"
content_preservation: "maintain code formatting, links"
structured_output: "sections, code_blocks, references"
```

### Research Papers
```yaml
extraction_focus: "abstract, methodology, results, conclusions"
content_organization: "academic structure preservation"
structured_output: "abstract, sections, citations, figures"
```

### Product Pages
```yaml
extraction_focus: "product details, specifications, pricing"
data_extraction: "structured product information"
structured_output: "product_info, specs, pricing, reviews"
```

## Error Handling

### Network Errors
- **Timeout**: Request exceeds timeout limit
- **Connection Failed**: Cannot establish connection
- **DNS Resolution**: Cannot resolve hostname
- **SSL/TLS Errors**: Certificate or encryption issues

### Content Errors
- **404 Not Found**: Requested page doesn't exist
- **403 Forbidden**: Access denied to content
- **500 Server Error**: Server-side processing errors
- **Rate Limited**: Too many requests to server

### Processing Errors
- **Content Too Large**: Page exceeds size limits
- **Invalid Format**: Unable to parse content
- **Extraction Failed**: Cannot extract requested content
- **Encoding Issues**: Character encoding problems

## Performance Optimization

### Caching Strategy
- **Memory Cache**: Fast access for recent requests
- **Persistent Cache**: Longer-term storage for frequently accessed content
- **Cache Invalidation**: Smart refresh based on content type
- **Cache Sharing**: Shared cache across multiple tool instances

### Request Optimization
- **Connection Pooling**: Reuse connections for multiple requests
- **Parallel Fetching**: Concurrent requests for multiple URLs
- **Request Batching**: Combine related requests
- **Smart Retry**: Exponential backoff with jitter

## Security Features

### URL Safety
- **Blacklist Checking**: Block known malicious domains
- **Protocol Validation**: Only allow HTTP/HTTPS protocols
- **Redirect Limits**: Prevent infinite redirect loops
- **Content Size Limits**: Prevent memory exhaustion

### Content Sanitization
- **Script Removal**: Strip JavaScript and executable content
- **Safe HTML**: Allow only safe HTML tags
- **Link Validation**: Verify extracted links
- **Privacy Protection**: Remove tracking parameters

## Performance Characteristics

```yaml
cost: medium (depends on page size and processing)
latency: medium (5-30 seconds depending on site response)
side_effects: "Creates cache files, makes external HTTP requests"
error_modes: ["timeout", "connection_failed", "content_too_large", "rate_limited"]
cache_enabled: true
concurrent_requests: "limited to prevent abuse"
```

## Usage Examples

**Fetch and summarize news article:**
```
Input: {
  url: "https://example.com/news/article",
  extraction_prompt: "Extract the main news story, key facts, and quotes",
  output_format: "structured",
  extract_links: false
}
Output: {
  success: true,
  content: {
    headline: "Major Tech Announcement",
    summary: "Company announces new product...",
    key_facts: ["fact1", "fact2", "fact3"],
    quotes: ["quote from CEO", "analyst comment"]
  },
  metadata: {
    title: "Article Title",
    author: "Reporter Name",
    published: "2024-01-15"
  }
}
```

**Extract documentation content:**
```
Input: {
  url: "https://docs.example.com/api/reference",
  extraction_prompt: "Extract API documentation including endpoints, parameters, and examples",
  output_format: "markdown",
  extract_links: true
}
Output: {
  success: true,
  content: "# API Reference\n\n## Endpoints\n...",
  links: [
    {"text": "Getting Started", "url": "/getting-started"},
    {"text": "Authentication", "url": "/auth"}
  ],
  metadata: {
    title: "API Reference",
    last_updated: "2024-01-10"
  }
}
```

**Research multiple sources:**
```
Input: {
  url: "https://research.example.com/papers/ai-safety",
  extraction_prompt: "Extract research methodology, key findings, and conclusions",
  output_format: "summary",
  cache_duration: 60
}
Output: {
  success: true,
  content: "Research Summary: This study investigates...",
  metadata: {
    paper_title: "AI Safety Research",
    authors: ["Dr. Smith", "Dr. Johnson"],
    publication_date: "2024-01-01",
    citation_count: 42
  }
}
```

## Integration with Claude Code WebFetch

### Direct Tool Mapping
```yaml
RealWebFetchTool_request → WebFetch_tool_call
parameters:
  url: "{input.url}"
  prompt: "{input.extraction_prompt}"
```

### Enhanced Processing
- **Intelligent Prompting**: Optimizes extraction prompts based on content type
- **Content Classification**: Automatically detects content type and adjusts processing
- **Quality Assessment**: Evaluates content quality and completeness
- **Format Optimization**: Chooses best output format for content type

## Cache Management

### Cache Storage
```json
{
  "cache_entry": {
    "url": "https://example.com/page",
    "content": "processed content...",
    "metadata": {...},
    "timestamp": "2024-01-15T10:30:00Z",
    "expiry": "2024-01-15T10:45:00Z",
    "access_count": 3,
    "content_hash": "sha256:abc123..."
  }
}
```

### Cache Strategies
- **Time-Based**: Expire after specified duration
- **Content-Based**: Check for content changes
- **Usage-Based**: Prioritize frequently accessed content
- **Size-Based**: Manage cache size and memory usage

## Training Data Format

```json
{
  "tool_execution": {
    "tool": "RealWebFetchTool",
    "inputs": {
      "url": "https://example.com/article",
      "extraction_prompt": "Extract main content and key points",
      "output_format": "structured"
    },
    "claude_code_calls": [
      {
        "tool": "WebFetch",
        "url": "https://example.com/article",
        "prompt": "Extract main content and key points"
      }
    ],
    "outputs": {
      "success": true,
      "content": {...},
      "metadata": {...}
    },
    "performance": {
      "fetch_time": "3.2s",
      "processing_time": "1.1s",
      "cache_hit": false,
      "content_size": "15KB"
    }
  }
}
```

## Advanced Features

### Intelligent Content Recognition
- **Content Type Detection**: Automatically identify content type (news, docs, research)
- **Structure Analysis**: Understand page layout and organization
- **Quality Assessment**: Evaluate content quality and reliability
- **Language Detection**: Identify content language for appropriate processing

### Multi-URL Operations
- **Batch Fetching**: Process multiple URLs efficiently
- **Cross-Reference**: Find connections between related pages
- **Site Crawling**: Navigate through linked content systematically
- **Comparison**: Compare content across multiple sources

### Specialized Extractors
- **Academic Papers**: Extract citations, methodology, results
- **News Articles**: Extract facts, quotes, sources
- **Product Pages**: Extract specifications, pricing, reviews
- **Technical Docs**: Extract code examples, API references

This tool provides the foundation for all web-based data collection and analysis within the LLMunix framework, offering reliable, intelligent, and efficient web content access.