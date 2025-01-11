---
title: "Weather-Forecast [Project]"
description: "Want to check the weather from the command line? In this blog, we’ll show you a simple Python weather tool using the OpenWeatherMap API."
date: 2023-06-24 00:00:00 +0000
categories: [Project, Python]
tags: [Project, Python]
image: 
    path: assets/img/misc/weather.jpeg
    alt: Architecture Flow Diagram
---

# A Command-Line Weather Checker Using OpenWeatherMap API

Weather data plays a vital role in daily life, whether it's planning activities or studying climate trends. To address this need, I developed a Command-Line Weather Forecasting Tool that retrieves real-time weather information and forecasts using the OpenWeatherMap API. This blog explores its features and functionality.

The project is available on GitHub: [Weather-Forecast](https://github.com/paulrounak/Weather-Forecast.git).

---

## Key Features

The Weather Forecasting Tool provides essential weather information for any city. Here are its standout features:

1. **Current Weather**  
   Get real-time weather details, including temperature, wind speed, humidity, weather conditions (e.g., sunny, cloudy, rainy), and "feels like" temperature.

2. **5-Day Weather Forecast**  
   Access detailed hourly weather forecasts for the next five days, helping users plan their activities effectively.

3. **Support for Metric and Imperial Units**  
   Choose between metric (Celsius, m/s) and imperial (Fahrenheit, mph) units for temperature and wind speed.

4. **Help Documentation**  
   A built-in help feature guides users on available commands and options, ensuring ease of use.

5. **Error Handling**  
   The tool gracefully handles errors such as invalid city names or API issues, providing informative error messages.

---

## How to Use the Tool

Using the Weather Forecasting Tool is simple. Follow these steps:

### Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/paulrounak/Weather-Forecast.git
    ```

2. Navigate to the project directory:

    ```bash
    cd Weather-Forecast
    ```

3. Obtain an OpenWeatherMap API key from [OpenWeatherMap](https://openweathermap.org/). Replace the placeholder key in the script with your API key.

### Running the Script

Run the script directly from the terminal with the desired options:

#### __Examples__

- **Current Weather in Metric Units:**

    ```bash
    python weathermap.py -c Hawaii
    ```

- **5-Day Forecast in Imperial Units:**

    ```bash
    python weathermap.py -F Hawaii
    ```

### Help Command

To view available options, use the `-h` flag:

```bash
python weathermap.py -h
```

This displays:

- `-c`: Current weather in metric units.
- `-f`: 5-day forecast in metric units.
- `-C`: Current weather in imperial units.
- `-F`: 5-day forecast in imperial units.
- `-h`: Help documentation.

---

## How It Works

### Validating Input

The script validates user-provided input to ensure correctness. Invalid city names or incorrect flags trigger a help message for guidance.

### Fetching Weather Data

The tool uses the OpenWeatherMap API to fetch real-time weather and forecasts. Depending on the selected options, it constructs API requests for current conditions or 5-day forecasts in the chosen unit system.

### Parsing and Displaying Data

The fetched JSON data is parsed and displayed in a user-friendly format. For forecasts, the data is organized by date and time.

### Error Handling

The tool handles errors such as non-existent cities or API connectivity issues, displaying appropriate messages to ensure a smooth user experience.

---

## Development Insights

### Role of GitHub Copilot

During development, **GitHub Copilot** proved invaluable by:

- **Code Generation:** Translating comments into functional code.
- **Optimization:** Suggesting efficient coding approaches.
- **Auto-Suggestions:** Recommending functions and libraries.
- **Documentation Assistance:** Generating comments and usage guides.

---

## Conclusion

The Weather Forecasting Tool is a simple yet powerful command-line application for real-time and forecasted weather data. Its support for different units, error handling, and detailed help documentation make it a reliable tool for users.

This project highlights the capabilities of Python, APIs, and tools like GitHub Copilot in enhancing productivity. Whether you're a beginner or an experienced developer, this tool is a great resource to learn and build upon.

Feel free to explore the code, make modifications, or contribute to this open-source project!
