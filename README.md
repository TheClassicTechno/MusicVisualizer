# MusicVisualizer
Taking our team's 2022 music visualizer app and moving its code to GitHub- for mit blueprint hackathon:

https://replit.com/@techno-jules/MusicVisualizer (older version)
https://replit.com/@ArchimedesLi/MusicVisualizer (newer version)

MusicVisualizer is an interactive web application that parses MIDI files and creates real-time visual representations of musical notes.  Each note is rendered as a geometric shape with properties determined by its pitch, duration, and velocity, creating an immersive audio-visual experience.

## Features

- **MIDI File Upload**: Upload any `.midi` file to visualize
- **Sample Song**: Built-in demo track to test the visualizer
- **Real-time Rendering**: Shapes appear synchronized with music playback
- **Dynamic Visual Effects**:
  - **Triangles**: Short notes (< 0.4s) with static positioning
  - **Circles**: Medium notes (0.4-1s) with falling animation
  - **Squares**:  Long notes (> 1s) with shrinking effect
- **Color Coding**: 8-color palette based on pitch modulation (RGB spectrum)
- **Responsive Canvas**: Full-screen visualization that adapts to window size
- **Fade Effects**: Smooth opacity transitions as notes conclude

## Visual Mapping

The visualizer uses an intelligent mapping system to convert musical properties into visual elements:

| Musical Property | Visual Representation |
|-----------------|----------------------|
| **Pitch** | Y-axis position & color (pitch % 8) |
| **Velocity** | X-axis position & size contribution |
| **Duration** | Shape type & animation duration |
| **Note Timing** | Spawn time & synchronized appearance |

### Color Scheme
- Pitch % 8 = 0: Cyan (`rgb(0, 179, 255)`)
- Pitch % 8 = 1: Red (`rgb(255, 0, 0)`)
- Pitch % 8 = 2: Orange (`rgb(255, 165, 0)`) - Force Circle
- Pitch % 8 = 3: Yellow (`rgb(255, 255, 0)`)
- Pitch % 8 = 4: Green (`rgb(0, 255, 0)`)
- Pitch % 8 = 5: Blue (`rgb(0, 0, 255)`)
- Pitch % 8 = 6: Purple (`rgb(160, 32, 240)`)
- Pitch % 8 = 7: Magenta (`rgb(200, 0, 255)`) - Force Circle

## Getting Started

### Prerequisites
- Modern web browser with HTML5 Canvas support
- MIDI files (`.mid` or `.midi` format)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/TheClassicTechno/MusicVisualizer.git
cd MusicVisualizer
```

2. Open `index.html` in your web browser (no build process required)

### Usage

1. **Load a MIDI file**: Click the file input button and select a `.midi` file
   - OR click "Use Sample Song" to load the built-in demo
2. **Start visualization**: Click "Click to play~" button
3. **Enjoy**:  Watch as geometric shapes appear and animate in sync with the music

### Core Components

#### `midi.js` - MIDI Processing
- Parses MIDI files using FileReader API and Tone.js MIDI library
- Extracts note data (pitch, velocity, start time, duration)
- Implements quicksort algorithm to organize notes chronologically
- Handles both file uploads and sample song loading
- Manages audio playback synchronization

#### `render.js` - Visualization Engine
- Converts musical notes into shape objects with visual properties
- Runs animation loop at 50 FPS
- Implements three animation effects:
  - **Fall**: Gravity-based downward movement
  - **Shrink**: Progressive size reduction
  - **Fade**: Opacity decrease in final 20% of duration
- Processes up to 25 concurrent shapes for performance optimization
- Draws triangles, squares, and circles on HTML5 Canvas

## Animation System

The visualizer uses a time-based animation system: 
1. Notes are scheduled based on their `start` time from the MIDI file
2. Shapes spawn 1. 5 seconds after clicking play (audio sync delay)
3. Each shape persists for its calculated `duration`
4. Effects apply dynamically based on elapsed time
5. Shapes are removed when their duration expires

## Performance

- **Frame Rate**: 50 FPS
- **Max Concurrent Shapes**: 25 (prevents performance degradation)
- **Canvas Resolution**:  Matches window dimensions (`innerWidth` × `innerHeight`)

## License

This project currently has no specified license. Please contact the repository owner for usage permissions. 
