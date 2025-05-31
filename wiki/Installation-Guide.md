# 📖 Installation Guide

This guide will walk you through installing and setting up the Wildcard Domain Bot on your server.

## 📋 Prerequisites

Before installing, make sure you have:

### ✅ **System Requirements**

- **Node.js 16+** - [Download from nodejs.org](https://nodejs.org/)
- **NPM 8+** - Usually comes with Node.js
- **Git** - For cloning repositories (optional)
- **Linux/Windows/macOS** - Any modern operating system

### ✅ **Accounts & Credentials**

- **Telegram Bot Token** - Get from [@BotFather](https://t.me/BotFather)
- **Cloudflare Account** - Sign up at [cloudflare.com](https://cloudflare.com)
- **Cloudflare Global API Key** - From your profile settings

### ✅ **Domain Requirements**

- **Domain registered** - Any domain you own
- **Domain on Cloudflare** - Add your domain to Cloudflare DNS

## 🚀 Installation Methods

### Method 1: Global Installation (Recommended)

This is the easiest way to get started:

```bash
# Install globally
npm install -g auto-wildcard-bot

# Run interactive setup
auto-wildcard-bot

# Follow the setup wizard
cd wildcard-bot
npm start
```

### Method 2: Local Installation

If you prefer local installation:

```bash
# Create project directory
mkdir my-wildcard-bot
cd my-wildcard-bot

# Install locally
npm init -y
npm install auto-wildcard-bot

# Create main file
echo "const WildcardBot = require('auto-wildcard-bot'); new WildcardBot().start();" > index.js

# Run the bot
node index.js
```

### Method 3: From Source (Developers)

For developers who want to modify the code:

```bash
# Clone repository
git clone https://github.com/AutoFTbot/Wildcard-Bot.git
cd Wildcard-Bot

# Install dependencies
npm install

# Copy environment file
cp .env.example .env

# Edit configuration
nano .env

# Start bot
npm start
```

## ⚙️ Step-by-Step Setup

### Step 1: Get Bot Token

1. **Open Telegram** and search for [@BotFather](https://t.me/BotFather)
2. **Send** `/newbot` command
3. **Choose a name** for your bot (e.g., "My Wildcard Bot")
4. **Choose a username** ending with 'bot' (e.g., "my_wildcard_bot")
5. **Copy the token** provided by BotFather

### Step 2: Get Cloudflare API Key

1. **Login** to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. **Go to** Profile → API Tokens
3. **Find** "Global API Key" section
4. **Click** "View" and enter your password
5. **Copy** the API key

### Step 3: Interactive Setup

Run the setup wizard:

```bash
auto-wildcard-bot
```

You'll see:

```
🌐 WILDCARD TELEGRAM BOT SETUP
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Welcome! Let's set up your Wildcard Telegram Bot in 3 easy steps:
  1️⃣  Bot Token Configuration
  2️⃣  Admin Setup
  3️⃣  Launch Bot

1️⃣  BOT TOKEN CONFIGURATION
ℹ Get your bot token from @BotFather on Telegram
ℹ Link: https://t.me/BotFather

Enter your bot token:
```

### Step 4: Configure Bot

1. **Enter your bot token** when prompted
2. **Enter your Telegram ID** as admin
3. **Choose data directory** (default recommended)
4. **Review configuration** before proceeding

### Step 5: Start Bot

```bash
cd wildcard-bot
npm start
```

You should see:

```
✅ Configuration loaded
📄 Created data files
🔧 All command handlers registered
🚀 Wildcard Bot started successfully!
📱 Bot username: @YourBotName
👑 Admin IDs: [your_id]
✨ Bot is ready to receive commands!
```

## 🔧 Configuration

### Environment Variables

Create `.env` file in your bot directory:

```bash
# Required
BOT_TOKEN=your_bot_token_here
ADMIN_IDS=123456789,987654321

# Optional
TELEGRAM_GROUP_ID=-1001234567890
WHATSAPP_API_URL=https://your-whatsapp-api.com
WHATSAPP_TOKEN=your_whatsapp_token

# Cloudflare (set via bot commands)
CF_GLOBAL_API_KEY=auto_set_by_bot
CF_EMAIL=auto_set_by_bot
```

### Configuration File

Edit `config/default.js`:

```javascript
module.exports = {
    // Admin user IDs (Telegram IDs)
    ADMIN_IDS: [123456789],

    // Bot settings
    BOT_USERNAME: 'YourBotUsername',

    // Domain limits
    LIMITS: {
        MAX_CUSTOM_SUBDOMAINS: 10,
        MAX_DOMAINS_PER_USER: 5,
    },

    // Default domains available to users
    DEFAULT_DOMAINS: ['yourdomain.com', 'anotherdomain.com'],

    // Notification settings
    NOTIFICATIONS: {
        TELEGRAM: {
            enabled: true,
            groupId: process.env.TELEGRAM_GROUP_ID,
        },
        WHATSAPP: {
            enabled: false,
            apiUrl: process.env.WHATSAPP_API_URL,
            token: process.env.WHATSAPP_TOKEN,
        },
    },
};
```

## 🐳 Docker Installation

Use Docker for containerized deployment:

### Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy source code
COPY . .

# Create data directory
RUN mkdir -p data

# Expose port (if needed)
EXPOSE 3000

# Start bot
CMD ["npm", "start"]
```

### Docker Compose

```yaml
version: '3.8'

services:
    wildcard-bot:
        build: .
        container_name: wildcard-bot
        restart: unless-stopped
        environment:
            - BOT_TOKEN=${BOT_TOKEN}
            - ADMIN_IDS=${ADMIN_IDS}
        volumes:
            - ./data:/app/data
            - ./config:/app/config
        networks:
            - bot-network

networks:
    bot-network:
        driver: bridge
```

### Running with Docker

```bash
# Build and run
docker-compose up -d

# View logs
docker-compose logs -f

# Stop
docker-compose down
```

## 🖥️ Production Deployment

### Using PM2

```bash
# Install PM2
npm install -g pm2

# Start bot with PM2
pm2 start index.js --name "wildcard-bot"

# Auto-restart on boot
pm2 startup
pm2 save

# Monitor
pm2 status
pm2 logs wildcard-bot
```

### Using Systemd

Create `/etc/systemd/system/wildcard-bot.service`:

```ini
[Unit]
Description=Wildcard Domain Bot
After=network.target

[Service]
Type=simple
User=ubuntu
WorkingDirectory=/home/ubuntu/wildcard-bot
ExecStart=/usr/bin/node index.js
Restart=always
RestartSec=10
Environment=NODE_ENV=production

[Install]
WantedBy=multi-user.target
```

Enable and start:

```bash
sudo systemctl daemon-reload
sudo systemctl enable wildcard-bot
sudo systemctl start wildcard-bot
sudo systemctl status wildcard-bot
```

## 🔧 Post-Installation

### Test Bot

1. **Find your bot** on Telegram
2. **Send** `/start` command
3. **Register** with Cloudflare: `/addcf <api_key> <email>`
4. **Test** wildcard setup: `/setupwildcard yourdomain.com`

### Setup Notifications

1. **Create Telegram group** for notifications
2. **Add your bot** to the group
3. **Get group ID** using [@userinfobot](https://t.me/userinfobot)
4. **Update** `TELEGRAM_GROUP_ID` in config

### Security Setup

1. **Secure your server** with firewall
2. **Use HTTPS** for webhooks (if applicable)
3. **Keep tokens secure** - never commit to git
4. **Regular updates** - keep bot updated

## ❌ Common Issues

### "Bot token invalid"

- Verify token is correct
- Check for extra spaces
- Generate new token if needed

### "Command not found: auto-wildcard-bot"

```bash
# Check global installation
npm list -g auto-wildcard-bot

# Reinstall if needed
npm install -g auto-wildcard-bot
```

### "Permission denied"

```bash
# Fix NPM permissions (Linux/Mac)
sudo chown -R $(whoami) ~/.npm
sudo chown -R $(whoami) /usr/local/lib/node_modules
```

### "Module not found"

```bash
# Clear npm cache
npm cache clean --force

# Reinstall
npm install
```

## 📞 Getting Help

If you encounter issues:

1. **Check the logs** - `pm2 logs` or `docker logs`
2. **Read troubleshooting** - [Troubleshooting Guide](Troubleshooting)
3. **GitHub Issues** - Report bugs
4. **Telegram Support** - [@AutoFtBot69](https://t.me/AutoFtBot69)

---

**Next: [⚙️ Configuration Guide](Configuration)**
