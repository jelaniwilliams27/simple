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
	
#### Sample API
	
	import requests
	import pandas as pd

	_Example: Get 2023 population by state from U.S. Census API_
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