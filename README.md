Lets`s read apache_logs  with known format. So, we can use regexp in separator


```python
import re
import pandas as pd

data = pd.read_csv(
    'apache_logs',
    sep=r'\s(?=(?:[^"]*"[^"]*")*[^"]*$)(?![^\[]*\])',
    engine='python',
    na_values='-',
    header=None,
    usecols=[0, 3, 4, 5, 6, 7, 8],
    names=['ip', 'time', 'request', 'status', 'size', 'referer', 'user_agent'])
```

Got DataFrame


```python
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ip</th>
      <th>time</th>
      <th>request</th>
      <th>status</th>
      <th>size</th>
      <th>referer</th>
      <th>user_agent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>83.149.9.216</td>
      <td>[17/May/2015:10:05:03 +0000]</td>
      <td>"GET /presentations/logstash-monitorama-2013/i...</td>
      <td>200</td>
      <td>203023.0</td>
      <td>"http://semicomplete.com/presentations/logstas...</td>
      <td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>83.149.9.216</td>
      <td>[17/May/2015:10:05:43 +0000]</td>
      <td>"GET /presentations/logstash-monitorama-2013/i...</td>
      <td>200</td>
      <td>171717.0</td>
      <td>"http://semicomplete.com/presentations/logstas...</td>
      <td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>83.149.9.216</td>
      <td>[17/May/2015:10:05:47 +0000]</td>
      <td>"GET /presentations/logstash-monitorama-2013/p...</td>
      <td>200</td>
      <td>26185.0</td>
      <td>"http://semicomplete.com/presentations/logstas...</td>
      <td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>83.149.9.216</td>
      <td>[17/May/2015:10:05:12 +0000]</td>
      <td>"GET /presentations/logstash-monitorama-2013/p...</td>
      <td>200</td>
      <td>7697.0</td>
      <td>"http://semicomplete.com/presentations/logstas...</td>
      <td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>83.149.9.216</td>
      <td>[17/May/2015:10:05:07 +0000]</td>
      <td>"GET /presentations/logstash-monitorama-2013/p...</td>
      <td>200</td>
      <td>2892.0</td>
      <td>"http://semicomplete.com/presentations/logstas...</td>
      <td>"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_1...</td>
    </tr>
  </tbody>
</table>
</div>



Filtering dataframe by column status with value = 404


```python
counted = data.loc[data['status'] == '404']['ip'].value_counts()
```

And printing 10, 20 top lines of them


```python
counted.head(10)
```




    208.91.156.11     60
    144.76.95.39      14
    91.236.75.25       8
    66.249.73.135      8
    75.97.9.59         6
    176.92.75.62       5
    130.237.218.86     4
    84.137.208.44      4
    198.245.61.43      3
    78.173.140.106     3
    Name: ip, dtype: int64




```python
counted.head(20)
```




    208.91.156.11      60
    144.76.95.39       14
    91.236.75.25        8
    66.249.73.135       8
    75.97.9.59          6
    176.92.75.62        5
    130.237.218.86      4
    84.137.208.44       4
    198.245.61.43       3
    78.173.140.106      3
    188.165.243.45      3
    95.78.54.93         3
    195.250.34.144      3
    111.199.235.239     2
    144.76.194.187      2
    122.166.142.108     2
    193.244.33.47       2
    89.107.177.18       2
    204.62.56.3         2
    212.90.148.107      2
    Name: ip, dtype: int64




```python

```
