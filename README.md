# Maven Mega Mart

### not completed - still in progress

Maven MegaMart is a multinational corporation that operates a chain of retail and grocery stores. They recently received a sample of data from a new retailer 
they’re looking to acquire, and they need to identify and deliver key insights about their sales history.<br/>
Our task is to analyze over 2 million transactions by product, household, and store to get a better understanding of the retailer’s main strengths. 
From there, you need to review the company’s discount scheme to assess whether they can expect to attract customers without losing margin. <br/>
We are using Python to:
- Read in multiple flat files efficiently.
- Join tables to provide a single source of information.
- Shape & aggregate sales data to calculate KPIs.
- Visualize the data to communicate the findings.

We will be using few DataFrames:
- Transactions: the primary DaraFrame 
- Products: contains the data of Brand and Department for the category of our data.
- Households: to analyze our sales figures by some of these demographic qualities.

We also going to combine our data in some way to perform these analysis.

### Key Objectives
- Read in data from multiple CSV files
- Explore the data ( millions of rows )
- Join multiple DataFrames
- Filter, sort, and aggregate the data to pipoint and summarize important information
- Work with datetime fields to analyze time series
- Build plots to communicate key insights
- Optimize the import workflow
- Write out summary tables for stakeholders


## Read the data and change the columns' data type

### transaction dataframe

```
path = "data/project_transactions.csv"
cols = ["household_key", "BASKET_ID", "DAY", "PRODUCT_ID", "QUANTITY", "SALES_VALUE"]
dtypes = {
    "DAY": "Int64",
    "QUANTITY": "Int32",
    "STORE_ID": "Int32"
}

transactions = pd.read_csv(path, dtype=dtypes, usecols=cols)
```

![01.png](resources/01.png)

now we need to create Data column based on the value of 'DAY' for `transaction` table and drop the `"DAY"` column
```
transactions = transactions.assign(
    Date = (pd.to_datetime("2016", format='%Y')
    + pd.to_timedelta(transactions["DAY"].sub(1).astype(str) + ' days'))
).drop(["DAY"], axis=1)
```

![02.png](resources/02.png)
