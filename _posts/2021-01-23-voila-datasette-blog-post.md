---
toc: true
layout: post
description: voila datasette blog post
categories: [blog posts]
title: Creating a daily monitoring dashboard and database for the stockmarket with voila and datasette
---

To create a daily updated dashboard which will be sent to your email daily, the following steps are needed:

+ Create a publically accessable database with datasette
+ Create an applicaiton which draws data from that database with voila and heroku
+ Set up a shell script on a crontab that will update the database and send you an email

```
start = pd.to_datetime('2018-01-01')
end = pd.to_datetime('today')

FXAIX_stock = web.DataReader('FXAIX', 'yahoo', start, end)
FXAIX_stock.head()

SP500_stock = web.DataReader('^GSPC', 'yahoo', start, end)
SP500_stock.head()

Russell_2000_stock = web.DataReader('^RUT', 'yahoo', start, end)
Russell_2000_stock.head()


stocks = pd.concat([SP500_stock['Open'], Russell_2000_stock['Open'], FXAIX_stock['Open']], axis = 1)

stocks.columns = ['SP500_stock','Russell_2000_stock', 'FXAIX_stock']

stocks.reset_index(level=0, inplace=True)
stocks
```


```
engine = db.create_engine('sqlite:///stocks.db')
connection = engine.connect()
metadata = db.MetaData()


stocks_table = db.Table('index_stocks_table', metadata, 
    db.Column('Date',db.Date, nullable=True, index=False),
    db.Column('SP500_stock',db.Integer, nullable=True),
    db.Column('Russell_2000_stock',db.Integer, nullable=True),
    db.Column('FXAIX_stock', db.Numeric, nullable=True)
)

metadata.create_all(engine) 
```




```

stocks.to_sql('index_stocks_table', con=engine, if_exists='replace', index=False)
```



```
sql = "SELECT * FROM index_stocks_table LIMIT 10"
cnxn = connection
df = pd.read_sql(sql, cnxn)
print(df.head(10))
```



```
#!/bin/bash
python stocks.py
datasette publish heroku -n heroku-app stocks.db
```




```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline




```
df = pd.read_csv('https://herokuappname.herokuapp.com/stocks/index_stocks_table.csv?_size=max')
df['FXAIX_stock'].plot(figsize = (12, 8))
plt.title('S&P 500 Index')

df[["Date", "SP500_stock", 'Russell_2000_stock']].plot(figsize = (12, 8))
plt.title('S&P 500 and Russell_2000')
```

echo 'numpy
pandas
ipywidgets
matplotlib
voila
ipykernel
matplotlib
quandl
statsmodels
datetime' > requirements.txt



```
git add . && git commit -m 'update' && git push heroku master && git pull
```


