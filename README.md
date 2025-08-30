# Fitness Dashboard with Power BI


# 🎯 Why WeatherAPI?
  WeatherAPI.com is a simple and powerful service that returns live, historical, and forecast weather data — perfect for Power BI. The data is available in JSON format, making it easy to process and transform.

# 🛠️ Prerequisites
  
  ✅ Power BI Desktop installed
  
  ✅ Basic Power BI data model knowledge
  
# 🪜 Steps
### ✅ Import fitness and membership data
Bringing in user profiles, activity logs, membership details, etc.

### ✅ Create different KPIs using DAX measures
Calculating metrics like BMR, TDEE, BMI, Weight Loss Calories, Active vs Expired Members, Renewal Rate, etc.

### ✅ Track membership progress with dates
Using date columns (Start Date, Expiry Date, Renewal Date) to calculate active vs expired membership status.

### ✅ Visualize active vs expired members
Pie chart / bar chart showing membership distribution.

Could even include trend over time.

### ✅ Build custom visuals like an SVG progress bar
Showing progress toward weight goal, calorie target, or membership completion percentage.

# Few important Measures:
### 🎨 SVG BarChart for Membership Period
  
	SVG_BarChart = 
	VAR ProgressValue = [ProgressPercentage]
	VAR BarWidth = 260
	VAR ProgressWidth = BarWidth * ProgressValue
	VAR Select_Color = SELECTEDVALUE(ColorCodes[Codes])
	VAR SVG_Data_URL = "data:image/svg+xml;utf8,"
	VAR SVG =
		"<svg width='400' height='40' xmlns='http://www.w3.org/2000/svg'>" &
		"<rect x='10' y='10' width='" & BarWidth & "' height='20' rx='10' ry='10' fill='#555' />" &
		"<rect x='10' y='10' width='" & ProgressWidth & "' height='20' rx='10' ry='10' fill='" & Select_Color & "' />" &
		"<text x='330' y='25' font-family='Arial' font-size='20' font-weight='bold' fill='#E6E6E6' text-anchor='end' alignment-baseline='middle'>" &
			ROUND(ProgressValue*100, 0) & "%" &
		"</text>" &
		"</svg>"
	RETURN
		SVG_Data_URL & SVG

### 🎨 BMI:

	BMI = 
	VAR _Weight = SELECTEDVALUE('Weight'[Weight])   // in kg
	VAR _Height = SELECTEDVALUE(Height[Height])   // in cm
	RETURN
	    DIVIDE(_Weight, (_Height / 100) ^ 2)
	
### 🎨 BMR:
	BMR = 
	VAR _Gender = SELECTEDVALUE('Members'[Gender])   // "Male" or "Female"
	VAR _Age    = SELECTEDVALUE(Age[Age])      // in years
	VAR _Height = SELECTEDVALUE(Height[Height])   // in cm
	VAR _Weight = SELECTEDVALUE('Weight'[Weight])   // in kg
	VAR Result =
	    SWITCH(
	        TRUE(),
	        _Gender = "Male",   10 * _Weight + 6.25 * _Height - 5 * Age + 5,
	        _Gender = "Female", 10 * _Weight + 6.25 * _Height - 5 * Age - 161,
	        BLANK()
	    )
	RETURN Result
 ### 🎨 TDEE:
	TDEE = 
	VAR BMRValue = [BMR]
	VAR ActivityFactor =
	    SELECTEDVALUE(Slider_Activity[ActivityFactor])
	RETURN
	    BMRValue * ActivityFactor


# 💡 Quick Tip:
Keep these generic DAX measures as templates for reuse.

# 🎉 Conclusion
This Power BI Fitness Dashboard is a great project to learn how to:

🔆 Write DAX measures

🔆 Track KPIs for a fitness/gym business

🔆 Create interactive dashboards with custom visuals

🔆 Present your work in a professional way
