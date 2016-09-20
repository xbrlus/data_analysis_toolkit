---
title: Balance Sheet Comparison Template
keywords: template
toc: false
summary: "This section contains balance sheet comparison worksheets using XBRL data."
sidebar: templates_sidebar
permalink: BSCompareTemplate.html
folder: templates
---

Google Sheet and Excel versions of the balance sheet template linked here can be used for your analysis by doing the following:

1. Create an online copy of the <a href="https://docs.google.com/spreadsheets/d/1NT6dPSJAu8GJX8pq-MlZ17ORixNW7nkW0pdIMq90nH4/edit?usp=sharing" target="_blank">Google Sheet</a> or download [Excel 2013 or later](https://github.com/xbrlus/data_analysis_toolkit/blob/master/templates/BSCompare.xlsx?raw=true) and/or [Excel legacy](https://github.com/xbrlus/data_analysis_toolkit/blob/master/templates/BSCompare.xlsm?raw=true) files to your computer. 

2. Replace the demo API key with your valid API key in the sheet (get a free API key from XBRL US at http://xbrl.us/apirequest). The demo key will expire, so copy your own key into the cell to replace the temporary API key.

3. Customize the analysis by changing the green cells for ticker symbol and time periods requested.

### Notes 
 The Google Sheet templates use [custom functions](gsheetFunctions) to pull the values from the API.  To get a copy of these functions take a copy of the spreadsheet using File>Make a Copy. This will duplicate the spreadsheets with  the custom functions.  These functions allow you to make up to 20,000 calls to the API.  In addition the function caches the results to conserve the number of calls made. The cache is flushed after 6 hours.
