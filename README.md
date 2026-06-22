# 🏥 CareFirst AI Medical Receptionist (WhatsApp Pipeline)

An intelligent, fault-tolerant AI medical receptionist designed for WhatsApp. This project features a robust 3-tier LLM fallback architecture to ensure maximum uptime, routing patient inquiries seamlessly from WhatsApp through Twilio, into a FastAPI backend, and out to state-of-the-art language models.

---

## 🚀 Key Features

* **3-Tier LLM Fallback (Waterfall Architecture):** To eliminate API downtime, the system attempts to process messages using **OpenAI (GPT-4o-mini)**. If that fails, it instantly falls back to **Groq (Llama 3)**, and uses **Google Gemini (1.5 Flash)** as a final safety net.
* **Empathetic AI Persona:** Configured via system instructions as "Sarah," a helpful clinic receptionist who enforces conversational brevity, collects appointment details, and strictly avoids giving unauthorized medical advice.
* **Production-Ready Security:** Uses environment variables (`python-dotenv`) to decouple sensitive third-party API tokens from source code, preventing accidental leaks.
* **Asynchronous Webhook Routing:** Built on **FastAPI** to handle incoming message payloads via Twilio’s TwiML protocols with minimal latency.

---

## 🛠️ Tech Stack

* **Language:** Python 3.10+
* **Framework:** FastAPI & Uvicorn
* **Communication APIs:** Twilio (WhatsApp Sandbox)
* **AI Ecosystem:** OpenAI SDK, Groq SDK, Google Generative AI SDK
* **Tunneling Tool:** Ngrok

---

## ⚙️ Architecture Flow

1. **Patient** sends a WhatsApp message to the Twilio Sandbox number.
2. **Twilio** captures the event and forwards an HTTP POST webhook to a public **Ngrok** endpoint.
3. **Ngrok** tunnels the traffic securely to your local **FastAPI** server (`/webhook/whatsapp`).
4. **FastAPI** extracts the text message and runs it through the multi-model fallback script.
5. The selected **LLM** generates a response adhering to the clinic guidelines.
6. **FastAPI** wraps the text response in standard `MessagingResponse` TwiML XML.
7. **Twilio** relays the XML text payload back to the patient's phone.

---

## 💻 Local Installation & Setup

### 1. Clone the Repository
```bash
git clone [https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git)
cd medical-clinic-agent