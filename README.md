[DESCRIPTION]
This is a web-based 2D game engine built using the p5.js library. It 
combines a robust UI/Menu system with a procedural tile-based RPG engine. 
The project is designed to run in a web browser, utilizing a local Node.js 
server to handle asset loading and map data.

[SYSTEM ARCHITECTURE: HOW IT RUNS]
The application utilizes a "Host/Overlay" architecture to separate the 
User Interface (UI) from the Game Loop.

1. The Server (Node.js):
   - The system requires a local server (`scripts\map_server.js`) to bypass 
     browser CORS (Cross-Origin Resource Sharing) restrictions.
   - This allows the game to fetch JSON maps and assets (images/sounds) 
     dynamically.

2. The Frontend (Two Contexts):
   - Context A (The Menu): `1-Menu_Index.html`
     This is the "Host" page. It handles the start screen, audio settings, 
     and persistent storage. When "Play" is clicked, it creates an iframe.
     
   - Context B (The Game): `3-Game_Index.html`
     This loads inside the iframe created by the Menu. It contains the 
     physics engine, player controller, and procedural generation logic.

3. Communication:
   - The Menu and Game communicate via the Window `postMessage` API. 
   - The Menu sends volume/difficulty settings to the Game.
   - The Game sends status updates (e.g., "music stopped") back to the Menu.

[SETUP & INSTALLATION]
Before launching the game, you must ensure the following:

1. **DOWNLOAD ASSETS:**
   To run the game properly, you need to download the assets found on: 
   "3-Assets"
   *Make sure these files are placed in the 'assets' folder in the root 
   directory so the code can find the images and sounds.*

2. **INSTALL NODE.JS:**
   Ensure Node.js is installed on your machine to run the local server.

[HOW TO LAUNCH]
A batch script is provided to automate the startup process.

1. Run the file `start-game.bat`.

2. What the script does:
   - Sets the working directory.
   - Launches the local map server in a minimized window .
   - Waits 2 seconds for the server to initialize .
   - Automatically opens your default web browser to the game index 
     (http://localhost:3000) .

*Note: The batch file is required to bypass browser security restrictions 
that block loading files directly from the hard drive.*

[CONTROLS]
- W / A / S / D : Move Player
- Shift (Hold)  : Sprint
- Spacebar      : Jump / Interaction
- Escape        : Open/Close In-Game Settings Menu
- P             : Debug - Regenerate Map

[KEY FEATURES]
1. Procedural Generation:
   - Uses Perlin noise to generate terrain (Grass, Forest, Cliffs).
   - Implements a "river carving" algorithm that erodes paths through the 
     map and builds bridges.
   - Generates "Clear Areas" to ensure safe player spawn points.

2. Settings & Persistence:
   - Audio: Master, Music, and SFX sliders.
   - Accessibility: Text size scaling and color-blindness modes.
   - Saves: Map data and player progress are serialized to `localStorage` 
     or can be downloaded as JSON files.

3. Asset Management:
   - Includes a custom `AssetTracker` system.
   - Displays a loading bar overlay while images and sounds are fetching 
     to prevent the game from starting with missing textures.

[FILE MANIFEST]
- 1-Menu_Index.html : Entry point for the Main Menu.
- 2-Menu.js         : Logic for UI, Settings, and Iframe management.
- 3-Game_Index.html : The container for the gameplay loop.
- 4-Game.js         : Core engine (Physics, Rendering, Map Gen).
- start-game.bat    : Windows startup script.
- p5.min.js         : The core graphics/sound library.

[IMPORTANT] 
Need to download the assets file using the link below extract it and ensure its in the same file as the game:
https://1drv.ms/f/c/8e5a52451405f274/IgCSF9oiaVyjSKsOCovrC9PXAYlzLnrhE3nfuAmLtBrSFX8?e=aMclJ7
