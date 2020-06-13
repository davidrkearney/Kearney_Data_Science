---
toc: true
layout: post
description: 1st Markdown Post
categories: [markdown]
title: Data Science, Big Data and Healthcare Research
---
# Data Science, Big Data and Healthcare Research

## This post will consider the use of hive, spark, and for machine learning pipelines and workflows. Here's a footnote [^1].



```python
from alive_progress import alive_bar, showtime, show_bars, show_spinners, config_handler
config_handler.set_global(theme='ascii', spinner='notes', bar='solid')

with alive_bar(3) as bar:
    df = pd.read_csv('../../data/csvs/example.csv')
    bar('file read, printing file')
    print(df.head)
    bar('data printed ok, printing methods of data')
    print(dir(df))
    bar('process complete')



```



## Footnotes

[^1]: [links](https://www.markdownguide.org/cheat-sheet/)
