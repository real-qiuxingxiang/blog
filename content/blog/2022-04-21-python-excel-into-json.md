---
title: Python Excel 和 Json 互转
author: Q
type: post
date: 2022-04-21T07:07:05+00:00
url: /blog/1155
views:
  - 131
categories:
  - Programming
tags:
  - Python

---
## 一、Excel 转 Json

```python
import pandas
pandas.read_excel("Data.xlsx", sheet_name=0).to_json("1.json", orient="records", force_ascii=False)
```

## 二、Json 转 Excel

```python
import pandas
pandas.read_json("input.json",dtype=str).to_excel("output.xlsx")
```