# ⚙️ Configuration Guide

Complete guide for configuring your Wildcard Domain Bot.

## 📋 Table of Contents

- [🚀 Quick Setup](#-quick-setup)
- [🔧 Configuration Files](#-configuration-files)
- [🌍 Environment Variables](#-environment-variables)
- [🔐 Authentication Setup](#-authentication-setup)
- [🌐 Cloudflare Configuration](#-cloudflare-configuration)
- [📱 Notification Settings](#-notification-settings)
- [👑 Admin Configuration](#-admin-configuration)
- [🔒 Security Settings](#-security-settings)
- [⚡ Performance Tuning](#-performance-tuning)

---

## 🚀 Quick Setup

### Interactive Setup (Recommended)

```bash
# Global installation
npm install -g auto-wildcard-bot

# Run interactive setup
auto-wildcard-bot

# Follow the prompts to configure:
# ✅ Bot Token
# ✅ Cloudflare Credentials
# ✅ Admin User IDs
# ✅ Notification Settings
```

### Manual Configuration

```bash
# Create configuration directory
mkdir -p ~/.wildcard-bot

# Copy example configuration
cp /usr/local/lib/node_modules/auto-wildcard-bot/config/default.example.js ~/.wildcard-bot/config.js

# Edit configuration
nano ~/.wildcard-bot/config.js
```

---

## 🔧 Configuration Files

### File Structure

```
~/.wildcard-bot/
├── config.js          # Main configuration file
├── .env               # Environment variables
├── data/
│   ├── config.json    # User configurations
│   ├── custom_subdomains.json  # Custom subdomain data
│   └── admin_usage.json        # Admin usage statistics
├── logs/
│   ├── bot.log        # General bot logs
│   ├── error.log      # Error logs
│   └── access.log     # Access logs
└── backups/
    ├── config_backup_YYYYMMDD.json
    └── data_backup_YYYYMMDD.tar.gz
```

### Main Configuration File

**Location:** `~/.wildcard-bot/config.js`

```javascript
module.exports = {
    // ============= BASIC SETTINGS =============
    BOT_TOKEN: process.env.BOT_TOKEN || 'your_bot_token_here',

    // Admin user IDs (Telegram user IDs)
    ADMIN_IDS: [
        123456789, // Replace with your Telegram user ID
        987654321, // Add more admin IDs as needed
    ],

    // ============= DATABASE SETTINGS =============
    DATA_DIR: './data',
    BACKUP_DIR: './backups',
    BACKUP_INTERVAL: 24 * 60 * 60 * 1000, // 24 hours in milliseconds
    AUTO_BACKUP: true,

    // ============= CLOUDFLARE SETTINGS =============
    CLOUDFLARE: {
        DEFAULT_EMAIL: '', // Leave empty for user-specific config
        DEFAULT_API_KEY: '', // Leave empty for user-specific config
        TIMEOUT: 30000, // 30 seconds
        RETRY_ATTEMPTS: 3,
        RATE_LIMIT: {
            REQUESTS_PER_MINUTE: 100,
            BURST_LIMIT: 10,
        },
    },

    // ============= NOTIFICATION SETTINGS =============
    NOTIFICATIONS: {
        TELEGRAM_GROUP: {
            enabled: true,
            chatId: process.env.TELEGRAM_GROUP_ID || '',
            silentMode: false,
        },
        WHATSAPP: {
            enabled: false,
            apiUrl: process.env.WHATSAPP_API_URL || '',
            token: process.env.WHATSAPP_TOKEN || '',
            phoneNumber: process.env.WHATSAPP_PHONE || '',
        },
        WEBHOOK: {
            enabled: false,
            url: process.env.WEBHOOK_URL || '',
            secret: process.env.WEBHOOK_SECRET || '',
            headers: {
                'Content-Type': 'application/json',
            },
        },
    },

    // ============= SECURITY SETTINGS =============
    SECURITY: {
        RATE_LIMITING: {
            enabled: true,
            maxRequestsPerMinute: 20,
            banDuration: 10 * 60 * 1000, // 10 minutes
        },
        COMMAND_COOLDOWN: {
            enabled: true,
            cooldownSeconds: 3,
        },
        ADMIN_ONLY_COMMANDS: ['stats', 'broadcast', 'userinfo', 'testnotif'],
        ALLOWED_DOMAINS: [], // Empty = allow all domains
        BLOCKED_USERS: [], // Telegram user IDs to block
    },

    // ============= PERFORMANCE SETTINGS =============
    PERFORMANCE: {
        POLLING_TIMEOUT: 30, // Telegram polling timeout
        MAX_CONCURRENT_OPERATIONS: 5,
        CACHE_TTL: 300, // 5 minutes
        LOG_LEVEL: 'info', // debug, info, warn, error
        ENABLE_METRICS: true,
    },

    // ============= FEATURE FLAGS =============
    FEATURES: {
        DOMAIN_MANAGEMENT: true,
        SUBDOMAIN_CREATION: true,
        ANALYTICS: true,
        CACHE_CLEARING: true,
        USER_STATISTICS: true,
        AUTO_NOTIFICATIONS: true,
    },

    // ============= LOCALIZATION =============
    LOCALE: {
        DEFAULT_LANGUAGE: 'id', // Indonesian
        TIMEZONE: 'Asia/Jakarta',
        DATE_FORMAT: 'DD/MM/YYYY HH:mm:ss',
    },
};
```

---

## 🌍 Environment Variables

### `.env` File

Create a `.env` file in the bot directory:

```bash
# ============= REQUIRED SETTINGS =============
BOT_TOKEN=123456789:ABCdefGHIjklMNOpqrsTUVwxyz
ADMIN_IDS=123456789,987654321

# ============= CLOUDFLARE (Optional - can be set per user) =============
CLOUDFLARE_EMAIL=your@email.com
CLOUDFLARE_API_KEY=your_global_api_key_here

# ============= NOTIFICATIONS =============
TELEGRAM_GROUP_ID=-1001234567890
WHATSAPP_API_URL=https://your-whatsapp-api.com
WHATSAPP_TOKEN=your_whatsapp_token
WHATSAPP_PHONE=1234567890

# ============= WEBHOOKS =============
WEBHOOK_URL=https://your-domain.com/webhook
WEBHOOK_SECRET=your_webhook_secret

# ============= DEVELOPMENT =============
NODE_ENV=production
DEBUG=wildcard:*
LOG_LEVEL=info

# ============= DATABASE =============
DATA_DIR=./data
BACKUP_ENABLED=true
BACKUP_INTERVAL=86400000

# ============= SECURITY =============
RATE_LIMIT_ENABLED=true
MAX_REQUESTS_PER_MINUTE=20
COMMAND_COOLDOWN=3
```

### Environment Variable Priority

1. **Command line arguments** (highest priority)
2. **`.env` file**
3. **System environment variables**
4. **Configuration file defaults** (lowest priority)

---

## 🔐 Authentication Setup

### 1. Telegram Bot Token

**Getting Your Token:**

1. Start chat with [@BotFather](https://t.me/BotFather)
2. Send `/newbot`
3. Choose bot name and username
4. Copy the token provided

**Format:** `123456789:ABCdefGHIjklMNOpqrsTUVwxyz`

```javascript
// In config.js
BOT_TOKEN: '123456789:ABCdefGHIjklMNOpqrsTUVwxyz'

// Or in .env
BOT_TOKEN=123456789:ABCdefGHIjklMNOpqrsTUVwxyz
```

### 2. Admin User IDs

**Finding Your Telegram ID:**

1. Message [@userinfobot](https://t.me/userinfobot)
2. It will reply with your user ID
3. Add to admin list

```javascript
// In config.js
ADMIN_IDS: [
    123456789, // Your Telegram user ID
    987654321, // Another admin
];

// Or in .env
(ADMIN_IDS = 123456789), 987654321;
```

### 3. Security Token Generation

**Generate secure tokens:**

```javascript
// Generate random tokens
const crypto = require('crypto');

// For webhook secret
const webhookSecret = crypto.randomBytes(32).toString('hex');

// For API tokens
const apiToken = crypto.randomBytes(16).toString('hex');
```

---

## 🌐 Cloudflare Configuration

### Global Configuration (Optional)

Set default Cloudflare credentials that all users will use:

```javascript
// In config.js
CLOUDFLARE: {
    DEFAULT_EMAIL: 'your@email.com',
    DEFAULT_API_KEY: 'your_global_api_key',
    TIMEOUT: 30000,
    RETRY_ATTEMPTS: 3
}
```

### Per-User Configuration (Recommended)

Allow each user to set their own Cloudflare credentials:

```javascript
// Leave these empty in config.js
CLOUDFLARE: {
    DEFAULT_EMAIL: '',
    DEFAULT_API_KEY: '',
}

// Users will configure via bot commands:
// /addcf email@domain.com your_api_key
```

### Getting Cloudflare Credentials

1. **Login to Cloudflare Dashboard**
2. **Go to My Profile → API Tokens**
3. **Find "Global API Key" section**
4. **Click "View" and enter password**
5. **Copy the API key**

### Testing Cloudflare Configuration

```bash
# Test API access
curl -X GET "https://api.cloudflare.com/client/v4/accounts" \
     -H "X-Auth-Email: your@email.com" \
     -H "X-Auth-Key: your_api_key" \
     -H "Content-Type: application/json"
```

---

## 📱 Notification Settings

### Telegram Group Notifications

**Setup Steps:**

1. **Create a Telegram group**
2. **Add your bot to the group**
3. **Get group ID using [@userinfobot](https://t.me/userinfobot)**
4. **Configure in bot**

```javascript
NOTIFICATIONS: {
    TELEGRAM_GROUP: {
        enabled: true,
        chatId: '-1001234567890', // Negative number for groups
        silentMode: false // Set true for silent notifications
    }
}
```

### WhatsApp Notifications

**Requirements:**

- WhatsApp Business API
- Valid API endpoint
- Authentication token

```javascript
NOTIFICATIONS: {
    WHATSAPP: {
        enabled: true,
        apiUrl: 'https://your-whatsapp-api.com/send',
        token: 'your_api_token',
        phoneNumber: '1234567890' // Without + or country code
    }
}
```

### Webhook Notifications

Send notifications to your own endpoint:

```javascript
NOTIFICATIONS: {
    WEBHOOK: {
        enabled: true,
        url: 'https://your-domain.com/webhook',
        secret: 'your_webhook_secret',
        headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer your_token'
        }
    }
}
```

**Webhook Payload Example:**

```json
{
    "timestamp": "2024-01-15T10:30:00.000Z",
    "event": "domain_created",
    "user": {
        "id": 123456789,
        "username": "john_doe",
        "first_name": "John"
    },
    "data": {
        "domain": "example.com",
        "subdomain": "api.example.com",
        "action": "created"
    }
}
```

---

## 👑 Admin Configuration

### Admin Privileges

Admins can use these commands:

- `/stats` - View bot statistics
- `/broadcast` - Send messages to all users
- `/userinfo` - Get user information
- `/testnotif` - Test notification systems

### Admin-Only Features

```javascript
SECURITY: {
    ADMIN_ONLY_COMMANDS: [
        'stats',
        'broadcast',
        'userinfo',
        'testnotif',
        'clearcache', // Optional: restrict cache clearing
    ];
}
```

### Multiple Admin Management

```javascript
// Add multiple admins
ADMIN_IDS: [
    123456789, // Primary admin
    987654321, // Secondary admin
    555666777, // Technical admin
];

// Or load from environment
ADMIN_IDS: process.env.ADMIN_IDS?.split(',').map((id) => parseInt(id)) || [];
```

---

## 🔒 Security Settings

### Rate Limiting

Prevent spam and abuse:

```javascript
SECURITY: {
    RATE_LIMITING: {
        enabled: true,
        maxRequestsPerMinute: 20,
        banDuration: 10 * 60 * 1000, // 10 minutes
        whitelistedUsers: [123456789] // Admin IDs are auto-whitelisted
    }
}
```

### Command Cooldown

Prevent rapid command execution:

```javascript
SECURITY: {
    COMMAND_COOLDOWN: {
        enabled: true,
        cooldownSeconds: 3,
        exemptCommands: ['help', 'start'], // No cooldown for these
        exemptUsers: [123456789] // Admins exempt
    }
}
```

### Domain Restrictions

Limit which domains can be managed:

```javascript
SECURITY: {
    ALLOWED_DOMAINS: [
        'example.com',
        'mysite.com',
        '*.allowed-domain.com' // Wildcard support
    ],
    BLOCKED_DOMAINS: [
        'spam-domain.com',
        'malicious-site.com'
    ]
}
```

### User Blocking

Block specific users:

```javascript
SECURITY: {
    BLOCKED_USERS: [
        999888777, // Blocked user ID
        111222333, // Another blocked user
    ];
}
```

---

## ⚡ Performance Tuning

### Bot Performance

```javascript
PERFORMANCE: {
    POLLING_TIMEOUT: 30, // Telegram polling timeout
    MAX_CONCURRENT_OPERATIONS: 5, // Parallel operations
    REQUEST_TIMEOUT: 30000, // 30 seconds
    KEEP_ALIVE: true
}
```

### Caching Configuration

```javascript
PERFORMANCE: {
    CACHE_TTL: 300, // 5 minutes
    CACHE_SIZE: 1000, // Max cached items
    CACHE_ENABLED: true,
    CACHE_DOMAINS: true,
    CACHE_USER_CONFIG: true
}
```

### Logging Configuration

```javascript
PERFORMANCE: {
    LOG_LEVEL: 'info', // debug, info, warn, error
    MAX_LOG_SIZE: '10MB',
    MAX_LOG_FILES: 5,
    LOG_ROTATION: true,
    COMPRESS_LOGS: true
}
```

### Memory Management

```javascript
PERFORMANCE: {
    MAX_MEMORY_USAGE: '500MB',
    GARBAGE_COLLECTION: true,
    MEMORY_CHECK_INTERVAL: 60000, // 1 minute
    AUTO_RESTART_ON_MEMORY_LIMIT: true
}
```

---

## 🔄 Configuration Validation

### Validate Your Configuration

```bash
# Check configuration syntax
node -c ~/.wildcard-bot/config.js

# Test configuration loading
auto-wildcard-bot --validate-config

# Test specific features
auto-wildcard-bot --test-cloudflare
auto-wildcard-bot --test-notifications
```

### Common Configuration Errors

| Error                              | Cause                       | Solution                        |
| ---------------------------------- | --------------------------- | ------------------------------- |
| **"BOT_TOKEN is required"**        | Missing or invalid token    | Check token format and validity |
| **"Invalid admin ID"**             | Non-numeric admin ID        | Ensure admin IDs are numbers    |
| **"Cloudflare connection failed"** | Invalid API credentials     | Verify email and API key        |
| **"Notification send failed"**     | Invalid notification config | Check API URLs and tokens       |

---

## 🔄 Configuration Updates

### Updating Configuration

```bash
# Edit configuration
nano ~/.wildcard-bot/config.js

# Restart bot to apply changes
pm2 restart auto-wildcard-bot

# Or if running directly
# Stop with Ctrl+C and restart
auto-wildcard-bot
```

### Hot Reload (Development)

```javascript
// Enable hot reload in development
if (process.env.NODE_ENV === 'development') {
    require('fs').watchFile('./config.js', () => {
        delete require.cache[require.resolve('./config.js')];
        console.log('🔄 Configuration reloaded');
    });
}
```

### Configuration Backup

```bash
# Backup current configuration
cp ~/.wildcard-bot/config.js ~/.wildcard-bot/config.js.backup

# Backup with timestamp
cp ~/.wildcard-bot/config.js ~/.wildcard-bot/config.js.$(date +%Y%m%d_%H%M%S)
```

---

## 📝 Configuration Examples

### Basic Setup

```javascript
module.exports = {
    BOT_TOKEN: 'your_bot_token',
    ADMIN_IDS: [123456789],
    CLOUDFLARE: {
        DEFAULT_EMAIL: '',
        DEFAULT_API_KEY: '',
    },
};
```

### Production Setup

```javascript
module.exports = {
    BOT_TOKEN: process.env.BOT_TOKEN,
    ADMIN_IDS: process.env.ADMIN_IDS.split(',').map(Number),
    SECURITY: {
        RATE_LIMITING: { enabled: true, maxRequestsPerMinute: 30 },
        COMMAND_COOLDOWN: { enabled: true, cooldownSeconds: 2 },
    },
    NOTIFICATIONS: {
        TELEGRAM_GROUP: { enabled: true, chatId: process.env.GROUP_ID },
    },
    PERFORMANCE: {
        LOG_LEVEL: 'warn',
        CACHE_TTL: 600,
        MAX_CONCURRENT_OPERATIONS: 10,
    },
};
```

---

**Next: [📖 Commands Reference](Commands-Reference) | [🚨 Troubleshooting](Troubleshooting)**
