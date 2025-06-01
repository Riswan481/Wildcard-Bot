# 🌐 Auto Wildcard Telegram Bot

<div align="center">

[![npm version](https://badge.fury.io/js/auto-wildcard-bot.svg)](https://www.npmjs.com/package/auto-wildcard-bot)
[![Downloads](https://img.shields.io/npm/dm/auto-wildcard-bot.svg)](https://www.npmjs.com/package/auto-wildcard-bot)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js](https://img.shields.io/badge/Node.js-20%2B-green.svg)](https://nodejs.org/)
[![GitHub stars](https://img.shields.io/github/stars/AutoFTbot/Wildcard-Bot.svg?style=social&label=Star)](https://github.com/AutoFTbot/Wildcard-Bot)

**🚀 The most advanced Telegram bot for automated Cloudflare wildcard domain management**

[📖 Documentation](https://github.com/AutoFTbot/Wildcard-Bot/wiki) • [🚀 Quick Start](#-quick-start) • [💬 Support](https://t.me/AutoFtBot69) • [🐛 Issues](https://github.com/AutoFTbot/Wildcard-Bot/issues)

</div>

---

## 📋 Table of Contents

- [✨ Features](#-features)
- [🚀 Quick Start](#-quick-start)
- [📦 Installation](#-installation)
- [⚙️ Configuration](#️-configuration)
- [📱 Usage](#-usage)
- [🎯 Commands](#-commands)
- [👑 Admin Features](#-admin-features)
- [🔧 Advanced Configuration](#-advanced-configuration)
- [🚀 Deployment](#-deployment)
- [🛠️ Development](#️-development)
- [❓ FAQ](#-faq)
- [🆘 Troubleshooting](#-troubleshooting)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## ✨ Features

### 🎯 Core Functionality
- **🌐 Wildcard Domain Management** - Automated Cloudflare wildcard DNS setup
- **🤖 Telegram Bot Interface** - Complete bot management via Telegram
- **👥 Multi-User Support** - Each user manages their own domains
- **🔐 Secure Configuration** - Encrypted API key storage
- **📊 Real-time Analytics** - Domain statistics and monitoring
- **⚡ Lightning Fast** - Optimized for performance

### 🛡️ Security & Management
- **👑 Admin Dashboard** - Complete administrative control
- **🔒 Permission System** - Role-based access control
- **📢 Broadcast System** - Mass communication tools
- **🛡️ Rate Limiting** - Built-in abuse protection
- **📝 Comprehensive Logging** - Detailed activity tracking

### 🔧 Technical Features
- **📦 NPM Package** - Global installation support
- **🎨 Interactive Setup** - Beautiful CLI wizard
- **🔄 Auto-restart** - Process management ready
- **📱 Telegram Notifications** - Real-time alerts
- **🌍 Environment Variables** - Flexible configuration

---

## 🚀 Quick Start

Get your bot running in under 3 minutes!

### 1️⃣ Install Globally
```bash
npm install -g auto-wildcard-bot
```

### 2️⃣ Run Interactive Setup
```bash
auto-wildcard-bot
```

### 3️⃣ Start Your Bot
```bash
cd auto-wildcard-bot
npm start
```

**🎉 That's it! Your bot is now live and ready to manage wildcard domains!**

---

## 📦 Installation

### Prerequisites
- **Node.js 20+** - [Download here](https://nodejs.org/)
- **Telegram Bot Token** - Get from [@BotFather](https://t.me/BotFather)
- **Cloudflare Account** - [Sign up here](https://cloudflare.com/)

### Method 1: Global Installation (Recommended)
```bash
# Install globally
npm install -g auto-wildcard-bot

# Run setup wizard
auto-wildcard-bot
```

### Method 2: Local Installation
```bash
# Clone repository
git clone https://github.com/AutoFTbot/Wildcard-Bot.git
cd Wildcard-Bot

# Install dependencies
npm install

# Start bot
npm start
```

### Method 3: Docker (Coming Soon)
```bash
docker run -d --name wildcard-bot \
  -e BOT_TOKEN=your_token \
  -e ADMIN_IDS=your_id \
  auto-wildcard-bot:latest
```

---

## ⚙️ Configuration

### Environment Variables
Create a `.env` file in your project root:

```env
# 🤖 Bot Configuration
BOT_TOKEN=1234567890:ABCdefGHIjklMNOpqrsTUVwxyz
ADMIN_IDS=123456789,987654321

# 📢 Notifications
TELEGRAM_GROUP_ID=-1001234567890

# 🔧 Optional Settings
MAX_CUSTOM_DOMAINS=10
NODE_ENV=production
LOG_LEVEL=info
```

### Configuration File
Customize your bot behavior in `config/default.js`:

```javascript
module.exports = {
    // Admin Configuration
    ADMIN_IDS: [123456789, 987654321],
    
    // Domain Limits
    MAX_CUSTOM_DOMAINS: 10,
    MAX_DOMAINS_PER_USER: 5,
    
    // Available Domains
    DEFAULT_DOMAINS: [
        'yourdomain.com',
        'example.org',
        'demo.net'
    ],
    
    // Notification Settings
    NOTIFICATIONS: {
        TELEGRAM: {
            enabled: true,
            groupId: process.env.TELEGRAM_GROUP_ID || '',
        },
    },
    
    // Security Settings
    FORBIDDEN_KEYWORDS: [
        'admin', 'root', 'api', 'mail'
    ],
    
    // Rate Limiting
    RATE_LIMITS: {
        SETUP_WILDCARD: {
            PER_USER: 3,
            COOLDOWN: 3600
        }
    }
};
```

---

## 📱 Usage

### For End Users

#### 1. Initial Setup
```
/start → Welcome message and setup guide
/addcf <api_key> <email> → Register Cloudflare credentials
```

#### 2. Domain Management
```
/listdomain → View available domains
/setupwildcard example.com → Setup wildcard for domain
/new subdomain.example.com → Create custom subdomain
/mysub → View your subdomains
```

#### 3. Analytics & Monitoring
```
/analytics example.com → View domain statistics
/clearcache example.com → Clear Cloudflare cache
```

### For Bot Owners (Admins)

#### 1. User Management
```
/stats → Bot usage statistics
/userinfo 123456789 → View user details
/broadcast Hello everyone! → Message all users
```

#### 2. System Management
```
/testnotif → Test notification system
```

---

## 🎯 Commands

### 🔰 Basic Commands
| Command | Description | Usage |
|---------|-------------|-------|
| `/start` | Welcome message & setup guide | `/start` |
| `/help` | Show all available commands | `/help` |
| `/ping` | Check bot responsiveness | `/ping` |

### 🔧 Configuration Commands
| Command | Description | Usage |
|---------|-------------|-------|
| `/addcf` | Add Cloudflare credentials | `/addcf <api_key> <email>` |
| `/cfconfig` | View current configuration | `/cfconfig` |
| `/updatecf` | Update Cloudflare credentials | `/updatecf <api_key> <email>` |
| `/deletecf` | Remove configuration | `/deletecf` |

### 🌐 Domain Management Commands
| Command | Description | Usage |
|---------|-------------|-------|
| `/listdomain` | Show available domains | `/listdomain` |
| `/setupwildcard` | Setup wildcard domain | `/setupwildcard <domain>` |
| `/new` | Create custom subdomain | `/new <subdomain.domain.com>` |
| `/mysub` | View your subdomains | `/mysub` |
| `/searchdomain` | Search domains | `/searchdomain <keyword>` |
| `/delsub` | Delete subdomain | `/delsub <subdomain>` |

### 📊 Analytics Commands
| Command | Description | Usage |
|---------|-------------|-------|
| `/analytics` | View domain statistics | `/analytics <domain>` |
| `/clearcache` | Clear Cloudflare cache | `/clearcache <domain>` |

---

## 👑 Admin Features

### 📊 Statistics Dashboard
```
📊 BOT STATISTICS

👥 Users & Domains:
• Registered Users: 150
• Active Domains: 45
• Total Subdomains: 1,234

⚡ System Status:
• Uptime: 7d 12h 30m
• Memory Usage: 45.2 MB
• Node.js Version: v20.10.0

🤖 Bot Info:
• Bot Username: @YourWildcardBot
• Last Updated: 2024-01-15 14:30:25
```

### 📢 Broadcast System
Send messages to all registered users:
```
/broadcast 🚨 Scheduled maintenance in 1 hour. All services will be temporarily unavailable.
```

### 👤 User Management
Get detailed user information:
```
/userinfo 123456789

👤 USER INFORMATION
🆔 User ID: 123456789
📱 Telegram: @username (John Doe)
📧 Cloudflare Email: user@example.com
🌐 Custom Domains: 5
📅 Registration: 2024-01-10 09:15:32
```

---

## 🔧 Advanced Configuration

### Custom Domain Setup
Add your own domains to the bot:

```javascript
// config/default.js
DEFAULT_DOMAINS: [
    'your-domain.com',
    'another-domain.net',
    'example.org'
]
```

### Notification Customization
Configure Telegram notifications:

```javascript
NOTIFICATIONS: {
    TELEGRAM: {
        enabled: true,
        groupId: process.env.TELEGRAM_GROUP_ID,
        // Custom message templates
        templates: {
            welcome: '🎉 New user registered: {username}',
            domainSetup: '🌐 Wildcard setup: {domain} by {user}'
        }
    }
}
```

### Rate Limiting Configuration
Prevent abuse with custom rate limits:

```javascript
RATE_LIMITS: {
    SETUP_WILDCARD: {
        PER_USER: 5,        // Max 5 setups per user
        COOLDOWN: 3600      // 1 hour cooldown
    },
    ANALYTICS: {
        PER_USER: 10,       // Max 10 requests per hour
        COOLDOWN: 300       // 5 minutes between requests
    }
}
```

---

## 🚀 Deployment

### Production Deployment with PM2
```bash
# Install PM2 globally
npm install -g pm2

# Start bot with PM2
pm2 start index.js --name "wildcard-bot"

# Enable auto-restart on server reboot
pm2 startup
pm2 save

# Monitor logs
pm2 logs wildcard-bot

# Restart bot
pm2 restart wildcard-bot
```

### Environment Setup for Production
```bash
# Set production environment
export NODE_ENV=production

# Increase memory limit if needed
node --max-old-space-size=2048 index.js
```

### Nginx Reverse Proxy (Optional)
If you plan to add webhooks:

```nginx
server {
    listen 80;
    server_name your-bot-domain.com;
    
    location /webhook {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

---

## 🛠️ Development

### Project Structure
```
auto-wildcard-bot/
├── 📁 bin/
│   └── wildcard-bot.js         # CLI entry point
├── 📁 config/
│   ├── constants.js            # Application constants
│   └── default.js              # Default configuration
├── 📁 handlers/
│   ├── adminHandlers.js        # Admin command handlers
│   ├── cloudflareHandlers.js   # Cloudflare operations
│   ├── configHandlers.js       # Configuration management
│   ├── domainHandlers.js       # Domain operations
│   └── generalHandlers.js      # General bot commands
├── 📁 lib/
│   └── WildcardBot.js          # Main bot class
├── 📁 services/
│   ├── CloudflareManager.js    # Cloudflare API wrapper
│   └── NotificationService.js  # Notification system
├── 📁 utils/
│   ├── fileUtils.js            # File operations
│   ├── systemUtils.js          # System utilities
│   └── validation.js           # Input validation
├── 📁 data/                    # Bot data storage
├── index.js                    # Application entry point
├── package.json                # Dependencies
└── README.md                   # Documentation
```

### Running in Development Mode
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

# Start in development mode
npm run dev
```

### Code Style and Linting
```bash
# Run linter
npm run lint

# Fix linting issues
npm run lint:fix

# Format code
npm run format

# Run all checks
npm run check
```

### Testing
```bash
# Test configuration
npm run test:config

# Test notifications
npm run test:notifications

# Test Cloudflare connection
npm run test:cloudflare
```

---

## ❓ FAQ

### **Q: How do I get a Telegram Bot Token?**
A: Message [@BotFather](https://t.me/BotFather) on Telegram, use `/newbot` command, and follow the instructions.

### **Q: Where do I find my Cloudflare Global API Key?**
A: Go to [Cloudflare Dashboard](https://dash.cloudflare.com) → My Profile → API Tokens → Global API Key → View

### **Q: How do I get my Telegram ID?**
A: Message [@userinfobot](https://t.me/userinfobot) on Telegram to get your user ID.

### **Q: Can I use custom domains?**
A: Yes! Add your domains to the `DEFAULT_DOMAINS` array in `config/default.js`.

### **Q: Is there a limit on users or domains?**
A: You can configure limits in `config/default.js`. Default is 5 domains per user.

### **Q: How do I update the bot?**
A: Run `npm update -g auto-wildcard-bot` for global installations.

---

## 🆘 Troubleshooting

### Common Issues

#### 🔴 Bot not responding
```bash
# Check if bot is running
ps aux | grep node

# Check logs
pm2 logs wildcard-bot

# Restart bot
pm2 restart wildcard-bot
```

#### 🔴 "Bot token invalid" error
- Verify your bot token in `.env` file
- Make sure token format is correct: `1234567890:ABCdefGHIjklMNOpqrsTUVwxyz`
- Check if bot was deleted in @BotFather

#### 🔴 Cloudflare API errors
- Verify Global API Key and email in user configuration
- Check if domain is added to Cloudflare account
- Ensure API key has necessary permissions

#### 🔴 Notifications not working
- Verify `TELEGRAM_GROUP_ID` in environment variables
- Make sure bot is added to the notification group
- Check if bot has permission to send messages

#### 🔴 Domain setup fails
- Ensure domain is registered in Cloudflare
- Check DNS propagation status
- Verify Cloudflare account permissions

### Debug Mode
Enable detailed logging:
```bash
export LOG_LEVEL=debug
npm start
```

### Getting Help
1. Check our [Wiki](https://github.com/AutoFTbot/Wildcard-Bot/wiki)
2. Search [existing issues](https://github.com/AutoFTbot/Wildcard-Bot/issues)
3. Join our [Telegram group](https://t.me/AutoFtBot69)
4. Create a [new issue](https://github.com/AutoFTbot/Wildcard-Bot/issues/new)

---

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### 🐛 Bug Reports
- Use the [issue template](https://github.com/AutoFTbot/Wildcard-Bot/issues/new?template=bug_report.md)
- Include detailed reproduction steps
- Provide relevant logs and screenshots

### ✨ Feature Requests
- Check [existing requests](https://github.com/AutoFTbot/Wildcard-Bot/issues?q=is%3Aissue+is%3Aopen+label%3Aenhancement)
- Use the [feature template](https://github.com/AutoFTbot/Wildcard-Bot/issues/new?template=feature_request.md)
- Explain the use case and benefits

### 💻 Code Contributions
1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes and test thoroughly
4. Follow our coding standards (run `npm run lint`)
5. Commit with clear messages: `git commit -m 'Add amazing feature'`
6. Push to your branch: `git push origin feature/amazing-feature`
7. Open a Pull Request

### 📚 Documentation
- Improve existing documentation
- Add examples and use cases
- Translate to other languages
- Create video tutorials

---

## 📈 Roadmap

### 🚀 Upcoming Features
- [ ] **Web Dashboard** - Browser-based management interface
- [ ] **Docker Support** - Containerized deployment
- [ ] **Multi-language** - Support for multiple languages
- [ ] **Advanced Analytics** - Detailed usage statistics
- [ ] **Custom Commands** - User-defined bot commands
- [ ] **Backup System** - Automated data backups
- [ ] **Plugin System** - Extensible architecture

### 🎯 Long-term Goals
- [ ] **Cloud Hosting** - Managed hosting service
- [ ] **Mobile App** - Native mobile application
- [ ] **Enterprise Features** - Advanced business features
- [ ] **API Gateway** - RESTful API interface

---

## 📊 Statistics

<div align="center">

![GitHub repo size](https://img.shields.io/github/repo-size/AutoFTbot/Wildcard-Bot)
![GitHub code size](https://img.shields.io/github/languages/code-size/AutoFTbot/Wildcard-Bot)
![Lines of code](https://img.shields.io/tokei/lines/github/AutoFTbot/Wildcard-Bot)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/AutoFTbot/Wildcard-Bot)

</div>

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 AutoFTbot Team

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

## 🙏 Acknowledgments

- **Telegraf.js** - Telegram Bot API framework
- **Cloudflare** - DNS and CDN services
- **Node.js Community** - Runtime environment
- **Contributors** - Everyone who helped improve this project

---

## 📞 Support & Community

<div align="center">

### 💬 Get Help

[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/AutoFtBot69)
[![GitHub Issues](https://img.shields.io/badge/GitHub-Issues-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/AutoFTbot/Wildcard-Bot/issues)

### 🌟 Stay Updated

[![GitHub Watch](https://img.shields.io/github/watchers/AutoFTbot/Wildcard-Bot.svg?style=social&label=Watch)](https://github.com/AutoFTbot/Wildcard-Bot)
[![GitHub Star](https://img.shields.io/github/stars/AutoFTbot/Wildcard-Bot.svg?style=social&label=Star)](https://github.com/AutoFTbot/Wildcard-Bot)
[![GitHub Fork](https://img.shields.io/github/forks/AutoFTbot/Wildcard-Bot.svg?style=social&label=Fork)](https://github.com/AutoFTbot/Wildcard-Bot)

---

**⭐ If this project helped you, please give it a star!**

**Made with ❤️ by the AutoFTbot Team**

[🚀 Get Started Now](https://www.npmjs.com/package/auto-wildcard-bot) • [📖 Read the Docs](https://github.com/AutoFTbot/Wildcard-Bot/wiki) • [💬 Join Community](https://t.me/AutoFtBot69)

</div>
