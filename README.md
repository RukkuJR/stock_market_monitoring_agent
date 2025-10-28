# 📈 Stock Market Tracker with n8n Automation

An automated stock portfolio monitoring system that tracks your investments, calculates performance metrics, and sends daily updates via Telegram. Built with n8n, Notion, and Alpha Vantage API.

## 🎯 Overview

This automation workflow monitors stock portfolios stored in a Notion database, fetches real-time market data, calculates growth metrics, and delivers personalized performance reports through Telegram.

## ✨ Features

- **Automated Daily Updates**: Scheduled monitoring of your stock portfolio
- **Real-time Data**: Fetches current forex rates and stock prices via Alpha Vantage
- **Performance Analytics**: Calculates investment growth and percentage returns
- **Telegram Notifications**: Receives formatted reports directly in Telegram
- **Multi-Asset Support**: Tracks both stocks and commodities (Gold)
- **Notion Integration**: Manages portfolio data in a structured database


<img width="1430" height="642" alt="stock1" src="https://github.com/user-attachments/assets/be096a8c-8595-40be-aa4e-f46681e4a7a6" />

## 🏗️ Architecture Flow

```
Schedule Trigger (Daily)
    ↓
Notion (Get Database)
    ↓
Loop Over Items (For Each Stock)
    ↓
    ├→ Wait (Rate Limiting)
    ↓
    ├→ HTTP Request (Alpha Vantage API)
    ↓
    ├→ Notion (Update Database)
    ↓
Google Gemini Chat Model (Generate Report)
    ↓
Send Telegram Message
```

## 📊 Workflow Components

1. **Schedule Trigger**: Initiates the workflow at configured intervals
2. **Notion Integration**: Retrieves stock data from your database
3. **Loop Processing**: Iterates through each stock in your portfolio
4. **Wait Node**: Implements rate limiting between API calls
5. **HTTP Request**: Fetches market data from Alpha Vantage
6. **AI Agent**: Uses Google Gemini to generate insights and summaries
7. **Telegram Bot**: Delivers formatted notifications

## 🗄️ Notion Database Structure

<img width="1470" height="543" alt="stock3" src="https://github.com/user-attachments/assets/d3a4a04d-6344-4abf-99ca-63a58c65490a" />

Your Notion database should include the following properties:

| Property | Type | Description |
|----------|------|-------------|
| Ticker | Text | Stock ticker symbol (e.g., NVDA, TSM) |
| Name | Text | Full company/asset name |
| Type | Select | Asset type (STOCK, GOLD, etc.) |
| FOREX RATE | Number | Current exchange rate |
| Investment Amount | Number | Total invested (in MYR) |
| Growth | Formula | Percentage growth calculation |
| Growth Value | Number | Absolute profit/loss |

## 📋 Prerequisites

- n8n instance (self-hosted or cloud)
- Notion account with API access
- Alpha Vantage API key (free tier available)
- Telegram bot token
- Google Gemini API access

## ⚙️ Setup Instructions

### 1. Clone the Workflow

Import the n8n workflow JSON file into your n8n instance.

### 2. Configure API Credentials

- **Notion**: Add your integration token and database ID
- **Alpha Vantage**: Insert your API key
- **Telegram**: Configure your bot token and chat ID
- **Google Gemini**: Add your API credentials

### 3. Set Up Notion Database

Create a Notion database with the structure outlined above and populate it with your stocks.

### 4. Adjust Schedule

Modify the Schedule Trigger node to run at your preferred time (default: daily at 11:25 AM).

### 5. Test the Workflow

Run a manual execution to verify all connections work correctly.

## 📱 Sample Output

```
Hi Socku: This is how you stocks have performed so far

Name: NVDA
Investment Amount: RM 548.94182
Growth: 47.208277919%
Growth Value: RM 259.14598

Name: GOLD
Investment Amount: RM 1164.72
Growth: 8.91304347834%
Growth Value: RM 103.812
```

## 🔧 Customization Options

- **Update Frequency**: Adjust the schedule trigger interval
- **Additional Metrics**: Modify formulas in Notion for custom calculations
- **Notification Format**: Customize the Gemini prompt for different report styles
- **Asset Types**: Extend support for crypto, forex, or other instruments

## 🚀 Use Cases

- **Personal Portfolio Tracking**: Monitor investment performance daily
- **Family Finance Management**: Keep stakeholders informed
- **Learning Tool**: Understand market movements and investment returns
- **Multi-Currency Portfolios**: Track international investments with forex rates

## 🛡️ Rate Limiting

The workflow includes a Wait node to respect Alpha Vantage's API rate limits (typically 5 calls/minute for free tier).

## 🐛 Troubleshooting

**Issue**: API calls failing
- Verify API keys are correct and active
- Check Alpha Vantage rate limits

**Issue**: Telegram not receiving messages
- Confirm bot token and chat ID
- Ensure bot has permission to send messages

**Issue**: Notion data not updating
- Verify database ID and integration permissions
- Check property names match exactly


output
<img width="480" height="592" alt="stock2" src="https://github.com/user-attachments/assets/11ebc39b-54e1-4bf6-b5fb-e16fb82fea1a" />

