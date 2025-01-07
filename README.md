# Weather App

This is a simple weather app where users can input a city and get weather information.

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="styles.css">
</head>

<body>
    <div class="container">
        <h1>Weather App</h1>
        <input type="text" id="locationInput" placeholder="Enter a city">
        <button id="searchButton">Search</button>
        <div class="weather-info">
            <h2 id="location"></h2>
            <p id="temperature"></p>
            <p id="description"></p>
        </div>
    </div>
    <script src="script.js"></script>
</body>

</html>

# Weather App JavaScript Code

This JavaScript code fetches weather data from the OpenWeather API based on user input and displays the result on the webpage.

## Code Breakdown

### 1. **API Key and URL**
```javascript
const apiKey = 'fd3317f04449db47fe65c3e3cae45af1';
const apiUrl = 'https://api.openweathermap.org/data/2.5/weather';
apiKey: The key used to authenticate requests to the OpenWeather API.
apiUrl: The base URL for accessing the weather data endpoint of the OpenWeather API.
### 2. **DOM elements**
const locationInput = document.getElementById('locationInput');
const searchButton = document.getElementById('searchButton');
const locationElement = document.getElementById('location');
const temperatureElement = document.getElementById('temperature');
const descriptionElement = document.getElementById('description');

locationInput: The input field where the user enters the name of the city.
searchButton: The button that triggers the weather data fetch.
locationElement: A DOM element where the city name will be displayed.
temperatureElement: A DOM element where the temperature will be shown.
descriptionElement: A DOM element where the weather description will be shown.
### 3. **Event Listener for the Search Button**
##javascript code
searchButton.addEventListener('click', () => {
    const location = locationInput.value;
    if (location) {
        fetchWeather(location);
    }
});
The click event listener on the searchButton triggers the weather data fetch.
It checks if the locationInput field is not empty and calls the fetchWeather function with the entered city name.
### 4. **Fetch Weather Data**
javascript code
function fetchWeather(location) {
    const url = `${apiUrl}?q=${location}&appid=${apiKey}&units=metric`;

    fetch(url)
        .then(response => response.json())
        .then(data => {
            locationElement.textContent = data.name;
            temperatureElement.textContent = `${Math.round(data.main.temp)}°C`;
            descriptionElement.textContent = data.weather[0].description;
        })
        .catch(error => {
            console.error('Error fetching weather data:', error);
        });
}
fetchWeather(location): A function that fetches weather data from the OpenWeather API for a given location.
It constructs the API URL with the location, API key, and units (metric for Celsius).
fetch(url): Sends a GET request to the OpenWeather API.
.then(response => response.json()): Parses the API response as JSON.
.then(data => {...}): Handles the data by updating the DOM elements to display the city name, temperature (rounded to the nearest degree), and weather description.
.catch(error => {...}): Logs any errors in the console if the API request fails.
### 5. **Error Handling**
javascript code
.catch(error => {
    console.error('Error fetching weather data:', error);
});
If there is an error while fetching the weather data (e.g., invalid city name or network issues), the error is logged in the console.