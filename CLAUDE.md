# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**MD Universe** is an AR/VR knowledge visualization application built with Unity 2022.3 LTS and AR Foundation. The goal is to create a spatial interface to navigate and explore 1500+ markdown files in 3D space, combining temporal navigation (Chronos) with knowledge graph relationships (Ananke).

**Sprint Goal:** 30-day MVP to navigate markdown files through space and time
**Current Status:** Day 1 - Foundation setup (Unity project not yet created)

## Development Environment

- **Platform:** Ubuntu Linux
- **Unity Version:** Unity 2022.3 LTS (Long-Term Support)
- **Language:** C#
- **AR Framework:** AR Foundation (cross-platform AR support)
- **IDE:** Visual Studio or JetBrains Rider (auto-generated project files are gitignored)

## Common Commands

### Unity Project Setup (When Unity Project is Created)

Unity projects are typically managed through the Unity Editor, but these commands are useful:

```bash
# Open Unity project (from Unity Hub or command line)
unity-editor -projectPath ./Unity-Project

# Build project for specific platform (example)
unity-editor -projectPath ./Unity-Project -buildTarget Android -quit -batchmode

# Run tests
unity-editor -projectPath ./Unity-Project -runTests -testPlatform PlayMode
```

### Git Workflow

```bash
# Standard workflow
git status
git add .
git commit -m "descriptive message"
git push

# View project history
git log --oneline --graph

# Current branch
git branch
```

### File Management

The markdown archive is large (111MB) and gitignored:
```bash
# Count markdown files
find MD-Files-Archive -name "*.md" | wc -l

# Search markdown content
grep -r "search term" MD-Files-Archive/
```

## High-Level Architecture

### Core Systems (To Be Implemented)

1. **MD File Management System**
   - Loads and parses 1500+ markdown files from `MD-Files-Archive/Deep-seek/`
   - Files are organized by date and topic categories
   - System must index files efficiently for runtime querying
   - Expected location: `Assets/Scripts/Data/`

2. **3D Spatial Visualization**
   - Renders markdown files as 3D objects in virtual space
   - Spatial layout represents knowledge relationships
   - Expected location: `Assets/Scripts/Visualization/`

3. **Chronos (Timeline Navigation)**
   - Files are organized temporally based on timestamps in filenames
   - Users can navigate forward/backward through time
   - Expected location: `Assets/Scripts/Core/TimelineManager.cs`

4. **Ananke (Relationship Mapping)**
   - Knowledge graph that connects related markdown files
   - Visualizes connections between concepts/topics
   - Expected location: `Assets/Scripts/Core/KnowledgeGraph.cs`

5. **AR/VR Interface**
   - Uses AR Foundation for cross-platform AR/VR support
   - Handles user interaction, gestures, and device tracking
   - Expected location: `Assets/Scripts/AR/`

### Expected Unity Project Structure

```
Unity-Project/
├── Assets/
│   ├── Scenes/              # Unity scene files
│   │   ├── MainScene.unity
│   │   └── ARExperience.unity
│   ├── Scripts/
│   │   ├── Core/            # Core systems (KnowledgeGraph, TimelineManager)
│   │   ├── Data/            # File loading, parsing, indexing
│   │   ├── Visualization/   # 3D rendering and spatial layout
│   │   ├── AR/              # AR Foundation integration
│   │   ├── UI/              # User interface components
│   │   └── Utils/           # Utility functions
│   ├── Prefabs/             # Reusable game objects
│   ├── Materials/           # Visual materials and shaders
│   ├── Resources/           # Runtime-loaded resources
│   └── Plugins/             # Third-party packages
├── Packages/
│   └── manifest.json        # Unity package dependencies
└── ProjectSettings/         # Unity project configuration
```

### System Interactions

```
User Input (AR/VR)
    ↓
AR Interface Layer (gesture recognition, device tracking)
    ↓
Core Engine (Unity)
    ↓
Knowledge Graph System ← Timeline Manager
    ↓
3D Visualization Layer
    ↓
MD File Data (loaded from MD-Files-Archive)
```

The Knowledge Graph and Timeline Manager work together to determine which files to display and how to position them in 3D space.

## Key Directories

- **`/Unity-Project/`** - Main Unity project (empty at Day 1, to be created)
- **`/MD-Files-Archive/Deep-seek/`** - 1500+ markdown files organized by date/topic (111MB, gitignored)
- **`/Documentation/`** - Project documentation
- **`/Documentation/Daily-Logs/`** - Daily development logs (gitignored for privacy)
- **`/Assets-Exports/`** - Exported Unity assets and external files
- **`/.claude/`** - Claude Code workspace configuration

## Build & Testing

### Building the Unity Project

When the Unity project is created, builds are configured through Unity's Build Settings. Target platforms:
- Android (ARCore for AR)
- iOS (ARKit for AR)
- Standalone (Windows/Linux for development/testing)

Build outputs go to `/Build/` or `/Builds/` (gitignored).

### Testing Approach

Unity Test Framework (UTF) should be used for testing:
- **Editor Tests:** Test data processing, parsing, graph algorithms (in `Tests/Editor/`)
- **PlayMode Tests:** Test AR interactions, visualization, runtime behavior (in `Tests/PlayMode/`)

## Important Development Notes

### Gitignore Rules

- Unity build artifacts (`Library/`, `Temp/`, `Obj/`, `Build/`, `Logs/`) are gitignored
- IDE files (`.vs/`, `.idea/`, `*.csproj`, `*.sln`) are auto-generated and gitignored
- The large markdown archive (`MD-Files-Archive/`) is gitignored
- Daily logs (`Documentation/Daily-Logs/`) are gitignored for privacy
- The actual Unity project files (`Assets/`, `ProjectSettings/`, `Packages/`) WILL be committed once created

### File Loading Strategy

The markdown files in `MD-Files-Archive/Deep-seek/` must be:
1. Loaded at runtime (not embedded in the build to keep build size reasonable)
2. Parsed efficiently (consider streaming or lazy loading for 1500+ files)
3. Indexed for fast searching and relationship mapping
4. The archive directory structure already provides date-based organization

### AR Foundation Setup

When implementing AR:
- Use AR Foundation's cross-platform APIs for device tracking and plane detection
- Test on physical devices (Android/iOS) as AR Simulator has limitations
- Consider fallback to VR mode for devices without AR support

### Performance Considerations

With 1500+ markdown files:
- Don't load all files at once - implement streaming/pagination
- Use object pooling for 3D file representations
- Optimize rendering with LOD (Level of Detail) for distant objects
- Profile regularly using Unity Profiler to identify bottlenecks

## Markdown Archive Structure

Files in `MD-Files-Archive/Deep-seek/` are organized by topic and date:
- Startup/business planning
- AI research and development
- AR technology exploration
- Quantum physics
- IoT projects
- Music generation
- Security research
- Various technical topics

Many filenames include timestamps (e.g., `07.07.2025 Startup Build/`) which should be parsed for the Chronos timeline system.
