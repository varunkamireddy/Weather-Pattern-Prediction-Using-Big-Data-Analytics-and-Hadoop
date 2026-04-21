# 🔐 API Key Setup Guide

## Indian Weather API (indianapi.in)

PathSafe uses the **Indian Weather API** for real-time weather data with IMD (Indian Meteorological Department) integration. The app also has a **free fallback** (Open-Meteo) that works without any API key.

---

### Step 1: Get Your API Key

1. Go to [https://indianapi.in/weather-api](https://indianapi.in/weather-api)
2. Click **"Sign in to get API key"**
3. Create a free account (1000 free requests included)
4. Copy your API key from the dashboard

### Step 2: Add the API Key

1. In the project root, copy `.env.example` to `.env`:
   ```bash
   cp .env.example .env
   ```

2. Open `.env` and replace the placeholder:
   ```
   VITE_INDIAN_WEATHER_API_KEY=your_actual_api_key_here
   ```

### Step 3: Run the Project

```bash
# Install dependencies
npm install

# Start the development server
npm run dev
```

The app will start at `http://localhost:8080`

---

## How It Works

| API Key Status | Behavior |
|---|---|
| ✅ Valid key in `.env` | Uses Indian Weather API (IMD data for Indian cities) |
| ❌ No key / invalid key | Falls back to Open-Meteo (free, global coverage) |

Both modes provide full functionality — the Indian Weather API offers IMD-sourced data specifically optimized for Indian cities.

---

## API Endpoints Used

| Endpoint | Purpose |
|---|---|
| `GET /global/current?location=lat,lng` | Weather for any map click (lat/lng) |
| `GET /india/weather?city=CityName` | IMD data for Indian cities |

All requests include the header: `x-api-key: YOUR_API_KEY`

---

## Troubleshooting

- **Weather shows "No data"**: Check your API key is correct and you haven't exceeded the free tier limit
- **App works but no Indian API data**: The app automatically falls back to Open-Meteo — check browser console for API errors
- **CORS errors**: The Indian Weather API supports browser requests; ensure you're using `https://weather.indianapi.in`

---

## Security Note

⚠️ The `VITE_` prefix means this key is exposed in the browser bundle. This is acceptable for client-side weather apps, but:
- Do NOT commit `.env` to version control (it's in `.gitignore`)
- Use the free tier or a dedicated key for this project
- For production, consider proxying through a backend
