# Leaflet and IndexedDB caching map tiles  
This project is a web application that utilizes the [Leaflet.js](https://leafletjs.com/) library for interactive maps and adds functionality for caching map tiles using `IndexedDB`.
## Features

- **Tile Caching**: 
  - Map tiles are cached locally in the browser using `IndexedDB` to allow offline access or to reduce redundant network requests.

- **Persistent Cache (manual clear only)**:
  - Cached tiles are kept indefinitely and are **never deleted automatically**. The only way to remove them is the **Clear cache** button in the status panel.

- **Storage Quota Management**:
  - The app reads the browser storage quota via `navigator.storage.estimate()`. Caching of **new** tiles is skipped above 95% usage (existing tiles are left untouched).

- **Status Panel**:
  - A small on-screen panel shows online/offline status, the number of cached tiles, current storage usage, and a button to clear the cache.

- **Network Request Retries**:
  - If a tile request fails, the app automatically retries up to three times with a delay between each attempt.

## How it Works

1. **Leaflet for Map Rendering**: 
   The app uses [Leaflet.js](https://leafletjs.com/) to render an interactive map on the page.

2. **Caching with IndexedDB**:
   - When the map loads, it retrieves map tiles via HTTP requests using the native `fetch` API (no external HTTP client needed).
   - Each tile is stored in the browser's `IndexedDB` keyed by its URL, so it can be re-used on later requests.
   
3. **Storage Management**:
   - The app checks the browser’s storage quota using the `navigator.storage.estimate()` API. Above 95% usage it stops caching new tiles to avoid exceeding the limit. Existing cached tiles are never removed automatically — use the Clear cache button.

4. **Retry Mechanism**:
   - The tile fetch function uses a retry mechanism to handle network failures. If a tile fails to load, the app retries the request up to three times with a 1-second delay between attempts.

## Technologies Used

- **Leaflet.js**: A leading open-source library for interactive maps.
- **IndexedDB**: A low-level browser storage API used for caching map tiles.
- **Fetch API**: The native browser API used to handle network requests.

## Setup and Installation

To run this project locally, follow the steps below:

1. **Clone the repository**:

   ```bash
   git clone https://github.com/JohnCamelTry/leaflet-cache-tile.git
   cd leaflet-cache-tile
   
2. **Open the project**:

Open index.html in your browser.

3. **Developer Tools**:

To verify that map tiles are being cached correctly, open your browser’s developer tools (press F12).
Navigate to the Applications tab.
Under Storage, expand the IndexedDB section.
Look for the database associated with this project, and you’ll be able to inspect the cached tiles within it.

