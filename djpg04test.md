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

#### Goal: 
To analyze public spending, legislation, crime, and demographics.

#### Examples of APIs used:
* U.S. Census Bureau API - Population, income, housing, race, education
* Federal Election Commission (FEC) API - Campaign donations and expenditures
* Data.gov APIs - Federal datasets across hundreds of topics
* City/County open-data APIs - Local budgets, permits, police calls, or property records
	
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
	
#### Insight Provided: 
Note which states gained or lost the most people year-over-year.
___

## Economics and Finance

#### Goal:
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
	
#### Insight Provided: 
Analyze unemployment rate trends over time and correlate with policy changes.
___


## Environment and Climate

#### Goal:
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

	
#### Insight Provided: 
Monitor air quality trends and compare between urban and rural regions.
___

## Public Safety and Justice

#### Goal:
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

	
#### Insight Provided: 
Monitor air quality trends and compare between urban and rural regions.
___


## Health Data

#### Goal:
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

	
#### Insight Provided: 
Track new COVID-19 cases and deaths by state and date.
___