# 📧 TempMail Pro - Disposable Email Service

A modern, single-page temporary email application built with vanilla HTML, CSS, and JavaScript. This project uses the **[Mail.tm](https://mail.tm)** API to provide free disposable email addresses.

![TempMail Pro Screenshot](https://img.shields.io/badge/Status-Live-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)
![Mail.tm API](https://img.shields.io/badge/Powered%20by-Mail.tm%20API-purple)

---

## 🌐 Live Demo

**👉 [Access TempMail Pro Here](https://git-26-09-2025.s3.us-east-1.amazonaws.com/index.html)**

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 📬 **Instant Email** | Generate random temporary email addresses instantly |
| ✏️ **Custom Email** | Create your own custom username with available domains |
| 📥 **Real-time Inbox** | View incoming emails with auto-refresh (every 10 seconds) |
| 📖 **Read Emails** | Full email viewing with HTML content support |
| 📎 **Attachments** | Download email attachments |
| 🗑️ **Delete Emails** | Delete individual or all emails |
| 📋 **Copy to Clipboard** | One-click copy email address |
| 🌓 **Dark/Light Theme** | Toggle between dark and light modes |
| 🔍 **Search & Filter** | Search emails and filter by read/unread status |
| 💾 **Session Persistence** | Email session saved in browser localStorage |
| 📊 **Statistics** | View total emails, unread count, and session time |
| 📱 **Responsive Design** | Works on desktop, tablet, and mobile |

---

## 🏗️ Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│                 │     │                 │     │                 │
│   User Browser  │────▶│   AWS S3        │────▶│   Mail.tm API   │
│                 │     │   (Static Host) │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                              │
                              │ index.html
                              │ (Single Page App)
                              ▼
                        ┌─────────────────┐
                        │  GitHub Actions │
                        │  (CI/CD)        │
                        └─────────────────┘
```

---

## 🚀 Deployment

### Automated Deployment with GitHub Actions

This project includes a GitHub Actions workflow that automatically syncs the `index.html` to an AWS S3 bucket on every push.

#### Workflow File: `.github/workflows/mail.yml`

```yaml
name: Deploy To S3

on:
  push:
    branches:
    - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: checkout
      uses: actions/checkout@v1

    - name: AWS CredConfig
      uses: aws-actions/Configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{secrets.AWS_SECRET_ACCESS_KEY}}
        aws-region: us-east-1
        
    - name: Deploy Static Test Page to S3
      run: aws s3 sync . s3://git-26-09-2025 --delete
```

---

## 📡 API Reference

This project uses the **Mail.tm API**. Key endpoints:

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/domains` | GET | Get available email domains |
| `/accounts` | POST | Create new email account |
| `/token` | POST | Get authentication token |
| `/messages` | GET | Get all messages |
| `/messages/{id}` | GET | Get specific message |
| `/messages/{id}` | DELETE | Delete message |

📚 **Full API Documentation:** [https://docs.mail.tm](https://docs.mail.tm)

---

## 🛡️ Security Considerations

- ⚠️ **Temporary emails only** - Don't use for sensitive accounts
- ⚠️ **Public emails** - Anyone with the address can potentially access
- ✅ **No server-side storage** - All data stored in browser only
- ✅ **HTTPS recommended** - Your S3 bucket uses HTTPS

---


## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 Your Name

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---
