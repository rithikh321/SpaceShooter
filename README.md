# Space Shooter

Space Shooter is a fast 2D arcade game for Android. 

Built using JavaScript and the HTML5 Canvas API, running inside an Android WebView. Deployed using Android Studio. There are no heavy game engines used like Unity. This makes the game incredibly fast, responsive, and lightweight.

---

## Download & Play

**Note: Please open this link on your Android device** to download and install the .APK file:<br>
[[ Click here to download ]](https://rithikh321.github.io/SpaceShooter/)

---

## How It Works

### The Game Loop
The game runs on a strict loop, 60 times a second. Every frame, it updates the math for where objects should be, wipes the screen pure black, and redraws everything.

### Stutter-Free Audio
Loading new sound files during gameplay causes mobile phones to lag. To fix this, the engine uses an **Audio Pool**. It pre-loads a small batch of sounds when the game starts and simply reuses them, keeping the game completely smooth during heavy action.

---

## Matrix Sprites (No Images Used)

There are no image files (like PNGs) in this game. Images take up memory and look blurry when scaled. Instead, the game uses a text grid to paint graphics pixel by pixel. 

     SPRITE GENERATION LOGIC
     * '0' = Empty space (Transparent)
     * '1' = Main Color (Neon Cyan)
     * '2' = Engine Color (Pure White)

    const playerShip = [
      "0  0  0  1  0  0  0",  
      "0  0  1  2  1  0  0",  
      "0  1  1  2  1  1  0",  
      "1  1  1  1  1  1  1"   
    ];

    // The engine loops through the grid. 
    // If it sees a '1' or '2', it draws a square.
    // This makes the ship scale perfectly to any screen size.

---

## Core Functions

Instead of relying on a physics engine, the game calculates everything using raw math and logic:

    function handleInput() {
        i. Gets raw touch coordinates from the screen
        ii. Adds an offset so your finger stays below the ship
        iii. Smoothly glides the ship to the new position
    }

    function checkCollisions() {
        i. Draws invisible boxes around bullets and enemies
        ii. IF (Bullet overlaps Enemy):
               -> Delete Bullet
               -> Damage Enemy
               -> Play Sound & Add Score
    }

    function spawnParticles() {
        // Math-based explosions (No video files used)
        // Generates tiny colored squares and assigns them 
        // Random X and Y speeds to fly outward.
    }

---

## Boss Mechanics

When you reach a high score, normal enemies stop and 1 of 5 bosses will appear. Each has a unique math algorithm for movement and attacks:

      Titan: {
        color: "Red",
        movement: "Slow and heavy",
        attack: "Fires massive rectangular missiles"
      },
      Widow: {
        color: "Green",
        movement: "Fast zig-zag patterns",
        attack: "Shoots high-speed tracking needles"
      },
      Core: {
        color: "Cyan",
        movement: "Stationary in center",
        attack: "Blasts rings of plasma in full 360 degrees"
      },
      Phantom: {
        color: "Purple",
        movement: "Sweeps horizontally across the screen",
        attack: "Fires wide, horizontal walls of lasers"
      },
      Lancer: {
        color: "Yellow",
        movement: "Drops very low toward the player",
        attack: "Fires thick, deadly vertical laser beams"
      }
