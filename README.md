# 📱 WhatsApp Lead Notification Workflow
> **Instantly notify your phone via WhatsApp the moment a new lead submits a form — powered by n8n and Twilio.**

---

## 📌 Project Overview

Responding to leads fast is critical — studies show that responding within 5 minutes increases conversion rates dramatically. This workflow ensures that the moment a lead fills out a form, a WhatsApp message is fired directly to the business owner's phone with the lead's details — enabling instant, real-time response. Built using n8n's HTTP Request node and Twilio's WhatsApp Business API, this workflow demonstrates real client-facing automation that any business can deploy.

---

## ✨ Features

- 📋 **Custom Lead Form** — Built-in n8n form to capture Name, Email, and Message
- 💬 **Instant WhatsApp Notification** — Message delivered to phone in under 5 seconds
- 🔗 **Twilio WhatsApp API** — Industry-standard business messaging integration
- ⚙️ **HTTP Request Node** — Custom API call with Basic Auth and Form URL-encoded body
- ⚡ **Real-time Trigger** — Fires immediately on every form submission
- 🔁 **24/7 Active** — Runs continuously once published

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| **n8n** | Workflow automation engine |
| **n8n Form Trigger** | Lead capture form |
| **Twilio WhatsApp API** | Sending WhatsApp messages |
| **HTTP Request Node** | Custom REST API call to Twilio |
| **Basic Auth** | Secure Twilio API authentication |

---


### Workflow Canvas
> *Form Trigger → HTTP Request (all nodes green ✅)*

<img width="1909" height="909" alt="Screenshot 2026-04-25 101811" src="https://github.com/user-attachments/assets/761fe7f9-b5cd-4205-b345-eff9e2273e45" />


### WhatsApp Message Received
> *Real-time WhatsApp notification on phone with lead details*

<img width="1258" height="916" alt="Screenshot 2026-04-25 101931" src="https://github.com/user-attachments/assets/c04ecfce-3d1b-4afc-9f5e-1988c789efd5" />


---

## 🚀 Installation & Setup

### Prerequisites
- n8n account → [cloud.n8n.io](https://cloud.n8n.io)
- Twilio account → [twilio.com](https://twilio.com) (free trial available)
- WhatsApp on your phone

### Step 1 — Import the Workflow
```bash
# 1. Clone this repository
git clone https://github.com/asnahar1s/n8n-workflows.git

# 2. Open your n8n dashboard
# Go to cloud.n8n.io

# 3. Click "Add workflow" → "..." menu → "Import from file"
# Select: WhatsApp-Notification-Workflow.json
```

### Step 2 — Set Up Twilio
1. Sign up at [twilio.com](https://twilio.com)
2. Go to **Messaging → Try it out → Send a WhatsApp message**
3. Join the sandbox by sending this message from your WhatsApp:
```
join <your-sandbox-keyword>
```
to the Twilio sandbox number: `+1 415 523 8886`

4. Note down your credentials:
```
Account SID: ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
Auth Token:  your_auth_token (click eye icon to reveal)
From Number: whatsapp:+14155238886
To Number:   whatsapp:+your_phone_number
```

### Step 3 — Configure HTTP Request Node in n8n
Set these parameters in the HTTP Request node:

```
Method: POST
URL: https://api.twilio.com/2010-04-01/Accounts/YOUR_ACCOUNT_SID/Messages.json

Authentication: Generic Credential Type → Basic Auth
Username: YOUR_ACCOUNT_SID
Password: YOUR_AUTH_TOKEN

Send Body: ON
Specify Body: Using Fields Below
Body Content Type: Form Urlencoded

Parameters:
  From → whatsapp:+14155238886
  To   → whatsapp:+YOUR_PHONE_NUMBER
  Body → New lead from {{ $('On form submission').item.json.Name }}! Email: {{ $('On form submission').item.json.Email }}
```

### Step 4 — Activate
- Click **Publish** in n8n → workflow is live!

---

## 📋 Usage

1. Open your n8n form URL (or embed it on a website)
2. Lead fills in Name, Email, Message → submits
3. Within 5 seconds you receive a WhatsApp message:
```
New lead from [Name]!
```
4. Respond to the lead immediately while they're still warm!

---

## 📂 Project Structure

```
n8n-workflows/
│
├── WhatsApp-Notification-Workflow.json   # Import this into n8n
│
├── screenshots/
│   ├── whatsapp-canvas.png               # n8n workflow canvas
│   └── whatsapp-message.png              # WhatsApp notification received
│
└── WhatsApp-Notification-README.md       # This file
```
## Screenshots

---

## 📊 Results & Performance

| Metric | Value |
|--------|-------|
| Avg. execution time | ~2.5 seconds |
| Nodes in workflow | 2 |
| Message delivery time | Under 5 seconds |
| API used | Twilio WhatsApp REST API |
| Auth method | Basic Auth (Account SID + Auth Token) |
| Uptime | 24/7 when activated |

---

## 💡 Challenges & Learnings

- **Twilio sandbox setup** — Had to send a join code from WhatsApp before the sandbox could send messages; learned the difference between sandbox testing and production WhatsApp Business API
- **HTTP Request node config** — Parameters must go in the **Body** (Form URL-encoded), not Query Parameters — a critical distinction when calling REST APIs
- **Basic Auth in n8n** — Used "Generic Credential Type → Basic Auth" with Account SID as username and Auth Token as password
- **Expression syntax** — Used `{{ $('On form submission').item.json.Name }}` to pull live form data into the WhatsApp message body dynamically

---

## 🔮 Future Improvements

- [ ] Upgrade to **Twilio Production WhatsApp** with a verified business number
- [ ] Add **lead details** to message — company, phone number, and message content
- [ ] Create a **two-way WhatsApp flow** — business can reply directly from WhatsApp
- [ ] Combine with **Lead Gen Workflow** so leads are saved to Airtable AND WhatsApp fires simultaneously
- [ ] Add **time-based filtering** — only send WhatsApp during business hours

---

## 👩‍💻 Author

**Asna** — BSc Computer Science @ University of West London (RAK Campus, UAE)
Specializing in Cloud Security, AI Automation & API Integrations

- [GitHub](https://github.com/asnahar1s)
- [LinkedIn](https://www.linkedin.com/in/asna-haris-684058319/)
- asnaharis06@gmail.com
