# Google Calendar MCP Server

A **Model Context Protocol (MCP)** server built with Node.js that fetches events from a **public Google Calendar** using an API key.  

---

## 🚀 Features
- Exposes an MCP tool `getMyCalendarDataByDate` that retrieves events for a specific date.
- Fetches events from a **public Google Calendar** using the Google Calendar API.
- Validates input dates and returns results in a clean, structured format.
- Handles errors gracefully.

---

## 📦 Requirements
- Node.js >= 18
- A **public Google Calendar**
- A **Google API key** with **Calendar API** enabled

---

## ⚙️ Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/paularinzee/mcp-google-calendar.git
   cd mcp-google-calendar
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Create a `.env` file**
   ```env
   GOOGLE_PUBLIC_API_KEY=your_api_key_here
   CALENDAR_ID=your_calendar_id_here
   ```

   - Get your API key from **Google Cloud Console**.  
   - Make sure your Google Calendar is set to **public**.  
   - Find your **Calendar ID** under *Settings → Integrate calendar*.  

4. **Run the server**
   ```bash
   node index.js
   ```

---

## 🧪 Testing

### Direct API Test
Confirm your API key + calendar ID are valid:
```bash
curl "https://www.googleapis.com/calendar/v3/calendars/$CALENDAR_ID/events?key=$GOOGLE_PUBLIC_API_KEY"
```

### MCP Tool Test
If you’re using an MCP client (e.g., Claude Desktop), add this to your `claude_desktop_config.json`:

```json
{
    mcpServers: {
        "sumits-calendar-data": {
            command: "node",
            args: ["/full/path/to/project/server.js"],
            env: {
                GOOGLE_API_KEY: "...",
                CALENDAR_ID: "...",
            },
        },
    },
}
```

Then call the tool:
```json
"Do I have any meetings today?"
```

**Example Response:**
```
"Yes, you have a meeting with Dr. Chuck at 4:00 PM."
```

If no events exist:
```
"No, you do not have any meetings scheduled for tomorrow."
```

---

## 📂 Project Structure
```
google-calendar-mcp/
│── sever.js        # MCP server code
│── package.json    # Dependencies & scripts
│── .env            # API key & calendar ID (not committed)
│── .gitignore      # Ignore node_modules, .env, logs, etc.
│── README.md       # Project documentation
```

---

## 📖 Notes
- Works **only with public calendars** when using API keys.  
