# 🚀 Quick Start Guide

Get your AutoFT Bot Wildcard up and running in under 5 minutes!

## ⚡ 1-Minute Setup

### Step 1: Install the Bot

```bash
npm install -g autoft-bot-wildcard
```

### Step 2: Run Setup Wizard

```bash
autoft-bot-wildcard
```

### Step 3: Start Your Bot

```bash
cd autoft-bot-wildcard
npm start
```

**🎉 That's it! Your bot is now live!**

---

## 📋 Prerequisites

Before starting, make sure you have:

- ✅ **Node.js 16+** - [Download here](https://nodejs.org/)
- ✅ **Telegram Bot Token** - Get from [@BotFather](https://t.me/BotFather)
- ✅ **Your Telegram ID** - Get from [@userinfobot](https://t.me/userinfobot)
- ✅ **Cloudflare Account** - [Sign up here](https://cloudflare.com/)

---

## 🤖 Getting Bot Token

1. **Message @BotFather** on Telegram
2. **Use `/newbot` command**
3. **Choose a name** for your bot (e.g., "My Wildcard Bot")
4. **Choose a username** (must end with "bot", e.g., "mywildcardbot")
5. **Copy the token** provided (format: `1234567890:ABCdefGHIjklMNOpqrsTUVwxyz`)

---

## 🆔 Getting Your Telegram ID

1. **Message @userinfobot** on Telegram
2. **Copy your User ID** (a number like `123456789`)
3. **Save this number** - you'll need it for admin access

---

## ⚙️ Interactive Setup

The setup wizard will ask for:

### 1. Bot Token
```
Enter your bot token: 1234567890:ABCdefGHIjklMNOpqrsTUVwxyz
```

### 2. Admin ID
```
Enter your Telegram ID: 123456789
```

### 3. Notification Group (Optional)
```
Telegram Group ID for notifications (optional, press Enter to skip): -1001234567890
```

The wizard will:
- ✅ Create project directory
- ✅ Generate configuration files
- ✅ Install dependencies
- ✅ Set up environment

---

## 🚀 First Commands

Once your bot is running:

### 1. Start the Bot
Send `/start` to your bot on Telegram

### 2. Add Cloudflare Credentials
```
/addcf your_api_key your_email@domain.com
```

### 3. List Available Domains
```
/listdomain
```

### 4. Setup Your First Wildcard
```
/setupwildcard yourdomain.com
```

### 5. View Your Domains
```
/mysub
```

---

## 🌐 Getting Cloudflare Credentials

### Global API Key

1. **Go to [Cloudflare Dashboard](https://dash.cloudflare.com)**
2. **Click on your profile** (top right)
3. **Select "My Profile"**
4. **Go to "API Tokens" tab**
5. **Find "Global API Key"**
6. **Click "View"** and copy the key

### Email
Use the **same email** you used to register your Cloudflare account.

---

## 🔧 Quick Configuration

### Manual .env Setup (Alternative)

If you prefer manual setup, create `.env` file:

```env
# Bot Configuration
BOT_TOKEN=1234567890:ABCdefGHIjklMNOpqrsTUVwxyz
ADMIN_IDS=123456789

# Optional: Notifications
TELEGRAM_GROUP_ID=-1001234567890

# Optional: Settings
MAX_CUSTOM_DOMAINS=5
NODE_ENV=production
```

---

## 🎯 Usage Flow

### For Regular Users

1. **Start** → `/start`
2. **Configure** → `/addcf <api_key> <email>`
3. **Browse** → `/listdomain`
4. **Setup** → `/setupwildcard domain.com`
5. **Manage** → `/mysub`

### For Admins

1. **Monitor** → `/stats`
2. **Broadcast** → `/broadcast message`
3. **User Info** → `/userinfo 123456789`
4. **Test** → `/testnotif`

---

## 🚨 Quick Troubleshooting

### Bot Not Responding?
```bash
# Check if running
pm2 status

# Restart
pm2 restart autoft-bot-wildcard
```

### Commands Not Working?
```bash
# Check token
echo $BOT_TOKEN

# Verify admin ID
echo $ADMIN_IDS
```

### Installation Failed?
```bash
# Update npm
npm install -g npm@latest

# Reinstall
npm install -g autoft-bot-wildcard --force
```

---

## 📱 Production Setup

### Using PM2 (Recommended)

```bash
# Install PM2
npm install -g pm2

# Start with PM2
pm2 start index.js --name "autoft-bot-wildcard"

# Enable auto-restart
pm2 startup
pm2 save

# Monitor
pm2 status
pm2 logs autoft-bot-wildcard
```

---

## 🎉 Success Checklist

- [ ] ✅ Bot responds to `/start`
- [ ] ✅ Admin commands work (`/stats`)
- [ ] ✅ Cloudflare integration works (`/addcf`)
- [ ] ✅ Domain listing works (`/listdomain`)
- [ ] ✅ Wildcard setup works (`/setupwildcard`)
- [ ] ✅ Notifications work (if configured)

---

## 📚 Next Steps

1. **📖 Read [Commands Reference](Commands.md)** - Learn all available commands
2. **🔧 Check [Configuration Guide](Configuration.md)** - Advanced settings
3. **📢 Join [Updates Channel](https://t.me/AutoFtFile)** - Get latest news and updates
4. **⭐ Star the [Repository](https://github.com/AutoFTbot/Wildcard-Bot)** - Support the project

---

## 🆘 Need Help?

- **📖 Documentation**: [Full Wiki](Home.md)
- **🔧 Issues**: [Troubleshooting Guide](Troubleshooting.md)
- **📢 Updates**: [Channel](https://t.me/AutoFtFile)
- **👨‍💻 Developer**: [Contact](https://t.me/AutoFtBot69)
- **🐛 Bug Reports**: [GitHub Issues](https://github.com/AutoFTbot/Wildcard-Bot/issues)

---

**🚀 Ready to manage wildcard domains like a pro!** 