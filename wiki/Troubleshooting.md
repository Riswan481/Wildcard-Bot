# 🆘 Troubleshooting Guide

Solutions for common issues with AutoFT Bot Wildcard.

## 🚨 Common Issues

### 🔴 Bot Not Responding

**Symptoms**: Bot doesn't respond to commands or shows as offline

**Solutions**:

1. **Check if bot is running**
   ```bash
   # Check running processes
   ps aux | grep node
   
   # For PM2 users
   pm2 status
   pm2 logs autoft-bot-wildcard
   ```

2. **Restart the bot**
   ```bash
   # Regular restart
   npm start
   
   # PM2 restart
   pm2 restart autoft-bot-wildcard
   ```

3. **Check bot token**
   ```bash
   # Verify token format
   echo $BOT_TOKEN
   # Should be: 1234567890:ABCdefGHIjklMNOpqrsTUVwxyz
   ```

4. **Verify network connectivity**
   ```bash
   # Test internet connection
   ping telegram.org
   
   # Test Telegram API
   curl -s "https://api.telegram.org/bot$BOT_TOKEN/getMe"
   ```

---

### 🔴 "Bot Token Invalid" Error

**Symptoms**: Error message about invalid bot token

**Solutions**:

1. **Verify token in .env file**
   ```env
   BOT_TOKEN=1234567890:ABCdefGHIjklMNOpqrsTUVwxyz
   ```

2. **Check token format**
   - Must contain numbers, colon, and alphanumeric characters
   - No spaces or extra characters
   - Copy directly from @BotFather

3. **Regenerate token**
   - Message @BotFather
   - Use `/token` command
   - Select your bot
   - Copy new token

4. **Check if bot was deleted**
   - Message @BotFather
   - Use `/mybots` to see your bots
   - If missing, create new bot

---

### 🔴 Admin Commands Not Working

**Symptoms**: Admin commands return "unauthorized" or don't work

**Solutions**:

1. **Verify admin ID**
   ```bash
   # Check current admin IDs
   echo $ADMIN_IDS
   
   # Get your Telegram ID
   # Message @userinfobot
   ```

2. **Check .env configuration**
   ```env
   ADMIN_IDS=123456789,987654321
   ```

3. **Restart bot after changes**
   ```bash
   pm2 restart autoft-bot-wildcard
   # or
   npm start
   ```

4. **Test admin access**
   ```bash
   # Try basic admin command
   /stats
   ```

---

### 🔴 Cloudflare API Errors

**Symptoms**: "Invalid Cloudflare credentials" or API errors

**Solutions**:

1. **Verify API key and email**
   ```bash
   # Test Cloudflare API
   curl -X GET "https://api.cloudflare.com/client/v4/user" \
        -H "X-Auth-Email: your@email.com" \
        -H "X-Auth-Key: your_api_key"
   ```

2. **Check API key permissions**
   - Use Global API Key (not scoped token)
   - Ensure account has domain access
   - Verify email matches Cloudflare account

3. **Verify domain in Cloudflare**
   - Domain must be added to Cloudflare
   - DNS must be active (not just registered)
   - Check zone status

4. **Update credentials**
   ```
   /updatecf new_api_key new_email@domain.com
   ```

---

### 🔴 Domain Setup Failures

**Symptoms**: Wildcard setup fails or DNS not created

**Solutions**:

1. **Check domain availability**
   ```
   /listdomain
   ```

2. **Verify domain in Cloudflare**
   - Domain must be in your Cloudflare account
   - DNS zone must be active
   - Check nameservers

3. **Check DNS propagation**
   ```bash
   # Check DNS records
   dig @8.8.8.8 *.yourdomain.com
   nslookup *.yourdomain.com
   ```

4. **Review Cloudflare logs**
   - Check Cloudflare dashboard
   - Look for API errors
   - Verify zone settings

---

### 🔴 Notifications Not Working

**Symptoms**: No notifications received in Telegram group

**Solutions**:

1. **Verify group ID**
   ```env
   TELEGRAM_GROUP_ID=-1001234567890
   ```

2. **Check bot group permissions**
   - Add bot to group
   - Give "Send Messages" permission
   - Make bot admin if needed

3. **Test notifications**
   ```
   /testnotif
   ```

4. **Check group ID format**
   - Must be negative number
   - Use @userinfobot in group to get correct ID

---

### 🔴 Installation Issues

**Symptoms**: NPM install fails or command not found

**Solutions**:

1. **Check Node.js version**
   ```bash
   node --version
   # Must be 16+ 
   ```

2. **Update NPM**
   ```bash
   npm install -g npm@latest
   ```

3. **Clear NPM cache**
   ```bash
   npm cache clean --force
   ```

4. **Reinstall globally**
   ```bash
   npm install -g autoft-bot-wildcard --force
   ```

5. **Check global installation**
   ```bash
   which autoft-bot-wildcard
   npm list -g autoft-bot-wildcard
   ```

6. **Alternative: Use npx**
   ```bash
   npx autoft-bot-wildcard
   ```

---

## 🔍 Debug Mode

### Enable Debug Logging

```bash
export LOG_LEVEL=debug
npm start
```

### Check Log Files

```bash
# PM2 logs
pm2 logs autoft-bot-wildcard

# Application logs
tail -f bot.log

# System logs
journalctl -u autoft-bot-wildcard
```

---

## 🧪 Testing Commands

### Test Bot Connectivity

```bash
# Test basic response
curl -s "https://api.telegram.org/bot$BOT_TOKEN/getMe"
```

### Test Cloudflare API

```bash
# Test API connection
curl -X GET "https://api.cloudflare.com/client/v4/zones" \
     -H "X-Auth-Email: your@email.com" \
     -H "X-Auth-Key: your_api_key"
```

### Test DNS Resolution

```bash
# Check DNS propagation
dig @8.8.8.8 yourdomain.com
nslookup yourdomain.com 1.1.1.1
```

---

## 📊 Performance Issues

### High Memory Usage

**Solutions**:
1. Restart bot regularly
2. Increase server memory
3. Check for memory leaks in logs

### Slow Response Times

**Solutions**:
1. Check internet connectivity
2. Monitor Cloudflare API limits
3. Review rate limiting settings

### Bot Timeouts

**Solutions**:
1. Increase timeout settings
2. Check server resources
3. Monitor API response times

---

## 🔧 Configuration Validation

### Validate Environment

```bash
# Check all environment variables
env | grep -E "(BOT_TOKEN|ADMIN_IDS|TELEGRAM_GROUP_ID)"

# Test configuration
autoft-bot-wildcard --validate-config
```

### Configuration Checklist

- [ ] ✅ BOT_TOKEN is set and valid
- [ ] ✅ ADMIN_IDS contains your Telegram ID
- [ ] ✅ TELEGRAM_GROUP_ID is correct (if used)
- [ ] ✅ Node.js version is 16+
- [ ] ✅ Cloudflare credentials are valid
- [ ] ✅ Domains are in Cloudflare account
- [ ] ✅ Bot has required permissions

---

## 🆘 Getting Help

### Before Asking for Help

1. **Check this troubleshooting guide**
2. **Enable debug logging**
3. **Collect error messages**
4. **Test basic connectivity**
5. **Review configuration**

### Where to Get Help

1. **📖 Documentation**: [Wiki](https://github.com/AutoFTbot/Wildcard-Bot/wiki)
2. **💬 Telegram Group**: [Support Group](https://t.me/AutoFtBot69)
3. **🐛 GitHub Issues**: [Report Bug](https://github.com/AutoFTbot/Wildcard-Bot/issues/new)
4. **📧 Email**: Contact through GitHub

### When Reporting Issues

Include:
- **Error messages** (full text)
- **Configuration** (without sensitive data)
- **Steps to reproduce**
- **System information** (OS, Node.js version)
- **Log files** (relevant sections)

---

## 🚀 Quick Fixes

### Bot Stops Working Suddenly

```bash
# Quick restart
pm2 restart autoft-bot-wildcard

# Check status
pm2 status

# View recent logs
pm2 logs autoft-bot-wildcard --lines 50
```

### Commands Return Errors

```bash
# Verify bot token
curl -s "https://api.telegram.org/bot$BOT_TOKEN/getMe"

# Restart bot
npm start
```

### Cannot Create Subdomains

```bash
# Check Cloudflare connection
/cfconfig

# Update credentials if needed
/updatecf your_api_key your_email@domain.com

# Test domain availability
/listdomain
```

---

**Still having issues? Join our [Telegram group](https://t.me/AutoFtBot69) for live support!** 