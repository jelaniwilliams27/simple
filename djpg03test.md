# How to Use Public APIs
Public APIs are accessible and available to everyone for free to enhance their own applications. Different types of data journalists will use different public APIs depending on their given area of research. Below are steps on how to utilize public APIs for data journalism.

The code shown in the following steps is included to show examples of what code in the different steps looks like. For this document, it is not critical to learn the syntax, but it is important to become familiar with the format.
### Step 1 - Find and Read the API Documentation

* Every reputable API should be accompanied by a Readme file that describes the API's purpose, how to use it, licensing details, credits, and and other information.has a base URL and endpoints that define what data you can access.

* The documentation describes:
	- Available data (e.g. reports, quantifiable details)
	- Parameters (e.g. location, date range)
	- API Key Requirements (e.g. fully open, require registration)
		
### Step 2 - Request an API Key (if required)

* Some APIs require a sign up to obtain a free key designed to identify the user, prevents abuse, and tracks usage limits.
* The following Python code shows the key in an API request:
		
		params = {"api_key": "YOUR_KEY_HERE"}

### Step 3 - Make a Request

* Python has a built-in requests library. The simplest call looks like the following:

		import requests
		response = requests.get("https://api.example.com/data", params={"param": "value"})

* Data is typically returned in JSON format, which is structured like a Python dictionary.

### Step 4 - Inspect the Response

* Always check the status code to ensure the request worked (see the following example):

		if response.status_code == 200:
			print("Success!")
		else:
			print("Error:", response.status_code)


* Next, the raw JSON API data from the server may be viewed:

		data = response.json()
		print(data)

### Step 5 - Load the Data into a Python Object

* The JSON response is read as a Python dictionary or list. Example:

		data = response.json()

* Pandas is a Python library used to analyze data. JSON data is loaded into Pandas DataFrame for analysis:

		import pandas as pd
		df = pd.DataFrame(data)

* At this point, "df" is used like a spreadsheet in memory to sort, filter, and graph data.

### Step 6 - Clean and Analyze the Data

* Cleaning the data ensures that all values can be analyzed uniformally per data type for smooth analysis. Convert text fields to numbers or dates:

		df["value"] = df["value"].astype(float)
		df["date"] = pd.to_datetime(df["date"])

* Perform filtering, grouping, or calculations with the following:

		df.groupby("state")["POP"].sum()

* Create visualizations using libraries like matplotlib or plotly.

### Step 7 - Save or Export the Data

* Cleaned data may be saved for later use:

		df.to_csv("population_data.csv", index=False)

* The data may ben exported to Excel or JSON:

		df.to_excel("output.xlsx")

* One or more of the following options are typical next steps for handling the exported data:
	- Load it into Google Sheets for editors to review
	- Import it into Tableau or Flourish for interactive charts
	- Store it in a database for larger projects
	- Publish it via data journalism dashboards or GitHub repositories