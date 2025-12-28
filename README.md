# Assignment 2: Backend API Integration & Service Development

A full-stack web application that integrates OpenWeather API and News API to provide real-time weather information and related news for cities around the world. The backend processes all API requests on the server side, ensuring secure API key management and clean data presentation.

## 🌟 Features

### Core Requirements
- **Weather Data Integration**: Fetches real-time weather data from OpenWeather API
  - Temperature (in Celsius)
  - Weather description
  - Coordinates (latitude/longitude)
  - Feels-like temperature
  - Wind speed
  - Country code
  - Rain volume for the last 3 hours
  - Additional data: humidity, pressure, visibility

### Additional API Integration
- **News API Integration**: Fetches relevant news articles based on the country of the searched city
  - Top headlines from the country
  - Article titles, descriptions, images, and links
  - Publication dates and sources

### User Interface
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile devices
- **Modern UI**: Clean, user-friendly interface with smooth animations
- **Real-time Updates**: Instant weather and news updates when searching for a city
- **Error Handling**: User-friendly error messages for invalid inputs or API failures

## 📋 Prerequisites

Before running this application, ensure you have:

- **Node.js** (v14 or higher) installed on your system
- **npm** (Node Package Manager) installed
- API keys for:
  - [OpenWeather API](https://openweathermap.org/api) (Free tier available)
  - [News API](https://newsapi.org/) (Free tier available)

## 🚀 Setup Instructions

### 1. Clone or Download the Project

Navigate to the project directory:
```bash
cd ASSignment2
```

### 2. Install Dependencies

Install all required packages using npm:
```bash
npm install
```

This will install the following dependencies:
- `express`: Web server framework
- `axios`: HTTP client for API requests
- `dotenv`: Environment variable management
- `cors`: Cross-Origin Resource Sharing support

### 3. Configure Environment Variables

Create a `.env` file in the root directory of the project:

```bash
# Create .env file
touch .env
```

Add the following content to the `.env` file:

```env
PORT=3000
OPENWEATHER_API_KEY=your_openweather_api_key_here
NEWS_API_KEY=your_news_api_key_here
```

**Important**: Replace `your_openweather_api_key_here` and `your_news_api_key_here` with your actual API keys.

#### Getting API Keys:

1. **OpenWeather API Key**:
   - Visit [https://openweathermap.org/api](https://openweathermap.org/api)
   - Sign up for a free account
   - Navigate to API keys section
   - Copy your API key

2. **News API Key**:
   - Visit [https://newsapi.org/](https://newsapi.org/)
   - Sign up for a free account
   - Copy your API key from the dashboard

### 4. Start the Server

Run the server using npm:
```bash
npm start
```

For development with auto-reload (if nodemon is installed):
```bash
npm run dev
```

The server will start on `http://localhost:3000` (or the port specified in your `.env` file).

### 5. Access the Application

Open your web browser and navigate to:
```
http://localhost:3000
```

## 📖 API Usage Details

### Weather API Endpoint

**GET** `/api/weather/:city`

Fetches weather data for a specified city.

**Parameters:**
- `city` (path parameter): Name of the city (e.g., "London", "New York", "Tokyo")

**Example Request:**
```bash
GET http://localhost:3000/api/weather/London
```

**Example Response:**
```json
{
  "temperature": 15,
  "description": "clear sky",
  "coordinates": {
    "lat": 51.5074,
    "lon": -0.1278
  },
  "feelsLike": 14,
  "windSpeed": 3.5,
  "countryCode": "GB",
  "rainVolume": 0,
  "humidity": 65,
  "pressure": 1015,
  "visibility": "10.0",
  "cityName": "London",
  "icon": "01d"
}
```

### News API Endpoints

**GET** `/api/news/country/:countryCode`

Fetches top news headlines for a specific country.

**Parameters:**
- `countryCode` (path parameter): ISO country code (e.g., "us", "gb", "jp")
- `limit` (query parameter, optional): Number of articles to return (default: 5)

**Example Request:**
```bash
GET http://localhost:3000/api/news/country/gb?limit=5
```

**Example Response:**
```json
{
  "articles": [
    {
      "title": "Article Title",
      "description": "Article description...",
      "url": "https://example.com/article",
      "urlToImage": "https://example.com/image.jpg",
      "publishedAt": "2024-01-15T10:30:00Z",
      "source": "BBC News"
    }
  ],
  "count": 5
}
```

**GET** `/api/news/search/:query`

Searches for news articles by keyword.

**Parameters:**
- `query` (path parameter): Search query
- `limit` (query parameter, optional): Number of articles to return (default: 5)

**Example Request:**
```bash
GET http://localhost:3000/api/news/search/weather?limit=5
```

## 🏗️ Project Structure

```
ASSignment2/
│
├── server.js                 # Main server file
├── package.json              # Project dependencies and scripts
├── .env                      # Environment variables (create this file)
├── README.md                 # This file
│
├── routes/                   # API route handlers
│   ├── weather.js           # Weather API routes
│   └── news.js              # News API routes
│
├── services/                 # Business logic and API integrations
│   ├── weatherService.js    # OpenWeather API service
│   └── newsService.js       # News API service
│
└── public/                   # Frontend static files
    ├── index.html           # Main HTML file
    ├── css/
    │   └── style.css        # Stylesheet with responsive design
    └── js/
        └── app.js           # Frontend JavaScript logic
```

## 🎨 Design Decisions

### Backend Architecture

1. **Server-Side API Integration**: All third-party API calls are made on the server side to:
   - Protect API keys from client-side exposure
   - Ensure better security and control
   - Process and format data before sending to the client
   - Reduce client-side dependencies

2. **Modular Structure**: The codebase is organized into:
   - **Routes**: Handle HTTP requests and responses
   - **Services**: Contain business logic and API communication
   - Clear separation of concerns for maintainability

3. **Error Handling**: Comprehensive error handling at multiple levels:
   - Service layer catches API errors
   - Route layer handles HTTP errors
   - Frontend displays user-friendly error messages

### Frontend Design

1. **Responsive Design**: Implemented using:
   - CSS Grid and Flexbox for flexible layouts
   - Media queries for different screen sizes (mobile, tablet, desktop)
   - Relative units (rem, %) for scalable typography

2. **User Experience**:
   - Loading indicators for async operations
   - Clear error messages
   - Smooth transitions and hover effects
   - Accessible form inputs and buttons

3. **Modern CSS**:
   - CSS variables for consistent theming
   - Gradient backgrounds
   - Card-based layout with shadows
   - Smooth animations

### API Integration Choices

1. **OpenWeather API**: Selected because:
   - Free tier available
   - Comprehensive weather data
   - Reliable and well-documented
   - Provides all required fields (temperature, description, coordinates, feels-like, wind speed, country code, rain volume)

2. **News API**: Selected because:
   - Free tier available
   - Country-based filtering
   - Rich article data (images, descriptions, sources)
   - Enhances user experience by providing context about the location

## 🧪 Testing the API

You can test the API endpoints using:

1. **Browser**: Navigate to the URLs directly
2. **cURL**: Use command-line tool
   ```bash
   curl http://localhost:3000/api/weather/London
   ```
3. **Postman**: Import and test endpoints (see screenshot section)

## 📸 Screenshots

To complete your submission, please take screenshots of:

1. **Web Application**: The main interface showing weather data and news
2. **Postman/API Testing**: API responses from the endpoints
3. **Responsive Design**: Application on different screen sizes (optional but recommended)

## 🔧 Troubleshooting

### Server won't start
- Ensure Node.js is installed: `node --version`
- Check if port 3000 is already in use
- Verify all dependencies are installed: `npm install`

### API errors
- Verify API keys are correctly set in `.env` file
- Check API key validity on respective API websites
- Ensure internet connection is active
- Check API rate limits (free tiers have usage limits)

### City not found
- Ensure city name is spelled correctly
- Try using the full city name with country code (e.g., "London, UK")
- Some city names may need alternative spellings

### News not loading
- News API free tier has rate limits
- Some country codes may not return results
- Check browser console for detailed error messages

## 📝 License

This project is created for educational purposes as part of Assignment 2.

## 👤 Author

Created as part of Assignment 2: Backend API Integration & Service Development

---

**Note**: Remember to add your `.env` file to `.gitignore` if committing to version control to protect your API keys!

