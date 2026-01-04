# UI Library Documentation

> **Author / Remake:** @! nfpw (Discord)

This document explains how to use the UI library shown in the example script. It covers configuration, window creation, tabs, sections, components, and utilities.

---

## 1. Getting Started

### 1.1 Loading the Library

```lua
local library = loadstring(game:HttpGet("https://raw.githubusercontent.com/nfpw/XXSCRIPT/refs/heads/main/Library/Module.lua"))()
```

### 1.2 Optional GUI Configuration

You may define a global `gui_config` table **before** creating the window.

```lua
gui_config = {
    Color = Color3.fromRGB(255, 255, 255),
    Keybind = Enum.KeyCode.Insert,
    Assets = false,
    MinHeight = 100,
    MaxHeight = 600,
    InitialHeight = 400,
    MinWidth = 300,
    MaxWidth = 800,
    InitialWidth = 500
}
```

| Field | Description |
|------|------------|
| `Color` | Main accent color |
| `Keybind` | Key to toggle the UI (PC only) |
| `Assets` | Enable custom background image |
| `Min/Max/InitialHeight` | Window height limits |
| `Min/Max/InitialWidth` | Window width limits |

If omitted, the library will use defaults.

---

## 2. Creating the Window

```lua
local window = library:CreateWindow(gui_config, gethui())
```

### 2.1 Setting Window Title

```lua
library:SetWindowName("Example Name")
```

---

## 3. Tabs

Tabs organize content inside the window.

```lua
local tab = window:CreateTab("Main")
```

Multiple tabs can be created.

---

## 4. Sections

Sections group UI elements inside a tab.

```lua
local section = tab:CreateSection("Section Name")
```

### Optional Side Placement

```lua
tab:CreateSection("Right Section", "right")
```

If no side is provided, placement is automatic.

---

## 5. UI Components

### 5.1 Toggles

```lua
section:CreateToggle("Toggle Name", defaultValue, function(value)
    print(value)
end)
```

#### Toggle Types

```lua
section:CreateToggle(
    "Danger Toggle",
    false,
    callback,
    "dangerous",
    "Optional description"
)
```

Supported styles:
- `dangerous`
- `buggy`

#### Toggle With Keybind

```lua
local toggle = section:CreateToggle("Keybind Toggle", false, callback)

toggle:CreateKeybind("K", function(key)
    print(key)
end, "Toggle")
```

Modes:
- `Toggle` (default)
- `Hold`

---

### 5.2 Color Picker

```lua
section:CreateColorpicker(
    "Color Picker",
    function(color, transparency)
        print(color, transparency)
    end,
    false,
    false,
    optionalToggle
)
```

Can be linked to a toggle or used standalone.

---

### 5.3 Labels

```lua
section:CreateLabel("Simple label")
```

#### Wrapped Label

```lua
section:CreateLabel("Long text", true)
```

#### Dynamic Labels

```lua
local label = section:CreateLabel("Text")
label:UpdateText("New Text")
```

#### Divider

```lua
section:CreateDivider()
```

---

### 5.4 Buttons

```lua
section:CreateButton("Click Me", function()
    print("clicked")
end)
```

#### Long Button

```lua
section:CreateButton("Long Button", callback, true)
```

---

### 5.5 Text Boxes

```lua
section:CreateTextBox(
    "Title",
    "Placeholder",
    false,
    function(value)
        print(value)
    end
)
```

| Parameter | Description |
|---------|------------|
| NumbersOnly | Set `true` to restrict to numbers |

---

### 5.6 Sliders

```lua
section:CreateSlider(
    "Slider Name",
    min,
    max,
    default,
    precise,
    function(value)
        print(value)
    end
)
```

| Precise | Behavior |
|-------|---------|
| true | Integers only |
| false | Decimals allowed |

---

### 5.7 Dropdowns

```lua
section:CreateDropdown(
    "Choose Option",
    {"A", "B", "C"},
    function(value)
        print(value)
    end,
    "A",
    false
)
```

| Parameter | Description |
|---------|------------|
| Default | Preselected value |
| MultiSelect | Allow multiple selections |

---

## 6. Fonts

Retrieve all available fonts:

```lua
for _, font in Enum.Font:GetEnumItems() do
    print(font.Name)
end
```

Change font at runtime:

```lua
window:SetFont("Gotham")
```

---

## 7. Notifications & HUD

```lua
window:Notify("Title", "Content", 5)
```

### Watermark / HUD

```lua
local hud = library:Hud()
hud:SetText("My UI | Time")
```

---

## 8. Background Customization

```lua
window:SetBackground("123456789")
window:SetTileOffset(100)
window:SetTileScale(0.5)
window:SetBackgroundColor(Color3.fromRGB(40,40,40))
window:SetBackgroundTransparency(0.5)
```

> `Assets` must be enabled in `gui_config` to use image backgrounds.

---

## 9. Config Manager

### Loading

```lua
local config_manager = loadstring(game:HttpGet("https://raw.githubusercontent.com/nfpw/XXSCRIPT/refs/heads/main/Library/ConfigManager.lua"))()
```

### Setup

```lua
config_manager:SetLibrary(library)
config_manager:SetWindow(window)
config_manager:SetFolder("Example Name")
config_manager:BuildConfigSection(settingsTab)
config_manager:LoadAutoloadConfig()
```

Allows saving, loading, and auto-loading UI configs.

---

## 10. Notes

- This library is **not verified by ScriptBlox**
- Use at your own risk
- Intended for PC environments

---

## 11. Credits

- UI Library & GUI Remake: **@! nfpw**
- Example Script: Provided by user

---

**End of Documentation**

