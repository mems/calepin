- https://code.google.com/p/yahoo-finance-managed/wiki/csvHistQuotesDownload
- https://www.google.com/finance/converter?a=1&from=%@&to=%@
- Google Finance https://code.google.com/p/googlefinance/source/browse/trunk/GoogleFinanceDemo/Finance.Web/HistoricalPrices.cs?r=43#47

		// http://www.google.com/finance/historical?q=NASDAQ:CSCO&histperiod=daily
		// http://www.google.com/finance/historical?q=NASDAQ:CSCO&histperiod=weekly
		// http://www.google.com/finance/historical?cid=99624&startdate=Oct+7%2C+2004&enddate=Oct+6%2C+2009&histperiod=weekly
		// http://www.google.com/finance/historical?cid=99624&startdate=Oct+7%2C+2004&enddate=Oct+6%2C+2009
    	
		// csv output file.
		// http://www.google.com/finance/historical?cid=99624&startdate=Oct+7%2C+2004&enddate=Oct+6%2C+2009&output=csv
    	
		/*
		cid = Company Id
		startdate = Start date of the historical prices
		enddate = End date of the historical prices
		histperiod = weekly or daily history periods
		start = index on which to display the historical price
		num = number of historical prices to display (this has some max like 100 or 200)
		output = output the data in a format (I think it currently supports CSV only)
    	
		http://www.google.com/finance/historical?cid=700146&startdate=Oct+10%2C+2008&enddate=Oct+9%2C+2009&output=csv
    	
		http://www.google.com/finance/historical?cid=700146&startdate=Oct+9%2C+2008&enddate=Oct+9%2C+2009&histperiod=weekly&output=csv
    	
		http://www.google.com/finance/historical?cid=700146&startdate=Oct%209%2C%202008&enddate=Oct%209%2C%202009&histperiod=weekly&start=0&num=20
		*/
	 