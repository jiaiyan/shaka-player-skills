# Shaka Player Skills Library

A comprehensive skill library for Shaka Player development, providing expert guidance on adaptive media streaming with DASH, HLS, and MSF formats.

## Overview

This skill library provides structured guidance for developing with [Shaka Player](https://github.com/shaka-project/shaka-player), an open-source JavaScript library for adaptive media playback maintained by Google. It covers everything from basic setup to advanced customization.

## Features

- **Basic Usage**: Setup and initialization guidance
- **Configuration**: Streaming, buffering, ABR, and language settings
- **DRM Support**: Widevine, PlayReady, and FairPlay configuration
- **Error Handling**: Comprehensive error management and recovery
- **Offline Storage**: Download and playback content offline
- **Plugin Development**: Create custom extensions
- **UI Customization**: Controls, localization, and accessibility
- **Build Customization**: Optimize bundle size

## Installation
```bash
npx skills add https://github.com/jiaiyan/shaka-player-skills --skill shaka-player-skills
```

## Available Skills

### 1. Basic Usage (`shaka-player-basic-usage`)

Helps set up and initialize Shaka Player for adaptive media streaming.

**Topics covered**:

- HTML structure with video element
- JavaScript initialization
- Error handling setup
- Browser support checks
- Polyfill configuration

### 2. Configuration (`shaka-player-configuration`)

Configures player settings for optimal playback experience.

**Topics covered**:

- Streaming configuration
- Buffering settings
- ABR (Adaptive Bitrate) configuration
- Language preferences
- Low latency streaming

### 3. DRM Setup (`shaka-player-drm-setup`)

Configures Digital Rights Management for protected content.

**Topics covered**:

- License server configuration
- Widevine, PlayReady, FairPlay setup
- Clear Key for testing
- Robustness settings
- Persistent license support

### 4. Error Handling (`shaka-player-error-handling`)

Implements comprehensive error handling strategies.

**Topics covered**:

- Error structure and codes
- Severity levels
- Retry mechanisms
- Error recovery strategies
- Debugging techniques

### 5. Offline Storage (`shaka-player-offline-storage`)

Implements offline download and playback capabilities.

**Topics covered**:

- Content download
- Progress tracking
- Storage management
- Offline DRM support
- IndexedDB configuration

### 6. Plugin Development (`shaka-player-plugin-development`)

Develops custom plugins to extend functionality.

**Topics covered**:

- Manifest parser plugins
- Text parser plugins
- Networking plugins
- ABR manager plugins
- Polyfill plugins

### 7. UI Customization (`shaka-player-ui-customization`)

Customizes the player user interface.

**Topics covered**:

- UI library setup
- Control customization
- Chromecast integration
- VR playback
- Localization and accessibility

### 8. Build Customization (`shaka-player-build-customization`)

Optimizes build size and creates custom configurations.

**Topics covered**:

- Build system overview
- Feature inclusion/exclusion
- Custom build configs
- Bundle size analysis
- Plugin integration

## Quick Start

### Basic Player Setup

```javascript
// Install polyfills
shaka.polyfill.installAll();

// Check browser support
if (shaka.Player.isBrowserSupported()) {
  const video = document.getElementById('video');
  const player = new shaka.Player();
  await player.attach(video);
  
  // Listen for errors
  player.addEventListener('error', (event) => {
    console.error('Error:', event.detail);
  });
  
  // Load content
  await player.load('https://example.com/manifest.mpd');
}
```

### With Configuration

```javascript
player.configure({
  streaming: {
    bufferingGoal: 120,      // 2 minutes buffer
    rebufferingGoal: 30      // 30 seconds rebuffer target
  },
  abr: {
    enabled: true,
    defaultBandwidthEstimate: 500000
  },
  preferredAudioLanguage: 'en-US'
});
```

### With DRM

```javascript
player.configure({
  drm: {
    servers: {
      'com.widevine.alpha': 'https://license.example.com/widevine',
      'com.microsoft.playready': 'https://license.example.com/playready'
    }
  }
});
```

## API Reference

### Player Methods

| Method                      | Description                      |
| --------------------------- | -------------------------------- |
| `attach(video)`             | Attach player to video element   |
| `load(uri)`                 | Load manifest and start playback |
| `configure(config)`         | Set player configuration         |
| `getConfiguration()`        | Get current configuration        |
| `getVariantTracks()`        | Get available video/audio tracks |
| `selectVariantTrack(track)` | Select specific track            |

### Configuration Sections

| Section                  | Description                      |
| ------------------------ | -------------------------------- |
| `streaming`              | Buffering and streaming settings |
| `abr`                    | Adaptive bitrate settings        |
| `drm`                    | DRM configuration                |
| `manifest`               | Manifest parsing settings        |
| `preferredAudioLanguage` | Preferred audio language         |
| `preferredTextLanguage`  | Preferred subtitle language      |

## Project Structure

```
shaka-player-skills/
├── SKILL.md                          # Root skill file
├── README.md                         # This file
├── README_CN.md                      # Chinese documentation
├── AGENTS.md                         # Agent documentation
├── shaka-player-basic-usage/
│   └── SKILL.md
├── shaka-player-build-customization/
│   └── SKILL.md
├── shaka-player-configuration/
│   └── SKILL.md
├── shaka-player-drm-setup/
│   └── SKILL.md
├── shaka-player-error-handling/
│   └── SKILL.md
├── shaka-player-offline-storage/
│   └── SKILL.md
├── shaka-player-plugin-development/
│   └── SKILL.md
└── shaka-player-ui-customization/
    └── SKILL.md
```

## Contributing

When adding new skills or updating existing ones:

1. Follow the existing SKILL.md format
2. Include front matter with `name` and `description`
3. Provide clear "When to Use" guidance
4. Include practical code examples
5. Reference related skills

## Related Resources

- [Shaka Player Documentation](https://shaka-player-demo.appspot.com/docs/api/index.html)
- [Shaka Player GitHub](https://github.com/shaka-project/shaka-player)
- [Shaka Player Demo](https://shaka-player-demo.appspot.com/)
- [API Reference](https://shaka-player-demo.appspot.com/docs/api/shaka.html)

## License

This skill library is provided under the MIT License. See the [LICENSE](https://opensource.org/licenses/MIT) file for details.
