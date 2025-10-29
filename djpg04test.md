# Key Research Fields
This section contains ten examples with APIs for different fields of research. Each example will contain a topic area, the data journalist's goal within that area, what the API searches for, and sample API code. The following areas will be highlighted in this section:

- Government and Civic
- Economy
- Environment
- Justice
- Health
- Transport
- Social Media
- Housing
- Education

## Government and Civic Data

#### :white_check_mark: Goal: 
To analyze public spending, legislation, crime, and demographics.

#### Examples of APIs used:
* U.S. Census Bureau API - Population, income, housing, race, education
* Federal Election Commission (FEC) API - Campaign donations and expenditures
* Data.gov APIs - Federal datasets across hundreds of topics
* City and County open-data APIs - Local budgets, permits, police calls, or property records
	
#### What each API looks for:
* Who funds which political candidates
* Changes in population or economic trends
* How cities spend taxpayer money
* Public safety or zoning trends
	
#### Sample API:
	
	import requests
	import pandas as pd

	# Example: Get 2023 population by state from U.S. Census API
	url = "https://api.census.gov/data/2023/pep/population"
	params = {
		"get": "NAME,POP",
		"for": "state:*"
	}
	response = requests.get(url, params=params)
	data = response.json()

	# Convert to DataFrame
	df = pd.DataFrame(data[1:], columns=data[0])
	df["POP"] = df["POP"].astype(int)
	df = df.sort_values("POP", ascending=False)

	print(df.head())
	
#### :mag: Insight Provided: 
Note which states gained or lost the most people year-over-year.
___

## Economics and Finance

#### :white_check_mark: Goal:
To report on economic trends, inequality, and inflation.

#### Examples of APIs used:
* Federal Reserve (FRED) API - Interest rates, employment, GDP
* SEC’s EDGAR API - Corporate filings and executive compensation
* World Bank / IMF APIs - Global economic indicators
	
#### What each API looks for:
* Wage and employment trends
* Market volatility indicators
* Regional economic disparities
* Financial transparency or corruption
	
#### Sample API:
	
	import requests
	import pandas as pd

	API_KEY = "YOUR_FRED_API_KEY"
	url = "https://api.stlouisfed.org/fred/series/observations"
	params = {
		"series_id": "UNRATE",  # U.S. unemployment rate
		"api_key": API_KEY,
		"file_type": "json"
	}

	response = requests.get(url, params=params)
	data = response.json()

	df = pd.DataFrame(data["observations"])
	df["value"] = df["value"].astype(float)
	df["date"] = pd.to_datetime(df["date"])

	print(df.tail())
	
#### :mag: Insight Provided: 
Analyze unemployment rate trends over time and correlate with policy changes.
___


## Environment and Climate

#### :white_check_mark: Goal:
To report on climate change, pollution, disasters, or resource management.

#### Examples of APIs used:
* NOAA Climate Data API - Temperature, storms, droughts
* EPA AirNow API - Air quality data (AQI)
* USGS Earthquake API - Seismic activity
* NASA Earth Data APIs - Satellite imagery and global temperature data
	
#### What each API looks for:
* Climate trends over time (e.g. rising temperatures)
* Air or water quality by region
* Natural disaster frequency or impact
* Effects of policy on emissions

#### Sample API:
	
	import requests
	import pandas as pd

	API_KEY = "YOUR_AIRNOW_API_KEY"
	url = "https://www.airnowapi.org/aq/observation/latLong/current/"
	params = {
		"format": "application/json",
		"latitude": 39.2904,  # Example: Baltimore, MD
		"longitude": -76.6122,
		"distance": 25,
		"API_KEY": API_KEY
	}

	response = requests.get(url, params=params)
	data = response.json()

	df = pd.DataFrame(data)
	print(df[["ReportingArea", "AQI", "Category"]])

	
#### :mag: Insight Provided: 
Monitor air quality trends and compare between urban and rural regions.
___

## Public Safety and Justice

#### :white_check_mark: Goal:
To uncover patterns in policing, incarceration, or emergency response.

#### Examples of APIs used:
* FBI Crime Data API - Crime rates by type and geography
* City police open-data APIs - Arrests, incidents, calls for service
* DOJ or court APIs - Sentencing data or case outcomes
	
#### What each API looks for:
* Disparities in policing or sentencing
* Trends in violent vs. property crimes
* Local responses to public safety issues

#### Sample API:
	
	import requests
	import pandas as pd

	API_KEY = "YOUR_FBI_API_KEY"
	url = "https://api.usa.gov/crime/fbi/sapi/api/summarized/state/MD/violent-crime/2018/2023"
	params = {"API_KEY": API_KEY}

	response = requests.get(url, params=params)
	data = response.json()

	df = pd.DataFrame(data["results"])
	print(df[["year", "offense", "actual"]])

	
#### :mag: Insight Provided: 
Monitor air quality trends and compare between urban and rural regions.
___


## Health Data

#### :white_check_mark: Goal:
To track health trends, disease outbreaks, and healthcare access.

#### Examples of APIs used:
* CDC API - Case counts, mortality data, public health metrics
* WHO API - Global health indicators
* OpenFDA API - Drug recalls, side effects, and approvals
	
#### What each API looks for:
* COVID-19 trends or vaccination rates
* Geographic or demographic disparities in healthcare
* Medication safety or recall frequency

#### Sample API:
	
	import requests
	import pandas as pd

	url = "https://data.cdc.gov/resource/9mfq-cb36.json"
	params = {"state": "MD", "$limit": 10}

	response = requests.get(url, params=params)
	data = response.json()

	df = pd.DataFrame(data)
	print(df[["submission_date", "new_case", "new_death"]])

	
#### :mag: Insight Provided: 
Track new COVID-19 cases and deaths by state and date.
___


## Transportation and Infrastructure

#### :white_check_mark: Goal:
To report on mobility, safety, and infrastructure investment.

#### Examples of APIs used:
* U.S. DOT / NHTSA APIs - Traffic accidents, recalls, infrastructure spending
* Transit APIs (e.g. MTA, WMATA) - Public transit ridership and delays
* FAA / FlightAware APIs - Flight paths and delays
	
#### What each API looks for:
* Accident rates or causes
* Public transportation usage trends
* Infrastructure gaps in underserved areas

#### Sample API:
	
	import requests
	import pandas as pd

	url = "https://api.nhtsa.gov/recalls/recallsByVehicle"
	params = {"make": "Toyota", "model": "Camry", "year": 2021}

	response = requests.get(url, params=params)
	data = response.json()

	df = pd.DataFrame(data["results"])
	print(df[["Component", "Summary"]].head())

#### :mag: Insight Provided: 
Identify recall trends by brand or model for consumer reporting.
___


## Social Media and Digital Behavior

#### :white_check_mark: Goal:
To measure public sentiment, misinformation, and online activity.

#### Examples of APIs used:
* X / Twitter API, Reddit API, YouTube Data API
* CrowdTangle API (Facebook/Instagram data)
	
#### What each API looks for:
* How topics or hashtags trend over time
* Misinformation spread or coordinated activity
* Sentiment toward policies or events

#### Sample API:
	
	import requests
	import pandas as pd

	# Using Pushshift (historical Reddit API)
	url = "https://api.pushshift.io/reddit/search/submission/"
	params = {
		"q": "climate change",
		"subreddit": "news",
		"size": 10,
		"sort": "desc",
		"sort_type": "score"
	}

	response = requests.get(url, params=params)
	data = response.json()

	df = pd.DataFrame(data["data"])
	print(df[["title", "score", "url"]])
	
#### :mag: Insight Provided: 
Analyze which topics related to “climate change” gain the most traction.
___


## Housing and Real Estate

#### :white_check_mark: Goal:
To analyze housing affordability and gentrification.

#### Examples of APIs used:
* Realtor APIs - Home prices, rental costs
* HUD API - Affordable housing availability
* Local property tax APIs
	
#### What each API looks for:
* Home price trends vs. income growth
* Eviction or foreclosure rates
* Changes in neighborhood demographics

#### Sample API:
	
	import requests
	import pandas as pd

	url = "https://www.huduser.gov/hudapi/public/fmr/data/2023"
	params = {"state": "MD"}

	response = requests.get(url, params=params)
	data = response.json()

	df = pd.DataFrame(data["data"])
	print(df[["county_name", "fmr_2br"]].head())

	
#### :mag: Insight Provided: 
Compare average rent prices across Maryland counties.

___

## Education

#### :white_check_mark: Goal:
To investigate funding, outcomes, and equity in schools.

#### Examples of APIs used:
* U.S. Department of Education APIs - School performance, graduation rates
* IPEDS API - College and university data
* State education open data
	
#### What each API looks for:
* Achievement gaps across regions
* School funding and resource allocation
* Trends in enrollment or tuition

#### Sample API:
	
	import requests
	import pandas as pd

	API_KEY = "YOUR_ED_API_KEY"
	url = "https://api.data.gov/ed/collegescorecard/v1/schools"
	params = {
		"api_key": API_KEY,
		"fields": "school.name,location.state,latest.student.size,latest.cost.tuition.in_state",
		"school.state": "MD",
		"per_page": 5
	}

	response = requests.get(url, params=params)
	data = response.json()

	df = pd.DataFrame(data["results"])
	print(df)
	
#### :mag: Insight Provided: 
Compare tuition costs and enrollment sizes for Maryland colleges.