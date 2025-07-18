# Weather App 🌤️

A modern, responsive React-based weather application that provides current weather information and 5-day forecasts for any city worldwide. Features real-time weather data from OpenWeatherMap API with dynamic background changes based on weather conditions.

## 🚀 Features

- **Current Weather Display**: Real-time weather information including temperature, humidity, wind speed, and conditions
- **Location-based Weather**: Automatic detection of user's current location using geolocation API
- **City Search**: Search weather for any city worldwide
- **5-Day Forecast**: Detailed hourly forecast for the next 5 days
- **Dynamic Backgrounds**: Background images change based on current weather conditions
- **Responsive Design**: Optimized for desktop and mobile devices
- **Error Handling**: User-friendly error messages for invalid city names

## 🏗️ Application Architecture

```mermaid
graph TB
    A[App.js] --> B[WeatherDetails.js]
    B --> C[MyContext Provider]
    C --> D[Header.js]
    C --> E[Search.js]
    C --> F[Forecast.js]
    C --> G[Fivedays_Forecast.js]
    
    D --> H[Search Input]
    D --> I[Location Button]
    E --> J[Current Weather Display]
    F --> K[Today's Hourly Forecast]
    G --> L[5-Day Detailed Forecast]
    
    B --> M[OpenWeatherMap API]
    M --> N[Current Weather Data]
    M --> O[Forecast Data]
    
    style A fill:#e1f5fe
    style B fill:#f3e5f5
    style C fill:#fff3e0
    style M fill:#e8f5e8
```

## 🔄 Data Flow Diagram

```mermaid
sequenceDiagram
    participant User
    participant Header
    participant WeatherDetails
    participant API as OpenWeatherMap API
    participant Search
    participant Forecast
    participant FiveDays

    User->>Header: Enter city name / Click location
    Header->>WeatherDetails: Update city state
    WeatherDetails->>API: Fetch current weather
    API-->>WeatherDetails: Return weather data
    WeatherDetails->>WeatherDetails: Set background based on weather
    WeatherDetails->>API: Fetch 5-day forecast
    API-->>WeatherDetails: Return forecast data
    WeatherDetails->>Search: Pass current weather data
    WeatherDetails->>Forecast: Pass today's forecast
    Search-->>User: Display current weather
    Forecast-->>User: Display hourly forecast
    
    User->>Forecast: Click "More" button
    Forecast->>WeatherDetails: Toggle more state
    WeatherDetails->>FiveDays: Show detailed forecast
    FiveDays-->>User: Display 5-day forecast
```

## 🧩 Component Structure

```mermaid
classDiagram
    class App {
        +render()
    }
    
    class WeatherDetails {
        -city: string
        -data: object
        -forecastdata: object
        -more: boolean
        -error: string
        +fetchData()
        +fetchForecast()
        +setBackground()
        +handleClick()
    }
    
    class Header {
        +handleKeyPress()
        +fetchLocation()
        +render()
    }
    
    class Search {
        +getDirection()
        +render()
    }
    
    class Forecast {
        +groupForecastByDay()
        +render()
    }
    
    class FiveDaysForecast {
        +groupForecastByDay()
        +scroll()
        +render()
    }
    
    class MyContext {
        +city
        +data
        +forecastdata
        +more
        +error
        +fetchData
        +handleClick
    }
    
    App --> WeatherDetails
    WeatherDetails --> MyContext
    WeatherDetails --> Header
    WeatherDetails --> Search
    WeatherDetails --> Forecast
    WeatherDetails --> FiveDaysForecast
    MyContext --> Header
    MyContext --> Search
    MyContext --> Forecast
    MyContext --> FiveDaysForecast
```

## 🎯 User Journey Flow

```mermaid
flowchart TD
    A[User Opens App] --> B{Has Default City?}
    B -->|Yes| C[Load Karur Weather]
    B -->|No| D[Show Search Interface]
    
    C --> E[Display Current Weather]
    D --> F{User Action}
    
    F -->|Types City| G[Search Weather]
    F -->|Clicks Location| H[Get GPS Location]
    
    G --> I{Valid City?}
    I -->|Yes| E
    I -->|No| J[Show Error Message]
    
    H --> K{Location Available?}
    K -->|Yes| L[Fetch Weather by Coordinates]
    K -->|No| M[Show Location Error]
    
    L --> E
    J --> F
    M --> F
    
    E --> N[Show Today's Forecast]
    N --> O{User Clicks More?}
    O -->|Yes| P[Show 5-Day Forecast]
    O -->|No| Q[Stay on Current View]
    
    P --> R{User Clicks Back?}
    R -->|Yes| E
    R -->|No| S[Browse Detailed Forecast]
    
    S --> T[Scroll Through Days]
    T --> R
    
    style A fill:#e3f2fd
    style E fill:#e8f5e8
    style P fill:#fff3e0
    style J fill:#ffebee
```

## 🛠️ Technology Stack

```mermaid
graph LR
    A[Frontend] --> B[React 18.3.1]
    A --> C[React Context API]
    A --> D[React Hooks]
    
    E[HTTP Client] --> F[Axios 1.10.0]
    
    G[UI/UX] --> H[React Icons 5.5.0]
    G --> I[CSS3]
    G --> J[Responsive Design]
    
    K[Utilities] --> L[Moment.js 2.30.1]
    
    M[API] --> N[OpenWeatherMap API]
    N --> O[Current Weather Endpoint]
    N --> P[5-Day Forecast Endpoint]
    
    Q[Deployment] --> R[GitHub Pages]
    Q --> S[gh-pages 6.1.1]
    
    style A fill:#e1f5fe
    style E fill:#f3e5f5
    style G fill:#e8f5e8
    style K fill:#fff3e0
    style M fill:#fce4ec
    style Q fill:#f1f8e9
```

## 📦 Project Structure

```
weather-app/
├── public/
│   ├── index.html
│   ├── favicon.ico
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
├── src/
│   ├── App.js                 # Main app component
│   ├── App.css               # Global styles
│   ├── index.js              # App entry point
│   ├── index.css             # Base styles
│   ├── WeatherDetails.js     # Main container & context provider
│   ├── Header.js             # Search input & location button
│   ├── Search.js             # Current weather display
│   ├── Forecast.js           # Today's hourly forecast
│   └── Fivedays_Forecast.js  # 5-day detailed forecast
├── package.json              # Dependencies & scripts
└── README.md                 # Project documentation
```

## 🔑 API Integration

```mermaid
graph TD
    A[WeatherDetails Component] --> B{API Call Type}
    
    B -->|Current Weather| C[GET /weather]
    B -->|5-Day Forecast| D[GET /forecast]
    
    C --> E[Query Parameters]
    D --> F[Query Parameters]
    
    E --> G[q: city name]
    E --> H[appid: API key]
    
    F --> I[q: city name]
    F --> J[appid: API key]
    
    G --> K[OpenWeatherMap API]
    H --> K
    I --> K
    J --> K
    
    K --> L{Response Status}
    
    L -->|200 OK| M[Parse Weather Data]
    L -->|404 Not Found| N[Show Error Message]
    L -->|Other Error| O[Handle API Error]
    
    M --> P[Update Component State]
    M --> Q[Set Dynamic Background]
    
    P --> R[Render Weather UI]
    Q --> S[Apply Weather Theme]
    
    style K fill:#e8f5e8
    style N fill:#ffebee
    style O fill:#ffebee
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- npm or yarn package manager
- OpenWeatherMap API key

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Dharshinipriya-11/Weather-App.git
   cd Weather-App
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up API key**
   - Get your free API key from [OpenWeatherMap](https://openweathermap.org/api)
   - Replace the API key in `src/WeatherDetails.js` and `src/Header.js`

4. **Start the development server**
   ```bash
   npm start
   ```

5. **Open your browser**
   - Navigate to [http://localhost:3000](http://localhost:3000)

## 📱 Available Scripts

### `npm start`
Runs the app in development mode. The page will reload when you make changes.

### `npm test`
Launches the test runner in interactive watch mode.

### `npm run build`
Builds the app for production to the `build` folder with optimized performance.

### `npm run deploy`
Deploys the application to GitHub Pages.

## 🎨 Features in Detail

### Dynamic Background System
The application automatically changes its background image based on current weather conditions:
- **Clear Sky**: Bright, sunny landscapes
- **Clouds**: Cloudy sky imagery
- **Rain**: Rainy weather scenes
- **Thunderstorm**: Dramatic storm imagery
- **Default**: Generic weather background

### Responsive Forecast Display
- **Today's View**: Shows current weather + today's hourly forecast
- **5-Day View**: Detailed daily breakdown with hourly data
- **Horizontal Scrolling**: Navigate through time periods easily

### Geolocation Integration
- Automatic location detection using browser's geolocation API
- Fallback to manual city search if location access is denied
- Error handling for location services

## 🔧 Configuration

### API Configuration
```javascript
const key = "your_openweathermap_api_key";
```

### Default City
```javascript
const [city, setCity] = useState("Karur");
```

## 🚀 Deployment

The app is configured for deployment to GitHub Pages:

1. **Build the project**
   ```bash
   npm run build
   ```

2. **Deploy to GitHub Pages**
   ```bash
   npm run deploy
   ```

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgments

- [OpenWeatherMap](https://openweathermap.org/) for providing the weather API
- [React](https://reactjs.org/) team for the amazing framework
- [Create React App](https://create-react-app.dev/) for the project setup
- [Unsplash](https://unsplash.com/) for the beautiful weather background images

## 📞 Contact

**Dharshinipriya-11** - [GitHub Profile](https://github.com/Dharshinipriya-11)

Project Link: [https://github.com/Dharshinipriya-11/Weather-App](https://github.com/Dharshinipriya-11/Weather-App)