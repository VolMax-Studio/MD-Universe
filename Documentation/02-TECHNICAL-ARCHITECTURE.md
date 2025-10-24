# 🔧 MD UNIVERSE - Technical Architecture

## CORE COMPONENTS

### 1. MD File Parser
```csharp
public class MDFileParser {
    public static MDDocument ParseFile(string filePath) {
        // Read file content
        // Extract metadata (title, date, tags)
        // Parse markdown structure
        // Return structured document object
    }
}
```

### 2. Timeline Generator
```csharp
public class TimelineGenerator {
    public List GenerateTimeline(List files) {
        // Sort files by creation date
        // Calculate 3D positions along timeline
        // Create visual nodes for each file
        // Return positioned timeline structure
    }
}
```

### 3. AR Visualization Manager
```csharp
public class ARVisualizationManager : MonoBehaviour {
    // AR session management
    // Plane detection
    // Object placement in AR space
    // User interaction handling
}
```

### 4. Gesture Controller
```csharp
public class GestureController : MonoBehaviour {
    // Swipe detection (timeline navigation)
    // Pinch detection (zoom in/out)
    // Tap detection (file selection)
    // Two-finger rotation (view angle change)
}
```

### 5. File Display System
```csharp
public class FileDisplayPanel : MonoBehaviour {
    // Show file content
    // Render markdown formatting
    // Handle scrolling
    // Quick preview vs full view
}
```

## DATA STRUCTURES

### MDDocument
```csharp
public class MDDocument {
    public string Title;
    public string FilePath;
    public DateTime CreatedDate;
    public DateTime ModifiedDate;
    public List Tags;
    public string Content;
    public List LinkedFiles; // [[wikilinks]]
}
```

### TimelineNode
```csharp
public class TimelineNode {
    public MDDocument Document;
    public Vector3 Position3D;
    public GameObject VisualRepresentation;
    public List ConnectedNodes;
}
```

## AR FOUNDATION SETUP

### Required Packages
- AR Foundation (com.unity.xr.arfoundation)
- ARCore XR Plugin (Android)
- ARKit XR Plugin (iOS)

### Scene Structure
```
AR Scene
├── AR Session
├── AR Session Origin
│   └── AR Camera
├── Timeline Container
│   └── File Nodes (instantiated)
├── UI Canvas
│   └── File Display Panel
└── Gesture Manager
```

## FILE SYSTEM INTEGRATION

### Android Permissions
```xml


```

### File Access Pattern
```csharp
// Use Android Storage Access Framework
string folderPath = "/storage/emulated/0/Documents/MD-Files/";
string[] files = Directory.GetFiles(folderPath, "*.md");
```

## PERFORMANCE CONSIDERATIONS

### Optimization Strategies
- **LOD (Level of Detail):** Distant files show simplified icons
- **Culling:** Only render files in view frustum
- **Lazy loading:** Load file content only when selected
- **Object pooling:** Reuse file node GameObjects
- **Async operations:** Load files on background thread

### Target Performance
- Frame rate: 60 FPS stable
- File load time: <100ms per file
- Timeline generation: <2s for 1000 files
- Memory usage: <500MB for 1500 files

## DEVELOPMENT WORKFLOW

### Git Workflow
```bash
# Daily commits
git add .
git commit -m "feat: Add timeline positioning algorithm"
git push origin main
```

### Testing Strategy
- **Unit tests:** Parser, timeline generator
- **Integration tests:** AR placement, gesture controls
- **Manual testing:** Galaxy Tab S10 device testing
- **Beta testing:** 5 users, feedback iteration

## TECHNOLOGY DECISIONS

### Why Unity?
- Cross-platform (Android/iOS)
- Mature AR Foundation
- Strong C# ecosystem
- Your existing knowledge

### Why AR Foundation?
- Platform agnostic
- Regular updates from Unity
- Good documentation
- Industry standard

### Why Local-First?
- Privacy (user data stays on device)
- Offline functionality
- No backend costs (initially)
- Faster performance

## FUTURE TECHNICAL ROADMAP

### Phase 2 Features
- Cloud sync (optional)
- Multi-device support
- Collaborative spaces
- AI summarization integration

### Phase 3 Features
- VR mode (Meta Quest)
- Voice commands
- Advanced graph algorithms
- Real-time collaboration

**Current Focus: Phase 1 MVP - Local, Single-user, Core Features Only!** 🎯
