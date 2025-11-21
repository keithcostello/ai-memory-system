# VSCode Migration Guide

**Purpose:** Outline for implementing the memory system as a VSCode extension  
**Status:** Planning document (not implemented)  
**Target:** Developers interested in creating the extension

---

## Overview

The memory system design is already well-structured for VSCode integration, with command patterns and file organization that align with VSCode extension practices. This document outlines how the current memory system could be migrated to a VSCode extension with minimal architectural changes.

---

## Current Readiness Assessment

The memory system is approximately **85% ready** for VSCode implementation. The existing design includes:

- **Command Structure**: Slash commands already map directly to VSCode commands
- **Menu Organization**: Hierarchical structure ready for sidebar panels
- **File Patterns**: Consistent naming and organization for automated validation
- **Validation Rules**: Clear constraints that can be programmatically enforced
- **Refresh/Check Functions**: Memory system integrity features that can be automated

---

## Extension Architecture

### Core Components

```
memory-vscode-extension/
├── package.json          # Extension manifest
├── src/
│   ├── extension.ts      # Extension entry point
│   ├── commands/         # Command implementations
│   │   ├── menu.ts       # Menu command handler
│   │   ├── project.ts    # Project commands
│   │   ├── session.ts    # Session commands
│   │   ├── file.ts       # File operations
│   │   ├── memory.ts     # Memory check/refresh
│   ├── ui/              
│   │   ├── menu.ts       # Menu UI components
│   │   ├── sidebar.ts    # Main sidebar panel
│   │   ├── views/        # Different menu views
│   ├── validators/       
│   │   ├── structure.ts  # File structure validation
│   │   ├── content.ts    # Content format validation
│   │   ├── maintenance.ts # FIFO maintenance checks
│   ├── utils/
│   │   ├── github.ts     # GitHub integration
│   │   ├── parser.ts     # File content parsing
│   │   ├── templates.ts  # Template generators
```

---

## Command Mapping

The slash commands from the memory system map directly to VSCode commands:

| Memory System Command | VSCode Command |
|----------------------|----------------|
| `/menu` | `memory.showMenu` |
| `/start` | `memory.sessionStart` |
| `/end` | `memory.sessionEnd` |
| `/project` | `memory.projectManagement` |
| `/doc` | `memory.documentation` |
| `/file` | `memory.fileOperations` |
| `/status` | `memory.statusChecks` |
| `/memory refresh` | `memory.refresh` |
| `/memory check` | `memory.check` |

**Registration Example:**

```typescript
context.subscriptions.push(
  vscode.commands.registerCommand('memory.showMenu', () => {
    MenuProvider.showMenu();
  })
);

context.subscriptions.push(
  vscode.commands.registerCommand('memory.refresh', () => {
    MemoryManager.refreshMemory();
  })
);
```

---

## UI Components

### Main Sidebar

A sidebar extension with tabs for different menu sections:

```typescript
export class MemorySidebarProvider implements vscode.WebviewViewProvider {
  public static readonly viewType = 'memory-sidebar';
  
  constructor(private readonly context: vscode.ExtensionContext) {}
  
  resolveWebviewView(
    webviewView: vscode.WebviewView,
    context: vscode.WebviewViewResolveContext,
    token: vscode.CancellationToken
  ) {
    webviewView.webview.html = this.getHtmlForWebview(webviewView.webview);
    
    // Handle messages from the webview
    webviewView.webview.onDidReceiveMessage(message => {
      switch (message.command) {
        case 'menuSelect':
          this.handleMenuSelection(message.menuId);
          return;
        // Other message handlers
      }
    });
  }
  
  private getHtmlForWebview(webview: vscode.Webview) {
    // Generate menu HTML structure
  }
  
  private handleMenuSelection(menuId: string) {
    // Process menu selection
  }
}
```

### Menu System Implementation

The current numbered menu system translates directly to a tree view:

```typescript
export class MenuTreeProvider implements vscode.TreeDataProvider<MenuItem> {
  private _onDidChangeTreeData = new vscode.EventEmitter<MenuItem | undefined>();
  readonly onDidChangeTreeData = this._onDidChangeTreeData.event;
  
  constructor(private menuItems: MenuItem[]) {}
  
  getTreeItem(element: MenuItem): vscode.TreeItem {
    return element;
  }
  
  getChildren(element?: MenuItem): Thenable<MenuItem[]> {
    if (!element) {
      return Promise.resolve(this.menuItems);
    }
    
    return Promise.resolve(element.children || []);
  }
  
  refresh(): void {
    this._onDidChangeTreeData.fire(undefined);
  }
}

class MenuItem extends vscode.TreeItem {
  constructor(
    public readonly label: string,
    public readonly collapsibleState: vscode.TreeItemCollapsibleState,
    public readonly command?: vscode.Command,
    public readonly children?: MenuItem[]
  ) {
    super(label, collapsibleState);
    this.tooltip = label;
    this.description = '';
  }
}
```

---

## Validators and File Watchers

### Structure Validation

```typescript
export class StructureValidator {
  static validateRepository(workspaceFolder: vscode.WorkspaceFolder): ValidationResult {
    const requiredDirs = [
      'PATTERNS',
      'projects'
    ];
    
    const requiredFiles = [
      'README.md',
      'MEMORY_MENU.md',
      'PERSISTENT_MEMORY_LITE.md'
    ];
    
    // Check directories and files exist
    // Return validation results with errors and warnings
  }
  
  static validateProject(projectPath: string): ValidationResult {
    const requiredProjectDirs = [
      'PROJECT',
      'SESSION',
      'DOCUMENTS'
    ];
    
    const requiredProjectFiles = [
      'PROJECT/WAITING_ON.md',
      'PROJECT/COMMON_MISTAKES.md',
      'SESSION/CURRENT_CONTEXT.md',
      'SESSION/SESSION_LOG.md'
    ];
    
    // Check project structure
    // Return validation results
  }
}
```

### File Watchers

```typescript
export class FileWatcherService {
  private fileWatchers: vscode.FileSystemWatcher[] = [];
  
  constructor(private workspaceFolder: vscode.WorkspaceFolder) {
    this.setupWatchers();
  }
  
  private setupWatchers() {
    // Watch for changes to critical files
    this.watchFile('**/PROJECT/WAITING_ON.md', this.onWaitingOnChange.bind(this));
    this.watchFile('**/SESSION/CURRENT_CONTEXT.md', this.onContextChange.bind(this));
    this.watchFile('**/PATTERNS/**', this.onPatternChange.bind(this));
    
    // Watch for new projects
    this.watchFile('**/projects/**/README.md', this.onNewProject.bind(this));
  }
  
  private watchFile(globPattern: string, callback: (uri: vscode.Uri) => void) {
    const watcher = vscode.workspace.createFileSystemWatcher(
      new vscode.RelativePattern(this.workspaceFolder, globPattern)
    );
    
    watcher.onDidChange(callback);
    watcher.onDidCreate(callback);
    
    this.fileWatchers.push(watcher);
  }
  
  private onWaitingOnChange(uri: vscode.Uri) {
    // Check FIFO maintenance
    // Validate format
    // Offer suggestions for updates
  }
  
  // Other change handlers
}
```

---

## Memory Manager Implementation

The Memory Manager persona can be implemented as a service that maintains context about the current operational mode:

```typescript
export class MemoryManagerService {
  private context: 'architect' | 'librarian' | 'archivist' | 'handoff' = 'architect';
  
  constructor(private workspaceFolder: vscode.WorkspaceFolder) {}
  
  public setContext(newContext: 'architect' | 'librarian' | 'archivist' | 'handoff') {
    this.context = newContext;
    // Update UI to reflect context
    vscode.window.showInformationMessage(`Memory Manager: Switched to ${newContext} context`);
  }
  
  public getContext() {
    return this.context;
  }
  
  public refreshMemory() {
    // Read PATTERNS folder and project files
    // Update internal state
    vscode.window.showInformationMessage('Memory refreshed');
  }
  
  public performIntegrityCheck() {
    // Check file structure
    // Validate content formats
    // Verify maintenance
    // Return results
  }
  
  // Context-specific functions based on the current mode
  public performContextAction(action: string, args: any) {
    switch(this.context) {
      case 'architect':
        // Handle architect context actions
        break;
      case 'librarian':
        // Handle librarian context actions
        break;
      case 'archivist':
        // Handle archivist context actions
        break;
      case 'handoff':
        // Handle handoff context actions
        break;
    }
  }
}
```

---

## Implementation Steps

1. **Create Extension Scaffold**
   - Use Yeoman generator for VSCode extension
   - Configure initial package.json

2. **Implement Core Services**
   - File system operations
   - GitHub integration
   - Memory Manager service

3. **Build UI Components**
   - Sidebar view
   - Menu system
   - Project selector

4. **Implement Commands**
   - Port slash commands to VSCode commands
   - Connect to UI components
   - Implement validation

5. **Add Validators**
   - File structure validation
   - Content format validation
   - Maintenance checks

6. **Create Templates and Snippets**
   - Convert PATTERNS into snippets
   - Implement template generators

---

## Benefits of VSCode Integration

1. **Automatic Validation**
   - Instant feedback on file structures
   - Format validation as you type
   - FIFO maintenance alerts

2. **UI-based Navigation**
   - Click through menu instead of typing commands
   - Visual project selection
   - Drag-and-drop file organization

3. **Integrated Editing**
   - Context-aware snippet suggestions
   - Template generation
   - Preview handoff documents

4. **Automation**
   - Auto-refresh on file changes
   - Scheduled maintenance checks
   - Automatic timestamp creation

5. **Git Integration**
   - Commit management within the extension
   - Branch visualization
   - Pull/push notifications

---

## Conclusion

The memory system is fundamentally ready for VSCode implementation. The clear command structure, standardized file organization, and explicit validation rules provide a solid foundation for automation. 

A VSCode extension would primarily add UI components and automatic enforcement around the existing system rather than requiring significant architectural changes. This high level of migration readiness reflects the thoughtful design of the memory system.

---

**Author:** Memory System Team  
**Date:** 2025-11-21  
**Version:** 1.0