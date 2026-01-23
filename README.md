# BlackHoleUI Documentation

**Roblox UI Library**  
**Modified by: Leviform**  
**Current Version: 1.3 (January 2026)**

BlackHoleUI is a modern, feature-rich UI library for Roblox exploit development. It features smooth animations, mobile support, advanced theming, and comprehensive UI elements.

## Quick Start

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/BloxCrypto/BlackHoleUI/refs/heads/main/BlackHole.lua"))()

local Window = Library:Window({
    Logo = "123748867365417",        -- Logo asset ID
    Size = UDim2.new(0, 535, 0, 346), -- Window size
    FadeSpeed = 0.15,                 -- Animation speed
    PagePadding = 19,                 -- Sidebar spacing
    IsMobile = true,                  -- Mobile toggle button
    MobileAsset = "109391165290124"   -- Mobile button icon
})
```

## Table of Contents
- [Window Creation](#window-creation)
- [Pages & Navigation](#pages--navigation)
- [SubPages](#subpages)
- [Sections](#sections)
- [UI Elements](#ui-elements)
  - [Toggle](#toggle)
  - [Slider](#slider)
  - [Dropdown](#dropdown)
  - [Button](#button)
  - [Keybind](#keybind)
  - [Colorpicker](#colorpicker)
  - [Textbox](#textbox)
  - [Label](#label)
- [Theming](#theming)
- [Configs](#configs)
- [Icons](#icons)
- [Notifications](#notifications)

## Window Creation

```lua
local Window = Library:Window({
    Logo = "assetid",           -- Sidebar logo (default: "123748867365417")
    Size = UDim2.new(0, 535, 0, 346), -- Window dimensions
    FadeSpeed = 0.2,            -- Fade animation speed (0.1-0.5)
    PagePadding = 19,           -- Space between sidebar pages
    IsMobile = true,            -- Show mobile toggle button
    MobileAsset = "assetid"     -- Mobile button icon
})
```

**Features:**
- Draggable & resizable window
- Smooth fade animations
- Mobile-optimized toggle button
- Auto-centering on screen

## Pages & Navigation

```lua
local Page1 = Window:Page({
    Icon = "109391165290124",  -- Page icon asset ID or lucide.dev
    Search = true              -- Enable search bar (Search Bar is in BETA)
})

Window:Seperator() -- Visual separator in sidebar
```

**Icons Available:** Use `Library.Icons["icon_name"]` or raw asset IDs
- 100+ Lucide.dev icons included
- Custom asset IDs supported

## SubPages

Dual-column layout within pages:

```lua
local SubPage1 = Page1:SubPage({Name = "Aimbot"})
local SubPage2 = Page1:SubPage({Name = "Visuals"})
```

**Layout:** Left/Right scrolling columns with automatic sizing

## Sections

Organize elements with titled sections:

```lua
local Section = SubPage:Section({
    Name = "Main Settings",
    Side = "Left"  -- "Left" or "Right"
})
```

## UI Elements

### Toggle
```lua
local Toggle = Section:Toggle({
    Name = "Enable Aimbot",
    Flag = "AimbotEnabled",    -- Auto-saves to config
    Default = false,
    Callback = function(Value)
        print("Aimbot:", Value)
    end
})

-- Chainable extensions
Toggle:Keybind({
    Name = "Bind",
    Flag = "AimbotBind",
    Default = Enum.KeyCode.X,
    Mode = "Toggle",           -- "Toggle", "Hold", "Always"
    Callback = function(Key)
        print("Key pressed:", Key)
    end
})

Toggle:Colorpicker({
    Name = "Target Color",
    Flag = "AimbotColor",
    Default = Color3.fromRGB(255, 0, 0),
    Callback = function(Color, Alpha)
        print("Color changed:", Color, Alpha)
    end
})
```

**Toggle Methods:**
- `Toggle:Get()` → Returns current value
- `Toggle:Set(Value)` → Set toggle state
- `Toggle:SetVisibility(Boolean)` → Show/hide

### Slider
```lua
Section:Slider({
    Name = "FOV Size",
    Flag = "FOVSize",
    Min = 0,
    Max = 500,
    Default = 100,
    Suffix = "px",
    Decimals = 1,              -- 0-2 decimal places
    Callback = function(Value)
        print("FOV:", Value)
    end
})
```

### Dropdown
```lua
-- Single selection
Section:Dropdown({
    Name = "Target Selection",
    Flag = "TargetMode",
    Items = {"Head", "HumanoidRootPart", "Random"},
    Multi = false,
    MaxSize = 120,             -- Dropdown height limit
    Callback = function(Value)
        print("Selected:", Value)
    end
})

-- Multi selection
Section:Dropdown({
    Name = "Hitboxes",
    Flag = "HitboxList",
    Items = {"Head", "Torso", "Arms", "Legs"},
    Multi = true,
    Callback = function(Table)
        print("Selected:", table.concat(Table, ", "))
    end
})
```

### Button
```lua
Section:Button({
    Name = "Teleport to Target",
    Callback = function()
        print("Teleporting...")
    end
}):SubButton({  -- Chainable sub-button
    Name = "Reset Position",
    Callback = function()
        print("Reset!")
    end
})
```

### Keybind
```lua
Section:Keybind({
    Name = "Aimbot Bind",
    Flag = "AimbotKey",
    Default = Enum.KeyCode.Q,
    Mode = "Hold",             -- "Toggle", "Hold", "Always"
    Callback = function(Key, Mode)
        print("Key:", Key.Name, Mode)
    end
})
```

**Modes:**
- `Toggle` - Press once to enable/disable
- `Hold` - Active while key held
- `Always` - Always active after binding

### Colorpicker
```lua
Section:Label("Visuals"):Colorpicker({
    Name = "ESP Color",
    Flag = "ESPColor",
    Default = Color3.fromRGB(255, 0, 255),
    Callback = function(Color, Alpha)
        print("Color:", Color, "Alpha:", Alpha)
    end
})
```

**Features:**
- HSV color picker
- Alpha slider
- Rainbow toggle
- Hex value output

### Textbox
```lua
Section:Textbox({
    Name = "Custom Prediction",
    Flag = "PredictionValue",
    Default = "1.0",
    Placeholder = "Enter number...",
    Callback = function(Value)
        print("Prediction:", Value)
    end
})
```

### Label
```lua
local Label = Section:Label("Advanced", "Left")
Label:Colorpicker({...})
Label:Keybind({...})
```

## Theming

**Live theme editor (auto-generated):**
```lua
-- Settings tab automatically creates color pickers for:
-- Background, Inline, Text, Element, Image, Accent, Light Accent, Border
```

**Methods:**
- `Library:ChangeTheme("Accent", Color3.new(1, 0, 0))`
- All theme changes animate instantly

## Configs

**Full config system included:**
```lua
-- Auto-refresh dropdown with all .json configs
Library:SaveConfig("myconfig")
Library:LoadConfig(configString)
Library:DeleteConfig("myconfig")
Library:GetConfig() -- Returns JSON string
Library:RefreshConfigsList(Dropdown)
```

**Storage:** `zoophack/Configs/*.json`

## Icons

**64+ Lucide icons built-in:**
```lua
Library.Icons.home
Library.Icons.settings  
Library.Icons.users
Library.Icons.zap
-- Full list in source code
```

## Notifications

```lua
Library:Notification("Title", "Message", 5) -- 5 second duration
```

**Features:**
- Auto-sizing
- Smooth slide-in/out
- Stackable notifications

## Advanced Features

**Search System:**
- Real-time filtering across all elements
- Works with SubPages and Pages

**Mobile Support:**
- Draggable toggle button
- Touch-optimized controls

**Performance:**
- Object pooling
- Efficient tweening
- Minimal garbage collection

## Example Structure

```
Window
├── Pages (Sidebar)
│   ├── Page 1 [Icon] ⭐ (Active)
│   ├── Page 2 [Icon]
│   └── Separator ─────
├── SubPages (Horizontal)
│   ├── Aimbot    ├── Visuals
│   └── Rage      └── Misc
└── Sections (Vertical)
    ├── Toggle + Extensions
    ├── Slider
    └── Dropdown
```

**Credits:** Leviform  
**Discord:** [Join for support](https://discord.gg/DNqW4xGbZd)

*Designed for Roblox exploit UIs. Optimized for Synapse X, Script-Ware, and other major executors.*
