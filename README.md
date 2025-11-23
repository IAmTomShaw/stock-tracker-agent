# Stock Tracker Agent

An AI-powered agent that tracks selected stock prices, analyzes market news when significant price changes occur, and keeps you informed via automated SMS messages. You can also interact with the agent by sending SMS commands to add or remove stocks from your tracker list.

![Stock Tracker Agent Diagram](docs/example.jpg)

---

## 🎯 Use Case

- **Monitor** stocks for significant price movements
- **Receive** concise market news summaries when price changes are detected
- **Get** instant SMS alerts for actionable events
- **Control** your tracker list by sending SMS commands (add/remove stocks)

---

## 🚀 Features

- Automated stock tracking and alerting
- Market news analysis using AI
- SMS notifications via Twilio
- Interactive SMS commands to manage your tracker list
- FastAPI web service for deployment
- Test and research modes for local development

---

## 📋 Prerequisites

- Python 3.11+
- Twilio account and phone number
- OpenAI API key
- [requirements.txt](requirements.txt) dependencies

---

## ⚙️ Environment Setup

Create a `.env` file in the project root with the following variables (see `.env.example`):

```env
OPENAI_API_KEY=your-openai-api-key
TWILIO_PHONE_NUMBER=your_twilio_phone_number
TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TARGET_PHONE_NUMBER=your_personal_phone_number
WEBHOOK_URL=your_twilio_webhook_url
```

> **Note:**  
> `WEBHOOK_URL` should be set to the exact public URL Twilio uses to POST to your `/receive-message` endpoint (e.g., your ngrok or production HTTPS URL).

---

## 🔧 Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd stock-tracker-agent
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Set up environment variables:
   ```bash
   cp .env.example .env
   # Edit .env with your credentials
   ```

---

## 🚀 Running the Project

### FastAPI Deployment

Run the agent as a web service using FastAPI and Uvicorn:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

- The `/receive-message` endpoint processes incoming SMS messages from Twilio.
- The agent tracks stocks and sends alerts automatically.

### Twilio Setup

1. Set up your Twilio phone number and credentials in `.env`.
2. Configure Twilio to POST incoming SMS to your server's `/receive-message` endpoint.
3. Only messages from your `TARGET_PHONE_NUMBER` will be processed.
4. Make sure `WEBHOOK_URL` in your `.env` matches the public URL Twilio uses to reach your endpoint.

### SMS Commands

You can instruct the agent to manage your stock tracker list via plain text SMS command such as:

- **Add a stock**: e.g., `Start tracking AAPL`
- **Remove a stock**: e.g., `Stop tracking MSFT`
- **List tracked stocks**: e.g., `What stocks am I tracking?`
- **Get stock price**: e.g., `What is the price of AAPL?`

- The agent will confirm actions and update your tracker list.

### Test Mode

You can run the agent in test mode for local testing:

```bash
python main.py -test
```

- This starts a chat terminal for manual interaction and runs the stock tracker every minute.

To trigger a research pipeline for a specific stock:

```bash
python main.py -test -research <SYMBOL>
```

Example:
```bash
python main.py -test -research AAPL
```

---

## 🐳 Docker Deployment

### Build and Run

1. Build the Docker image:
   ```bash
   docker build -t stock-tracker-agent .
   ```

2. Run with Docker:
   ```bash
   docker run -p 8000:8000 --env-file .env stock-tracker-agent
   ```

3. Or use Docker Compose (if you have a `docker-compose.yml`):
   ```bash
   docker-compose up --build
   ```

---

## 🛠️ Project Structure

```
stock-tracker-agent/
├── main.py                # FastAPI app and entry point
├── lib/                   # Core logic (agents, SMS, stock checker, tools, tracker)
├── resources/             # Data files (alert history, tracker list)
├── requirements.txt       # Python dependencies
├── .env                   # Environment variables
└── README.md              # This file
```

---

## 📝 How It Works

1. **Tracking**: The agent checks prices for stocks in your tracker list.
2. **Alerting**: If a stock moves >1% up or down from previous close, the agent:
   - Runs a research pipeline to analyze news and market events
   - Summarizes findings in under 160 characters
   - Sends an SMS alert to your phone
3. **Interaction**: You can add/remove stocks by sending SMS commands to the agent.

---

## 🐛 Troubleshooting

- Ensure your `.env` variables are correct and match your Twilio/OpenAI accounts.
- Check Twilio webhook configuration for correct endpoint and authentication.
- Make sure `WEBHOOK_URL` matches the public URL Twilio uses.
- Review logs for error details.

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📞 Support

For issues and questions:
- Create an issue in the repository
- Check existing documentation
- Review logs for error details

---

**Enjoy automated stock tracking and market insights delivered straight to