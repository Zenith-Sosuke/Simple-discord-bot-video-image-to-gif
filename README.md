# Discord GIF Converter Bot

Converts videos and images to GIF format. Automatically handles file size so output stays under Discord's 8MB limit.

## Features

- Converts MP4, MOV, AVI, WEBM, MKV, FLV, WMV to GIF
- Converts PNG, JPG, JPEG, BMP, TIFF, WEBP to animated GIFs
- Automatically adjusts quality/resolution when output would be too large
- Accepts both URLs and direct file uploads
- Slash commands and prefix commands both work

## Prerequisites

- Node.js v16.9.0+
- FFmpeg installed and in PATH
- Discord bot token and client ID

## Setup

### 1. Install FFmpeg

**Windows:** Download from [ffmpeg.org](https://ffmpeg.org/download.html), extract to `C:\ffmpeg`, add `C:\ffmpeg\bin` to PATH.

**macOS:**
```bash
brew install ffmpeg
```

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt install ffmpeg
```

### 2. Install dependencies

```bash
git clone <your-repo-url>
cd discord-gif-bot
npm install discord.js dotenv axios fluent-ffmpeg uuid
```

### 3. Create a Discord application

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. New Application → Bot → Add Bot
3. Copy the **Bot Token**
4. Copy the **Application ID** from General Information

### 4. Create `.env`

```env
BOT_TOKEN=your_bot_token_here
CLIENT_ID=your_client_id_here
PREFIX=your_prefix_here
```

### 5. Invite the bot

Replace `YOUR_CLIENT_ID`:
```
https://discord.com/api/oauth2/authorize?client_id=YOUR_CLIENT_ID&permissions=274877908032&scope=bot%20applications.commands
```

Required permissions: Send Messages, Use Slash Commands, Attach Files, Read Message History.

### 6. Run

```bash
node index.js
```

## Usage

### Slash commands

```
/gif attachment:[file]
/gif attachment:[file] duration:5 fps:15 width:600
/gif url:https://example.com/video.mp4 duration:10
```

### Prefix commands

```
!gif https://example.com/video.mp4
!gif https://example.com/video.mp4 8 12 500
```

For uploads, attach the file and run `!gif [duration] [fps] [width]`.

## Options

| Option | Default | Range | Notes |
|--------|---------|-------|-------|
| `duration` | 10s | 1–30 | Max clip length for videos |
| `fps` | 10 | 1–30 | Higher = larger file |
| `width` | 480px | 100–1000 | Height scales automatically |
| `loop` | true | true/false | Slash commands only |

## Project structure

```
discord-gif-bot/
├── index.js
├── package.json
├── .env
├── temp/         # auto-created, auto-cleaned
└── README.md
```

## Troubleshooting

**FFmpeg not found** — run `ffmpeg -version` to check it's in PATH.

**Slash commands not appearing** — wait a few minutes for Discord to sync, or rejoin the server.

**File still too large after conversion** — try a shorter duration or smaller width. The bot optimizes automatically but has limits.

**Bot not responding** — check permissions, verify the token, make sure the bot is online.

## Deployment

```bash
npm install -g pm2
pm2 start index.js --name gif-bot
```

Temp files are cleaned up after each conversion. No manual maintenance needed.
.DS_Store
```
