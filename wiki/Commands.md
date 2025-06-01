# 📖 Commands Reference

Complete reference for all AutoFT Bot Wildcard commands.

## 🔰 Basic Commands

### `/start`
**Description**: Welcome message and setup guide  
**Usage**: `/start`  
**Access**: All users

Shows welcome message, bot features, and guides new users through initial setup.

### `/help`
**Description**: Show all available commands  
**Usage**: `/help`  
**Access**: All users

Displays list of available commands based on user permissions.

### `/ping`
**Description**: Check bot responsiveness  
**Usage**: `/ping`  
**Access**: All users

Simple health check to verify bot is responding.

---

## 🔧 Configuration Commands

### `/addcf`
**Description**: Add Cloudflare credentials  
**Usage**: `/addcf <api_key> <email>`  
**Access**: All users  
**Example**: `/addcf abcd1234efgh5678 user@example.com`

Registers your Cloudflare Global API Key and email for domain management.

### `/cfconfig`
**Description**: View current Cloudflare configuration  
**Usage**: `/cfconfig`  
**Access**: All users

Shows your stored Cloudflare credentials (email and masked API key).

### `/updatecf`
**Description**: Update Cloudflare credentials  
**Usage**: `/updatecf <api_key> <email>`  
**Access**: All users  
**Example**: `/updatecf new_key new_email@example.com`

Updates your existing Cloudflare credentials.

### `/deletecf`
**Description**: Remove Cloudflare configuration  
**Usage**: `/deletecf`  
**Access**: All users

Removes your stored Cloudflare credentials. Requires confirmation.

---

## 🌐 Domain Management Commands

### `/listdomain`
**Description**: Show available domains  
**Usage**: `/listdomain`  
**Access**: All users

Displays list of available domains for wildcard setup.

### `/setupwildcard`
**Description**: Setup wildcard domain  
**Usage**: `/setupwildcard <domain>`  
**Access**: All users  
**Example**: `/setupwildcard example.com`

Creates wildcard DNS record (*.domain.com) in Cloudflare.

### `/new`
**Description**: Create custom subdomain  
**Usage**: `/new <subdomain.domain.com>`  
**Access**: All users  
**Example**: `/new blog.example.com`

Creates a specific subdomain DNS record.

### `/mysub`
**Description**: View your subdomains  
**Usage**: `/mysub`  
**Access**: All users

Shows all domains and subdomains you've created.

### `/searchdomain`
**Description**: Search domains  
**Usage**: `/searchdomain <keyword>`  
**Access**: All users  
**Example**: `/searchdomain blog`

Search through available domains by keyword.

### `/delsub`
**Description**: Delete subdomain  
**Usage**: `/delsub <subdomain>`  
**Access**: All users  
**Example**: `/delsub blog.example.com`

Removes a subdomain DNS record from Cloudflare.

---

## 📊 Analytics Commands

### `/analytics`
**Description**: View domain statistics  
**Usage**: `/analytics <domain>`  
**Access**: All users  
**Example**: `/analytics example.com`

Shows domain usage statistics and DNS record information.

### `/clearcache`
**Description**: Clear Cloudflare cache  
**Usage**: `/clearcache <domain>`  
**Access**: All users  
**Example**: `/clearcache example.com`

Purges Cloudflare cache for the specified domain.

---

## 👑 Admin Commands

### `/stats`
**Description**: Bot usage statistics  
**Usage**: `/stats`  
**Access**: Admins only

Shows comprehensive bot statistics including user count, domains, uptime.

### `/broadcast`
**Description**: Send message to all users  
**Usage**: `/broadcast <message>`  
**Access**: Admins only  
**Example**: `/broadcast Server maintenance at 2 PM UTC`

Sends a message to all registered bot users.

### `/userinfo`
**Description**: View user details  
**Usage**: `/userinfo <user_id>`  
**Access**: Admins only  
**Example**: `/userinfo 123456789`

Shows detailed information about a specific user.

### `/testnotif`
**Description**: Test notification system  
**Usage**: `/testnotif`  
**Access**: Admins only

Sends a test notification to verify Telegram integration.

---

## 🚨 Important Notes

### Rate Limits
- Wildcard setup: 3 per user per hour
- Analytics requests: 10 per user per hour
- General commands: No strict limits

### Permissions
- **All users**: Configuration, domain management, analytics
- **Admins only**: Statistics, broadcasting, user management

### Error Handling
Commands will respond with error messages if:
- Missing required parameters
- Invalid Cloudflare credentials
- Domain not found
- Rate limits exceeded
- Insufficient permissions

---

## 📱 Quick Command Summary

| Category | Commands |
|----------|----------|
| **Basic** | `/start`, `/help`, `/ping` |
| **Config** | `/addcf`, `/cfconfig`, `/updatecf`, `/deletecf` |
| **Domains** | `/listdomain`, `/setupwildcard`, `/new`, `/mysub`, `/searchdomain`, `/delsub` |
| **Analytics** | `/analytics`, `/clearcache` |
| **Admin** | `/stats`, `/broadcast`, `/userinfo`, `/testnotif` |

---

**Need help with a specific command? Join our [updates channel](https://t.me/AutoFtFile) for the latest information!** 