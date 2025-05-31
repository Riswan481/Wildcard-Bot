# 🚨 Troubleshooting Guide

Common issues and their solutions for Wildcard Domain Bot.

## 🔍 Quick Diagnosis

| Symptom                 | Likely Cause                 | Quick Fix                          |
| ----------------------- | ---------------------------- | ---------------------------------- |
| **Bot not responding**  | Token invalid or bot offline | Check token, restart bot           |
| **"Command not found"** | Bot not installed globally   | `npm install -g auto-wildcard-bot` |
| **"Permission denied"** | Not admin or not registered  | Check user ID in config            |
| **"Handler undefined"** | Missing function exports     | Update to latest version           |
| **Cloudflare errors**   | Invalid API key or email     | Verify credentials                 |

---

## 🤖 Bot Installation Issues

### Problem: "Command not found: wildcard-bot"

**Symptoms:**

```bash
bash: wildcard-bot: command not found
'wildcard-bot' is not recognized as an internal or external command
```

**Causes:**

- Package not installed globally
- NPM global path not in system PATH
- Permission issues

**Solutions:**

#### Solution 1: Global Installation

```bash
# Uninstall if already installed
npm uninstall -g auto-wildcard-bot

# Reinstall globally
npm install -g auto-wildcard-bot

# Verify installation
npm list -g auto-wildcard-bot
```

#### Solution 2: Fix NPM Permissions (Linux/Mac)

```bash
# Fix ownership
sudo chown -R $(whoami) ~/.npm
sudo chown -R $(whoami) /usr/local/lib/node_modules

# Alternative: Use NPX
npx auto-wildcard-bot
```

#### Solution 3: Windows PATH Issues

```bash
# Add NPM global path to system PATH
npm config get prefix
# Add the returned path to your system PATH
```

### Problem: "Module not found" errors

**Symptoms:**

```bash
Error: Cannot find module 'telegraf'
Error: Cannot find module 'node-fetch'
```

**Solutions:**

```bash
# Clear npm cache
npm cache clean --force

# Remove node_modules and reinstall
rm -rf node_modules package-lock.json
npm install

# For global installation
npm install -g auto-wildcard-bot --force
```

---

## 🔑 Authentication & Token Issues

### Problem: "Bot token invalid"

**Symptoms:**

```bash
❌ Failed to start: 401: Bot Token is required
Error: 401 Unauthorized
```

**Solutions:**

#### Solution 1: Verify Token Format

```bash
# Token should look like this:
# 123456789:ABCdefGHIjklMNOpqrsTUVwxyz

# Check for:
- Colon (:) in the middle
- No extra spaces
- Correct length (45+ characters)
```

#### Solution 2: Generate New Token

1. Go to [@BotFather](https://t.me/BotFather)
2. Send `/mybots`
3. Select your bot
4. Choose "API Token"
5. Select "Revoke current token"
6. Copy the new token

#### Solution 3: Environment Variables

```bash
# Check .env file
cat .env

# Ensure format:
BOT_TOKEN=your_token_here
# No quotes, no extra spaces
```

### Problem: "Admin access denied"

**Symptoms:**

```bash
⚠️ Akses ditolak! Hanya admin yang dapat menggunakan fitur ini.
```

**Solutions:**

#### Check Admin IDs Configuration

```javascript
// In config/default.js
module.exports = {
    ADMIN_IDS: [123456789, 987654321], // Your Telegram user IDs
    // ...
};
```

#### Find Your Telegram ID

1. Message [@userinfobot](https://t.me/userinfobot)
2. It will reply with your user ID
3. Add this ID to `ADMIN_IDS` array
4. Restart the bot

---

## 🌐 Cloudflare Integration Issues

### Problem: "Kredensial tidak valid"

**Symptoms:**

```bash
❌ Kredensial tidak valid
❌ Global API Key tidak valid
❌ Gagal koneksi ke Cloudflare
```

**Solutions:**

#### Solution 1: Verify API Key

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Click Profile → **My Profile**
3. Go to **API Tokens** tab
4. Find **Global API Key** section
5. Click **View** and enter password
6. Copy the EXACT key (no spaces)

#### Solution 2: Check Email

- Use the EXACT email from your Cloudflare account
- Case-sensitive
- No typos

#### Solution 3: Test API Access

```bash
# Test with curl
curl -X GET "https://api.cloudflare.com/client/v4/accounts" \
     -H "X-Auth-Email: your@email.com" \
     -H "X-Auth-Key: your_global_api_key" \
     -H "Content-Type: application/json"
```

### Problem: "Domain tidak ditemukan"

**Symptoms:**

```bash
❌ Domain tidak terdaftar di Cloudflare
❌ DNS zones not accessible
```

**Solutions:**

#### Verify Domain Setup

1. **Check domain in Cloudflare:**

    - Login to Cloudflare Dashboard
    - Verify domain is listed
    - Ensure DNS is active (not just parking)

2. **Check nameservers:**

    ```bash
    # Check if nameservers point to Cloudflare
    nslookup -type=ns yourdomain.com

    # Should show something like:
    # yourdomain.com nameserver = alex.ns.cloudflare.com
    # yourdomain.com nameserver = betty.ns.cloudflare.com
    ```

3. **Wait for propagation:**
    - DNS changes can take 24-48 hours
    - Check status in Cloudflare dashboard

---

## 📱 Bot Runtime Issues

### Problem: Bot stops responding randomly

**Symptoms:**

- Bot was working, now silent
- No error messages
- Process still running

**Diagnosis:**

```bash
# Check if bot process is running
ps aux | grep node
pm2 status

# Check logs
pm2 logs wildcard-bot
tail -f /path/to/bot/logs/error.log
```

**Solutions:**

#### Solution 1: Memory Issues

```bash
# Check memory usage
free -h
pm2 monit

# Restart bot
pm2 restart wildcard-bot

# Increase memory limit
pm2 start index.js --max-memory-restart 500M
```

#### Solution 2: Rate Limiting

```bash
# Telegram rate limiting
# Wait 10-30 minutes before retrying
# Reduce broadcast frequency
```

#### Solution 3: Network Issues

```bash
# Test internet connection
ping telegram.org
ping api.cloudflare.com

# Check DNS resolution
nslookup api.telegram.org
```

### Problem: "Handler is undefined" errors

**Symptoms:**

```bash
TypeError: Cannot read property 'handler' of undefined
Handler is undefined for command: /start
```

**Solutions:**

#### Update to Latest Version

```bash
# Check current version
npm list -g auto-wildcard-bot

# Update to latest
npm update -g auto-wildcard-bot

# Or reinstall
npm uninstall -g auto-wildcard-bot
npm install -g auto-wildcard-bot@latest
```

#### Clear Cache and Reinstall

```bash
# Clear all caches
npm cache clean --force
rm -rf ~/.npm
rm -rf node_modules

# Reinstall
npm install
```

---

## 📊 Database & Data Issues

### Problem: "Cannot read config file"

**Symptoms:**

```bash
Error: ENOENT: no such file or directory, open 'config.json'
Failed to read user configuration
```

**Solutions:**

#### Create Missing Data Files

```bash
# Navigate to bot directory
cd wildcard-bot

# Create data directory if missing
mkdir -p data

# Create empty config files
echo '{}' > data/config.json
echo '{}' > data/custom_subdomains.json
echo '{}' > data/admin_usage.json
```

#### Fix File Permissions

```bash
# Fix permissions (Linux/Mac)
chmod 644 data/*.json
chmod 755 data/

# For Windows, ensure user has write access
```

### Problem: "Data corruption" or invalid JSON

**Symptoms:**

```bash
SyntaxError: Unexpected token in JSON
Invalid JSON in config file
```

**Solutions:**

#### Restore from Backup

```bash
# Check for backup files
ls -la backups/

# Restore latest backup
cp backups/config_backup_latest.json data/config.json
```

#### Reset Data Files

```bash
# Backup corrupted files first
cp data/config.json data/config.json.corrupted

# Reset to empty state
echo '{}' > data/config.json
echo '{}' > data/custom_subdomains.json

# Users will need to re-register
```

---

## 🔧 Performance Issues

### Problem: Slow response times

**Symptoms:**

- Commands take long to respond
- Timeouts on Cloudflare operations
- Users complaining about delays

**Diagnosis:**

```bash
# Check system resources
top
htop
df -h

# Check network latency
ping api.cloudflare.com
curl -w "@curl-format.txt" -o /dev/null -s "https://api.cloudflare.com/client/v4/accounts"
```

**Solutions:**

#### Optimize Bot Configuration

```javascript
// In config/default.js
module.exports = {
    // Reduce polling interval
    POLLING_TIMEOUT: 10,

    // Limit concurrent operations
    MAX_CONCURRENT_REQUESTS: 5,

    // Cache configuration
    CACHE_TTL: 300, // 5 minutes
};
```

#### Database Optimization

```bash
# Clean up old data
node scripts/cleanup.js

# Optimize JSON files
node scripts/optimize-data.js
```

---

## 📱 Notification Issues

### Problem: Telegram notifications not working

**Symptoms:**

```bash
❌ Telegram Group: Gagal terkirim
Failed to send notification to group
```

**Solutions:**

#### Verify Group Setup

1. **Add bot to group:**

    - Add your bot to the notification group
    - Give admin privileges (optional but recommended)

2. **Get correct Group ID:**

    ```bash
    # Add @userinfobot to your group
    # It will show the group ID (negative number)
    # Example: -1001234567890
    ```

3. **Update configuration:**
    ```bash
    # In .env file
    TELEGRAM_GROUP_ID=-1001234567890
    ```

### Problem: WhatsApp notifications failing

**Symptoms:**

```bash
❌ WhatsApp: Gagal terkirim
WhatsApp API connection failed
```

**Solutions:**

#### Check API Configuration

```javascript
// In config/default.js
NOTIFICATIONS: {
    WHATSAPP: {
        enabled: true, // Must be true
        apiUrl: 'https://your-api.com', // Correct URL
        token: 'your_token_here' // Valid token
    }
}
```

#### Test API Connection

```bash
# Test with curl
curl -X POST "https://your-whatsapp-api.com/send" \
     -H "Authorization: Bearer your_token" \
     -H "Content-Type: application/json" \
     -d '{"to": "1234567890", "message": "test"}'
```

---

## 🛠️ Development & Debug Issues

### Problem: Debug mode not working

**Enable Debug Logging:**

```bash
# Set environment variable
export DEBUG=wildcard:*

# Or in .env file
DEBUG=wildcard:*
NODE_ENV=development

# Start bot with debug
npm run dev
```

### Problem: Development setup issues

**Solutions:**

```bash
# Clone fresh repository
git clone https://github.com/AutoFTbot/Wildcard-Bot.git
cd Wildcard-Bot

# Install dependencies
npm install

# Copy environment template
cp .env.example .env

# Edit configuration
nano .env

# Run in development mode
npm run dev
```

---

## 📞 Getting Additional Help

### When to Contact Support

Contact support if you:

- ✅ Tried all solutions above
- ✅ Checked logs for specific errors
- ✅ Updated to latest version
- ✅ Have specific error messages to share

### How to Report Issues

**Include this information:**

1. **Environment:**

    - OS version
    - Node.js version (`node --version`)
    - Bot version (`npm list auto-wildcard-bot`)

2. **Error details:**

    ```bash
    # Copy exact error messages
    # Include full stack traces
    # Share relevant logs
    ```

3. **Steps to reproduce:**
    - What command was used
    - Expected vs actual behavior
    - When the issue started

### Support Channels

1. **📚 GitHub Issues** - [Report bugs](https://github.com/AutoFTbot/Wildcard-Bot/issues)
2. **💬 Telegram Support** - [@AutoFtBot69](https://t.me/AutoFtBot69)
3. **📖 Wiki** - Check other wiki pages
4. **🔍 Search** - Search existing issues first

---

## 🔧 Emergency Recovery

### Complete Bot Reset

If nothing else works:

```bash
# 1. Stop bot
pm2 stop wildcard-bot

# 2. Backup important data
cp -r data/ data_backup/

# 3. Uninstall completely
npm uninstall -g auto-wildcard-bot
rm -rf ~/.npm/auto-wildcard-bot
rm -rf /usr/local/lib/node_modules/auto-wildcard-bot

# 4. Clean install
npm cache clean --force
npm install -g auto-wildcard-bot@latest

# 5. Restore data
cp -r data_backup/ data/

# 6. Restart
wildcard-bot
```

### Data Recovery

```bash
# Find backup files
find . -name "*backup*" -type f
find . -name "*.json.bak" -type f

# Restore from Git (if using version control)
git checkout HEAD -- data/
git log --oneline data/

# Manual recovery
# Check logs for recent successful states
tail -100 logs/bot.log | grep "SUCCESS"
```

---

**Need immediate help? Contact [@AutoFtBot69](https://t.me/AutoFtBot69)**

**Next: [🛡️ Security Guide](Security-Guide)**
