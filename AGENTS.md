# Shaka Player Skills - Agent Documentation

This document describes the agents and their interactions within the Shaka Player Skills Library.

## Overview

The Shaka Player Skills Library provides specialized guidance through a collection of focused skills. Each skill is designed to address specific aspects of Shaka Player development.

## Skill Agents

### 1. Basic Usage Agent

**Skill Name**: `shaka-player-basic-usage`

**Purpose**: Guides users through initial Shaka Player setup and integration.

**Capabilities**:
- Generate HTML structure for video elements
- Provide JavaScript initialization code
- Implement error handling patterns
- Configure browser support checks
- Set up polyfills

**Interaction Pattern**:
```
User: "I need to add Shaka Player to my web app"
Agent: Invokes shaka-player-basic-usage skill
       Provides complete setup with HTML and JavaScript
       Includes error handling and browser checks
```

**Output Format**:
- Complete HTML page structure
- JavaScript initialization code
- Error handling implementation
- Browser compatibility guidance

---

### 2. Configuration Agent

**Skill Name**: `shaka-player-configuration`

**Purpose**: Helps users optimize player configuration for their specific use case.

**Capabilities**:
- Configure streaming parameters
- Set up buffering strategies
- Tune ABR behavior
- Configure language preferences
- Enable low latency streaming

**Interaction Pattern**:
```
User: "How do I configure buffering for slow networks?"
Agent: Invokes shaka-player-configuration skill
       Analyzes use case
       Provides optimized configuration
       Explains each setting
```

**Output Format**:
- Configuration object with explanations
- Best practices for the use case
- Performance considerations

---

### 3. DRM Agent

**Skill Name**: `shaka-player-drm-setup`

**Purpose**: Assists with DRM configuration for protected content.

**Capabilities**:
- Configure license servers
- Set up Widevine, PlayReady, FairPlay
- Implement Clear Key for testing
- Configure robustness levels
- Handle persistent licenses

**Interaction Pattern**:
```
User: "I need to play Widevine protected content"
Agent: Invokes shaka-player-drm-setup skill
       Provides license server configuration
       Explains robustness options
       Includes testing guidance
```

**Output Format**:
- DRM configuration object
- License server setup
- Robustness level recommendations
- Platform compatibility notes

---

### 4. Error Handling Agent

**Skill Name**: `shaka-player-error-handling`

**Purpose**: Implements robust error handling and recovery strategies.

**Capabilities**:
- Parse error codes and categories
- Implement retry mechanisms
- Create fallback strategies
- Debug error scenarios
- Log and analyze errors

**Interaction Pattern**:
```
User: "My player keeps failing with network errors"
Agent: Invokes shaka-player-error-handling skill
       Analyzes error patterns
       Provides retry configuration
       Suggests recovery strategies
```

**Output Format**:
- Error handling code
- Retry configuration
- Recovery strategy implementation
- Debugging guidance

---

### 5. Offline Storage Agent

**Skill Name**: `shaka-player-offline-storage`

**Purpose**: Enables offline download and playback capabilities.

**Capabilities**:
- Download content for offline use
- Track download progress
- Manage stored content
- Handle offline DRM
- Configure storage settings

**Interaction Pattern**:
```
User: "I want users to download videos for offline viewing"
Agent: Invokes shaka-player-offline-storage skill
       Provides download implementation
       Shows progress tracking
       Explains storage management
```

**Output Format**:
- Storage initialization code
- Download implementation
- Progress tracking UI
- Content management functions

---

### 6. Plugin Development Agent

**Skill Name**: `shaka-player-plugin-development`

**Purpose**: Guides development of custom plugins and extensions.

**Capabilities**:
- Create manifest parsers
- Develop text/caption parsers
- Implement networking plugins
- Build custom ABR managers
- Add browser polyfills

**Interaction Pattern**:
```
User: "I need to support a custom manifest format"
Agent: Invokes shaka-player-plugin-development skill
       Provides parser interface
       Shows implementation pattern
       Explains registration process
```

**Output Format**:
- Plugin interface definition
- Implementation code
- Registration code
- Integration guidance

---

### 7. UI Customization Agent

**Skill Name**: `shaka-player-ui-customization`

**Purpose**: Helps customize the player user interface.

**Capabilities**:
- Set up UI library
- Customize controls
- Enable Chromecast
- Configure VR playback
- Implement localization

**Interaction Pattern**:
```
User: "How do I add a custom button to the player controls?"
Agent: Invokes shaka-player-ui-customization skill
       Shows custom button implementation
       Explains registration process
       Provides configuration example
```

**Output Format**:
- UI setup code
- Custom control implementation
- Configuration options
- Accessibility considerations

---

### 8. Build Customization Agent

**Skill Name**: `shaka-player-build-customization`

**Purpose**: Optimizes build size and creates custom configurations.

**Capabilities**:
- Analyze bundle size
- Exclude unused features
- Create custom build configs
- Add custom plugins to build
- Configure build variants

**Interaction Pattern**:
```
User: "My bundle is too large, how can I reduce it?"
Agent: Invokes shaka-player-build-customization skill
       Analyzes requirements
       Suggests exclusions
       Provides build command
       Shows size comparison
```

**Output Format**:
- Build commands
- Custom config files
- Size analysis
- Feature comparison

---

### 9. Subtitle Development Agent

**Skill Name**: `shaka-player-subtitle-development`

**Purpose**: Provides comprehensive guidance for subtitle integration, styling, and multi-language support.

**Capabilities**:
- Load external subtitles (WebVTT, TTML)
- Customize subtitle appearance (font, size, color, background)
- Implement multi-language subtitle switching
- Handle subtitle events and errors
- Configure subtitle positioning and display

**Interaction Pattern**:
```
User: "How do I add Chinese subtitles to my video?"
Agent: Invokes shaka-player-subtitle-development skill
       Shows addTextTrackAsync usage
       Provides styling options
       Explains language switching
```

**Output Format**:
- Subtitle loading code
- CSS styling examples
- Language switching implementation
- Event handling setup

---

## Agent Interaction Scenarios

### Scenario 1: New Project Setup

```
1. User requests basic setup
2. Basic Usage Agent provides initial code
3. Configuration Agent suggests optimal settings
4. Error Handling Agent adds error management
```

### Scenario 2: DRM Content

```
1. User requests DRM playback
2. DRM Agent provides configuration
3. Error Handling Agent adds DRM error handling
4. Offline Storage Agent (optional) for offline DRM
```

### Scenario 3: Custom Plugin

```
1. User requests custom functionality
2. Plugin Development Agent provides implementation
3. Build Customization Agent integrates into build
4. Configuration Agent shows runtime setup
```

### Scenario 4: Performance Optimization

```
1. User reports performance issues
2. Configuration Agent tunes settings
3. Build Customization Agent reduces bundle
4. Error Handling Agent improves reliability
```

## Best Practices for Agent Usage

1. **Start with Basic Usage**: Always begin with proper setup
2. **Add Configuration**: Customize for your use case
3. **Implement Error Handling**: Never skip error management
4. **Optimize Build**: Reduce bundle size for production
5. **Test Thoroughly**: Verify all configurations work together

## Agent Communication

Agents can reference each other for related functionality:

- Basic Usage → Configuration, Error Handling
- Configuration → DRM, Offline Storage
- DRM → Error Handling, Offline Storage
- Plugin Development → Build Customization
- UI Customization → Configuration

## Version Compatibility

All agents are designed for Shaka Player v4.x. Check the [Shaka Player documentation](https://shaka-player-demo.appspot.com/docs/api/index.html) for the latest API changes.
