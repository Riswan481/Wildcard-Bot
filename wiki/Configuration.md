# 🔧 Configuration Guide

Complete guide for configuring AutoFT Bot Wildcard.

## 🚀 Quick Setup

### Method 1: Interactive Setup (Recommended)

```bash
# Install globally
npm install -g autoft-bot-wildcard

# Run setup wizard
autoft-bot-wildcard
```

The interactive setup will guide you through:
1. Bot token configuration
2. Admin ID setup
3. Optional notification group setup
4. Automatic file generation

### Method 2: Manual Configuration

Create a `.env` file in your project root with the required variables.

---

## 🔑 Environment Variables

### Required Variables

#### `BOT_TOKEN`
**Description**: Telegram Bot Token from @BotFather  
**Required**: Yes  
**Example**: `BOT_TOKEN=1234567890:ABCdefGHIjklMNOpqrsTUVwxyz`

How to get:
1. Message [@BotFather](https://t.me/BotFather) on Telegram
2. Use `/newbot` command
3. Follow the instructions
4. Copy the token provided

#### `ADMIN_IDS`
**Description**: Telegram User IDs with admin access  
**Required**: Yes  
**Format**: Comma-separated list  
**Example**: `ADMIN_IDS=123456789,987654321`

How to get your Telegram ID:
1. Message [@userinfobot](https://t.me/userinfobot)
2. Copy the user ID provided
3. Add to ADMIN_IDS

### Optional Variables

#### `TELEGRAM_GROUP_ID`
**Description**: Group ID for notifications  
**Required**: No  
**Example**: `TELEGRAM_GROUP_ID=-1001234567890`

How to get group ID:
1. Add [@userinfobot](https://t.me/userinfobot) to your group
2. Send any message
3. Copy the group ID (negative number)

#### `MAX_CUSTOM_DOMAINS`
**Description**: Maximum custom domains per user  
**Required**: No  
**Default**: 5  
**Example**: `MAX_CUSTOM_DOMAINS=10`

#### `NODE_ENV`
**Description**: Environment mode  
**Required**: No  
**Default**: development  
**Options**: `development`, `production`  
**Example**: `NODE_ENV=production`

#### `LOG_LEVEL`
**Description**: Logging verbosity  
**Required**: No  
**Default**: info  
**Options**: `error`, `warn`, `info`, `debug`  
**Example**: `LOG_LEVEL=debug`

---

## 📄 Configuration Files

### `.env` File Example

```env
# 🤖 Bot Configuration
BOT_TOKEN=1234567890:ABCdefGHIjklMNOpqrsTUVwxyz
ADMIN_IDS=123456789,987654321

# 📢 Notifications (Optional)
TELEGRAM_GROUP_ID=-1001234567890

# 🔧 Optional Settings
MAX_CUSTOM_DOMAINS=5
NODE_ENV=production
LOG_LEVEL=info
```

### `config/default.js` File

Create a configuration file for advanced settings:

```javascript
module.exports = {
    // Admin Configuration
    ADMIN_IDS: [123456789, 987654321],

    // Domain Limits
    MAX_CUSTOM_DOMAINS: 5,
    MAX_DOMAINS_PER_USER: 10,

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
        'admin', 'root', 'api', 'mail', 'www'
    ],

    // Rate Limiting
    RATE_LIMITS: {
        SETUP_WILDCARD: {
            PER_USER: 3,
            COOLDOWN: 3600  // 1 hour
        },
        ANALYTICS: {
            PER_USER: 10,
            COOLDOWN: 300   // 5 minutes
        }
    }
};
```

---

## 🌐 Domain Configuration

### Adding Custom Domains

Edit the `DEFAULT_DOMAINS` array in `config/default.js`:

```javascript
DEFAULT_DOMAINS: [
    'yourdomain.com',
    'anotherdomain.net',
    'example.org'
]
```

### Domain Requirements

Domains must:
- Be registered in your Cloudflare account
- Have active DNS zone
- Allow API management

---

## 🔒 Security Configuration

### Admin Access

Only users listed in `ADMIN_IDS` can:
- View bot statistics
- Broadcast messages
- Access user information
- Test notifications

### Rate Limiting

Configure limits to prevent abuse:

```javascript
RATE_LIMITS: {
    SETUP_WILDCARD: {
        PER_USER: 3,        // Max 3 setups per user
        COOLDOWN: 3600      // 1 hour cooldown
    }
}
```

### Forbidden Keywords

Prevent creation of sensitive subdomains:

```javascript
FORBIDDEN_KEYWORDS: [
    'admin', 'root', 'api', 'mail', 'www', 'ftp'
]
```

---

## 📢 Notification Configuration

### Telegram Notifications

Configure notifications in `config/default.js`:

```javascript
NOTIFICATIONS: {
    TELEGRAM: {
        enabled: true,
        groupId: process.env.TELEGRAM_GROUP_ID || '',
    }
}
```

### Notification Events

Bot sends notifications for:
- ✅ Successful wildcard setup
- ❌ Setup failures
- 👤 New user registrations
- 🚨 Error alerts

---

## 🔍 Validation

### Test Configuration

```bash
# Method 1: CLI validation
autoft-bot-wildcard --validate-config

# Method 2: Test notifications
autoft-bot-wildcard --test-notifications

# Method 3: Test Cloudflare connection
autoft-bot-wildcard --test-cloudflare
```

### Configuration Checklist

- [ ] ✅ Bot token is valid
- [ ] ✅ Admin IDs are correct
- [ ] ✅ Telegram group ID is valid (if used)
- [ ] ✅ Domains are in Cloudflare
- [ ] ✅ Rate limits are appropriate
- [ ] ✅ Forbidden keywords are set

---

## 🚀 Production Deployment

### Environment Setup

```bash
# Set production environment
export NODE_ENV=production

# Start with PM2
pm2 start index.js --name "autoft-bot-wildcard"

# Enable auto-restart
pm2 startup
pm2 save
```

### Best Practices

1. **Use environment variables** for sensitive data
2. **Set appropriate rate limits** to prevent abuse
3. **Configure logging level** based on needs
4. **Enable notifications** for monitoring
5. **Regularly backup** configuration files

---

## 🆘 Troubleshooting Configuration

### Common Issues

#### Bot not starting
```bash
# Check bot token
echo $BOT_TOKEN

# Validate token format
# Should be: number:letters_numbers
```

#### Admin commands not working
```bash
# Verify admin ID
echo $ADMIN_IDS

# Check if your ID is included
```

#### Notifications not working
```bash
# Check group ID
echo $TELEGRAM_GROUP_ID

# Ensure bot is added to group
# Ensure bot has send message permission
```

### Debug Mode

Enable debug logging:

```bash
export LOG_LEVEL=debug
npm start
```

---

**Need help with configuration? Join our [updates channel](https://t.me/AutoFtFile) for the latest guides and updates!** 