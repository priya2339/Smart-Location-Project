## Smart Location Documentation

This documentation outlines the structure and functionality of the "Nearby Places Finder" web application, built using HTML, CSS, and JavaScript. The app leverages Mapbox GL JS for map visualization and Geocoding API for location searches.

**Files:**

- **index.html:** The main HTML file that structures the web page.
- **style.css:** The CSS file that styles the user interface.
- **script.js:** The JavaScript file that handles the application's logic and interactions.

**index.html (index.html):**

1. **DOCTYPE Declaration:** Defines the document type as HTML5.
2. **HTML Element:** The root element of the HTML document.
3. **Head Section:** Contains meta information and links to external resources:
    - **meta charset:** Specifies the character encoding as UTF-8 for proper display of characters.
    - **meta viewport:** Configures the viewport for responsiveness on different devices.
    - **title:** Sets the title of the web page.
    - **link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/mapbox-gl/dist/mapbox-gl.css":** Includes Mapbox GL JS's default stylesheet for the map.
    - **link rel="stylesheet" href="style.css":** Links the external CSS file for custom styling.
4. **Body Section:** Contains the visible content of the web page:
    - **header:** Displays the application's title.
    - **main:** Contains the primary content of the page:
        - **div class="controls":** Holds the search input, button, and category selection dropdown.
        - **div id="map" class="map":** The container for the Mapbox map.
        - **div class="places-list":** Displays a list of nearby places.
    - **footer:** Displays copyright information.
    - **script src="https://cdn.jsdelivr.net/npm/mapbox-gl/dist/mapbox-gl.js":** Includes Mapbox GL JS's JavaScript library.
    - **script src="https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-directions/v4.0.0/mapbox-gl-directions.js":** Includes the Mapbox Directions plugin for routing functionality.
    - **link href="https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-directions/v4.0.0/mapbox-gl-directions.css" rel="stylesheet" />:** Includes the stylesheet for the Mapbox Directions plugin.
    - **script src="script.js":** Links the external JavaScript file containing the application's logic.

**style.css (style.css):**

1. **General Styles:**
    - **\*:** Resets default styles for all elements.
    - **body:** Applies basic styles for body content.
2. **Header Styles:**
    - **header:** Styles the header with background color, text color, and padding.
3. **Main Container Styles:**
    - **.main-container:** Defines styles for the main content area, including layout and padding.
4. **Map Styles:**
    - **.map:** Sets the size and appearance of the Mapbox map.
5. **Controls Styles:**
    - **.controls:** Styles the search input, button, and category dropdown area.
6. **Places List Styles:**
    - **.places-list ul, .places-list li:** Styles the list of nearby places with background colors, padding, margins, and hover effects.
7. **Place Container Styles:**
    - **.place-container:** Defines styles for individual place elements.
8. **Weather Info Styles:**
    - **.weather-info:** Styles the weather information container with background color, padding, and font styles.
9. **Footer Styles:**
    - **footer:** Styles the footer with background color, text color, padding, and positioning.
10. **Media Queries:**
    - **@media screen and (max-width: 1024px), @media screen and (max-width: 768px), @media screen and (max-width: 480px):** Provides responsive styles for different screen sizes, adjusting layout, font sizes, and element sizes.

**script.js (script.js):**

1. **Mapbox Access Token:**
    - **mapboxgl.accessToken = 'pk.eyJ1IjoiZ2F1cmF2bmciLCJhIjoiY20xdGx3ODhuMDNzNTJ0cHI2YWphY2p1ZCJ9.DCncOYgA91GXOkejz0CilQ';** Defines the Mapbox access token for map access.
2. **Pexels API Key:**
    - **const pexelsApiKey = '2LFJPIrvoT8OjnKDqJDES7pWP1UsebbVnaEOmAWTR9Bic1HgHRkbXch7';** Defines the Pexels API key for fetching place images.
3. **Map Initialization:**
    - **const map = new mapboxgl.Map(...):** Creates a new Mapbox map instance with default styles, center coordinates, and zoom level.
4. **Map Controls:**
    - **map.addControl(new mapboxgl.NavigationControl(), 'top-right');:** Adds the navigation control for zooming and panning.
    - **map.addControl(new mapboxgl.GeolocateControl({...}), 'top-left');:** Adds the geolocation control for locating the user's current location.
5. **Directions Initialization:**
    - **const directions = new MapboxDirections({...});:** Initializes the Mapbox Directions plugin for routing functionalities.
6. **Get User Location:**
    - **navigator.geolocation.getCurrentPosition(...):** Retrieves the user's current location using the Geolocation API.
    - **map.setCenter([longitude, latitude]);:** Sets the map's center to the user's location.
    - **new mapboxgl.Marker({ color: 'green' }).setLngLat(...).addTo(map);:** Adds a green marker to the map indicating the user's location.
7. **Fetch Nearby Places:**
    - **const nearbyPlacesResponse = await fetchNearbyPlaces([longitude, latitude], selectedCategory);:** Calls the `fetchNearbyPlaces` function to retrieve nearby places based on user location and selected category.
    - **displayNearbyPlaces(nearbyPlacesResponse.features, [longitude, latitude]);:** Calls the `displayNearbyPlaces` function to display the retrieved places.
8. **Fetch Weather Info:**
    - **const weatherInfo = await fetchWeatherByCoords(latitude, longitude);:** Calls the `fetchWeatherByCoords` function to retrieve weather information for the user's location.
    - **displayWeatherInfo(weatherInfo);:** Calls the `displayWeatherInfo` function to display the retrieved weather information.
9. **Search Button Event Listener:**
    - **document.getElementById('search-btn').addEventListener('click', async () => ...);:** Attaches a click event listener to the search button.
    - **const response = await fetch(`https://api.mapbox.com/geocoding/v5/mapbox.places/${encodeURIComponent(locationInput)}.json?access_token=${mapboxgl.accessToken}`);:** Fetches geocoding data from Mapbox API based on the user's input location.
    - **const locationCoords = data.features[0].geometry.coordinates;:** Extracts coordinates from the geocoding response.
    - **map.flyTo({ center: locationCoords, zoom: 14 });:** Flies the map to the searched location with a zoom level of 14.
    - **new mapboxgl.Marker().setLngLat(locationCoords).addTo(map);:** Adds a marker to the searched location.
    - **const nearbyPlacesResponse = await fetchNearbyPlaces(locationCoords, selectedCategory);:** Fetches nearby places for the searched location.
    - **displayNearbyPlaces(nearbyPlacesResponse.features, locationCoords);:** Displays the retrieved places for the searched location.
    - **const weatherInfo = await fetchWeatherByCoords(locationCoords[1], locationCoords[0]);:** Fetches weather information for the searched location.
    - **displayWeatherInfo(weatherInfo);:** Displays the retrieved weather information for the searched location.
10. **Show Route Function:**
    - **function showRoute(startCoords, endCoords, mode):** Takes start and end coordinates and a travel mode as input, sets the origin and destination for the Mapbox Directions plugin, and sets the travel profile.
11. **Fetch Nearby Places Function:**
    - **async function fetchNearbyPlaces(coords, category):** Takes coordinates and a category as input, constructs a request to the Mapbox Geocoding API, fetches the data, and returns the response.
12. **Display Nearby Places Function:**
    - **function displayNearbyPlaces(places, centerCoords):** Takes an array of places and center coordinates as input, clears the existing places list, and displays the places with their names, distances, and images in a list.
13. **Calculate Distance Function:**
    - **function calculateDistance(coords1, coords2):** Takes two sets of coordinates and calculates the distance between them using the Haversine formula.
14. **Degrees to Radians Function:**
    - **function deg2rad(deg):** Converts degrees to radians.
15. **Fetch Weather By Coordinates Function:**
    - **async function fetchWeatherByCoords(lat, lon):** Takes latitude and longitude as input, constructs a request to the OpenWeatherMap API, fetches the data, and returns the response.
16. **Fetch Image For Place Function:**
    - **async function fetchImageForPlace(placeName):** Takes a place name as input, constructs a request to the Pexels API, fetches the data, and returns the image URL of the first photo found for the place name. If no image is found, it returns a placeholder image URL.
17. **Display Weather Info Function:**
    - **function displayWeatherInfo(weatherInfo):** Takes weather data as input, retrieves the weather icon URL, and displays the temperature and weather description in the "weather-info" container.

**Key Features:**

- **Location Search:** Allows users to search for locations by name.
- **Current Location Tracking:** Uses the browser's Geolocation API to track the user's current location and display it on the map.
- **Nearby Places Discovery:** Fetches and displays nearby places based on the user's location and selected category.
- **Weather Information:** Displays the current weather conditions for the user's location or a searched location.
- **Routing Functionality:** Allows users to get directions between two points on the map.
- **Responsive Design:** Adapts the layout and styles for different screen sizes to provide a seamless user experience on various devices.

**Instructions:**

1. **Obtain Mapbox Access Token:** Visit [https://account.mapbox.com/](https://account.mapbox.com/) and create an account. Once logged in, create a new project and obtain an access token. Replace the placeholder token in `script.js` with your actual token.
2. **Obtain Pexels API Key:** Visit [https://www.pexels.com/api/](https://www.pexels.com/api/) and sign up for an account. Once logged in, obtain an API key. Replace the placeholder key in `script.js` with your actual key.
3. **Run the Application:** Open `index.html` in a web browser.

This documentation provides a comprehensive overview of the "Nearby Places Finder" application's structure and functionalities. Feel free to modify and enhance the application further to suit your specific needs and requirements. 
