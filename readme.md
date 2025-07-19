# WebRTC-Telestrator

A remote telestrator app using WebRTC. Use a remote device (such as a phone or tablet) to draw on your screen while recording/streaming via OBS. Rather than just having a blank 'greenscreen' to draw on, this app streams a specified display so that you can see exactly where you are drawing on your device.

> **Note**: This project is a revamped and re-written version of the original [WebRTC-Telestrator by BlankSourceCode](https://github.com/BlankSourceCode/WebRTC-Telestrator). It includes bug fixes, improved connection handling, and enhanced UI controls.

## Key Features

- **WebRTC-based streaming**: Real-time, low-latency screen sharing
- **Remote drawing capabilities**: Draw on any device and see it appear on the host
- **OBS integration**: Transparent overlay support for streaming/recording
- **Improved connection handling**: Fixed issues with reconnection after page refresh
- **Enhanced UI controls**: Adjustable offset and inset values for canvas positioning
- **Cross-platform support**: Works on Windows, Android, and iOS devices

## Prerequisites

- Node.js (v12 or higher)
- OBS Studio (for streaming/recording)
- A WebRTC-compatible browser (Chrome, Edge, Firefox, Safari)

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/BrennanB/WebRTC-Telestrator.git
   cd WebRTC-Telestrator
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the application:
   ```bash
   npm start
   ```
   
   Or with a custom port:
   ```bash
   npm start -- -p 9999
   ```

## Usage

### 1. Start the Server
Launch the application using `npm start`. This will:
- Start an HTTP server on port 8888 (default)
- Start a WebSocket server on port 8889 (HTTP port + 1)
- Display connection URLs in the console

### 2. Configure OBS Studio
1. In OBS, add a new **Browser Source**
2. Set the URL to: `http://localhost:8888/obs.html`
3. Set the width and height to match your canvas resolution (e.g., 1920x1080)
4. Check "Shutdown source when not visible" and "Refresh browser when scene becomes active"
5. Position this browser source as an overlay on your scene

### 3. Host a Session (on the streaming computer)
1. Open a modern browser (Chrome, Edge, Firefox) on your streaming machine
2. Navigate to `http://localhost:8888`
   - **Important**: Use `localhost`, not your machine name or IP, to avoid WebRTC security restrictions
3. Click the **"Host Session"** button
4. Select the window or screen you want to share:
   - Option 1: Select your entire monitor
   - Option 2: In OBS, right-click a source → "Windowed Projector (Source)" → Select that window

### 4. Join from a Remote Device
1. On your drawing device (tablet, phone, another computer), open a browser
2. Navigate to `http://[host-computer-ip]:8888`
   - Find your host computer's IP address using `ipconfig` (Windows) or `ifconfig` (Mac/Linux)
   - Example: `http://192.168.1.100:8888`
3. Click the **"Join"** button
4. You should now see the host's shared screen as your canvas background

### 5. Drawing Controls
Once connected, you'll see drawing tools at the top of the screen:
- **Offset**: Vertical spacing from the top (default: 12)
- **Inset**: Horizontal padding on sides (default: 1)
- **Clear** (⊗): Clear all drawings
- **Undo** (⟲): Undo last stroke
- **Color options**: White, black, red, green, blue, yellow, or custom color picker
- **Line width**: Adjustable slider for stroke thickness
- **Toggle tools** (⇊): Show/hide the toolbar
- **Fullscreen** (⇉): Enter/exit fullscreen mode

## Example

![Usage Demo](WebRTC-Telestrator.gif)

## Troubleshooting

### Common Issues

1. **"Join" button only works once**
   - This has been fixed in this version. The host now properly resets its connection when a new client joins.

2. **Can't connect from remote device**
   - Ensure your firewall allows connections on ports 8888 and 8889
   - Verify both devices are on the same network
   - Use the host computer's actual IP address, not `localhost`

3. **No video showing on remote device**
   - Make sure the host has clicked "Host Session" and selected a window/screen
   - Check that both devices support WebRTC
   - Try refreshing both browsers and reconnecting

4. **Drawing not showing in OBS**
   - Verify the Browser Source URL is correct: `http://localhost:8888/obs.html`
   - Check that the Browser Source is visible and properly positioned in your scene
   - Try refreshing the Browser Source in OBS

### Browser Compatibility
- **Host**: Chrome, Edge, Firefox (desktop only)
- **Client**: Chrome, Edge, Firefox, Safari (desktop and mobile)

## Development Setup

1. Clone this repository
2. Install dependencies: `npm install`
3. For development with auto-reload: `npm run dev` (if available)
4. For debugging in VS Code:
   - Open the project folder in VS Code
   - Press `F5` to start debugging
   - The debugger will attach to the Node.js process

## Contributing

Feel free to submit issues and pull requests. This project aims to provide a simple, reliable telestrator solution for content creators.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Original concept and implementation by [BlankSourceCode](https://github.com/BlankSourceCode/WebRTC-Telestrator)
- Rewritten with improved connection handling and UI enhancements