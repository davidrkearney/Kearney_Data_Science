---
toc: true
layout: post
description: Data Sources Blog Posts
categories: [Data Sources]
title: Data Sources
---

```
import pandas as pd
url = 'https://raw.githubusercontent.com/davidrkearney/Kearney_Data_Science/master/_notebooks/df_panel_fix.csv'
df = pd.read_csv(url, error_bad_lines=False)
df
```

