# Personal Bio — Terminal Edition

> A customizable, cyberpunk-inspired personal bio website featuring animated visuals, a live Discord presence, an interactive terminal, and a built-in SoundCloud music player.

A minimal, single-page personal website designed to showcase your identity, skills, social links, and current Discord activity — with a dark aesthetic, glitch effects, and a terminal-inspired interface.

Preview: https://superb-horse-71bf06.netlify.app/

**No frameworks. No build tools. Just HTML, CSS, and vanilla JavaScript.**

---

## Features

- **Terminal Boot Screen** — An animated startup sequence with simulated commands and a click-to-enter transition.
- **Animated Profile Card** — A profile avatar with a rotating gradient ring, glowing effects, a 3D flip animation, and a customizable username.
- **Glitch & Neon Effects** — Animated text, glowing accents, scanlines, background effects, and smooth transitions.
- **Customizable Theme** — Change the primary and accent colors to match your personal aesthetic.
- **Live Discord Presence** — Display your Discord status and activity in real time using the [Lanyard API](https://lanyard.rest/).
- **SoundCloud Music Player** — An integrated audio player with play/pause, volume control, seeking, track progress, and animated equalizer bars.
- **Dynamic Social Links & Auto-SVG Resolver** — Add any social platform in the config. Built-in icons load instantly, while additional platforms are automatically fetched and sanitized via Simple Icons CDN.
- **Interactive Terminal** — A draggable, resizable terminal window with custom commands, history navigation, and profile information.
- **Dynamic Username** — Your configured username automatically updates the page title, profile heading, footer, and terminal prompts.
- **Custom Skills** — Display programming languages, technologies, or any other tags with optional icons.
- **Responsive Design** — Adapts to different screen sizes, including mobile devices.
- **Custom Cursor** — A glowing cursor with a particle trail on devices with a mouse or trackpad.
- **Social Preview Metadata** — Open Graph and theme-color metadata for browser and social sharing previews.

---

## Tech Stack

| Technology | Purpose |
| --- | --- |
| HTML5 | Website structure |
| CSS3 | Styling, animations, effects, and responsive layout |
| Vanilla JavaScript | Configuration, DOM manipulation, and dynamic content |
| WebSocket | Real-time Discord presence updates |
| Lanyard API | Discord status and activity data |
| SoundCloud Widget API | Embedded music playback |
| Simple Icons CDN | Automatic SVG fallback for custom social links |
| Google Fonts | Orbitron and JetBrains Mono typography |

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/bluvs/Adv-Biosite.git
cd Adv-Biosite
```

### 2. Configure your profile

Open `index.html` and find the `SITE CONFIGURATION` section near the top of the file:

```js
window.CONFIG = {
    themeColor: "#ffffff",
    accentColor: "#d3d3d3",

    username: "yourname",
    discordId: "YOUR_DISCORD_ID",
    avatarPath: "avatar.png",

    musicUrl: "https://soundcloud.com/artist/track",
    trackTitle: "Your Favorite Song",

    about: "A short description about yourself",
    projects: "projects/  (soon)",

    contactLinks: {
        discord: "yourdiscord",
        telegram: "https://t.me/yourusername",
        github: "https://github.com/yourusername"
    },

    skills: [
        { name: "JavaScript", icon: "" },
        { name: "Python", icon: "" },
        { name: "HTML & CSS", icon: "" }
    ]
};
```

### 3. Add your avatar

Place your profile image in the project root and name it `avatar.png`, or change `avatarPath` to point to your own image.

```text
your-repository/
├── index.html
├── avatar.png
└── README.md
```

### 4. Run locally

You can open `index.html` directly in your browser. For a more consistent local development experience, run a simple HTTP server:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`.

### 5. Deploy with GitHub Pages

1. Push your files to a GitHub repository.
2. Open the repository's **Settings → Pages**.
3. Under **Build and deployment**, select **Deploy from a branch**.
4. Select your branch (usually `main`) and the root (`/`) folder.
5. Save and wait for GitHub Pages to publish your website.

No compilation or package installation is required.

---

## Configuration Guide

Everything is controlled from the `window.CONFIG` object.

| Option | Description |
| --- | --- |
| `themeColor` | Main theme color, used for accents and visual effects |
| `accentColor` | Glow color for borders, animations, and highlights |
| `username` | Profile name, page title, footer, and terminal username |
| `discordId` | Discord user ID used for Lanyard presence |
| `avatarPath` | Path to your profile picture |
| `musicUrl` | SoundCloud track URL |
| `trackTitle` | Custom title displayed in the player |
| `about` | Text returned by the terminal's `about` command |
| `projects` | Text returned by the terminal's `ls` command |
| `contactLinks` | Key-value object of social profiles and handles |
| `skills` | Array of skills displayed on the profile card |

### Changing the colors

To switch to a red theme:

```js
themeColor: "#ff003c",
accentColor: "#ff3355",
```

Any valid CSS color value (HEX, RGB, HSL) is supported.

### Changing your skills

Add or remove entries in the `skills` array:

```js
skills: [
    { name: "Python", icon: "" },
    { name: "C++", icon: "" },
    { name: "JavaScript", icon: "" },
    { name: "SQL", icon: "" }
]
```

Each entry contains a `name` and an optional `icon` prefix. Set `icon` to `""` for text-only tags.

### Configuring social links (Dynamic SVG System)

The `contactLinks` object dynamically generates buttons and terminal entries based on the keys you provide:

```js
contactLinks: {
    discord: "yourdiscord",
    telegram: "https://t.me/yourusername",
    github: "https://github.com/yourusername",
    tiktok: "https://www.tiktok.com/@yourusername",
    steam: "https://steamcommunity.com/id/yourusername",
    reddit: "https://www.reddit.com/user/yourusername"
}
```

How it works:
- **Zero-latency built-in icons:** `discord`, `telegram`, `github`, `tiktok`, `youtube`, `x` (`twitter`), `instagram`, `steam`, and `spotify` are bundled directly in the script.
- **Automatic CDN fallback:** Any other platform key (e.g., `reddit`, `gitlab`, `twitch`, `linkedin`) is automatically fetched from Simple Icons CDN, parsed safely via `DOMParser` (preventing XSS), and injected as a vector path.
- **Smart click behavior:**
  - Values starting with `http://` or `https://` open as external links in a new tab.
  - Plain text values (such as a Discord username) are automatically copied to the clipboard when clicked, showing a `copied` tooltip.
- **Terminal sync:** All configured links are automatically formatted and aligned in the terminal's `contact` command.

### Setting up music

Set `musicUrl` to a valid SoundCloud track URL and `trackTitle` to the display name:

```js
musicUrl: "https://soundcloud.com/artist/track-name",
trackTitle: "Artist — Track Name"
```

The player uses the SoundCloud Widget API. Playback depends on the availability and embedding permissions of the selected track.

---

## Interactive Terminal

The website includes a draggable, resizable terminal window with command history (`ArrowUp` / `ArrowDown`) and window controls.

Type `help` into the terminal to list the main commands:

| Command | Description |
| --- | --- |
| `help` | List available commands |
| `about` | Display your configured description |
| `skills` | Display your configured skills |
| `contact` | List all configured social links and handles |
| `status` | Check your live Discord presence |
| `music` | Toggle music playback |
| `discord` | Copy your Discord username to the clipboard |
| `whoami` | Print current terminal user (`guest`) |
| `ls` | List configured projects |
| `sudo` | Permission check easter egg |
| `clear` | Clear the terminal output |
| `dontopen` | Trigger a full-screen visual easter egg |

The terminal is a front-end simulation and does not execute system commands.

---

## Discord Presence Setup

The live presence feature uses [Lanyard](https://lanyard.rest/) over WebSocket to retrieve real-time Discord status updates.

1. Join the [Lanyard Discord server](https://discord.gg/lanyard).
2. Enable Developer Mode in Discord (**User Settings → Advanced → Developer Mode**), right-click your profile, and select **Copy User ID**.
3. Paste your numeric ID into `discordId` inside `window.CONFIG`.

Supported states include `online`, `idle`, `dnd`, and `offline`, along with active game status, Spotify playback, or custom status text.

---

## Project Structure

```text
.
├── index.html      # Main website, styling, scripts, and configuration
├── avatar.png      # Profile image
└── README.md       # Project documentation
```

---

## Privacy & Third-Party Services

This website runs entirely in the visitor's browser, utilizing the following external services:

- **Lanyard API:** Fetches real-time Discord presence data for the configured User ID.
- **SoundCloud Widget API:** Streams embedded audio.
- **Simple Icons CDN:** Queried only when a social platform key in `contactLinks` is not found in the local icon dictionary.
- **Google Fonts:** Loads the `Orbitron` and `JetBrains Mono` fonts.

Do not store private credentials, API keys, or access tokens in `index.html`.

---

## Contributing

1. Fork the repository.
2. Create a feature branch.
3. Commit your changes and test them in a browser.
4. Open a pull request with a clear description of the changes.

---

<p align="center">
  <b>Made for developers who like their profiles a little different.</b>
  <br />
  Customize it, make it yours, and share it with the world.
    Thanks V3nno for making the site which i could upgrade <3
</p>
