# Discord Bot - Node.js with JSX Support

A modern Discord bot built with Node.js and JSX support, designed for easy deployment on Render or other cloud platforms.

## 🚀 Features

- **Slash Commands** - Modern Discord interactions with `/ping`, `/hello`, `/info`, `/help`, and `/test`
- **Welcome Messages** - Customizable welcome messages for new server members with images/GIFs
- **Modular Structure** - Organized commands, events, and components
- **Auto-loading** - Automatically loads commands and events from their respective directories
- **Rich Embeds** - Beautiful embed components for enhanced user experience
- **Error Handling** - Comprehensive error handling and logging
- **Cloud Ready** - Optimized for deployment on platforms like Render, Heroku, etc.

## 📋 Prerequisites

1. **Node.js** (version 16.9.0 or higher)
   - Download from [nodejs.org](https://nodejs.org/)

2. **Discord Bot Application**
   - Go to [Discord Developer Portal](https://discord.com/developers/applications)
   - Create a new application
   - Go to "Bot" section and create a bot
   - Copy the bot token and client ID (you'll need these)

3. **Cloud Platform Account** (optional)
   - Sign up at [render.com](https://render.com), [heroku.com](https://heroku.com), or similar

## 🔧 Local Development

1. **Clone/Download** this repository

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Setup environment**:

   - Copy `.env.example` to `.env`
   - Add your Discord bot token and client ID:

   ```env
   DISCORD_TOKEN=your_discord_bot_token_here
   CLIENT_ID=your_bot_client_id_here
   ```

4. **Deploy commands** (first time setup):

   ```bash
   node deploy-commands.js
   ```

5. **Check configuration** (optional):

   ```bash
   npm run check
   ```

6. **Run locally**:

   ```bash
   npm start
   ```
   
   Or for development with auto-restart:

   ```bash
   npm run dev
   ```

## 🌐 Deploy to Render

> **📋 For detailed deployment instructions, see [RENDER_DEPLOYMENT.md](RENDER_DEPLOYMENT.md)**

### Quick Setup:

1. **Create Render Account**: Sign up at [render.com](https://render.com)
2. **Create Web Service** (not Background Worker)
3. **Connect your GitHub repository**
4. **Configure environment variables**:
   - `DISCORD_TOKEN`
   - `CLIENT_ID` 
   - `NODE_ENV=production`
5. **Deploy and test**

### UptimeRobot Monitoring:

1. **Sign up at [UptimeRobot](https://uptimerobot.com)**
2. **Add HTTP monitor** for your Render URL + `/health`
3. **Set 5-minute intervals** to keep bot awake

Your bot will be available at: `https://yourapp.onrender.com/health`

## 🎯 Bot Permissions & Invite

### Required Permissions

Your bot needs minimal permissions:

- **Send Messages**
- **Use Slash Commands**

### Invite URL

Use this URL format to invite your bot:

```url
https://discord.com/api/oauth2/authorize?client_id=YOUR_BOT_CLIENT_ID&permissions=2048&scope=bot%20applications.commands
```

Replace `YOUR_BOT_CLIENT_ID` with your actual bot's client ID from the Discord Developer Portal.

## 📁 File Structure

```
discord-bot/
├── bot.js                    # Main bot file
├── deploy-commands.js        # Command deployment script
├── package.json             # Dependencies and scripts
├── .env.example             # Environment variables template
├── .babelrc                 # Babel configuration for JSX
├── src/
│   ├── commands/            # Slash commands
│   │   ├── ping.js          # Ping command
│   │   ├── hello.js         # Hello command
│   │   ├── info.js          # Bot info command
│   │   ├── help.js          # Help command
│   │   └── index.js         # Command exports
│   ├── events/              # Bot events
│   │   ├── ready.js         # Bot ready event
│   │   ├── interactionCreate.js # Interaction handling
│   │   ├── guildCreate.js   # New guild event
│   │   ├── guildDelete.js   # Left guild event
│   │   └── index.js         # Event exports
│   └── components/          # Reusable components
│       └── Embeds.js        # Embed utilities
└── README.md               # This file
```

## 🔍 Available Commands

### `/ping`

- **Description**: Check bot latency and API response time
- **Usage**: `/ping`
- **Response**: Shows both message latency and WebSocket ping

### `/hello`

- **Description**: Sends a friendly greeting
- **Usage**: `/hello` or `/hello @user`
- **Options**:
  - `user` (optional): User to greet specifically

### `/info`

- **Description**: Displays comprehensive bot information
- **Usage**: `/info`
- **Shows**: Server count, uptime, memory usage, versions, and more

### `/help`

- **Description**: Shows all available commands and detailed usage information
- **Usage**: `/help` or `/help command:<command_name>`
- **Options**:
  - `command` (optional): Get detailed help for a specific command
- **Features**: Interactive help system with examples and detailed explanations

### `/test`

- **Description**: Simple test command to verify bot functionality
- **Usage**: `/test`
- **Purpose**: Quick way to check if the bot is responding to commands

## 🔍 Troubleshooting

### Commands Not Working? Try This Checklist:

**Step 1: Verify Basic Setup**
1. ✅ Check that `DISCORD_TOKEN` and `CLIENT_ID` are correct in `.env`
2. ✅ Run `node deploy-commands.js` to register commands
3. ✅ Ensure bot is online (check console for "Bot is ready!" message)
4. ✅ Verify bot has proper permissions in your Discord server

**Step 2: Check Discord Permissions**
- Bot needs "Send Messages" and "Use Application Commands" permissions
- Bot role should be above other roles that might block it
- Try the `/test` command first to verify basic functionality

**Step 3: Wait for Discord Cache**
- Slash commands can take 5-10 minutes to appear globally
- Try kicking and re-inviting the bot to refresh permissions
- Commands should appear when you type `/` in Discord

**Step 4: Check Console Logs**
- Look for command execution messages like: `🔧 Executing command: test by Username#1234`
- If you see this, the command is working; if not, check permissions
- Any errors will appear in red with `❌` prefix

**Step 5: Test Locally**
```bash
npm start
# Then try commands in Discord
```

### Common Issues

1. **Bot not responding to commands**:
   - Ensure commands are deployed with `node deploy-commands.js`
   - Check if `DISCORD_TOKEN` and `CLIENT_ID` are set correctly
   - Verify bot has proper permissions in your Discord server
   - **Wait 5-10 minutes** - Discord can take time to update slash commands globally
   - Try kicking and re-inviting the bot to refresh permissions
   - Check console/logs for errors

2. **Render deployment shows "No open ports detected"**:
   - Make sure you created a **Background Worker**, not a Web Service
   - Discord bots don't need HTTP ports - Background Workers are correct
   - If you accidentally created a Web Service, delete it and create a Background Worker instead

3. **Commands show up but don't execute**:
   - Check that the bot has "Use Application Commands" permission
   - Verify the bot role is above other roles that might block it
   - Try the `/test` command first to verify basic functionality
   - Check if the bot can send messages in the channel

4. **"Module not found" errors**:
   - Run `npm install` to install all dependencies
   - Check that Node.js version is 16.9.0 or higher
   - Ensure all JSX files are properly formatted

5. **Deployment failed**:
   - Ensure `package.json` is present and correct
   - Check that `npm start` command works locally
   - Review build logs for specific error messages
   - Make sure environment variables are set on the platform

6. **JSX compilation errors**:
   - Check that `.babelrc` file is present
   - Ensure all JSX files use proper syntax
   - Verify that imports are using correct file extensions

7. **Bot goes offline**:
   - Free tier on cloud platforms may sleep after inactivity
   - Consider upgrading to paid plans for 24/7 uptime
   - Check if there are any runtime errors in logs

### Platform-Specific Notes

- **Render Free Tier**:
  - Service sleeps after 15 minutes of inactivity
  - 750 hours/month limit
  - Service spins down and up automatically

- **Heroku Free Tier** (deprecated):
  - Consider using Render, Railway, or other alternatives

- **Keeping Bot Online**:
  - Upgrade to paid plans for always-on service
  - Implement uptime monitoring services

## 📊 Monitoring

- **Platform Dashboard**: Monitor deployment status and logs
- **Discord Server**: Test commands to verify bot is online
- **Console Output**: Check for connection confirmations and errors

## 🔄 Updates

To update your bot:

1. **Make changes** to your code
2. **Push changes** to your Git repository
3. **Platform auto-deploys** from your connected branch
4. **If you add new commands**, run `node deploy-commands.js` locally or add it to your build process
5. **Monitor logs** during deployment

## 💡 Extending the Bot

### Adding New Commands

1. Create a new `.jsx` file in `src/commands/`
2. Follow the existing command structure
3. Export the command as default
4. Run `node deploy-commands.js` to register the command

### Adding New Events

1. Create a new `.jsx` file in `src/events/`
2. Follow the existing event structure
3. Export the event as default
4. The bot will automatically load it on restart

### Using Components

- Import `EmbedComponents` from `src/components/Embeds.jsx`
- Use predefined embed types: `success`, `error`, `warning`, `info`
- Create custom embeds with the `custom` method

## 🆘 Support

- **Discord.js Guide**: [discordjs.guide](https://discordjs.guide/)
- **Discord.js Docs**: [discord.js.org](https://discord.js.org/)
- **Discord Developer Portal**: [discord.com/developers](https://discord.com/developers)
- **Node.js Docs**: [nodejs.org/docs](https://nodejs.org/docs/)
- **Render Docs**: [render.com/docs](https://render.com/docs)

---

**Happy coding!** 🚀