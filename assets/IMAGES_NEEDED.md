# 📸 Images Needed for README

## Quick Reference

| Image | Purpose | Suggested Tool | Priority |
|-------|---------|----------------|----------|
| `hero-banner.png` | Top banner showing terminal + AI + security | Figma/Excalidraw | 🔴 High |
| `architecture-overview.png` | System architecture diagram | Excalidraw/Draw.io | 🔴 High |
| `quickstart-demo.gif` | 30-sec demo: install → config → first prompt | asciinema + agg | 🔴 High |
| `opencode-tui.png` | OpenCode TUI with Nemotron selected | Screenshot | 🔴 High |
| `sigma-output.png` | Sample Sigma rule output | Screenshot | 🟡 Medium |
| `memory-forensics.png` | Memory forensics triage output | Screenshot | 🟡 Medium |
| `verify-install.png` | Verification commands output | Screenshot | 🟡 Medium |
| `why-this-stack.png` | 5 reasons visual | Excalidraw | 🟡 Medium |
| `learning-path.png` | 4-week path visual | Excalidraw | 🟡 Medium |
| `common-mistakes.png` | Visual mistakes guide | Excalidraw | 🟢 Low |
| `when-not-to-use.png` | When not to use visual | Excalidraw | 🟢 Low |

---

## How to Capture Each

### 1. Terminal Screenshots (PNG)
```bash
# macOS built-in
Cmd+Shift+4 → select terminal window

# Or use shottr (free, better)
brew install --cask shottr
```

### 2. Terminal Recording → GIF
```bash
# Install asciinema
brew install asciinema agg

# Record
asciinema rec demo.cast

# Convert to GIF
agg demo.cast quickstart-demo.gif
```

### 3. Architecture Diagrams (PNG)
**Tools:** Excalidraw (free, hand-drawn style), Draw.io, Figma

**Color Palette:**
- Terminal bg: `#1e1e2e`
- Accent cyan: `#06b6d4` (OpenCode)
- Accent green: `#22c55e` (NVIDIA)
- Accent amber: `#f59e0b` (Warnings)
- Text: `#cdd6f4`

### 4. Specific Capture Guide

#### `hero-banner.png` (1200×400)
```
┌─────────────────────────────────────────────────────────────┐
│  🛡️ SOC-Nemotron-CLI                                        │
│  Terminal-Based AI-Assisted Cybersecurity Operations        │
│                                                             │
│  [OpenCode Logo] + [NVIDIA Logo] = [Terminal with AI]      │
│                                                             │
│  Powered by NVIDIA Nemotron 3 Ultra (550B) + OpenCode CLI  │
└─────────────────────────────────────────────────────────────┘
```

#### `architecture-overview.png` (1000×600)
```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Analyst   │────▶│ OpenCode    │────▶│  Nemotron   │
│  Terminal   │     │   CLI       │     │  3 Ultra    │
└─────────────┘     └─────────────┘     └─────────────┘
       │                   │                   │
       ▼                   ▼                   ▼
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Log Files  │     │  Local      │     │  1M Token   │
│  PCAP/Logs  │     │  Tools      │     │  Context    │
│  Memory     │     │  (tshark,   │     │  550B Params│
│  Dumps      │     │  yara,      │     │  MoE Arch   │
└─────────────┘     └─────────────┘     └─────────────┘
```

#### `quickstart-demo.gif` (30 seconds)
Record these steps:
1. `curl -fsSL https://opencode.ai/install | bash`
2. `echo 'export PATH=...' >> ~/.zshrc && source ~/.zshrc`
3. `mkdir -p ~/soc-test && cd ~/soc-test`
4. `echo "ERROR Failed login from 192.168.1.100" > test.log`
5. `opencode "Read test.log, extract the IP..."`
6. Show AI response extracting IP

#### `opencode-tui.png`
- Open OpenCode TUI
- Run `/connect NVIDIA nvapi-xxx`
- Run `/models`
- Capture with Nemotron 3 Ultra highlighted

#### `sigma-output.png`
- Run Sigma prompt
- Capture the YAML output in terminal

#### `memory-forensics.png`
- Run memory forensics prompt with `--loop`
- Capture script generation + execution

---

## Style Guidelines

### Terminal Theme (for consistency)
```json
{
  "background": "#1e1e2e",
  "foreground": "#cdd6f4",
  "cursor": "#f5e0dc",
  "black": "#181825",
  "red": "#f38ba8",
  "green": "#a6e3a1",
  "yellow": "#f9e2af",
  "blue": "#89b4fa",
  "magenta": "#f5c2e7",
  "cyan": "#94e2d5",
  "white": "#bac2de"
}
```

### Image Dimensions
| Type | Width | Height |
|------|-------|--------|
| Hero banner | 1200px | 400px |
| Architecture | 1000px | 600px |
| Screenshots | 1000px | auto |
| GIF demo | 1000px | auto |
| Diagrams | 1000px | 600px |

### File Naming
- Use kebab-case: `hero-banner.png`
- Lowercase only
- Descriptive names

---

## Quick Capture Commands

```bash
# Create assets folder
mkdir -p assets

# Quick terminal screenshot (macOS)
# Cmd+Shift+4 → Space → Click terminal window

# Record demo
asciinema rec demo.cast
agg demo.cast quickstart-demo.gif

# Optimize images
brew install imagemagick
mogrify -strip -quality 85 assets/*.png
```

---

## After Adding Images

1. Commit to repo:
```bash
git add assets/ README.md
git commit -m "docs: add visual assets to README"
git push
```

2. Verify on GitHub - images should render automatically

---

## Alternative: Use Placeholders First

If you want to push README first and add images later, the markdown references will show as broken images but won't break the page. Replace with real images when ready.