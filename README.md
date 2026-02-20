# D.R.X UI Library

A clean, modern, and fully-featured GUI library for Roblox with built-in configuration save/load system.

**Educational Purpose:** This library is intended for learning Lua programming, UI design patterns, and game development concepts. Use responsibly and in accordance with Roblox Terms of Service.

## Features

- 🎨 **Clean Modern Design** - Minimalist dark theme with smooth animations
- 💾 **Save/Load System** - Persistent configurations with file-based storage
- 🔧 **Easy to Use** - Simple API for creating custom GUIs
- 📦 **Lightweight** - Single file library
- ⚡ **Responsive** - Smooth interactions and tweens
- 🎯 **Multiple Element Types** - Buttons, Toggles, Sliders, Labels, Textboxes, Keybinds
- 📱 **Draggable** - Move the GUI anywhere on screen
- 🔐 **Auto-Config Tab** - Configuration management tab automatically included

## Installation

### Method 1: GitHub Raw Link (Recommended)

1. Upload `drx-library.lua` to your GitHub repository
2. Get the raw link to the file
3. Load it in your script:

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPO/main/drx-library.lua"))()
```

### Method 2: Direct File

Simply paste the contents of `drx-library.lua` directly into your script environment.

## Quick Start

```lua
-- Load the library
local Library = loadstring(game:HttpGet("YOUR_GITHUB_RAW_LINK"))()

-- Create a window
local Window = Library:CreateWindow("My Settings Panel")

-- Create tabs
local MainTab = Window:CreateTab("Main", "🏠")
local PreferencesTab = Window:CreateTab("Preferences", "⚙")

-- Add elements
MainTab:AddLabel("Welcome!")

MainTab:AddButton("Test Button", function()
    print("Button clicked!")
end)

MainTab:AddToggle("Enable Feature", false, function(value)
    print("Feature is now:", value)
end)

MainTab:AddSlider("Volume", 0, 100, 50, function(value)
    print("Volume level:", value)
end)
```

## API Reference

### Creating a Window

```lua
local Window = Library:CreateWindow(title)
```

**Parameters:**
- `title` (string) - The title displayed in the top bar

**Returns:** Window object

---

### Creating a Tab

```lua
local Tab = Window:CreateTab(name, icon)
```

**Parameters:**
- `name` (string) - Tab name
- `icon` (string) - Emoji or text icon

**Returns:** Tab object

---

### Tab Elements

#### Add Button

```lua
Tab:AddButton(text, callback)
```

**Parameters:**
- `text` (string) - Button text
- `callback` (function) - Function called when clicked

**Example:**
```lua
MainTab:AddButton("Show Message", function()
    print("Hello from D.R.X!")
end)
```

---

#### Add Toggle

```lua
local toggle = Tab:AddToggle(text, default, callback)
```

**Parameters:**
- `text` (string) - Toggle label
- `default` (boolean) - Starting state
- `callback` (function) - Function called with new value

**Returns:** Toggle object with methods:
- `toggle:GetValue()` - Returns current state
- `toggle:SetValue(value)` - Sets state programmatically

**Example:**
```lua
local darkMode = MainTab:AddToggle("Dark Mode", false, function(enabled)
    print("Dark Mode:", enabled)
end)

-- Later...
darkMode:SetValue(true) -- Enable programmatically
```

---

#### Add Slider

```lua
local slider = Tab:AddSlider(text, min, max, default, callback)
```

**Parameters:**
- `text` (string) - Slider label
- `min` (number) - Minimum value
- `max` (number) - Maximum value
- `default` (number) - Starting value
- `callback` (function) - Function called with new value

**Returns:** Slider object with methods:
- `slider:GetValue()` - Returns current value
- `slider:SetValue(value)` - Sets value programmatically

**Example:**
```lua
local volumeSlider = MainTab:AddSlider("Music Volume", 0, 100, 50, function(value)
    -- Adjust music volume in your game
    print("Volume set to:", value)
end)
```

---

#### Add Label

```lua
local label = Tab:AddLabel(text)
```

**Parameters:**
- `text` (string) - Label text

**Returns:** Label object with methods:
- `label:SetText(text)` - Updates label text

**Example:**
```lua
local statusLabel = MainTab:AddLabel("Status: Ready")
-- Update later
statusLabel:SetText("Status: Active")
```

---

#### Add Textbox

```lua
local textbox = Tab:AddTextbox(placeholder, callback)
```

**Parameters:**
- `placeholder` (string) - Placeholder text
- `callback` (function) - Function called when Enter is pressed

**Returns:** Textbox object with methods:
- `textbox:GetText()` - Returns current text
- `textbox:SetText(text)` - Sets text programmatically
- `textbox:Clear()` - Clears the textbox

**Example:**
```lua
local nameBox = MainTab:AddTextbox("Enter name...", function(text)
    print("You entered:", text)
end)
```

---

#### Add Keybind

```lua
local keybind = Tab:AddKeybind(text, default, callback)
```

**Parameters:**
- `text` (string) - Keybind label
- `default` (string) - Default key name
- `callback` (function) - Function called when key changes

**Returns:** Keybind object with methods:
- `keybind:GetKey()` - Returns current key
- `keybind:SetKey(key)` - Sets key programmatically

**Example:**
```lua
local actionKey = MainTab:AddKeybind("Action Hotkey", "E", function(key)
    print("Hotkey set to:", key)
end)
```

---

## Configuration System

The library automatically includes a **Config** tab with save/load functionality.

### How It Works

1. All elements created with `AddToggle()`, `AddSlider()`, and `AddKeybind()` are automatically tracked
2. The Config tab provides:
   - Save current settings to a named config
   - Load previously saved configs
   - Delete configs
   - List of all saved configs

### Usage

```lua
-- Your elements are automatically saved when you use the Config tab
local speed = PlayerTab:AddSlider("Walk Speed", 16, 200, 16, function(value)
    -- Your code
end)

-- In the GUI:
-- 1. Enter a config name (e.g., "MyConfig")
-- 2. Click "💾 Save Config"
-- 3. Your settings are saved persistently
-- 4. Click "📂 Load Config" to restore them anytime
```

### Config Files

Configs are saved in: `workspace/DRX_Configs/[config_name].txt`

Each config stores all slider values, toggle states, and keybind settings.

---

## Complete Example

```lua
-- Load library
local Library = loadstring(game:HttpGet("YOUR_RAW_LINK"))()

-- Create window
local Window = Library:CreateWindow("Game Settings")

-- Create tabs
local AudioTab = Window:CreateTab("Audio", "🔊")
local VideoTab = Window:CreateTab("Video", "🎮")

-- Audio Tab
AudioTab:AddLabel("Sound Settings")

AudioTab:AddSlider("Master Volume", 0, 100, 75, function(value)
    print("Master Volume:", value)
    -- Apply volume to your game audio
end)

AudioTab:AddSlider("Music Volume", 0, 100, 50, function(value)
    print("Music Volume:", value)
    -- Apply to background music
end)

AudioTab:AddToggle("Mute Audio", false, function(enabled)
    print("Audio Muted:", enabled)
    -- Mute/unmute game sounds
end)

-- Video Tab
VideoTab:AddLabel("Display Settings")

VideoTab:AddToggle("Fullscreen", false, function(enabled)
    print("Fullscreen:", enabled)
    -- Toggle fullscreen mode
end)

VideoTab:AddSlider("Brightness", 0, 100, 50, function(value)
    print("Brightness:", value)
    -- Adjust screen brightness
end)
```

---

## Default Keybind

**RightShift** - Toggle GUI visibility (can be changed in Config tab)

---

## Requirements

Your scripting environment should support:
- `game:HttpGet()` (for loading from GitHub)
- File functions: `isfolder`, `makefolder`, `writefile`, `readfile`, `delfile`, `listfiles`

**Note:** This library is designed for educational purposes and local testing environments. Always respect Roblox Terms of Service.

---

## Tips

1. **Organization**: Use labels to organize sections within tabs
2. **Config Names**: Use descriptive names like "Audio_Preset" or "Video_High"
3. **Event Handling**: Connect to game events as needed:

```lua
-- Example: Reconnect settings when needed
game:GetService("RunService").Heartbeat:Connect(function()
    -- Update your UI or apply settings
end)
```

4. **Global Storage**: Store elements globally if you need to access them later:

```lua
_G.MyToggle = MainTab:AddToggle("Feature", false, callback)
-- Access anywhere: _G.MyToggle:SetValue(true)
```

---

## Customization

Want to change colors? Edit the `Colors` table at the top of the library:

```lua
local Colors = {
    Background = Color3.fromRGB(18, 18, 22),
    Surface = Color3.fromRGB(25, 25, 30),
    Primary = Color3.fromRGB(100, 100, 255), -- Change this!
    -- ... etc
}
```

---

## License

Free to use and modify. Credit appreciated but not required.

---

## Support

For issues or questions:
1. Check the example usage file
2. Ensure your environment supports required functions
3. Verify your GitHub raw link is correct

---

## Disclaimer

This library is provided for **educational purposes only** to learn about:
- Lua programming
- GUI design and UX patterns
- Data persistence and configuration management
- Event-driven programming

**Important:** 
- Use this library responsibly and in accordance with Roblox Terms of Service
- Do not use this library to create cheats, exploits, or violate any game rules
- The creators are not responsible for misuse of this library
- This is intended for learning and private testing in authorized environments only

---

**Created for educational purposes**
