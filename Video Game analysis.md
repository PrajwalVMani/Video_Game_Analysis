Importing required libraries


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

Loading the File


```python
df = pd.read_csv("D:/Power BI Stuff/vgsales.csv")
```

Checking to see if the file loaded properly


```python
df.head()
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
      <th>Rank</th>
      <th>Name</th>
      <th>Platform</th>
      <th>Year</th>
      <th>Genre</th>
      <th>Publisher</th>
      <th>NA_Sales</th>
      <th>EU_Sales</th>
      <th>JP_Sales</th>
      <th>Other_Sales</th>
      <th>Global_Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Wii Sports</td>
      <td>Wii</td>
      <td>2006.0</td>
      <td>Sports</td>
      <td>Nintendo</td>
      <td>41.49</td>
      <td>29.02</td>
      <td>3.77</td>
      <td>8.46</td>
      <td>82.74</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Super Mario Bros.</td>
      <td>NES</td>
      <td>1985.0</td>
      <td>Platform</td>
      <td>Nintendo</td>
      <td>29.08</td>
      <td>3.58</td>
      <td>6.81</td>
      <td>0.77</td>
      <td>40.24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Mario Kart Wii</td>
      <td>Wii</td>
      <td>2008.0</td>
      <td>Racing</td>
      <td>Nintendo</td>
      <td>15.85</td>
      <td>12.88</td>
      <td>3.79</td>
      <td>3.31</td>
      <td>35.82</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Wii Sports Resort</td>
      <td>Wii</td>
      <td>2009.0</td>
      <td>Sports</td>
      <td>Nintendo</td>
      <td>15.75</td>
      <td>11.01</td>
      <td>3.28</td>
      <td>2.96</td>
      <td>33.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Pokemon Red/Pokemon Blue</td>
      <td>GB</td>
      <td>1996.0</td>
      <td>Role-Playing</td>
      <td>Nintendo</td>
      <td>11.27</td>
      <td>8.89</td>
      <td>10.22</td>
      <td>1.00</td>
      <td>31.37</td>
    </tr>
  </tbody>
</table>
</div>



Checking the information of the data present


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 16598 entries, 0 to 16597
    Data columns (total 11 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   Rank          16598 non-null  int64  
     1   Name          16598 non-null  object 
     2   Platform      16598 non-null  object 
     3   Year          16327 non-null  float64
     4   Genre         16598 non-null  object 
     5   Publisher     16540 non-null  object 
     6   NA_Sales      16598 non-null  float64
     7   EU_Sales      16598 non-null  float64
     8   JP_Sales      16598 non-null  float64
     9   Other_Sales   16598 non-null  float64
     10  Global_Sales  16598 non-null  float64
    dtypes: float64(6), int64(1), object(4)
    memory usage: 1.4+ MB
    

Here we see that we have missing values in 2 of the fields namely, Year and Publisher. We also see that the Dtype for the Year variable is Float rather than date.


```python
df.isnull().sum()
```




    Rank              0
    Name              0
    Platform          0
    Year            271
    Genre             0
    Publisher        58
    NA_Sales          0
    EU_Sales          0
    JP_Sales          0
    Other_Sales       0
    Global_Sales      0
    dtype: int64



We have 271 missing values in year and 58 missing from publisher


```python
df.describe()
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
      <th>Rank</th>
      <th>Year</th>
      <th>NA_Sales</th>
      <th>EU_Sales</th>
      <th>JP_Sales</th>
      <th>Other_Sales</th>
      <th>Global_Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>16598.000000</td>
      <td>16327.000000</td>
      <td>16598.000000</td>
      <td>16598.000000</td>
      <td>16598.000000</td>
      <td>16598.000000</td>
      <td>16598.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>8300.605254</td>
      <td>2006.406443</td>
      <td>0.264667</td>
      <td>0.146652</td>
      <td>0.077782</td>
      <td>0.048063</td>
      <td>0.537441</td>
    </tr>
    <tr>
      <th>std</th>
      <td>4791.853933</td>
      <td>5.828981</td>
      <td>0.816683</td>
      <td>0.505351</td>
      <td>0.309291</td>
      <td>0.188588</td>
      <td>1.555028</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>1980.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.010000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>4151.250000</td>
      <td>2003.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.060000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>8300.500000</td>
      <td>2007.000000</td>
      <td>0.080000</td>
      <td>0.020000</td>
      <td>0.000000</td>
      <td>0.010000</td>
      <td>0.170000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>12449.750000</td>
      <td>2010.000000</td>
      <td>0.240000</td>
      <td>0.110000</td>
      <td>0.040000</td>
      <td>0.040000</td>
      <td>0.470000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>16600.000000</td>
      <td>2020.000000</td>
      <td>41.490000</td>
      <td>29.020000</td>
      <td>10.220000</td>
      <td>10.570000</td>
      <td>82.740000</td>
    </tr>
  </tbody>
</table>
</div>



Which Genre have the most games in the given dataset? 


```python
a = df['Genre'].value_counts()
a.shape
```




    (12,)



As the above count of values does not have any columns apart from the index, in the subsequent plot index is used to plaot the graph.


```python
plt.figure(figsize=(15,10))
sns.countplot(data = df, x ='Genre', order= df['Genre'].value_counts().index)
plt.ylabel("Count of Genre")
plt.title("Genre with the most games")
```




    Text(0.5, 1.0, 'Genre with the most games')




    
![png](output_15_1.png)
    


From this we see that the action Genre is the highest produced with over 3000 copies.

Which Year had them ost game releases?



```python
b = df['Year'].value_counts()
print(b)
```

    2009.0    1431
    2008.0    1428
    2010.0    1259
    2007.0    1202
    2011.0    1139
    2006.0    1008
    2005.0     941
    2002.0     829
    2003.0     775
    2004.0     763
    2012.0     657
    2015.0     614
    2014.0     582
    2013.0     546
    2001.0     482
    1998.0     379
    2000.0     349
    2016.0     344
    1999.0     338
    1997.0     289
    1996.0     263
    1995.0     219
    1994.0     121
    1993.0      60
    1981.0      46
    1992.0      43
    1991.0      41
    1982.0      36
    1986.0      21
    1989.0      17
    1983.0      17
    1990.0      16
    1987.0      16
    1988.0      15
    1985.0      14
    1984.0      14
    1980.0       9
    2017.0       3
    2020.0       1
    Name: Year, dtype: int64
    


```python
plt.figure(figsize = (20,10))
sns.countplot(data = df, x = 'Year', order = df['Year'].value_counts().index)
plt.xticks(rotation = 90)
```




    (array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
            17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33,
            34, 35, 36, 37, 38]),
     [Text(0, 0, '2009.0'),
      Text(1, 0, '2008.0'),
      Text(2, 0, '2010.0'),
      Text(3, 0, '2007.0'),
      Text(4, 0, '2011.0'),
      Text(5, 0, '2006.0'),
      Text(6, 0, '2005.0'),
      Text(7, 0, '2002.0'),
      Text(8, 0, '2003.0'),
      Text(9, 0, '2004.0'),
      Text(10, 0, '2012.0'),
      Text(11, 0, '2015.0'),
      Text(12, 0, '2014.0'),
      Text(13, 0, '2013.0'),
      Text(14, 0, '2001.0'),
      Text(15, 0, '1998.0'),
      Text(16, 0, '2000.0'),
      Text(17, 0, '2016.0'),
      Text(18, 0, '1999.0'),
      Text(19, 0, '1997.0'),
      Text(20, 0, '1996.0'),
      Text(21, 0, '1995.0'),
      Text(22, 0, '1994.0'),
      Text(23, 0, '1993.0'),
      Text(24, 0, '1981.0'),
      Text(25, 0, '1992.0'),
      Text(26, 0, '1991.0'),
      Text(27, 0, '1982.0'),
      Text(28, 0, '1986.0'),
      Text(29, 0, '1989.0'),
      Text(30, 0, '1983.0'),
      Text(31, 0, '1990.0'),
      Text(32, 0, '1987.0'),
      Text(33, 0, '1988.0'),
      Text(34, 0, '1985.0'),
      Text(35, 0, '1984.0'),
      Text(36, 0, '1980.0'),
      Text(37, 0, '2017.0'),
      Text(38, 0, '2020.0')])




    
![png](output_19_1.png)
    


Year 2009 and 2008 had the most releases as compared to all the other years.

TOP 5 YEARS GAMES RELEASED BY GENRE


```python
plt.figure(figsize = (20,10))
sns.countplot(data = df , x = "Year", hue = "Genre", order = df.Year.value_counts().iloc[:5].index)
```




    <AxesSubplot:xlabel='Year', ylabel='count'>




    
![png](output_22_1.png)
    


From this we can see that Action genre has been doing well consistantly.

WHICH YEAR HAD THE HIGHEST SALES WORLDWIDE ?



```python
c = df.groupby('Year')['Global_Sales'].sum()
c = c.reset_index()
print(c)
c.shape
```

          Year  Global_Sales
    0   1980.0         11.38
    1   1981.0         35.77
    2   1982.0         28.86
    3   1983.0         16.79
    4   1984.0         50.36
    5   1985.0         53.94
    6   1986.0         37.07
    7   1987.0         21.74
    8   1988.0         47.22
    9   1989.0         73.45
    10  1990.0         49.39
    11  1991.0         32.23
    12  1992.0         76.16
    13  1993.0         45.98
    14  1994.0         79.17
    15  1995.0         88.11
    16  1996.0        199.15
    17  1997.0        200.98
    18  1998.0        256.47
    19  1999.0        251.27
    20  2000.0        201.56
    21  2001.0        331.47
    22  2002.0        395.52
    23  2003.0        357.85
    24  2004.0        419.31
    25  2005.0        459.94
    26  2006.0        521.04
    27  2007.0        611.13
    28  2008.0        678.90
    29  2009.0        667.30
    30  2010.0        600.45
    31  2011.0        515.99
    32  2012.0        363.54
    33  2013.0        368.11
    34  2014.0        337.05
    35  2015.0        264.44
    36  2016.0         70.93
    37  2017.0          0.05
    38  2020.0          0.29
    




    (39, 2)



INDEX TO BE RESET IN ORDER TO CONSIDER THE VALUES TO BE COLUMNS. IF REQUIRED CHANGE THE NAMES AS PER LIKING.


```python
plt.figure(figsize = (20,10))
sns.barplot(data = c, x = 'Year', y ='Global_Sales')
plt.xticks(rotation = 45)
plt.xlabel("Year")
plt.ylabel("Global Sales")
```




    Text(0, 0.5, 'Global Sales')




    
![png](output_27_1.png)
    


YEARS 2008,2009 AND 2007 ARE THE HIGHEST GROSSING WORLWIDE. wE ALSO SEE THAT 2006 HAS QUITE A HIGH REVENUE GIVEN THE FACT THAT IT DID NOT HAVE HIGH NUMBER OF RELEASES.

 Which genre game have the highest sale price globally


```python
d = df.groupby('Genre')['Global_Sales'].sum()
d = d.reset_index()
d = d.sort_values(by =['Global_Sales'], ascending = True)
print(d)
```

               Genre  Global_Sales
    11      Strategy        175.12
    1      Adventure        239.04
    5         Puzzle        244.95
    9     Simulation        392.20
    2       Fighting        448.91
    6         Racing        732.04
    3           Misc        809.96
    4       Platform        831.37
    7   Role-Playing        927.37
    8        Shooter       1037.37
    10        Sports       1330.93
    0         Action       1751.18
    


```python
plt.figure(figsize = (20,10))
sns.barplot(data = d, x= 'Genre', y = 'Global_Sales')

```




    <AxesSubplot:xlabel='Genre', ylabel='Global_Sales'>




    
![png](output_31_1.png)
    


We can see that action sports and shooter ( Surprisingly ) are the top 3 highest earners worldwide.

WHICH PLATFORM HAVE THE HIGHEST  SALES GLOBALLY?



```python
e = df.groupby('Platform')['Global_Sales'].sum()
e = e.reset_index()
e = e.sort_values(by = ['Global_Sales'], ascending = True)
print(e)
```

       Platform  Global_Sales
    14     PCFX          0.03
    9        GG          0.04
    1       3DO          0.10
    24     TG16          0.16
    25       WS          1.42
    12       NG          1.44
    22      SCD          1.87
    3        DC         15.97
    8       GEN         28.36
    21      SAT         33.59
    20      PSV         61.93
    27     WiiU         81.86
    0      2600         97.08
    30     XOne        141.06
    7        GC        199.36
    23     SNES        200.05
    10      N64        218.88
    2       3DS        247.46
    11      NES        251.07
    5        GB        255.45
    29       XB        258.26
    13       PC        258.82
    18      PS4        278.10
    19      PSP        296.28
    6       GBA        318.50
    15       PS        730.66
    4        DS        822.49
    26      Wii        926.71
    17      PS3        957.84
    28     X360        979.96
    16      PS2       1255.64
    


```python
plt.figure(figsize = (20,10))
sns.barplot(data = e, x = 'Platform', y = 'Global_Sales')
plt.xlabel("Platform",fontsize = 15)
plt.ylabel(" Total Global Sales",fontsize = 15)
plt.title("Total Sales By Paltform", fontsize = 20)
plt.xticks(rotation = 45)
```




    (array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
            17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30]),
     [Text(0, 0, 'PCFX'),
      Text(1, 0, 'GG'),
      Text(2, 0, '3DO'),
      Text(3, 0, 'TG16'),
      Text(4, 0, 'WS'),
      Text(5, 0, 'NG'),
      Text(6, 0, 'SCD'),
      Text(7, 0, 'DC'),
      Text(8, 0, 'GEN'),
      Text(9, 0, 'SAT'),
      Text(10, 0, 'PSV'),
      Text(11, 0, 'WiiU'),
      Text(12, 0, '2600'),
      Text(13, 0, 'XOne'),
      Text(14, 0, 'GC'),
      Text(15, 0, 'SNES'),
      Text(16, 0, 'N64'),
      Text(17, 0, '3DS'),
      Text(18, 0, 'NES'),
      Text(19, 0, 'GB'),
      Text(20, 0, 'XB'),
      Text(21, 0, 'PC'),
      Text(22, 0, 'PS4'),
      Text(23, 0, 'PSP'),
      Text(24, 0, 'GBA'),
      Text(25, 0, 'PS'),
      Text(26, 0, 'DS'),
      Text(27, 0, 'Wii'),
      Text(28, 0, 'PS3'),
      Text(29, 0, 'X360'),
      Text(30, 0, 'PS2')])




    
![png](output_35_1.png)
    


  CONCLUSION : PLATFORM WITH THE HIGHEST SALES IS PS2 FOLLOWED BY XBOX360 AND PS3. 

WHICH ARE THE TOP GENRE BASED ON PLATFORM ? 


```python
f = df.groupby(['Platform','Genre'])['Genre'].count().reset_index(name = 'Count of games')
f.sort_values(by = ['Count of games'], ascending = True)
print(f)
```

        Platform         Genre  Count of games
    0       2600        Action              61
    1       2600     Adventure               2
    2       2600      Fighting               2
    3       2600          Misc               5
    4       2600      Platform               9
    ..       ...           ...             ...
    288     XOne  Role-Playing              13
    289     XOne       Shooter              33
    290     XOne    Simulation               3
    291     XOne        Sports              36
    292     XOne      Strategy               3
    
    [293 rows x 3 columns]
    


```python
plt.figure(figsize = (20,10))
sns.barplot(data = f, x = 'Platform', y = f['Count of games'], hue = 'Genre')
```




    <AxesSubplot:xlabel='Platform', ylabel='Count of games'>




    
![png](output_39_1.png)
    


WE GET A QUITE A FEW INTERESTING INSIGHTS FROM THIS. ON A GLOBAL STAGE WE HAVE SEEN THAT ACTION TOPS THE CHARTS BUT WHEN WE CHECK BY PLATFORM WE CAN ACIALLY SEE THAT SPORTS IS HIGHER. PS2 HAS HIGHER SPORTS COUNT OF GAMES COMPARED TO ACTION.

Which individual game have the highest sale price globally?


```python
top_games = df.head(20)
top_games = top_games[['Name','Year','Genre','Global_Sales']]
top_games.sort_values(by = 'Global_Sales', ascending = False)
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
      <th>Name</th>
      <th>Year</th>
      <th>Genre</th>
      <th>Global_Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Wii Sports</td>
      <td>2006.0</td>
      <td>Sports</td>
      <td>82.74</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Super Mario Bros.</td>
      <td>1985.0</td>
      <td>Platform</td>
      <td>40.24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mario Kart Wii</td>
      <td>2008.0</td>
      <td>Racing</td>
      <td>35.82</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wii Sports Resort</td>
      <td>2009.0</td>
      <td>Sports</td>
      <td>33.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pokemon Red/Pokemon Blue</td>
      <td>1996.0</td>
      <td>Role-Playing</td>
      <td>31.37</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Tetris</td>
      <td>1989.0</td>
      <td>Puzzle</td>
      <td>30.26</td>
    </tr>
    <tr>
      <th>6</th>
      <td>New Super Mario Bros.</td>
      <td>2006.0</td>
      <td>Platform</td>
      <td>30.01</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wii Play</td>
      <td>2006.0</td>
      <td>Misc</td>
      <td>29.02</td>
    </tr>
    <tr>
      <th>8</th>
      <td>New Super Mario Bros. Wii</td>
      <td>2009.0</td>
      <td>Platform</td>
      <td>28.62</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Duck Hunt</td>
      <td>1984.0</td>
      <td>Shooter</td>
      <td>28.31</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Nintendogs</td>
      <td>2005.0</td>
      <td>Simulation</td>
      <td>24.76</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Mario Kart DS</td>
      <td>2005.0</td>
      <td>Racing</td>
      <td>23.42</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Pokemon Gold/Pokemon Silver</td>
      <td>1999.0</td>
      <td>Role-Playing</td>
      <td>23.10</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Wii Fit</td>
      <td>2007.0</td>
      <td>Sports</td>
      <td>22.72</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wii Fit Plus</td>
      <td>2009.0</td>
      <td>Sports</td>
      <td>22.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Kinect Adventures!</td>
      <td>2010.0</td>
      <td>Misc</td>
      <td>21.82</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Grand Theft Auto V</td>
      <td>2013.0</td>
      <td>Action</td>
      <td>21.40</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Grand Theft Auto: San Andreas</td>
      <td>2004.0</td>
      <td>Action</td>
      <td>20.81</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Super Mario World</td>
      <td>1990.0</td>
      <td>Platform</td>
      <td>20.61</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Brain Age: Train Your Brain in Minutes a Day</td>
      <td>2005.0</td>
      <td>Misc</td>
      <td>20.22</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize = (20,10))
ax = sns.barplot(data = top_games, x = 'Name', y = 'Global_Sales', errorbar = None)
ax.bar_label(ax.containers[0], fontsize = 15)
plt.xlabel("Name of the Game",fontsize = 15)
plt.ylabel("Global Sales",fontsize = 15)
plt.xticks(rotation =90, fontsize = 15)
plt.title("Top 10 games with max global sales", fontsize = 20)
```




    Text(0.5, 1.0, 'Top 10 games with max global sales')




    
![png](output_43_1.png)
    


WII SPORTS SOLD THE MOST. 

SALES COMPARISION BY GENRE


```python
comp_df = df[['Genre','NA_Sales','EU_Sales','JP_Sales','Other_Sales']]
comp_df_gb = comp_df.groupby('Genre').sum().reset_index()
comp_df_gb = pd.melt(comp_df_gb, id_vars = 'Genre', value_vars = ['NA_Sales','EU_Sales','JP_Sales','Other_Sales'],var_name = 'Sales Area',value_name = 'Total Sales')
comp_df_gb.head()
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
      <th>Genre</th>
      <th>Sales Area</th>
      <th>Total Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Action</td>
      <td>NA_Sales</td>
      <td>877.83</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Adventure</td>
      <td>NA_Sales</td>
      <td>105.80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Fighting</td>
      <td>NA_Sales</td>
      <td>223.59</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Misc</td>
      <td>NA_Sales</td>
      <td>410.24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Platform</td>
      <td>NA_Sales</td>
      <td>447.05</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize = (20,10))
bx = sns.barplot(data = comp_df_gb, x = 'Genre', y = 'Total Sales', hue = 'Sales Area')
for c in bx.containers:
    bx.bar_label(c,  label_type = 'edge' , padding  = 1, fontsize = '12')
```


    
![png](output_47_0.png)
    


NA HAS THE HIGHEST SALES ACROSS THE WORLD. 

Now checking by Platform


```python
plat_df = df[['Platform', 'NA_Sales','EU_Sales','JP_Sales', 'Other_Sales']]
plat_grp = plat_df.groupby('Platform').sum().reset_index()
plat_grp = pd.melt(plat_grp, id_vars = 'Platform', value_vars = ['NA_Sales','EU_Sales','JP_Sales','Other_Sales'], var_name = 'Sales Area', value_name = 'Total Sales')
plat_grp.head()
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
      <th>Platform</th>
      <th>Sales Area</th>
      <th>Total Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2600</td>
      <td>NA_Sales</td>
      <td>90.60</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3DO</td>
      <td>NA_Sales</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3DS</td>
      <td>NA_Sales</td>
      <td>78.87</td>
    </tr>
    <tr>
      <th>3</th>
      <td>DC</td>
      <td>NA_Sales</td>
      <td>5.43</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DS</td>
      <td>NA_Sales</td>
      <td>390.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize = (20,10))
sns.barplot(plat_grp , x = 'Platform', y = 'Total Sales', hue = 'Sales Area')
```




    <AxesSubplot:xlabel='Platform', ylabel='Total Sales'>




    
![png](output_51_1.png)
    


CONC  : PS XBOX WII top of the market NA is always the leader.

TOP 20 Publishers 


```python
publish = df.groupby('Publisher')['Year'].count().reset_index(name = 'Count of titles')
publish_sort = publish.sort_values('Count of titles', ascending = False).reset_index().head(20)
print(publish_sort)
```

        index                               Publisher  Count of titles
    0     138                         Electronic Arts             1339
    1      21                              Activision              966
    2     347                      Namco Bandai Games              928
    3     525                                 Ubisoft              918
    4     275            Konami Digital Entertainment              823
    5     488                                     THQ              712
    6     359                                Nintendo              696
    7     456             Sony Computer Entertainment              682
    8     446                                    Sega              632
    9     494                    Take-Two Interactive              412
    10     85                                  Capcom              376
    11     53                                   Atari              347
    12    500                              Tecmo Koei              338
    13    465                             Square Enix              231
    14    549  Warner Bros. Interactive Entertainment              217
    15    126              Disney Interactive Studios              214
    16    137                       Eidos Interactive              196
    17    325                            Midway Games              196
    18      6                               505 Games              192
    19    323                  Microsoft Game Studios              189
    


```python
plt.figure (figsize = (20,10))
cx = sns.barplot(publish_sort, x = 'Publisher', y = 'Count of titles')
cx.bar_label(cx.containers[0])
plt.xlabel('Publisher', fontsize = 15)
plt.ylabel('Count of Titles', fontsize = 15)
plt.title('Top 20 Publishers',fontsize = 20)
plt.xticks(rotation = 90)
```




    (array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
            17, 18, 19]),
     [Text(0, 0, 'Electronic Arts'),
      Text(1, 0, 'Activision'),
      Text(2, 0, 'Namco Bandai Games'),
      Text(3, 0, 'Ubisoft'),
      Text(4, 0, 'Konami Digital Entertainment'),
      Text(5, 0, 'THQ'),
      Text(6, 0, 'Nintendo'),
      Text(7, 0, 'Sony Computer Entertainment'),
      Text(8, 0, 'Sega'),
      Text(9, 0, 'Take-Two Interactive'),
      Text(10, 0, 'Capcom'),
      Text(11, 0, 'Atari'),
      Text(12, 0, 'Tecmo Koei'),
      Text(13, 0, 'Square Enix'),
      Text(14, 0, 'Warner Bros. Interactive Entertainment'),
      Text(15, 0, 'Disney Interactive Studios'),
      Text(16, 0, 'Eidos Interactive'),
      Text(17, 0, 'Midway Games'),
      Text(18, 0, '505 Games'),
      Text(19, 0, 'Microsoft Game Studios')])




    
![png](output_55_1.png)
    


EA has the most titles released overall. 

Top global sales by publisher


```python
sal_pub = df.groupby('Publisher')['Global_Sales'].sum().reset_index(name = 'Total Sales Globally')
sal_pub = sal_pub.sort_values('Total Sales Globally', ascending = False).head(20)
print(sal_pub)
```

                                      Publisher  Total Sales Globally
    359                                Nintendo               1786.56
    138                         Electronic Arts               1110.32
    21                               Activision                727.46
    456             Sony Computer Entertainment                607.50
    525                                 Ubisoft                474.72
    494                    Take-Two Interactive                399.54
    488                                     THQ                340.77
    275            Konami Digital Entertainment                283.64
    446                                    Sega                272.99
    347                      Namco Bandai Games                254.09
    323                  Microsoft Game Studios                245.79
    85                                   Capcom                200.89
    53                                    Atari                157.22
    549  Warner Bros. Interactive Entertainment                153.89
    465                             Square Enix                145.18
    126              Disney Interactive Studios                119.96
    137                       Eidos Interactive                 98.98
    288                               LucasArts                 87.34
    66                       Bethesda Softworks                 82.14
    325                            Midway Games                 69.85
    


```python
plt.figure (figsize = (20,10))
cx = sns.barplot(sal_pub, x = 'Publisher', y = 'Total Sales Globally')
cx.bar_label(cx.containers[0])
plt.xlabel('Publisher', fontsize = 15)
plt.ylabel('Global Sales', fontsize = 15)
plt.title('Top Global Sales',fontsize = 20)
plt.xticks(rotation = 90)
```




    (array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
            17, 18, 19]),
     [Text(0, 0, 'Nintendo'),
      Text(1, 0, 'Electronic Arts'),
      Text(2, 0, 'Activision'),
      Text(3, 0, 'Sony Computer Entertainment'),
      Text(4, 0, 'Ubisoft'),
      Text(5, 0, 'Take-Two Interactive'),
      Text(6, 0, 'THQ'),
      Text(7, 0, 'Konami Digital Entertainment'),
      Text(8, 0, 'Sega'),
      Text(9, 0, 'Namco Bandai Games'),
      Text(10, 0, 'Microsoft Game Studios'),
      Text(11, 0, 'Capcom'),
      Text(12, 0, 'Atari'),
      Text(13, 0, 'Warner Bros. Interactive Entertainment'),
      Text(14, 0, 'Square Enix'),
      Text(15, 0, 'Disney Interactive Studios'),
      Text(16, 0, 'Eidos Interactive'),
      Text(17, 0, 'LucasArts'),
      Text(18, 0, 'Bethesda Softworks'),
      Text(19, 0, 'Midway Games')])




    
![png](output_59_1.png)
    



```python

```
