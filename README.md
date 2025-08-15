# Live Weather Dashboard with Power BI
# How to Develop a Power BI Dashboard with WeatherAPI
  Power BI is a fantastic tool for visualizing data — and you can easily integrate live weather data into your reports too. In this blog, we’ll walk you through the process of building a real-time weather dashboard powered by WeatherAPI, and then we’ll add some Air   Quality Index (AQI) indicators for a richer dashboard experience.

# 🎯 Why WeatherAPI?
  WeatherAPI.com is a simple and powerful service that returns live, historical, and forecast weather data — perfect for Power BI. The data is available in JSON format, making it easy to process and transform.

# 🛠️ Prerequisites
  ✅ A free or paid account on WeatherAPI.com
  
  ✅ Power BI Desktop installed
  
  ✅ Basic Power BI data model knowledge

# 🔑 Step 1: Get Your WeatherAPI Key
  Sign up at WeatherAPI.com, then copy your API key.
  
  You’ll use this key to authenticate API calls.

# 🌐 Step 2: Build the API URL
  For current weather data, use:
  
  https://api.weatherapi.com/v1/current.json?key=YOUR_API_KEY&q=CITY_NAME

# 🧠 Step 3: Connect Power BI to WeatherAPI
  Open Power BI Desktop.
  
  Click Get Data → Web.
  
  Enter your WeatherAPI URL.
  
  Click OK.

# 🧹 Step 4: Transform the Data
  Power BI will show a preview in the Power Query Editor:
  
  Expand the current record.
  
  Expand sub-records like condition or air_quality.
  
  Rename columns for clarity.
  
  Click Close & Apply.

# 📊 Step 5: Build Your Dashboard
  Add:
  
  ✅ Cards for temperature, humidity, etc.
  
  ✅ Gauges for wind speed.
  
  ✅ Charts for daily variations.
  
  And you can also set up filters/slicers for different cities.

# 🎨 Step 6: Styling & Interactivity
  Insert icons representing the current weather.
  
  Plot the map visual with city locations.
  
  Allow your users to select cities dynamically.

# ⚡ Step 7: Adding AQI Indicators with Reusable Measures
  You can easily incorporate Air Quality Index (AQI) data into your report using the current.air_quality part of the WeatherAPI response.
  
  Here’s a quick Power BI DAX pattern you can copy-paste and adapt to your needs:

### 🎨 Generic Template for AQI Color:
  DAX
  
    AQI Color TEMPLATE =
    VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]),0)
    RETURN
    SWITCH(
    TRUE(),
    AQI <= 50, "#43d946",
    AQI <= 100, "#fff570",
    AQI <= 150, "#ff9800",
    AQI <= 200, "#d99343",
    AQI <= 300, "#ff5b0f",
    "#d95243"
    )
  
  💡 Simply copy this measure and replace COLUMN_NAME with the air quality column you want to check — for example:
  
  pm2_5
  co
  no2

### 🎨 Generic Template for AQI Suggestion:
DAX

	AQI Suggestion TEMPLATE =
	VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]),0)
	RETURN
	SWITCH(
	TRUE(),
	AQI <= 50, "Air is clean and healthy",
	AQI <= 100, "Acceptable air quality, stay active",
	AQI <= 150, "Sensitive groups should reduce outdoor time",
	AQI <= 200, "Limit prolonged outdoor exertion",
	AQI <= 300, "Avoid outdoor activity if possible",
	"Stay indoors, wear a mask if outside"
	)

### 🎨 Generic Template for AQI Status:
DAX

	AQI Status TEMPLATE =
	VAR AQI = ROUND(SELECTEDVALUE('Current'[current.air_quality.COLUMN_NAME]),0)
	RETURN
	SWITCH(
	TRUE(),
	AQI <= 50, "Good",
	AQI <= 100, "Moderate",
	AQI <= 150, "Unhealthy for Sensitive",
	AQI <= 200, "Unhealthy",
	AQI <= 300, "Very Unhealthy",
	"Hazardous"
	)

✅ Again, just replace COLUMN_NAME with the pollutant of interest.

# 💡 Quick Tip:
Keep these generic DAX measures as templates — so when you want to add AQI visualizations for new pollutants like so2, no2, or o3, you only need to copy-paste and tweak one column name.

# 🎉 Conclusion
By integrating WeatherAPI into Power BI, you can create a dynamic weather dashboard with live data, then enrich it with custom AQI visualizations — all in a few easy steps. With these reusable DAX measures, your dashboard stays scalable, maintainable, and easy to enhance as your requirements grow.
