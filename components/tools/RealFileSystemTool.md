# Component: RealFileSystemTool

- **Name**: RealFileSystemTool
- **Type**: TOOL
- **Description**: Comprehensive file system operations using Claude Code's native Read/Write tools with advanced file management capabilities.

## Inputs

- `operation` (string): "read", "write", "list", "delete", "move", "copy", "mkdir", "exists", "info"
- `source_path` (string): Source file or directory path
- `target_path` (string): Target path (for move/copy operations)
- `content` (string): Content to write (for write operations)
- `recursive` (boolean): Apply operation recursively (default: false)
- `create_dirs` (boolean): Create parent directories if needed (default: true)
- `overwrite` (boolean): Overwrite existing files (default: false)

## Outputs

- `success` (boolean): Whether operation succeeded
- `result` (object): Operation-specific results
- `metadata` (object): File/directory metadata
- `error` (string): Error message if operation failed

## Tool Dependencies

- **Read**: Claude Code's native file reading
- **Write**: Claude Code's native file writing  
- **LS**: Claude Code's directory listing
- **Bash**: For advanced file operations

## Operations

### Read Operation
```yaml
operation: read
inputs: 
  - source_path: file to read
  - encoding: text encoding (default: utf-8)
outputs:
  - content: file contents
  - size: file size in bytes
  - last_modified: modification timestamp
```

### Write Operation
```yaml
operation: write
inputs:
  - target_path: file to write
  - content: content to write
  - create_dirs: create parent directories
outputs:
  - bytes_written: number of bytes written
  - created_dirs: directories created
```

### List Operation
```yaml
operation: list
inputs:
  - source_path: directory to list
  - recursive: include subdirectories
  - filter: file pattern filter
outputs:
  - files: list of files
  - directories: list of directories
  - total_items: count of items
```

### Delete Operation
```yaml
operation: delete
inputs:
  - source_path: file/directory to delete
  - recursive: delete directories recursively
outputs:
  - deleted_items: list of deleted items
  - total_deleted: count of deleted items
```

### Move Operation
```yaml
operation: move
inputs:
  - source_path: source location
  - target_path: target location
  - overwrite: overwrite existing files
outputs:
  - moved_items: list of moved items
  - conflicts: any conflicts encountered
```

### Copy Operation
```yaml
operation: copy
inputs:
  - source_path: source location
  - target_path: target location
  - recursive: copy directories recursively
outputs:
  - copied_items: list of copied items
  - bytes_copied: total bytes copied
```

### Directory Creation
```yaml
operation: mkdir
inputs:
  - target_path: directory path to create
  - recursive: create parent directories
outputs:
  - created_dirs: directories created
  - already_exists: directories that already existed
```

### File Existence Check
```yaml
operation: exists
inputs:
  - source_path: path to check
outputs:
  - exists: boolean existence status
  - type: "file", "directory", or "none"
```

### File Information
```yaml
operation: info
inputs:
  - source_path: path to analyze
outputs:
  - size: file size
  - created: creation timestamp
  - modified: modification timestamp
  - permissions: file permissions
  - type: file type information
```

## Logic

### EXECUTION MODE:

1. **Input Validation**:
   - Validate operation type and required parameters
   - Check path safety and permissions
   - Verify source files exist (for applicable operations)

2. **Operation Routing**:
   - Route to appropriate Claude Code tool
   - Handle operation-specific logic
   - Manage error conditions

3. **Advanced Operations**:
   - Use Bash tool for complex file operations
   - Implement atomic operations where possible
   - Handle batch operations efficiently

4. **Result Processing**:
   - Standardize output format across operations
   - Include comprehensive metadata
   - Report detailed success/error information

### SIMULATION MODE:
1. Simulate all file system operations
2. Generate realistic file system responses
3. Create training data for file management workflows

## Claude Code Tool Mapping

### Direct Mappings
```yaml
read_operation → Read tool
write_operation → Write tool  
list_operation → LS tool
```

### Bash-Based Operations
```yaml
delete_operation → "rm" command via Bash
move_operation → "mv" command via Bash
copy_operation → "cp" command via Bash
mkdir_operation → "mkdir" command via Bash
info_operation → "stat" command via Bash
```

## Error Handling

### File Access Errors
- **Permission Denied**: Insufficient permissions for operation
- **File Not Found**: Source file doesn't exist
- **Directory Not Empty**: Cannot delete non-empty directory
- **Disk Full**: Insufficient storage space

### Path Validation Errors
- **Invalid Path**: Malformed file path
- **Path Too Long**: Exceeds system limits
- **Reserved Names**: System-reserved filenames
- **Character Encoding**: Invalid characters in path

### Operation Conflicts
- **File Exists**: Target file already exists (when overwrite=false)
- **Directory Exists**: Target directory already exists
- **Cross-Device**: Move operation across file systems
- **Circular Reference**: Recursive operation would create loops

## Security Features

### Path Safety
- Prevents access outside allowed directories
- Validates against directory traversal attacks
- Enforces workspace-relative paths

### Operation Limits
- File size limits for read/write operations
- Recursion depth limits for directory operations
- Time limits for long-running operations

### Audit Logging
- Logs all file system operations
- Records access patterns and anomalies
- Maintains operation history for security review

## Performance Characteristics

```yaml
cost: low-medium (depends on operation and file size)
latency: variable (1s-30s depending on operation)
side_effects: "Modifies file system state"
error_modes: ["permission_denied", "file_not_found", "disk_full", "path_invalid"]
atomic_operations: "limited (depends on underlying system)"
batch_support: true
```

## Usage Examples

**Read file with metadata:**
```
Input: {
  operation: "read",
  source_path: "workspace/data/input.txt"
}
Output: {
  success: true,
  result: {
    content: "File contents...",
    size: 1247,
    last_modified: "2024-01-15T10:30:00Z"
  }
}
```

**Create directory structure:**
```
Input: {
  operation: "mkdir",
  target_path: "workspace/results/analysis/temp",
  recursive: true
}
Output: {
  success: true,
  result: {
    created_dirs: ["workspace/results", "workspace/results/analysis", "workspace/results/analysis/temp"]
  }
}
```

**Copy files with pattern:**
```
Input: {
  operation: "copy",
  source_path: "workspace/source/*.txt",
  target_path: "workspace/backup/",
  recursive: false
}
Output: {
  success: true,
  result: {
    copied_items: ["file1.txt", "file2.txt", "file3.txt"],
    bytes_copied: 5632
  }
}
```

**Get comprehensive file info:**
```
Input: {
  operation: "info",
  source_path: "workspace/important_file.json"
}
Output: {
  success: true,
  result: {
    size: 2048,
    created: "2024-01-14T15:20:00Z",
    modified: "2024-01-15T10:15:00Z",
    permissions: "rw-r--r--",
    type: "application/json"
  }
}
```

## Batch Operations

### Multiple File Processing
```yaml
operation: batch
batch_operations: [
  {operation: "read", source_path: "file1.txt"},
  {operation: "read", source_path: "file2.txt"},
  {operation: "write", target_path: "combined.txt", content: "..."}
]
```

### Directory Synchronization
```yaml
operation: sync
source_directory: "workspace/source/"
target_directory: "workspace/target/"
sync_mode: "mirror"  # mirror, update, merge
```

## Training Data Format

```json
{
  "tool_execution": {
    "tool": "RealFileSystemTool",
    "inputs": {
      "operation": "copy",
      "source_path": "workspace/data/",
      "target_path": "workspace/backup/",
      "recursive": true
    },
    "claude_code_calls": [
      {"tool": "LS", "path": "workspace/data/"},
      {"tool": "Bash", "command": "cp -r workspace/data/ workspace/backup/"},
      {"tool": "LS", "path": "workspace/backup/"}
    ],
    "outputs": {
      "success": true,
      "result": {
        "copied_items": ["file1.txt", "subdir/file2.txt"],
        "bytes_copied": 3456
      }
    },
    "performance": {
      "execution_time": "2.1s",
      "files_processed": 15,
      "directories_created": 3
    }
  }
}
```

## Advanced Features

### Smart Operations
- **Conflict Resolution**: Automatic handling of file conflicts
- **Progress Tracking**: Real-time progress for long operations
- **Resume Capability**: Resume interrupted operations
- **Integrity Checking**: Verify operation completeness

### Performance Optimization
- **Parallel Processing**: Multiple files processed simultaneously
- **Memory Management**: Efficient handling of large files
- **Caching**: Cache frequently accessed file metadata
- **Compression**: Optional compression for large data transfers

### Integration Capabilities
- **Version Control**: Git integration for tracked files
- **Cloud Storage**: Sync with cloud storage services
- **Database**: Store file metadata in searchable database
- **Monitoring**: Real-time file system monitoring

This tool serves as the primary interface between LLMunix agents and the actual file system, providing reliable, secure, and efficient file operations through Claude Code's native capabilities.