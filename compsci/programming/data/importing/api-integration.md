---
tags: programming, data
---

> connecting your code to real-world data sources
### what are API's?
- application programming interfaces - standardized ways for different software systems to communicate
- think of them as "data vending machines"... you put in a request, get back structured data
- most modern data (stock prices, economic indicators, social media analytics) is accessed through API's

### REST API fundamentals
- REST (Representational State Transfer) - the most common API architecture

- HTTP methods
	- GET - retrieved data (most common for [[data-analysis]])
	- POST - send data to create something new
	- PUT/PATCH - update existing data
	- DELETE - remove data

### authentication methods
- API keys - unique identifiers
	- OAuth - more complex  but secure token-based authentication
	- Headers - where you include your credentials

### rate limiting & error handling
- rate limits - APIs restrict how many requests per minute/hour
- status codes
	- 200 = success
	- 401 = unauthorized (bad api key)
	- 429 = too many requests (rate limit)
	- 500 = server error

### data pipeline... from API to analysis in [[python]]
1. request data from api
2. parse JSON response
3. convert to [[compsci/programming/libraries/pandas|pandas]] DataFrame
4. clean and process data
5. analyze using your existing methods

### common data sources for your analysis
- financial data (alpha vantage, yahoo finance API, etc)
- economic indicators (FRED)
- crypto data (CoinGecko)
- social sentiment (reddit or X API)
 