<div align="center">

# 📅 AI-Powered WhatsApp Appointment Assistant

**An n8n workflow that lets customers book, check, and manage appointments over WhatsApp using an AI agent connected to Google Calendar.**

![n8n](https://img.shields.io/badge/n8n-workflow-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)
![WhatsApp](https://img.shields.io/badge/WhatsApp-Business%20API-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)
![Groq](https://img.shields.io/badge/Groq-Llama%203.1-F55036?style=for-the-badge&logo=groq&logoColor=white)
![Google Calendar](https://img.shields.io/badge/Google%20Calendar-Scheduling-4285F4?style=for-the-badge&logo=googlecalendar&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

</div>

---

## 📋 Overview

This n8n workflow turns WhatsApp into a fully conversational appointment booking assistant. When a customer messages your WhatsApp Business number, an AI agent (powered by **Groq's Llama 3.1**) understands their request, checks your **Google Calendar** for availability, creates new appointments, and replies — all within the same WhatsApp chat.

## 🔄 How It Works

```
💬 WhatsApp Trigger  →  🤖 AI Agent (Groq)  →  📤 Send Message (WhatsApp)
                              │
                 ┌────────────┼────────────┐
                 ▼            ▼            ▼
             🗓️ Create   🕐 Date & Time  🔍 Search
            (new event)  (resolve "today",  (check existing
                          "tomorrow", etc.)   events — getAll)
```

| Node | Purpose |
|------|---------|
| **WhatsApp Trigger** | Fires whenever a new WhatsApp message arrives |
| **AI Agent** (Groq + Memory) | Understands the customer's request and decides which calendar tool to call |
| **Groq Chat Model** | The LLM (Llama 3.1 8B via Groq) powering the agent's reasoning |
| **Memory** | Keeps conversation context per WhatsApp sender, so the agent remembers earlier messages in the chat |
| **Create** (tool) | Creates a new event on Google Calendar once details are confirmed |
| **Date & Time** (tool) | Resolves relative dates/times ("tomorrow", "next Monday") to exact values |
| **Search** (tool) | Looks up existing events (`getAll`) to check availability before booking |
| **Send message** | Replies to the customer on WhatsApp with the agent's response |

## ✨ Features

- 💬 **Fully conversational** — customers book appointments by just chatting naturally
- 🧠 **Context-aware** — remembers the conversation per customer via session memory
- 📅 **Live calendar sync** — checks real availability before confirming a slot
- ⚡ **Fast responses** — powered by Groq for near-instant AI replies
- 🔁 **No manual back-and-forth** — the agent handles rescheduling logic on its own using calendar tools

## 🧰 Requirements

- An [n8n](https://n8n.io) instance (self-hosted or cloud)
- A **WhatsApp Business API** connection (trigger + send credentials)
- A **Groq API** credential
- A **Google Calendar API (OAuth2)** credential

## 🚀 Setup Instructions

1. **Import the workflow**
   In n8n, go to **Workflows → Import from File** and select [`AI-Powered_WhatsApp_Appointment_Assistant.json`](./AI-Powered_WhatsApp_Appointment_Assistant.json).

2. **Reconnect every credential**
   - `WhatsApp Trigger` and `Send message` → your WhatsApp Business API credentials
   - `Groq Chat Model` → your Groq API key
   - `Create` and `Search` (Google Calendar tools) → your Google Calendar OAuth2 account

3. **Set your calendar ID** in both the `Create` and `Search` nodes.

4. **Set your WhatsApp phone number ID** in the `Send message` node.

5. **Review the AI Agent's system prompt** — adjust tone, booking rules, and required fields (name, service type, etc.) to match your business.

6. **Test with a real WhatsApp message** before activating, to confirm the agent correctly checks availability and creates events.

7. **Activate the workflow** once verified.

## 📁 Repository Structure

```
├── AI-Powered_WhatsApp_Appointment_Assistant.json   # Reconstructed n8n workflow (needs configuration)
├── README.md                                         # You are here
└── LICENSE                                            # MIT License
```

## 🔒 Security Note

All credential IDs, phone number IDs, and calendar IDs in this file are placeholders. **Never commit real API keys, access tokens, or credential IDs to this repo.**

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](./LICENSE) file for details.

---

<div align="center">
Made with ❤️ using n8n + Groq + Google Calendar + WhatsApp
</div>
