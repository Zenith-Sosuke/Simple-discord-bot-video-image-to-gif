# Discord GIF Converter Bot 🎬

A powerful Discord bot that converts videos and images to optimized GIF format with automatic file size management.

## ✨ Features

- **Video to GIF**: Convert MP4, MOV, AVI, WEBM, MKV, FLV, WMV to GIF
- **Image to GIF**: Convert PNG, JPG, JPEG, BMP, TIFF, WEBP to animated GIFs
- **Smart Optimization**: Automatically adjusts settings to keep files under 8MB
- **Multiple Input Methods**: Support for URLs and direct file uploads
- **Slash Commands & Prefix**: Both modern slash commands and classic prefix commands
- **Customizable Settings**: Control duration, FPS, width, and looping

## 🚀 Quick Start

### Prerequisites

- **Node.js** (v16.9.0 or higher)
- **FFmpeg** installed and accessible in PATH
- **Discord Bot Token** and **Client ID**

### 1. Install FFmpeg

#### Windows:
1. Download from [ffmpeg.org](https://ffmpeg.org/download.html)
2. Extract to `C:\ffmpeg`
3. Add `C:\ffmpeg\bin` to your PATH environment variable

#### macOS:
```bash
brew install ffmpeg
```

#### Ubuntu/Debian:
```bash
sudo apt update
sudo apt install ffmpeg
```

### 2. Clone & Setup

```bash
git clone <your-repo-url>
cd discord-gif-bot
npm install
```

### 3. Required Dependencies

The bot uses these npm packages:

```json
{
  "dependencies": {
    "discord.js": "^14.0.0",
    "dotenv": "^16.0.0",
    "axios": "^1.0.0",
    "fluent-ffmpeg": "^2.1.0",
    "uuid": "^9.0.0"
  }
}
```

Install them with:
```bash
npm install discord.js dotenv axios fluent-ffmpeg uuid
```

### 4. Create Discord Application

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Click "New Application"
3. Name your bot (e.g., "GIF Converter")
4. Go to "Bot" section
5. Click "Add Bot"
6. Copy the **Bot Token**
7. Go to "General Information"
8. Copy the **Application ID** (Client ID)

### 5. Environment Setup

Create a `.env` file in your project root:

```env
BOT_TOKEN=your_bot_token_here
CLIENT_ID=your_client_id_here
PREFIX=your_prefix_here
```

**⚠️ Important**: Never commit your `.env` file! Add it to `.gitignore`.

### 6. Bot Permissions

Your bot needs these permissions:
- Send Messages
- Use Slash Commands
- Attach Files
- Read Message History
- Add Reactions (optional)

**Permission Integer**: `274877908032`

### 7. Invite Bot to Server

Use this URL (replace `YOUR_CLIENT_ID`):
```
https://discord.com/api/oauth2/authorize?client_id=YOUR_CLIENT_ID&permissions=274877908032&scope=bot%20applications.commands
```

### 8. Run the Bot

```bash
node index.js
```

You should see:
```
BotName#1234 is ready!
Updating slash commands...
Commands updated!
```

## 📁 Project Structure

```
discord-gif-bot/
├── index.js          # Main bot file
├── package.json      # Dependencies and scripts
├── .env              # Environment variables (create this)
├── .gitignore        # Git ignore file
├── temp/             # Temporary files (auto-created)
└── README.md         # This file
```

## 🎮 Usage Examples

### Slash Commands (Recommended)

**Basic conversion:**
```
/gif attachment:[upload your file]
```

**With custom settings:**
```
/gif attachment:[file] duration:5 fps:15 width:600
```

**From URL:**
```
/gif url:https://example.com/video.mp4 duration:10
```

**Image to GIF:**
```
/gif attachment:[image.png] duration:3 loop:true
```

### Prefix Commands

**Basic:**
```
!gif https://example.com/video.mp4
```

**With settings:**
```
!gif https://example.com/video.mp4 8 12 500
```

**Upload file + command:**
```
[Upload file] !gif 5 15 400
```

## ⚙️ Configuration Options

| Option | Description | Default | Range |
|--------|-------------|---------|-------|
| `duration` | Max seconds (videos) or loop duration (images) | 10 | 1-30 |
| `fps` | Frames per second | 10 | 1-30 |
| `width` | Width in pixels | 480 | 100-1000 |
| `loop` | Infinite loop (slash commands only) | true | true/false |

## 🛠️ Troubleshooting

### FFmpeg Issues

**Error: "FFmpeg not found"**
- Make sure FFmpeg is installed and in your PATH
- Test by running `ffmpeg -version` in terminal

**Error: "Permission denied"**
- On Linux/Mac, you might need to make FFmpeg executable
- Run: `chmod +x /usr/local/bin/ffmpeg`

### Bot Issues

**Bot doesn't respond:**
- Check bot has proper permissions in the server
- Verify bot token is correct
- Make sure bot is online (green status)

**Slash commands not showing:**
- Wait a few minutes for Discord to sync
- Try leaving and rejoining the server
- Check bot has `applications.commands` scope

**File too large errors:**
- Bot automatically optimizes, but very large files might still fail
- Try shorter duration or smaller dimensions
- Max output size is 8MB (Discord limit)

### Common Errors

**"Invalid argument" errors:**
- Usually caused by invalid file formats
- Make sure file isn't corrupted
- Try with a different file

**Memory issues:**
- Large files can cause memory problems
- Restart the bot if it becomes unresponsive
- Consider adding memory limits in production

## 🔧 Development

### Adding New Features

The bot is modular and easy to extend:

- **New commands**: Add to the `commands` array
- **New formats**: Update file type validation
- **New filters**: Modify the FFmpeg filter chains
- **New optimizations**: Add to the `tryConversion` function

### Testing

Test with various file types:
- Small videos (< 1MB)
- Large videos (> 50MB)  
- Different formats (MP4, MOV, etc.)
- Static images
- Animated GIFs

## 📝 .gitignore

Create a `.gitignore` file:

```gitignore
# Environment files
.env
.env.local
.env.production

# Dependencies
node_modules/

# Logs
*.log
npm-debug.log*

# Temporary files
temp/

# OS generated files
.DS_Store
Thumbs.db

# IDE files
.vscode/
.idea/
```

## 🚀 Deployment

### Hosting Options

**Free Options:**
- Railway
- Render
- Heroku (limited free tier)

**VPS Options:**
- DigitalOcean
- Linode  
- AWS EC2

### Production Considerations

1. **Process Manager**: Use PM2 to keep bot running
```bash
npm install -g pm2
pm2 start index.js --name gif-bot
```

2. **Error Handling**: Bot has built-in error handling and cleanup

3. **File Cleanup**: Temp files are automatically cleaned up

4. **Memory Management**: Bot cleans up resources after each conversion

## 📄 License

MIT License - feel free to modify and distribute!

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 💡 Tips

- **Large files**: Bot automatically optimizes, but smaller source files work better
- **Quality**: Higher FPS and resolution = larger files
- **Performance**: Bot processes one conversion at a time per server
- **Limits**: Discord has 8MB attachment limit - bot respects this

## 📞 Support

If you encounter issues:

1. Check the troubleshooting section
2. Verify FFmpeg installation
3. Check bot permissions
4. Look at console logs for errors
5. Open an issue on GitHub

---

**Happy GIF converting! 🎉**
