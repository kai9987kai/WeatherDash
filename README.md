# Weather API Pro Dashboard

A modern, single-file weather dashboard powered by the OpenWeather API. This project upgrades a basic “enter location and fetch weather” page into a polished weather application with current weather, forecast cards, air quality data, geolocation, saved locations, unit switching, smart weather advice, and export tools.

---

## Overview

**Weather API Pro Dashboard** lets users search for a city or use their browser location to view real-time weather information. It keeps the original core feature — entering a location and fetching weather data — while adding a much richer interface and more advanced functionality.

The app uses OpenWeather’s coordinate-based workflow:

1. User enters a place name.
2. The app uses OpenWeather Geocoding to find latitude and longitude.
3. The app fetches current weather, forecast, and air quality data using those coordinates.
4. The dashboard updates with weather metrics, forecast cards, advice, and raw JSON tools.

---

## Features

### Core Weather Search

- Search weather by city, town, or location name
- Supports country-specific searches such as `London,GB`
- Uses OpenWeather Geocoding for better location accuracy
- Displays current weather conditions
- Shows temperature, description, humidity, wind, pressure, cloud cover, visibility, sunrise, and sunset

### Current Weather Dashboard

- Large current temperature display
- Weather icon from OpenWeather
- Local update time
- Location name and country
- Coordinates display
- Weather condition description

### Forecast System

- Next 24-hour forecast cards
- 5-day forecast summary
- Daily high and low temperatures
- Rain probability
- Forecast icons
- Weather descriptions for each forecast period

### Air Quality Information

- Air Quality Index display
- AQI labels such as Good, Fair, Moderate, Poor, and Very Poor
- PM2.5 value
- PM10 value
- Ozone value
- Graceful fallback if AQI data cannot be loaded

### Browser Geolocation

- “Use My Location” button
- Uses browser geolocation permission
- Reverse geocoding to label the user’s location
- Works with latitude and longitude directly

### Smart Weather Advice

The dashboard automatically generates simple advice based on:

- Temperature
- Wind speed
- Rain chance
- Visibility
- General weather risk

Examples include:

- Cold weather warnings
- Heat risk warnings
- Rain advice
- Wind warnings
- Visibility alerts

### Saved Locations

- Recent searches are saved locally
- Favourite locations can be saved
- Favourites and recent locations appear as quick-access chips
- Uses `localStorage`, so saved data remains after refreshing the page

### Units and Language

Supports multiple unit modes:

- Metric Celsius
- Imperial Fahrenheit
- Kelvin

Supports several weather description languages:

- English
- Spanish
- French
- German
- Italian
- Japanese
- Simplified Chinese

### UI and UX Improvements

- Responsive dashboard layout
- Dark and light theme toggle
- Animated background effects
- Loading indicator
- Status pill
- Error messages
- Mobile-friendly controls
- Glassmorphism-style panels
- Clean forecast cards
- Accessible form labels

### Data Tools

- Copy weather summary to clipboard
- Show or hide raw JSON
- Download weather data as a `.json` file
- Useful for debugging, learning APIs, or saving weather snapshots

---

## Demo

Open the HTML file in a browser, enter a location, and click:

```text
Fetch Weather
````

Example searches:

```text
London
Crawley
Tokyo
New York
Paris,FR
London,GB
```

---

## Screenshots

You can add screenshots here after running the project:

```markdown
![Weather Dashboard Screenshot](screenshots/dashboard.png)
![Forecast Screenshot](screenshots/forecast.png)
![Light Theme Screenshot](screenshots/light-theme.png)
```

---

## Tech Stack

* HTML5
* CSS3
* Vanilla JavaScript
* OpenWeather API
* Browser Geolocation API
* LocalStorage API
* Clipboard API
* Blob/File Download API

No frameworks are required.

---

## API Services Used

This project uses OpenWeather endpoints:

* Geocoding API
* Reverse Geocoding API
* Current Weather API
* 5-Day / 3-Hour Forecast API
* Air Pollution API

---

## Getting Started

### 1. Download or Clone the Project

```bash
git clone https://github.com/your-username/weather-api-pro-dashboard.git
cd weather-api-pro-dashboard
```

Or simply save the HTML code as:

```text
index.html
```

---

### 2. Get an OpenWeather API Key

Create an account at OpenWeather and generate an API key.

You will need the key to fetch live weather data.

---

### 3. Add Your API Key

You have two options.

#### Option A: Paste the key in the app

Run the page, paste your key into the **OpenWeather API Key** field, then search for weather.

The key is saved in your browser’s `localStorage`.

#### Option B: Put the key directly in the code

Find this line:

```js
const DEFAULT_API_KEY = "YOUR_OPEN_WEATHER_API_KEY";
```

Replace it with your API key:

```js
const DEFAULT_API_KEY = "your_real_api_key_here";
```

---

### 4. Run the Project

Because this is a single-file app, you can open it directly:

```text
index.html
```

For best results, run it with a local development server.

Using Python:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

Using VS Code:

```text
Right-click index.html → Open with Live Server
```

---

## Project Structure

Simple single-file version:

```text
weather-api-pro-dashboard/
├── index.html
└── README.md
```

Optional expanded structure:

```text
weather-api-pro-dashboard/
├── index.html
├── README.md
├── screenshots/
│   ├── dashboard.png
│   ├── forecast.png
│   └── light-theme.png
└── assets/
    └── icon.png
```

---

## How It Works

### Location Search

When a user enters a location, the app calls OpenWeather’s Geocoding API and returns possible matches.

If multiple matches are found, the app displays clickable location chips so the user can choose the correct place.

---

### Weather Fetching

After coordinates are found, the app fetches:

```js
/data/2.5/weather
/data/2.5/forecast
/data/2.5/air_pollution
```

The requests are made in parallel with:

```js
Promise.all()
```

This makes the dashboard update faster.

---

### Local Storage

The app stores:

* API key
* selected units
* selected language
* selected theme
* recent searches
* favourite locations

LocalStorage keys are namespaced under:

```js
weatherPro
```

---

## Configuration

You can modify default behaviour inside the JavaScript section.

### Change Default API Key

```js
const DEFAULT_API_KEY = "YOUR_OPEN_WEATHER_API_KEY";
```

### Change Recent Search Limit

```js
state.recent = uniqueLimit([value, ...state.recent], 10);
```

### Change Favourite Limit

```js
state.favorites = uniqueLimit([value, ...state.favorites], 12);
```

### Change Request Timeout

```js
const timeout = setTimeout(() => controller.abort(), 15000);
```

---

## Main Buttons

| Button               | Description                                            |
| -------------------- | ------------------------------------------------------ |
| Fetch Weather        | Searches for the typed location and loads weather data |
| Use My Location      | Uses browser geolocation to fetch local weather        |
| Save Favorite        | Saves the current location as a favourite              |
| Copy Summary         | Copies a short weather summary to the clipboard        |
| Toggle Theme         | Switches between dark and light mode                   |
| Download JSON        | Downloads the latest weather data                      |
| Show / Hide Raw JSON | Toggles the raw API response viewer                    |

---

## Example Weather Summary

The copy summary tool generates text like:

```text
London: 14°C, scattered clouds. Feels like 13°C. Humidity 72%, wind 5 m/s.
```

---

## Error Handling

The app includes improved error handling for:

* Missing API key
* Invalid API key
* No matching location
* Network failure
* Request timeout
* Geolocation permission denial
* Air quality endpoint failure
* Invalid API responses

Instead of failing silently, the app displays a clear message in the interface.

---

## Browser Support

Recommended browsers:

* Chrome
* Edge
* Firefox
* Safari

Some features depend on browser support:

| Feature        | Requirement                 |
| -------------- | --------------------------- |
| Geolocation    | Browser permission required |
| Clipboard copy | Clipboard API support       |
| JSON download  | Blob and URL APIs           |
| Local saving   | LocalStorage support        |

---

## Security Notes

This is a front-end demo. API keys placed in client-side JavaScript can be seen by users.

For a production version, use a backend proxy to protect your API key.

Recommended production architecture:

```text
Browser → Your Backend → OpenWeather API
```

Do not expose private, paid, or restricted API keys in public repositories.

---

## Possible Future Improvements

* Add weather maps
* Add radar layers
* Add severe weather alerts
* Add hourly chart visualisations
* Add sunrise and sunset timeline
* Add PWA offline mode
* Add installable mobile app support
* Add map picker for coordinates
* Add weather history
* Add route weather planning
* Add custom notification alerts
* Add multi-location comparison
* Add backend API proxy for key security
* Add service worker caching
* Add accessibility testing improvements
* Add unit tests for data formatting functions

---

## Accessibility

Current accessibility improvements include:

* Labelled inputs
* Keyboard-friendly search with Enter key
* Clear button text
* High-contrast themes
* Responsive layout
* Visible status and error messages

Further improvements could include:

* ARIA live regions for weather updates
* Reduced-motion mode
* Better screen reader summaries
* Skip links
* More detailed icon alt text

---

## Known Limitations

* Requires an OpenWeather API key
* Weather accuracy depends on OpenWeather data
* Browser geolocation requires user permission
* Client-side API keys are not secure for production
* Some API features may depend on OpenWeather plan limits
* Forecast data is based on 3-hour intervals, not true minute-by-minute forecasting

---

## Development Notes

This project is intentionally built with vanilla HTML, CSS, and JavaScript so it is easy to understand, modify, and deploy.

No build system is required.

You can improve the project by separating the file into:

```text
index.html
style.css
app.js
```

For larger versions, consider using:

* Vite
* React
* Vue
* Svelte
* Express backend proxy
* Chart.js for graphs
* Leaflet or Mapbox for maps

---

## Deployment

You can deploy this project on:

* GitHub Pages
* Netlify
* Vercel
* Cloudflare Pages
* Any static hosting provider

For GitHub Pages:

1. Push the project to GitHub.
2. Go to repository settings.
3. Open **Pages**.
4. Select the branch.
5. Save and open the generated site URL.

Remember: for public deployment, avoid hardcoding private API keys.

---

## License

This project is open source and can be used, modified, and expanded freely.

Suggested license:

```text
MIT License
```

---

## Credits

Built with:

* OpenWeather API
* Vanilla JavaScript
* HTML5
* CSS3
* Browser Web APIs

---

## Author

Created by **kai9987kai**

---

## Summary

Weather API Pro Dashboard is a major upgrade from a simple weather lookup page. It keeps the original location search and weather display feature, then expands it into a complete browser-based weather dashboard with forecasts, air quality, smart advice, saved locations, themes, geolocation, export tools, and a much more polished user experience.

```
```
