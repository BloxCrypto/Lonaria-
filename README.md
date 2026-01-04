# UI Library Documentation (Remake v2)

> **UI Remake:** @! nfpw (Discord)
> **Status:** Unverified by ScriptBlox – use at your own risk

This document explains the API and usage of the UI library demonstrated in the example script. It is written as a clean reference + quick-start guide.

---

## Table of Contents

1. Quick Start
2. GUI Configuration
3. Creating the Window
4. Tabs & Sections
5. UI Components
6. Fonts
7. Notifications & HUD
8. Background & Styling
9. Config Manager
10. Notes & Credits

---

## 1. Quick Start

```lua
-- Optional config (can be omitted)
gui_config = {
    Color = Color3.fromRGB(255,255,255),
    Keybind = Enum.KeyCode.Insert,
    Assets = false,
    InitialHeight = 400,
    InitialWidth = 500
}

local library = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/nfpw/XXSCRIPT/refs/heads/main/Library/Module.lua"
))()

local window = library:CreateWindow(gui_config, gethui())
library:SetWindowName("Example Name")

local mainTab = window:CreateTab("Main")
local section = mainTab:CreateSection("Example")

section:CreateButton("Hello", function()
    print("Hello World")
end)
```

---

## 2. GUI Configuration

The `gui_config` table customizes window behavior and appearance.

| Key                     | Description             |
| ----------------------- | ----------------------- |
| `Color`                 | Accent color            |
| `Keybind`               | Toggle UI key           |
| `Assets`                | Enable background image |
| `MinHeight / MaxHeight` | Height limits           |
| `MinWidth / MaxWidth`   | Width limits            |
| `InitialHeight`         | Default height          |
| `InitialWidth`          | Default width           |

If not defined, defaults are used.

---

## 3. Creating the Window

```lua
local window = library:CreateWindow(gui_config, gethui())
library:SetWindowName("My UI")
```

---

## 4. Tabs & Sections

### Tabs

```lua
local tab = window:CreateTab("Main")
```

### Sections

```lua
local section = tab:CreateSection("My Section")
```

Optional side placement:

```lua
tab:CreateSection("Right Side", "right")
```

---

## 5. UI Components

### 5.1 Toggle

```lua
section:CreateToggle("My Toggle", false, function(state)
    print(state)
end)
```

#### Styled Toggles

```lua
section:CreateToggle(
    "Danger Toggle",
    false,
    callback,
    "dangerous",
    "Optional description"
)
```

Available styles:

* `dangerous`
* `buggy`

---

### 5.2 Toggle Keybind

```lua
local toggle = section:CreateToggle("Keybind Toggle", false, callback)

toggle:CreateKeybind("K", function(key)
    print(key)
end, "Toggle")
```

Modes:

* `Toggle` (default)
* `Hold`

---

### 5.3 Color Picker

```lua
section:CreateColorpicker(
    "Color Picker",
    function(color, transparency)
        print(color, transparency)
    end
)
```

Attach to a toggle (optional):

```lua
section:CreateColorpicker("Picker", callback, false, false, toggle)
```

---

### 5.4 Label

```lua
section:CreateLabel("Simple Label")
```

Wrapped text:

```lua
section:CreateLabel("Long text", true)
```

Dynamic update:

```lua
local label = section:CreateLabel("Text")
label:UpdateText("Updated")
```

Divider:

```lua
section:CreateDivider()
```

---

### 5.5 Button

```lua
section:CreateButton("Click", function()
    print("Clicked")
end)
```

Long button:

```lua
section:CreateButton("Long Button", callback, true)
```

---

### 5.6 TextBox

```lua
section:CreateTextBox(
    "Title",
    "Placeholder",
    false,
    function(text)
        print(text)
    end
)
```

Set `true` to allow numbers only.

---

### 5.7 Slider

```lua
section:CreateSlider(
    "Slider",
    min,
    max,
    default,
    precise,
    function(value)
        print(value)
    end
)
```

| Precise | Result           |
| ------- | ---------------- |
| `true`  | Integers only    |
| `false` | Decimals allowed |

---

### 5.8 Dropdown

```lua
section:CreateDropdown(
    "Select",
    {"A", "B", "C"},
    function(value)
        print(value)
    end,
    "A",
    false
)
```

Set last argument to `true` for multi-select.

---

## 6. Fonts

Get all available fonts:

```lua
for _, font in Enum.Font:GetEnumItems() do
    print(font.Name)
end
```

Set font:

```lua
window:SetFont("Gotham")
```

---

## 7. Notifications & HUD

### Notifications

```lua
window:Notify("Title", "Message", 5)
```

### HUD / Watermark

```lua
local hud = library:Hud()
hud:SetText("Example | Time")
```

---

## 8. Background & Styling

```lua
window:SetBackground("123456789")
window:SetTileOffset(100)
window:SetTileScale(0.5)
window:SetBackgroundColor(Color3.fromRGB(40,40,40))
window:SetBackgroundTransparency(0.5)
```

> `Assets = true` is required for background images.

---

## 9. Config Manager

```lua
local config_manager = loadstring(game:HttpGet(
    "https://raw.githubusercontent.com/nfpw/XXSCRIPT/refs/heads/main/Library/ConfigManager.lua"
))()

config_manager:SetLibrary(library)
config_manager:SetWindow(window)
config_manager:SetFolder("Example Name")
config_manager:BuildConfigSection(settingsTab)
config_manager:LoadAutoloadConfig()
```

Supports saving, loading, and auto-loading configs.

---

## 10. Notes & Credits

* PC-focused UI library
* Unverified by ScriptBlox
* Intended for scripting interfaces

**Credits:**

* UI Library & Design: **@! nfpw**

---

**End of Documentation**
