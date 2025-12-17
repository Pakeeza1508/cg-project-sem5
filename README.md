# 🎮 Drone Shooter - OpenGL FPS Game

> A fully-featured first-person shooter game built from scratch using C++ and OpenGL 3.3. No game engine required!

[![macOS Build](https://github.com/Pakeeza1508/cg-project-sem5/workflows/Build-macOS-arm64/badge.svg?branch=main)](https://github.com/Pakeeza1508/cg-project-sem5/actions) 
[![Linux Build](https://github.com/Pakeeza1508/cg-project-sem5/workflows/Build-Linux-x86/badge.svg?branch=main)](https://github.com/Pakeeza1508/cg-project-sem5/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📋 Table of Contents
- [Features](#-features)
- [Quick Start](#-quick-start)
- [Requirements](#-requirements)
- [Installation](#-installation)
- [Building](#-building)
- [Running](#-running)
- [Gameplay](#-gameplay)
- [Controls](#-controls)
- [Project Structure](#-project-structure)
- [Technical Stack](#-technical-stack)
- [Documentation](#-documentation)

## ✨ Features

### 🎯 Gameplay
- **4 Unique Environments**: Forest, Desert, Snow, Night
- **AI Enemy Drones**: Intelligent enemies that spawn in waves and shoot back
- **Dynamic Collision Detection**: Ray-box intersection for accurate hit detection
- **Health & Score System**: Track your health and kill count in real-time
- **Wave-Based Difficulty**: Enemies spawn progressively to increase challenge

### 🎨 Graphics
- **Custom Shader System**: Vertex, Fragment, and Geometry shaders
- **3D Model Rendering**: OBJ/MTL model support via Assimp
- **Skybox Rendering**: Environment-specific cubic skyboxes
- **Explosion Effects**: Geometry shader-based destruction animations
- **Instanced Rendering**: Optimized terrain object rendering

### 🔊 Audio
- **Sound Effects**: Gunfire, explosions, laser blasts, hover sounds
- **Spatial Audio**: Cross-platform audio engine with miniaudio
- **Ambient Sounds**: Looped background audio for immersion

### 🖼️ UI/Text Rendering
- **FreeType Font Rendering**: Anti-aliased text with dynamic positioning
- **HUD Display**: Real-time health and kill counter
- **Multiple Screens**: Title, in-game, and game-over screens

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/Pakeeza1508/cg-project-sem5.git
cd cg-project-sem5

# Install dependencies (see below for your OS)
# Then build and run:
mkdir build && cd build
cmake ..
cmake --build .
./Drone-Shooter  # Linux/macOS
# or
Drone-Shooter.exe  # Windows
```

## 📦 Requirements

### 💻 System Requirements

#### Minimum Specifications
- **OS**: Windows 10/11, macOS 10.14+, Ubuntu 18.04+ (or any modern Linux)
- **CPU**: Intel Core i3 / AMD Ryzen 3 or equivalent (dual-core, 2.0 GHz+)
- **RAM**: 4 GB
- **GPU**: OpenGL 3.3 compatible graphics card
  - Intel HD Graphics 4000 or newer
  - NVIDIA GeForce GTX 650 or newer
  - AMD Radeon HD 7750 or newer
- **Storage**: 500 MB free disk space
- **Display**: 800x600 minimum resolution

#### Recommended Specifications
- **CPU**: Intel Core i5 / AMD Ryzen 5 or better (quad-core, 2.5 GHz+)
- **RAM**: 8 GB
- **GPU**: Dedicated GPU with 2GB VRAM
  - NVIDIA GeForce GTX 1050 or newer
  - AMD Radeon RX 560 or newer
- **Storage**: 1 GB free disk space
- **Display**: 1920x1080 resolution

#### Graphics Requirements
- **OpenGL Version**: 3.3 Core Profile or higher
- **Driver Support**: Updated graphics drivers recommended

**Check OpenGL Support:**
```bash
# Linux
glxinfo | grep "OpenGL version"

# macOS
system_profiler SPDisplaysDataType

# Windows
Download OpenGL Extensions Viewer or GPU-Z
```

### ⚙️ Build Tools & Dependencies

### General
- **CMake**: 3.5 or higher
- **C++ Compiler**: C++17 support (GCC 7+, Clang 5+, MSVC 2017+)
- **Git**: For cloning the repository

### Platform-Specific Dependencies

#### 🍎 macOS (with Homebrew)
```bash
brew install cmake glfw assimp freetype
```

#### 🐧 Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install -y cmake g++ \
  libassimp-dev libfreetype6-dev libglfw3-dev \
  libx11-dev libxrandr-dev libxinerama-dev \
  libxcursor-dev libxi-dev
```

#### 🪟 Windows (with vcpkg)
```bash
vcpkg install glfw3:x64-windows assimp:x64-windows freetype:x64-windows
```

Or download pre-built binaries and set `CMAKE_PREFIX_PATH` appropriately.

## 📥 Installation

### Step 1: Clone Repository
```bash
git clone https://github.com/Pakeeza1508/cg-project-sem5.git
cd cg-project-sem5
```

### Step 2: Install Dependencies
Follow the platform-specific instructions above for your operating system.

### Step 3: Create Build Directory
```bash
mkdir build
cd build
```

### Step 4: Configure with CMake
```bash
cmake ..
```

If you encounter issues, specify your compiler explicitly:
```bash
# For specific compilers
cmake .. -DCMAKE_CXX_COMPILER=g++
cmake .. -DCMAKE_CXX_COMPILER=clang++
```

## 🔨 Building

### Debug Build (with symbols for debugging)
```bash
cd build
cmake .. -DCMAKE_BUILD_TYPE=Debug
cmake --build .
```

### Release Build (optimized for performance)
```bash
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release
cmake --build .
```

### Build with Parallel Jobs (faster on multi-core systems)
```bash
cmake --build . --parallel 4
```

### Verbose Output (for troubleshooting)
```bash
cmake --build . --verbose
```

## ▶️ Running

### First Time Setup
The game will ask you to choose an environment:
```
Choose the environment you want to play in (desert, forest, snow, night): forest
```

### Run from Build Directory
```bash
# Linux/macOS
./Drone-Shooter

# Windows
Drone-Shooter.exe
```

### Run from Project Root (if executable is placed there)
```bash
# Linux/macOS
./Drone-Shooter

# Windows
.\Drone-Shooter.exe
```

## 🎮 Gameplay

### Objective
Eliminate as many enemy drones as possible before your health reaches zero.

### Difficulty Progression
| Time | Enemies | Spawn Rate | Difficulty |
|------|---------|------------|-----------|
| 0-10s | 1-2 | Every 3s | Easy |
| 10-30s | 2-3 | Every 3s | Medium |
| 30s+ | 3 (max) | Every 3s | Hard |

### Player Status
- **Starting Health**: 100 HP
- **Damage per Hit**: 10 HP (from enemy lasers)
- **Ammunition**: Unlimited
- **Accuracy**: Perfect (direct aiming)

### Enemy Behavior
- **Max Concurrent**: 3 drones
- **Attack Interval**: Every 2 seconds
- **Damage Output**: 10 HP per hit
- **Spawn Interval**: 3 seconds between waves
- **Respawn Time**: 3 seconds after destruction

## ⌨️ Controls

| Key | Action |
|-----|--------|
| **W** | Move Forward |
| **A** | Move Left |
| **S** | Move Backward |
| **D** | Move Right |
| **Mouse** | Look Around |
| **Left Click** | Fire Weapon |
| **ENTER** | Start Game / Restart |
| **ESC** | Quit Game |

## 📁 Project Structure

```
cg-project-sem5/
├── src/                          # Implementation files
│   ├── player.cpp               # Player/camera logic
│   ├── enemy.cpp                # Enemy AI behavior
│   ├── world.cpp                # Environment rendering
│   ├── collision_detection.cpp  # Hit detection system
│   ├── shader.cpp               # Shader management
│   └── ...                      # Other implementations
├── include/                      # Header files
│   ├── player.h
│   ├── enemy.h
│   ├── world.h
│   ├── collision_detection.h
│   └── ...
├── shaders/                      # GLSL shader files
│   ├── model.vert/frag          # Standard 3D rendering
│   ├── skybox.vert/frag         # Sky rendering
│   ├── text.vert/frag           # Text rendering
│   ├── explode.vert/geom/frag   # Explosion effects
│   └── ...
├── CMakeLists.txt               # Build configuration
├── main.cpp                     # Entry point
├── README.md                    # This file
├── FINAL_PROJECT_REPORT.md      # Comprehensive technical documentation
└── .github/workflows/           # CI/CD automation
    ├── build-linux-x86.yml
    └── build-macos-arm64.yml
```

## 🔧 Technical Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Graphics API** | OpenGL 3.3 | Rendering engine |
| **Math Library** | GLM | Vector/matrix operations |
| **Window/Input** | GLFW 3 | Window management & input handling |
| **Model Loading** | Assimp | 3D model importing (OBJ/MTL) |
| **Image Loading** | STB Image | Texture loading |
| **Font Rendering** | FreeType | Text rendering |
| **Audio** | miniaudio | Sound effects |
| **Build System** | CMake | Cross-platform compilation |
| **Language** | C++17 | Source code |

## 📖 Documentation

### Comprehensive Project Report
For detailed technical information, architecture diagrams, code flow analysis, and design decisions, see [FINAL_PROJECT_REPORT.md](FINAL_PROJECT_REPORT.md).

### Key Topics Covered in Report:
- Complete feature breakdown
- Architecture & code organization
- Collision detection algorithm
- Rendering pipeline
- Game mechanics & balance
- Performance optimizations
- Future enhancements

## 🆘 Troubleshooting

### System Compatibility Check

#### Check if Your Laptop Can Run the Game
```bash
# Windows (PowerShell)
Get-WmiObject Win32_VideoController | Select-Object Name, DriverVersion

# Linux
lspci | grep VGA
glxinfo | grep "OpenGL"

# macOS
system_profiler SPDisplaysDataType | grep "Chipset Model"
```

**Common Issues:**
- **Integrated Graphics**: Most modern Intel/AMD integrated graphics (2015+) support OpenGL 3.3
- **Older Laptops**: Laptops before 2012 may not support OpenGL 3.3
- **Virtual Machines**: May have limited OpenGL support (use bare metal if possible)

### CMake Configuration Issues
```bash
# Clear build directory and reconfigure
rm -rf build
mkdir build
cd build
cmake ..
```

### Missing Dependencies
**macOS**: `brew install glfw assimp freetype`
**Linux**: `sudo apt install libassimp-dev libfreetype6-dev libglfw3-dev`
**Windows**: Use vcpkg or set `CMAKE_PREFIX_PATH`

### Build Failures
1. Check compiler version: `g++ --version` (needs C++17)
2. Verify CMake version: `cmake --version` (needs 3.5+)
3. Check verbose output: `cmake --build . --verbose`

### Runtime Issues
- **No window appears**: Check OpenGL support (see System Compatibility Check above)
- **Black screen**: Update graphics drivers from manufacturer's website
- **"OpenGL 3.3 not supported" error**: Your GPU is too old - upgrade or use a different machine
- **Crash on startup**: Ensure all dependencies are installed correctly
- **No sound**: Check audio device permissions and verify speakers/headphones work
- **Low FPS (<30 FPS)**: 
  - Close background applications
  - Update graphics drivers
  - Reduce screen resolution
  - Check if laptop is in power-saving mode (switch to high performance)
- **Game freezes**: Check CPU/RAM usage - may need to close other programs

### Performance Tips for Laptops
1. **Plug in your laptop** - Battery mode may limit GPU performance
2. **Update drivers** - Get latest graphics drivers from Intel/AMD/NVIDIA
3. **Close background apps** - Free up RAM and CPU
4. **Check thermals** - Overheating can cause throttling
5. **Use dedicated GPU** (if available) - Set the game to use NVIDIA/AMD GPU instead of integrated graphics

**Windows - Force Dedicated GPU:**
```
Settings → System → Display → Graphics Settings
→ Add "Drone-Shooter.exe" → Options → High Performance
```

## 🎬 Development Timeline

The project evolved through multiple releases:
- **Sept 2022**: Initial Minecraft-style scenery
- **Oct 2022**: Realistic scenery, sound effects, enemy AI
- **Dec 2023**: Multiple environments (forest, desert, snow, night)

## 📝 Credits & References

### Inspired By
- [Learn OpenGL](https://learnopengl.com) by Joey de Vries

### Libraries Used
- [GLFW](https://www.glfw.org/) - Window and input management
- [Assimp](https://www.assimp.org/) - 3D model importing
- [FreeType](https://freetype.org/) - Font rendering
- [miniaudio](https://github.com/mackron/miniaudio) - Audio engine
- [GLM](https://github.com/g-truc/glm) - Math library

### Resources
- [Scratch a Pixel](https://www.scratchapixel.com/) - Ray-box intersection
- [free3d.com](https://free3d.com/) - 3D models
- [soundjay.com](https://www.soundjay.com/) - Sound effects
- [freepbr.com](https://freepbr.com/) - Textures

## 📄 License

This project is provided as-is for educational purposes.

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest improvements
- Submit pull requests
- Share ideas for new features

## 📧 Contact

For questions or feedback, open an issue on GitHub.

---

**Happy Gaming! 🎮** 

Built with ❤️ for learning computer graphics with OpenGL
