# Roblox Gamepass Creator

Roblox Gamepass Creator is a powerful productivity extension designed to automate the tedious process of creating, pricing, and listing gamepasses for Roblox donation-based experiences like *Pls Donate*, *Meet People Across The World*, and *The Corner*.

## 🚀 Official Installation

For the most stable experience and automatic updates, install directly from the Chrome Web Store:

**[Install Roblox Gamepass Creator](https://chromewebstore.google.com/detail/roblox-gamepass-creator/mnhnckmekgknmjbmpfcipimndmoeibei?authuser=0&hl=en)**

---

## 🛠️ Manual Installation (Developer Mode)

If you prefer to run the extension from the source code or contribute to development, follow these steps:

1. **Clone or Download** this repository to your local machine.
2. Open Google Chrome and navigate to `chrome://extensions/`.
3. Enable **Developer mode** using the toggle in the top-right corner.
4. Click the **Load unpacked** button.
5. Select the root folder of this project (the one containing `manifest.json`).
6. The extension is now active! Navigate to any Roblox page to see the "Create Passes" button in your navbar.

---

## 🏗️ Technical Architecture

### Core Components
- **Content Script (`content/content.js`):** The engine of the extension. It injects a "Create Passes" button into the Roblox navbar and renders a custom UI using a **Shadow DOM** to ensure styles don't conflict with Roblox's native CSS.
- **Shadow UI:** A modern, draggable interface built with vanilla JavaScript and CSS variables for a sleek, dark-themed aesthetic.

### Permissions & Security
This extension follows the principle of least privilege, using only what is necessary:
- `storage`: To save your custom price presets and progress during automation.
- `host_permissions`: Specifically limited to `www.roblox.com`, `games.roblox.com`, and `apis.roblox.com` to communicate with official API endpoints.

---

## 📡 API Integration

The extension automates tasks by communicating directly with official Roblox REST APIs. It uses your existing browser session for authentication—no passwords or sensitive data are ever requested or stored.

### 1. Game Discovery
`https://games.roblox.com/v2/users/{userId}/games`  
Used to find the user's primary "root" experience where the gamepasses will be hosted.

### 2. Universe Mapping
`https://apis.roblox.com/universes/v1/places/{placeId}/universe`  
Maps the root place ID to a Universe ID, which is required for the modern Gamepass API.

### 3. Pass Creation
`https://apis.roblox.com/game-passes/v1/universes/{universeId}/game-passes`  
A `POST` request that generates the gamepass object within the selected universe.

### 4. Pricing & Listing
`https://apis.roblox.com/game-passes/v1/universes/{universeId}/game-passes/{passId}`  
A `PATCH` request that sets the gamepass price, toggles the "On Sale" status, and manages the "Regional Pricing" toggle.

### 5. Experience Questionnaire Automation
`https://apis.roblox.com/experience-questionnaire/v1/questionnaires/{universeId}/latest`  
`https://apis.roblox.com/experience-questionnaire/v1/responses/{universeId}/submissions`  
Automates the mandatory experience questionnaire by fetching the latest requirements and submitting a safe "No" response for all content categories.

---

## ✨ Features
- **Bulk Creation:** Create multiple gamepasses from custom presets in one click.
- **Custom Amount:** Toggle regional pricing per batch.
- **Regional Pricing Toggle:** Globally manage regional pricing defaults in settings.
- **Automatic Off-Sale:** Wipe all passes in an experience instantly.
- **Questionnaire Automation:** Automatically handle mandatory Roblox experience questionnaires.

---

## 📁 Project Structure

```text
├── content/
│   └── content.js         # Main logic and UI injection
├── icons/                 # Extension icons (16, 32, 48, 128)
├── manifest.json          # Extension configuration (MV3)
└── README.md              # Documentation
```

## ⚖️ Disclaimer

*Roblox Gamepass Creator is an independent project and is not affiliated with, authorized, maintained, sponsored, or endorsed by Roblox Corporation or any of its affiliates. Use this tool responsibly and in accordance with Roblox's Terms of Service.*
