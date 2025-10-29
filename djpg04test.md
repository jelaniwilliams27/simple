# Key Research Fields
This section contains ten examples with APIs for different fields of research. Each example will contain a topic area, the data journalist's goal within that area, what the API searches for, and sample API code.

### Government and Civic Data
Goal: To analyze public spending, legislation, crime, and demographics.

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

### Government and Civic Data
Goal: To report on economic trends, inequality, and inflation.

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