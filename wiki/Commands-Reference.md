# 📋 Commands Reference

Complete reference for all Wildcard Domain Bot commands.

## 🎯 Command Categories

| Category                                          | Description               | User Level       |
| ------------------------------------------------- | ------------------------- | ---------------- |
| **[🔰 Basic Commands](#-basic-commands)**         | Essential bot operations  | All Users        |
| **[⚙️ Configuration](#️-configuration-commands)** | Cloudflare setup          | All Users        |
| **[🌐 Domain Management](#-domain-management)**   | Wildcard & DNS operations | Registered Users |
| **[📊 Analytics & Info](#-analytics--info)**      | Statistics and monitoring | Registered Users |
| **[👑 Admin Commands](#-admin-commands)**         | Administrative functions  | Admins Only      |

---

## 🔰 Basic Commands

### `/start`

**Welcome message and bot introduction**

```
/start
```

**What it does:**

- Shows welcome message with bot capabilities
- Displays registration status
- Lists available commands based on user level
- Provides setup instructions for new users

**Example Response:**

```
🎉 SELAMAT DATANG!

🚀 Bot untuk mengelola wildcard domain dengan mudah!

📝 MULAI DENGAN REGISTRASI:
/addcf <global_api_key> <email>

🔑 Cara mendapat Global API Key:
1️⃣ Buka Cloudflare Dashboard
2️⃣ Klik profil → My Profile → API Tokens
3️⃣ Di Global API Key, klik "View" dan copy
```

### `/help`

**Comprehensive help and command guide**

```
/help
```

**What it does:**

- Shows detailed command explanations
- Provides usage tips and examples
- Displays different commands based on registration status
- Includes troubleshooting hints

---

## ⚙️ Configuration Commands

### `/addcf`

**Register with Cloudflare API credentials**

```
/addcf <global_api_key> <email>
```

**Parameters:**

- `global_api_key` - Your Cloudflare Global API Key
- `email` - Email associated with your Cloudflare account

**Example:**

```
/addcf c2bd7d84c1234567890abcdef77f5a8 user@example.com
```

**What it does:**

- Validates your Cloudflare credentials
- Stores encrypted API key and email
- Enables access to domain management features
- Sets up user profile in the system

**Error Messages:**

- `❌ Global API Key tidak valid` - Invalid API key format
- `❌ Format email tidak valid` - Invalid email format
- `❌ Kredensial tidak valid` - API key/email combination rejected by Cloudflare

### `/cfconfig`

**View your current Cloudflare configuration**

```
/cfconfig
```

**What it does:**

- Shows your registered email (masked for security)
- Displays masked API key (first 8 and last 4 characters)
- Shows registration date and last update
- Lists available commands for registered users

**Example Response:**

```
👤 KONFIGURASI AKTIF

📧 Email: user@example.com
🔑 API Key: c2bd7d84***f5a8
📅 Terdaftar: 31/05/2025, 10:30:25

⚡ Commands: /updatecf | /setupwildcard | /listdomain | /new | /mysub
```

### `/updatecf`

**Update your Cloudflare credentials**

```
/updatecf <new_global_api_key> <new_email>
```

**Parameters:**

- `new_global_api_key` - Your new Cloudflare Global API Key
- `new_email` - New email for your Cloudflare account

**Example:**

```
/updatecf d3ce8e95d2345678901bcdefg88g6b9 newemail@example.com
```

**What it does:**

- Validates new credentials with Cloudflare
- Updates your stored configuration
- Maintains your existing domain data
- Updates last modified timestamp

### `/deletecf`

**Remove your Cloudflare configuration**

```
/deletecf
/deletecf CONFIRM DELETE
```

**What it does:**

- Shows confirmation prompt (first usage)
- Permanently removes your configuration (with confirmation)
- Deletes all associated domain data
- Requires re-registration to use bot again

**Security:** Requires explicit confirmation to prevent accidental deletion.

---

## 🌐 Domain Management

### `/setupwildcard`

**Setup wildcard DNS for a domain**

```
/setupwildcard <domain>
```

**Parameters:**

- `domain` - The root domain to setup wildcard DNS for

**Example:**

```
/setupwildcard example.com
```

**What it does:**

- Creates wildcard DNS record (`*.example.com`)
- Configures Cloudflare Worker for subdomain routing
- Sets up SSL certificates automatically
- Enables dynamic subdomain creation
- Sends notifications to admin channels

**Requirements:**

- Domain must be registered in your Cloudflare account
- Domain must have active DNS zone
- Proper API permissions required

**Process:**

```
🔧 SETTING UP WILDCARD
█████████░░░░░░░░░░ 45%
⚡ Initializing connection...
📡 Connecting to Cloudflare API

🔐 AUTHENTICATING
███████████░░░░░░░░░ 65%
✅ API credentials verified
🌐 Establishing secure connection

🔍 VALIDATING DOMAIN
████████████████░░░░ 85%
✅ Domain found in Cloudflare
✅ DNS zones accessible

✨ WILDCARD SETUP COMPLETE! ✨
```

### `/listdomain`

**View all available domains**

```
/listdomain
```

**What it does:**

- Shows all default domains provided by admin
- Lists your custom domains
- Displays domain statistics
- Provides quick action commands

**Example Response:**

```
🌐 DAFTAR DOMAIN TERSEDIA

📊 Statistik:
• Total domain: 15
• Default domain: 10
• Custom domain: 5

🏠 Default Domain Wildcard:
1. api.example.com
2. cdn.example.com
3. app.example.com

🎯 Custom Domain Wildcard:
1. mysite.com (Milik Anda)
2. myblog.org (Milik Anda)

⚡ Quick Actions:
• /new <subdomain.domain> - Tambah custom domain
• /mysub - Lihat subdomain Anda
• /setupwildcard <domain> - Setup wildcard
```

### `/new`

**Add a new custom subdomain**

```
/new <subdomain.domain>
```

**Parameters:**

- `subdomain.domain` - The full subdomain you want to add

**Example:**

```
/new api.mysite.com
```

**What it does:**

- Validates subdomain format
- Checks against blacklisted words
- Verifies you haven't exceeded limits
- Adds subdomain to your custom list
- Makes it available for wildcard setup

**Validation Rules:**

- Maximum 63 characters
- Valid DNS naming conventions
- No prohibited words or patterns
- Unique across all users
- Respects user limits (default: 10 per user)

### `/mysub`

**View your custom subdomains**

```
/mysub
```

**What it does:**

- Lists all your custom subdomains
- Shows usage statistics
- Displays remaining quota
- Provides management commands

**Example Response:**

```
👤 SUBDOMAIN ANDA

📊 Total: 5/10

🎯 Daftar subdomain:
1. api.mysite.com
2. cdn.mysite.com
3. blog.mysite.com
4. shop.mysite.com
5. admin.mysite.com

⚡ Quick Actions:
• /new <subdomain.domain> - Tambah subdomain
• /delsub <subdomain.domain> - Hapus subdomain
• /searchdomain <keyword> - Cari domain
```

### `/delsub`

**Delete one of your custom subdomains**

```
/delsub <subdomain.domain>
```

**Parameters:**

- `subdomain.domain` - The subdomain you want to remove

**Example:**

```
/delsub old.mysite.com
```

**What it does:**

- Verifies subdomain belongs to you
- Removes subdomain from your list
- Updates your usage quota
- Cannot be undone

**Security:** Only allows deletion of subdomains you own.

### `/searchdomain`

**Search for domains by keyword**

```
/searchdomain <keyword>
```

**Parameters:**

- `keyword` - Search term to find matching domains

**Example:**

```
/searchdomain api
```

**What it does:**

- Searches through all available domains
- Finds partial matches in domain names
- Separates results by default vs custom domains
- Shows total match count

**Example Response:**

```
════❖ Hasil Pencarian ❖════

🔍 Kata kunci: "api"
📊 Ditemukan: 8 domain

📌 Default Domain (3):
1. api.example.com
2. apigateway.site.com
3. backend-api.domain.org

🔰 Custom Domain (5):
1. api.mysite.com
2. api-v2.blog.com
3. myapi.services.net
```

---

## 📊 Analytics & Info

### `/analytics`

**View domain analytics and statistics**

```
/analytics <domain>
```

**Parameters:**

- `domain` - Domain to analyze (optional)

**What it does:**

- Shows setup history for domain
- Displays usage statistics
- Performance metrics
- Recent activity logs

_Note: Currently maps to search functionality, enhanced analytics coming soon_

### `/clearcache`

**Clear Cloudflare cache for domain**

```
/clearcache <domain>
```

**Parameters:**

- `domain` - Domain to clear cache for

**What it does:**

- Sends cache purge request to Cloudflare
- Clears all cached content for domain
- Provides confirmation of cache clear

_Note: Simple implementation, returns success message_

---

## 👑 Admin Commands

_These commands are only available to users listed in `ADMIN_IDS` configuration_

### `/stats`

**View bot usage statistics**

```
/stats
```

**What it does:**

- Shows total registered users
- Displays domain setup statistics
- Active user metrics
- System health information

**Example Response:**

```
📊 BOT STATISTICS

👥 Users: 247 registered
🌐 Domains: 1,847 total setups
🎯 Active: 89 users this week
⚡ Uptime: 15 days, 7 hours

📈 Recent Activity:
• 23 new registrations today
• 67 wildcard setups this week
• 156 subdomains created
```

### `/broadcast`

**Send message to all registered users**

```
/broadcast <message>
```

**Parameters:**

- `message` - The message to send to all users

**Example:**

```
/broadcast Server maintenance scheduled for tomorrow 2 AM UTC
```

**What it does:**

- Sends message to all registered users
- Shows delivery statistics
- Handles failed deliveries gracefully
- Rate limits to avoid Telegram restrictions

**Example Response:**

```
📢 BROADCAST BERHASIL DIKIRIM

📊 Statistik pengiriman:
• Total pengguna: 247
• Berhasil dikirim: 245
• Gagal: 2
• Waktu kirim: 31/05/2025, 15:30:25

💬 Pesan yang dikirim:
Server maintenance scheduled for tomorrow 2 AM UTC
```

### `/testnotif`

**Test notification systems**

```
/testnotif
```

**What it does:**

- Tests Telegram group notifications
- Tests WhatsApp API integration
- Validates configuration settings
- Reports success/failure status

**Example Response:**

```
🧪 TEST NOTIFICATION RESULTS

✅ Telegram Group: Berhasil terkirim
❌ WhatsApp: Gagal terkirim

📊 Status: Sebagian notifikasi berfungsi ⚠️

💡 Tips:
• Pastikan bot sudah ditambahkan ke grup Telegram
• Cek konfigurasi WhatsApp API di config/default.js
• Verifikasi TELEGRAM_GROUP_ID di environment variables
```

### `/userinfo`

**Get detailed information about a user**

```
/userinfo <user_id>
```

**Parameters:**

- `user_id` - Telegram user ID to lookup

**Example:**

```
/userinfo 123456789
```

**What it does:**

- Shows user registration details
- Lists user's domains and subdomains
- Usage statistics and activity history
- Account status and permissions

---

## 🔧 Command Usage Tips

### **Command Format**

- All commands start with `/`
- Parameters separated by spaces
- No quotes needed around single-word parameters
- Use exact spacing as shown in examples

### **Parameter Types**

- `<required>` - Must be provided
- `[optional]` - Can be omitted
- `<choice1|choice2>` - Pick one option

### **Error Handling**

- Invalid commands show usage examples
- Permission errors explain access requirements
- Network errors suggest retry timing
- Validation errors provide specific guidance

### **Rate Limits**

- Commands are rate-limited per user
- Admin commands have higher limits
- Broadcast commands have special rate limiting
- Cloudflare API calls are throttled appropriately

### **Security Features**

- API keys are stored encrypted
- Sensitive data is masked in responses
- Admin commands verify user permissions
- Input validation prevents injection attacks

---

## 📞 Command Support

**Need help with a specific command?**

1. **Use `/help`** - Built-in help system
2. **Check examples** - Each command shows usage examples
3. **Read error messages** - They contain helpful guidance
4. **Ask in support** - [@AutoFtBot69](https://t.me/AutoFtBot69)

**Command not working?**

1. **Check syntax** - Ensure exact format
2. **Verify permissions** - Some commands need registration/admin
3. **Check limits** - You might have reached quotas
4. **Wait and retry** - Rate limiting might be active

---

**Next: [🔧 Advanced Usage](Advanced-Usage)**
