# Component: FileWriterTool

- **Name**: FileWriterTool
- **Type**: TOOL
- **Description**: Writes content to files in the workspace with error handling, backup management, and atomic operations.

## Inputs

- `file_path` (string): Path within workspace/ to write content
- `content` (string): Content to write to the file
- `mode` (string): "overwrite", "append", "create_only" (default: "overwrite")
- `encoding` (string): File encoding (default: "utf-8")
- `backup` (boolean): Create backup before overwriting (default: true)
- `atomic` (boolean): Use atomic write operations (default: true)

## Outputs

- `success` (boolean): Whether the write operation succeeded
- `file_path` (string): Full path of the written file
- `bytes_written` (number): Number of bytes written
- `backup_path` (string): Path to backup file (if created)
- `timestamp` (string): ISO timestamp of write operation

## Tool Dependencies

- **RealFileSystemTool**: For actual file operations
- Built-in error handling and validation

## Logic

### EXECUTION MODE:

1. **Path Validation**:
   - Ensure file_path is within workspace/ directory
   - Validate filename and directory structure
   - Check write permissions and disk space

2. **Backup Management** (if enabled):
   - Check if file exists
   - Create timestamped backup copy
   - Verify backup creation success

3. **Atomic Write Operation**:
   - Write to temporary file first
   - Validate content was written correctly
   - Atomically move to target location
   - Clean up temporary files

4. **Verification**:
   - Confirm file exists at target location
   - Verify file size and content integrity
   - Update file metadata

### SIMULATION MODE:
1. Simulate file system interactions
2. Generate realistic write operation results
3. Create training data for file management workflows

## Write Modes

### Overwrite Mode (default)
- Replaces existing file content completely
- Creates backup if file exists and backup=true
- Most common operation for saving results

### Append Mode
- Adds content to end of existing file
- Creates file if it doesn't exist
- Useful for logging and incremental data collection

### Create Only Mode
- Only creates new files, fails if file exists
- Prevents accidental overwrites
- Ideal for ensuring unique file creation

## Error Handling

### Common Error Scenarios
- **Permission Denied**: File or directory not writable
- **Disk Full**: Insufficient storage space
- **Path Not Found**: Directory doesn't exist
- **File Locked**: File in use by another process
- **Invalid Path**: Path contains invalid characters

### Recovery Strategies
- **Auto-Retry**: Retry write operations with exponential backoff
- **Alternative Paths**: Try alternative file locations
- **Cleanup**: Remove partial files on failure
- **Rollback**: Restore from backup on atomic operation failure

## Security Features

### Path Safety
- Restricts writes to workspace/ directory only
- Prevents directory traversal attacks
- Validates file extension and content type

### Content Validation
- Optional content sanitization
- File size limits
- Content type verification

### Audit Trail
- Logs all write operations
- Records file access patterns
- Maintains operation history

## Performance Characteristics

```yaml
cost: low (minimal computational overhead)
latency: low (1-5 seconds depending on file size)
side_effects: "Creates files, may create backups"
error_modes: ["permission_denied", "disk_full", "path_invalid", "file_locked"]
atomic_operations: true
backup_support: true
```

## Usage Examples

**Basic file write:**
```
Input: {
  file_path: "results/analysis.txt",
  content: "Analysis results...",
  mode: "overwrite"
}
Output: {success: true, file_path: "workspace/results/analysis.txt", bytes_written: 156}
```

**Append to log file:**
```
Input: {
  file_path: "logs/execution.log",
  content: "2024-01-15 10:30:00 - Task completed\n",
  mode: "append",
  backup: false
}
Output: {success: true, file_path: "workspace/logs/execution.log", bytes_written: 45}
```

**Safe creation of new file:**
```
Input: {
  file_path: "reports/unique_report.json",
  content: '{"data": "..."}',
  mode: "create_only",
  atomic: true
}
Output: {success: true, file_path: "workspace/reports/unique_report.json"}
```

## Integration with RealFileSystemTool

### Direct Mapping
```yaml
FileWriterTool_operation → Write_tool_call
parameters:
  file_path: "workspace/{input.file_path}"
  content: "{input.content}"
```

### Enhanced Features
- Automatic workspace/ prefix handling
- Backup management (not available in basic Write tool)
- Atomic operations with rollback
- Enhanced error reporting and recovery

## Training Data Format

```json
{
  "tool_execution": {
    "tool": "FileWriterTool",
    "inputs": {
      "file_path": "analysis/results.md",
      "content": "# Analysis Results\n...",
      "mode": "overwrite",
      "backup": true
    },
    "claude_code_calls": [
      {"tool": "Write", "file_path": "workspace/analysis/results.md", "content": "..."}
    ],
    "outputs": {
      "success": true,
      "file_path": "workspace/analysis/results.md", 
      "bytes_written": 1247,
      "backup_path": "workspace/.backups/results_20240115_103000.md"
    },
    "performance": {
      "execution_time": "0.8s",
      "backup_time": "0.2s",
      "verification_time": "0.1s"
    }
  }
}
```

## Best Practices

### File Organization
- Use descriptive filenames with timestamps
- Organize files in logical directory structures
- Maintain consistent naming conventions

### Content Management
- Include metadata headers in files
- Use appropriate file extensions
- Consider file size and performance implications

### Error Prevention
- Always validate inputs before writing
- Use atomic operations for critical files
- Maintain backups of important data
- Monitor disk space and permissions

### Performance Optimization
- Batch multiple writes when possible
- Use appropriate write modes for use case
- Clean up temporary and backup files regularly
- Monitor file system performance