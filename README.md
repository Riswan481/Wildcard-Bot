 🌐 AutoFT Bot Wildcard Instalasi
```bash
rm -rf autoft-bot-wildcard && \
npm install -g autoft-bot-wildcard && \
autoft-bot-wildcard && \
cd autoft-bot-wildcard && \
npm install -g pm2 && \
pm2 start index.js --name "autoft-bot-wildcard" && \
pm2 save && \
pm2 startup -y && \
pm2 status
```
