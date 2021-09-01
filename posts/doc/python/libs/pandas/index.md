# 

# Pandas

#### Author：zifeng  2019/4/3

### 创建数据帧


```python
import pandas as pd
import numpy as np
```


```python
# 通过直接给出序列内容创建数据帧
s = pd.Series([1, 2, 3, 4, 5, np.nan, 8])
print(s)
```

    0    1.0
    1    2.0
    2    3.0
    3    4.0
    4    5.0
    5    NaN
    6    8.0
    dtype: float64
    


```python
data = np.array([np.random.randint(3, 90) for i in range(30)]).reshape(5, 6)
pd.DataFrame(data)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>16</td>
      <td>45</td>
      <td>77</td>
      <td>13</td>
      <td>24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>3</td>
      <td>73</td>
      <td>41</td>
      <td>12</td>
      <td>75</td>
      <td>29</td>
    </tr>
    <tr>
      <th>2</th>
      <td>14</td>
      <td>70</td>
      <td>39</td>
      <td>89</td>
      <td>17</td>
      <td>76</td>
    </tr>
    <tr>
      <th>3</th>
      <td>43</td>
      <td>30</td>
      <td>6</td>
      <td>78</td>
      <td>65</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>50</td>
      <td>62</td>
      <td>46</td>
      <td>49</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 通过DataFrame方式创建数据帧

# 创建日期指针
dates = pd.date_range('20130101', periods=6)
dates

df = pd.DataFrame(np.random . randn(6, 4),
                  index=dates,
                  columns=list("ABCD"))
df
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')






<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.298945</td>
      <td>0.729744</td>
      <td>0.281129</td>
      <td>-0.048527</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>0.626489</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-0.774761</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>0.778775</td>
      <td>0.925483</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.934119</td>
      <td>-0.581168</td>
      <td>-0.178498</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.067255</td>
      <td>-1.591689</td>
      <td>0.511555</td>
      <td>-0.382439</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 其他的逐列导入数据的方式
df2 = pd.DataFrame({'A': 1.,
                    'B': pd.Timestamp('20130102'),
                    'C': pd.Series(1, index=list(range(4)), dtype='float32'),
                    'D': np.array([3] * 4, dtype='int32'),
                    'E': pd.Categorical(["test", "train", "test", "train"]),
                    'F': 'foo'})

df2
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 其他的逐列导入数据的方式,传入一个高维数据
df3 = pd.DataFrame({'A': 1.,
                    'B': pd.Timestamp('20130102'),
                    'C': pd.Series([1, 2, 3, 4, 5, 6], index=["A", 2, 3, 4, 5, 6], dtype='float32'),
                    'D': pd.Series([1, 2, 3, 4, 5, 6], index=list(range(6)), dtype='float32'),
                    'E': pd.Series([1, 2, "d", "4", 5, 6], index=list(range(6)))
                    })

df3
# 测试不同的设置index的方法，如果在多个属性中用了不同的方法，最后产生的
# 依然是一一对应的index-数据关系，不会产生冲突，但是会扩大数据帧
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>d</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>5.0</td>
      <td>6.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>6.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>A</th>
      <td>1.0</td>
      <td>2013-01-02</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### 数据帧数据提取
#### 数据帧的内置属性


```python
df2.dtypes  # 显示每一个数据帧列的数据类型

# 如果用pd.Series方法传入数据，默认为object属性
```




    A           float64
    B    datetime64[ns]
    C           float32
    D             int32
    E          category
    F            object
    dtype: object




```python
# df2.<TAB>  # noqa: E225, E999
# df2.A                  df2.bool
# df2.abs                df2.boxplot
# df2.add                df2.C
# df2.add_prefix         df2.clip
# df2.add_suffix         df2.clip_lower
# df2.align              df2.clip_upper
# df2.all                df2.columns
# df2.any                df2.combine
# df2.append             df2.combine_first
# df2.apply              df2.compound
# df2.applymap           df2.consolidate
# df2.D

```

#### 一些查看数据的方法


```python
df.head(3)
# 默认打印出前5行，可传入参数设置打印的数量
df.tail(3)
# 默认打印出后5行，可传入参数设置打印的数量
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.298945</td>
      <td>0.729744</td>
      <td>0.281129</td>
      <td>-0.048527</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>0.626489</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-0.774761</td>
    </tr>
  </tbody>
</table>
</div>






<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>0.778775</td>
      <td>0.925483</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.934119</td>
      <td>-0.581168</td>
      <td>-0.178498</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.067255</td>
      <td>-1.591689</td>
      <td>0.511555</td>
      <td>-0.382439</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.index
print("{:-^56}".format("分割线"))
df.columns
```




    DatetimeIndex(['2013-01-01', '2013-01-02', '2013-01-03', '2013-01-04',
                   '2013-01-05', '2013-01-06'],
                  dtype='datetime64[ns]', freq='D')



    --------------------------分割线---------------------------
    




    Index(['A', 'B', 'C', 'D'], dtype='object')



### 数据帧操作
#### 转化为numpy矩阵


```python
df.to_numpy()
print("{:-^56}".format("分割线"))
df2.to_numpy()
```




    array([[-1.29894505,  0.72974422,  0.28112929, -0.04852731],
           [-0.60847101,  0.15493327, -0.73042051,  0.62648929],
           [ 0.63036506, -0.68802041, -0.26871703, -0.77476082],
           [-0.33723249, -2.11799308,  0.77877497,  0.92548257],
           [ 0.32184238, -0.93411913, -0.58116761, -0.178498  ],
           [-0.06725543, -1.59168897,  0.51155514, -0.38243901]])



    --------------------------分割线---------------------------
    




    array([[1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'test', 'foo'],
           [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'train', 'foo'],
           [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'test', 'foo'],
           [1.0, Timestamp('2013-01-02 00:00:00'), 1.0, 3, 'train', 'foo']],
          dtype=object)



注意这种方式会直接去掉index or column labels 

#### 显示总体统计数据


```python
df.describe()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-0.226616</td>
      <td>-0.741191</td>
      <td>-0.001474</td>
      <td>0.027958</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.688267</td>
      <td>1.060723</td>
      <td>0.614927</td>
      <td>0.636404</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-1.298945</td>
      <td>-2.117993</td>
      <td>-0.730421</td>
      <td>-0.774761</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-0.540661</td>
      <td>-1.427297</td>
      <td>-0.503055</td>
      <td>-0.331454</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-0.202244</td>
      <td>-0.811070</td>
      <td>0.006206</td>
      <td>-0.113513</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.224568</td>
      <td>-0.055805</td>
      <td>0.453949</td>
      <td>0.457735</td>
    </tr>
    <tr>
      <th>max</th>
      <td>0.630365</td>
      <td>0.729744</td>
      <td>0.778775</td>
      <td>0.925483</td>
    </tr>
  </tbody>
</table>
</div>



#### 描述性统计


```python
df.mean()
```




    A   -0.226616
    B   -0.741191
    C   -0.001474
    D    0.027958
    dtype: float64




```python
df.mean(1) # 另一个轴方向
```




    2013-01-01   -0.084150
    2013-01-02   -0.139367
    2013-01-03   -0.275283
    2013-01-04   -0.187742
    2013-01-05   -0.342986
    2013-01-06   -0.382457
    Freq: D, dtype: float64



#### Apply方法

DataFrame.apply(func, axis=0, broadcast=False, raw=False, reduce=None, args=(), **kwds)
会把每一行或列（取决于axis=1or0）传入func并获取结果


```python
df.apply(np.cumsum)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.298945</td>
      <td>0.729744</td>
      <td>0.281129</td>
      <td>-0.048527</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-1.907416</td>
      <td>0.884677</td>
      <td>-0.449291</td>
      <td>0.577962</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-1.277051</td>
      <td>0.196657</td>
      <td>-0.718008</td>
      <td>-0.196799</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-1.614283</td>
      <td>-1.921336</td>
      <td>0.060767</td>
      <td>0.728684</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-1.292441</td>
      <td>-2.855455</td>
      <td>-0.520401</td>
      <td>0.550186</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-1.359697</td>
      <td>-4.447144</td>
      <td>-0.008846</td>
      <td>0.167747</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.apply(lambda x: x.max() - x.min())
```




    A    1.929310
    B    2.847737
    C    1.509195
    D    1.700243
    dtype: float64



#### 直方统计


```python
s = pd.Series(np.random.randint(0, 3, size=10))
s
```




    0    0
    1    0
    2    2
    3    1
    4    1
    5    1
    6    0
    7    0
    8    0
    9    2
    dtype: int64




```python
s.value_counts()
```




    0    5
    1    3
    2    2
    dtype: int64



#### 转制


```python
df.T
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2013-01-01 00:00:00</th>
      <th>2013-01-02 00:00:00</th>
      <th>2013-01-03 00:00:00</th>
      <th>2013-01-04 00:00:00</th>
      <th>2013-01-05 00:00:00</th>
      <th>2013-01-06 00:00:00</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>-1.298945</td>
      <td>-0.608471</td>
      <td>0.630365</td>
      <td>-0.337232</td>
      <td>0.321842</td>
      <td>-0.067255</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.729744</td>
      <td>0.154933</td>
      <td>-0.688020</td>
      <td>-2.117993</td>
      <td>-0.934119</td>
      <td>-1.591689</td>
    </tr>
    <tr>
      <th>C</th>
      <td>0.281129</td>
      <td>-0.730421</td>
      <td>-0.268717</td>
      <td>0.778775</td>
      <td>-0.581168</td>
      <td>0.511555</td>
    </tr>
    <tr>
      <th>D</th>
      <td>-0.048527</td>
      <td>0.626489</td>
      <td>-0.774761</td>
      <td>0.925483</td>
      <td>-0.178498</td>
      <td>-0.382439</td>
    </tr>
  </tbody>
</table>
</div>



#### 字符串方法


```python
s = pd.Series(['A', 'B', 'C', 'Aaba', 'Baca', np.nan, 'CABA', 'dog', 'cat'])
s.str.lower()
```




    0       a
    1       b
    2       c
    3    aaba
    4    baca
    5     NaN
    6    caba
    7     dog
    8     cat
    dtype: object



#### 排序


```python
# 通过轴的值（标签）进行排序
data = np.array([np.random.randint(3, 90) for i in range(30)]).reshape(5, 6)
raw = pd.DataFrame(data, index=[3, 5, 1, 4, 6], columns=list("ABCDEF"))
raw
raw.sort_index(axis=0, ascending=False)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>68</td>
      <td>17</td>
      <td>50</td>
      <td>83</td>
      <td>87</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>47</td>
      <td>57</td>
      <td>5</td>
      <td>58</td>
      <td>9</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>18</td>
      <td>16</td>
      <td>51</td>
      <td>45</td>
      <td>71</td>
      <td>87</td>
    </tr>
    <tr>
      <th>4</th>
      <td>84</td>
      <td>9</td>
      <td>24</td>
      <td>15</td>
      <td>84</td>
      <td>49</td>
    </tr>
    <tr>
      <th>6</th>
      <td>69</td>
      <td>36</td>
      <td>41</td>
      <td>78</td>
      <td>8</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>






<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>69</td>
      <td>36</td>
      <td>41</td>
      <td>78</td>
      <td>8</td>
      <td>40</td>
    </tr>
    <tr>
      <th>5</th>
      <td>47</td>
      <td>57</td>
      <td>5</td>
      <td>58</td>
      <td>9</td>
      <td>80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>84</td>
      <td>9</td>
      <td>24</td>
      <td>15</td>
      <td>84</td>
      <td>49</td>
    </tr>
    <tr>
      <th>3</th>
      <td>68</td>
      <td>17</td>
      <td>50</td>
      <td>83</td>
      <td>87</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>18</td>
      <td>16</td>
      <td>51</td>
      <td>45</td>
      <td>71</td>
      <td>87</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 通过值排序
raw.sort_values(by='B')
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>84</td>
      <td>9</td>
      <td>24</td>
      <td>15</td>
      <td>84</td>
      <td>49</td>
    </tr>
    <tr>
      <th>1</th>
      <td>18</td>
      <td>16</td>
      <td>51</td>
      <td>45</td>
      <td>71</td>
      <td>87</td>
    </tr>
    <tr>
      <th>3</th>
      <td>68</td>
      <td>17</td>
      <td>50</td>
      <td>83</td>
      <td>87</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>69</td>
      <td>36</td>
      <td>41</td>
      <td>78</td>
      <td>8</td>
      <td>40</td>
    </tr>
    <tr>
      <th>5</th>
      <td>47</td>
      <td>57</td>
      <td>5</td>
      <td>58</td>
      <td>9</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>



### 选择


```python
df['A']
```




    2013-01-01   -1.298945
    2013-01-02   -0.608471
    2013-01-03    0.630365
    2013-01-04   -0.337232
    2013-01-05    0.321842
    2013-01-06   -0.067255
    Freq: D, Name: A, dtype: float64




```python
df[0:3]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.298945</td>
      <td>0.729744</td>
      <td>0.281129</td>
      <td>-0.048527</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>0.626489</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-0.774761</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['20130102':'20130104']
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>0.626489</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-0.774761</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>0.778775</td>
      <td>0.925483</td>
    </tr>
  </tbody>
</table>
</div>



#### 通过标签选择


```python
# 通过提供index名
dates[1]
df.loc[dates[1]]
```




    Timestamp('2013-01-02 00:00:00', freq='D')






    A   -0.608471
    B    0.154933
    C   -0.730421
    D    0.626489
    Name: 2013-01-02 00:00:00, dtype: float64




```python
# 通过提供column名
df.loc[:, ['A', 'C']]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.298945</td>
      <td>0.281129</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>-0.730421</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.268717</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>0.778775</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.581168</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.067255</td>
      <td>0.511555</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 通过提供index和column名们
df.loc[[dates[0], dates[2]], ['A', 'B']]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.298945</td>
      <td>0.729744</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 通过提供index和column名
df.loc[dates[1], 'A']
```




    -0.6084710113141097




```python
# 更快的方式
# For getting fast access to a scalar (equivalent to the prior method):
s = df.at[dates[1], 'A']
```

#### 通过位置选择


```python
df.iloc[3]
```




    A   -0.337232
    B   -2.117993
    C    0.778775
    D    0.925483
    Name: 2013-01-04 00:00:00, dtype: float64




```python
df.iloc[3:5, 0:2]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.934119</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.iloc[1:3, :]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>0.626489</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-0.774761</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 批量指定选择
df.iloc[[0, 1, 5], [0, 2]]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.298945</td>
      <td>0.281129</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>-0.730421</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.067255</td>
      <td>0.511555</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.iloc[1, 1]
```




    0.15493327469578466




```python
# For getting fast access to a scalar (equivalent to the prior method):
df.iat[1, 1]
```




    0.15493327469578466



#### 基于条件表达式选择



```python
df[df.A > 0]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-0.774761</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.934119</td>
      <td>-0.581168</td>
      <td>-0.178498</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[df > 0]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>NaN</td>
      <td>0.729744</td>
      <td>0.281129</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>NaN</td>
      <td>0.154933</td>
      <td>NaN</td>
      <td>0.626489</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.778775</td>
      <td>0.925483</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.511555</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df4  = df.copy()
df4['E'] = ['one', 'one', 'two', 'three', 'four', 'three']
df4
df4[df4['E'].isin(['two', 'four'])]
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.298945</td>
      <td>0.729744</td>
      <td>0.281129</td>
      <td>-0.048527</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>0.626489</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-0.774761</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>0.778775</td>
      <td>0.925483</td>
      <td>three</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.934119</td>
      <td>-0.581168</td>
      <td>-0.178498</td>
      <td>four</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.067255</td>
      <td>-1.591689</td>
      <td>0.511555</td>
      <td>-0.382439</td>
      <td>three</td>
    </tr>
  </tbody>
</table>
</div>






<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-0.774761</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.934119</td>
      <td>-0.581168</td>
      <td>-0.178498</td>
      <td>four</td>
    </tr>
  </tbody>
</table>
</div>



### 赋值

#### 基于位置或标签


```python
s1 = pd.Series([1, 2, 3, 4, 5, 6], index=pd.date_range('20130102', periods=6))
df['F'] = s1
df
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>-1.298945</td>
      <td>0.729744</td>
      <td>0.281129</td>
      <td>-0.048527</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>0.626489</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-0.774761</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>0.778775</td>
      <td>0.925483</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.934119</td>
      <td>-0.581168</td>
      <td>-0.178498</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.067255</td>
      <td>-1.591689</td>
      <td>0.511555</td>
      <td>-0.382439</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.at[dates[0], 'A'] = 0
df.iat[0, 1] = 0
df.loc[:, 'D'] = np.array([5] * len(df))
df
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.281129</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>5</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>0.778775</td>
      <td>5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.934119</td>
      <td>-0.581168</td>
      <td>5</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.067255</td>
      <td>-1.591689</td>
      <td>0.511555</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



#### 基于表达式


```python
df5 = df.copy()
df5[df5 > 0] = -df5
df5
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>-0.281129</td>
      <td>-5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>-0.154933</td>
      <td>-0.730421</td>
      <td>-5</td>
      <td>-1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>-0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>-5</td>
      <td>-2.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>-0.778775</td>
      <td>-5</td>
      <td>-3.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>-0.321842</td>
      <td>-0.934119</td>
      <td>-0.581168</td>
      <td>-5</td>
      <td>-4.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.067255</td>
      <td>-1.591689</td>
      <td>-0.511555</td>
      <td>-5</td>
      <td>-5.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df


```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.281129</td>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>5</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>5</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>0.778775</td>
      <td>5</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2013-01-05</th>
      <td>0.321842</td>
      <td>-0.934119</td>
      <td>-0.581168</td>
      <td>5</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2013-01-06</th>
      <td>-0.067255</td>
      <td>-1.591689</td>
      <td>0.511555</td>
      <td>5</td>
      <td>5.0</td>
    </tr>
  </tbody>
</table>
</div>



### 缺失数据

pandas主要使用np.nan表示缺失的数据，一般情况下它不会参与计算


```python
df1 = df.reindex(index=dates[0:4], columns=list(df.columns) + ['E'])
df1.loc[dates[0]:dates[1], 'E'] = 1
df1
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.281129</td>
      <td>5</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>5</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>5</td>
      <td>2.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>0.778775</td>
      <td>5</td>
      <td>3.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



#### 删除所有缺少数据的行：


```python

df1.dropna(how='any')
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>5</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



#### 填写缺失的数据


```python
df1.fillna(value=0)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-01-01</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.281129</td>
      <td>5</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-02</th>
      <td>-0.608471</td>
      <td>0.154933</td>
      <td>-0.730421</td>
      <td>5</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2013-01-03</th>
      <td>0.630365</td>
      <td>-0.688020</td>
      <td>-0.268717</td>
      <td>5</td>
      <td>2.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2013-01-04</th>
      <td>-0.337232</td>
      <td>-2.117993</td>
      <td>0.778775</td>
      <td>5</td>
      <td>3.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



#### 获取某个位置是否缺失的布尔值


```python
pd.isna(df1.iloc[0])
```




    A    False
    B    False
    C    False
    D    False
    F     True
    E    False
    Name: 2013-01-01 00:00:00, dtype: bool



### 合并操作

#### 连接


```python
df = pd.DataFrame(np.random.randn(10, 4))
pieces = [df[3:7], df[:3], df[7:]]
pd.concat(pieces)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>1.022657</td>
      <td>-1.932082</td>
      <td>1.370112</td>
      <td>-0.857029</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.797997</td>
      <td>1.719741</td>
      <td>0.376259</td>
      <td>0.634603</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-0.086318</td>
      <td>0.327618</td>
      <td>0.417757</td>
      <td>-0.000512</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-1.317138</td>
      <td>-0.638319</td>
      <td>-0.819202</td>
      <td>-0.914410</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0.873689</td>
      <td>-0.227276</td>
      <td>-0.362998</td>
      <td>0.701491</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.096766</td>
      <td>1.690989</td>
      <td>-1.983586</td>
      <td>-0.232735</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.555661</td>
      <td>-1.168640</td>
      <td>-1.538744</td>
      <td>0.517871</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.269349</td>
      <td>-1.027657</td>
      <td>2.074734</td>
      <td>0.996608</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1.156438</td>
      <td>0.939047</td>
      <td>1.520113</td>
      <td>-0.234060</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.169248</td>
      <td>0.656213</td>
      <td>0.698909</td>
      <td>0.038606</td>
    </tr>
  </tbody>
</table>
</div>



#### 关系连接


```python
left = pd.DataFrame({'key': ['foo', 'foo'], 'lval': [1, 2]})
right = pd.DataFrame({'key': ['foo', 'foo'], 'rval': [4, 5]})
# 通过共同的主键，得到笛卡尔积
pd.merge(left, right, on='key')
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>1</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>foo</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
left = pd.DataFrame({'key': ['foo', 'bar'], 'lval': [1, 2]})
right = pd.DataFrame({'key': ['foo', 'bar'], 'rval': [4, 5]})
pd.merge(left, right, on='key')
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>key</th>
      <th>lval</th>
      <th>rval</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>1</td>
      <td>4</td>
    </tr>
    <tr>
      <th>1</th>
      <td>bar</td>
      <td>2</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



#### 追加


```python
df = pd.DataFrame(np.random.randn(8, 4), columns=['A', 'B', 'C', 'D'])
s = df.iloc[3]
df.append(s, ignore_index=True)
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.555553</td>
      <td>-0.895036</td>
      <td>0.685891</td>
      <td>-0.063173</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.883348</td>
      <td>0.196882</td>
      <td>-0.821545</td>
      <td>1.571110</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.073590</td>
      <td>-1.410319</td>
      <td>0.216424</td>
      <td>0.102808</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.909209</td>
      <td>0.496501</td>
      <td>-0.361447</td>
      <td>1.417946</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.871197</td>
      <td>1.142627</td>
      <td>1.057472</td>
      <td>0.797853</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.970707</td>
      <td>-1.427695</td>
      <td>-1.466132</td>
      <td>1.487051</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.111419</td>
      <td>-0.902179</td>
      <td>-0.806028</td>
      <td>-0.516934</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.068379</td>
      <td>1.384894</td>
      <td>-0.851670</td>
      <td>0.833989</td>
    </tr>
    <tr>
      <th>8</th>
      <td>-0.909209</td>
      <td>0.496501</td>
      <td>-0.361447</td>
      <td>1.417946</td>
    </tr>
  </tbody>
</table>
</div>



### 分组

根据某些共同特征分组


```python
df = pd.DataFrame({'A': ['foo', 'bar', 'foo', 'bar',
                          'foo', 'bar', 'foo', 'foo'],
                    'B': ['one', 'one', 'two', 'three',
                          'two', 'two', 'one', 'three'],
                    'C': np.random.randn(8),
                    'D': np.random.randn(8)})
df.groupby('A').sum()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bar</th>
      <td>-3.086910</td>
      <td>2.332698</td>
    </tr>
    <tr>
      <th>foo</th>
      <td>2.910966</td>
      <td>0.100083</td>
    </tr>
  </tbody>
</table>
</div>



#### 分层索引


```python
df.groupby(['A', 'B']).sum()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>C</th>
      <th>D</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">bar</th>
      <th>one</th>
      <td>-1.052167</td>
      <td>-0.276205</td>
    </tr>
    <tr>
      <th>three</th>
      <td>-0.289215</td>
      <td>2.387399</td>
    </tr>
    <tr>
      <th>two</th>
      <td>-1.745528</td>
      <td>0.221504</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">foo</th>
      <th>one</th>
      <td>1.059714</td>
      <td>2.904771</td>
    </tr>
    <tr>
      <th>three</th>
      <td>-0.598699</td>
      <td>-1.452691</td>
    </tr>
    <tr>
      <th>two</th>
      <td>2.449951</td>
      <td>-1.351997</td>
    </tr>
  </tbody>
</table>
</div>



#### 数据透视表


```python
df = pd.DataFrame({'A': ['one', 'one', 'two', 'three'] * 3,
                    'B': ['A', 'B', 'C'] * 4,
                    'C': ['foo', 'foo', 'foo', 'bar', 'bar', 'bar'] * 2,
                    'D': np.random.randn(12),
                    'E': np.random.randn(12)})
pd.pivot_table(df, values='D', index=['A', 'B'], columns=['C'])
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>C</th>
      <th>bar</th>
      <th>foo</th>
    </tr>
    <tr>
      <th>A</th>
      <th>B</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">one</th>
      <th>A</th>
      <td>2.932258</td>
      <td>-1.166233</td>
    </tr>
    <tr>
      <th>B</th>
      <td>-0.055568</td>
      <td>-0.108725</td>
    </tr>
    <tr>
      <th>C</th>
      <td>0.202673</td>
      <td>0.072446</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">three</th>
      <th>A</th>
      <td>-0.546039</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>B</th>
      <td>NaN</td>
      <td>-0.842628</td>
    </tr>
    <tr>
      <th>C</th>
      <td>-1.265070</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">two</th>
      <th>A</th>
      <td>NaN</td>
      <td>-1.174154</td>
    </tr>
    <tr>
      <th>B</th>
      <td>0.596137</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>C</th>
      <td>NaN</td>
      <td>-0.286620</td>
    </tr>
  </tbody>
</table>
</div>



#### 基于值分类


```python
df = pd.DataFrame({"id": [1, 2, 3, 4, 5, 6],
                   "raw_grade": ['a', 'b', 'd', 'a', 'c', 'e']})
df["grade"] = df["raw_grade"].astype("category")
df
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>raw_grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>a</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>d</td>
      <td>d</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
      <td>a</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>c</td>
      <td>c</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
      <td>e</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 在赋予类别新名字时，需要一一对应
df["grade"].cat.categories=["very bad", "bad", "medium",
                                               "good", "very good"]
df["grade"]
```




    0     very bad
    1          bad
    2         good
    3     very bad
    4       medium
    5    very good
    Name: grade, dtype: category
    Categories (5, object): [very bad, bad, medium, good, very good]




```python
# 按类别排序
df.sort_values(by="grade")
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>raw_grade</th>
      <th>grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>a</td>
      <td>very bad</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>a</td>
      <td>very bad</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>b</td>
      <td>bad</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>c</td>
      <td>medium</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>d</td>
      <td>good</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>e</td>
      <td>very good</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 统计
df.groupby("grade").size()
```




    grade
    very bad     2
    bad          1
    medium       1
    good         1
    very good    1
    dtype: int64



### 基本绘图


```python
import matplotlib.pyplot as plt
%matplotlib inline
ts = pd.Series(np.random.randn(1000),
               index=pd.date_range('1/1/2000', periods=1000))
ts = ts.cumsum()
ts
ts.plot()
```




    2000-01-01    0.038669
    2000-01-02    0.411492
    2000-01-03    0.266208
    2000-01-04    1.332535
    2000-01-05   -0.654468
    2000-01-06   -0.447763
    2000-01-07    0.770544
    2000-01-08    1.598329
    2000-01-09    1.613089
    2000-01-10    0.540908
    2000-01-11    1.139266
    2000-01-12    1.188583
    2000-01-13    1.245679
    2000-01-14    4.060981
    2000-01-15    2.812565
    2000-01-16    4.851942
    2000-01-17    3.151176
    2000-01-18    4.292820
    2000-01-19    5.120494
    2000-01-20    5.181488
    2000-01-21    4.683283
    2000-01-22    2.717448
    2000-01-23    2.982939
    2000-01-24    3.039121
    2000-01-25    3.693215
    2000-01-26    2.219011
    2000-01-27    3.532535
    2000-01-28    3.165745
    2000-01-29    4.474846
    2000-01-30    5.086082
                    ...   
    2002-08-28    2.325656
    2002-08-29    3.160520
    2002-08-30    2.548248
    2002-08-31    1.817108
    2002-09-01    0.901412
    2002-09-02    1.302504
    2002-09-03    0.278690
    2002-09-04    0.080650
    2002-09-05   -0.405733
    2002-09-06   -0.854966
    2002-09-07   -1.304620
    2002-09-08   -2.620561
    2002-09-09   -3.977022
    2002-09-10   -5.207439
    2002-09-11   -5.532969
    2002-09-12   -4.656171
    2002-09-13   -3.133814
    2002-09-14   -3.115265
    2002-09-15   -3.033105
    2002-09-16   -4.823847
    2002-09-17   -6.382040
    2002-09-18   -6.977646
    2002-09-19   -6.152706
    2002-09-20   -5.770494
    2002-09-21   -4.435720
    2002-09-22   -5.395591
    2002-09-23   -6.265424
    2002-09-24   -6.422010
    2002-09-25   -6.899457
    2002-09-26   -5.941435
    Freq: D, Length: 1000, dtype: float64


    <matplotlib.axes._subplots.AxesSubplot at 0x7fdf55d2b320>

```python
df = pd.DataFrame(np.random.randn(1000, 4), index=ts.index,
                  columns=['A', 'B', 'C', 'D'])
df = df.cumsum()
plt.figure()
df.plot()
plt.legend(loc='best')
```



### 数据的文件存取

#### CSV


```python
df.to_csv('foo.csv')
pd.read_csv('foo.csv')
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000-01-01</td>
      <td>0.143818</td>
      <td>0.825601</td>
      <td>1.039604</td>
      <td>1.697094</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2000-01-02</td>
      <td>0.194027</td>
      <td>0.643065</td>
      <td>1.914827</td>
      <td>1.235270</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2000-01-03</td>
      <td>0.666793</td>
      <td>0.275150</td>
      <td>0.098700</td>
      <td>0.812752</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2000-01-04</td>
      <td>-0.793407</td>
      <td>0.754334</td>
      <td>0.691709</td>
      <td>1.498190</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2000-01-05</td>
      <td>1.730559</td>
      <td>-0.619508</td>
      <td>-1.384804</td>
      <td>1.528816</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2000-01-06</td>
      <td>1.978805</td>
      <td>-2.190767</td>
      <td>0.065524</td>
      <td>2.526330</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2000-01-07</td>
      <td>2.431549</td>
      <td>-1.716606</td>
      <td>-0.706523</td>
      <td>3.505517</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2000-01-08</td>
      <td>1.970359</td>
      <td>-1.626837</td>
      <td>0.926610</td>
      <td>4.335613</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2000-01-09</td>
      <td>0.943482</td>
      <td>-2.392421</td>
      <td>1.195364</td>
      <td>3.485464</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2000-01-10</td>
      <td>1.239578</td>
      <td>-2.269245</td>
      <td>0.789975</td>
      <td>3.868188</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2000-01-11</td>
      <td>1.299172</td>
      <td>-2.469667</td>
      <td>1.553138</td>
      <td>2.051716</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2000-01-12</td>
      <td>0.722547</td>
      <td>-1.950724</td>
      <td>3.725853</td>
      <td>1.454443</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2000-01-13</td>
      <td>-0.801981</td>
      <td>-1.987893</td>
      <td>4.884199</td>
      <td>0.102235</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2000-01-14</td>
      <td>-2.377644</td>
      <td>-2.443604</td>
      <td>3.422795</td>
      <td>1.202295</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2000-01-15</td>
      <td>-2.907435</td>
      <td>-2.004747</td>
      <td>2.083326</td>
      <td>0.863934</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2000-01-16</td>
      <td>-3.799856</td>
      <td>-0.234113</td>
      <td>2.418112</td>
      <td>0.480386</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2000-01-17</td>
      <td>-5.829380</td>
      <td>0.262109</td>
      <td>2.226666</td>
      <td>0.096123</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2000-01-18</td>
      <td>-5.621640</td>
      <td>1.382906</td>
      <td>1.332345</td>
      <td>0.943462</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2000-01-19</td>
      <td>-5.246371</td>
      <td>1.408658</td>
      <td>0.463537</td>
      <td>-0.268818</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2000-01-20</td>
      <td>-6.103138</td>
      <td>2.122443</td>
      <td>0.226551</td>
      <td>-2.766564</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2000-01-21</td>
      <td>-5.385488</td>
      <td>1.431818</td>
      <td>0.770722</td>
      <td>-1.592509</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2000-01-22</td>
      <td>-4.941684</td>
      <td>2.108428</td>
      <td>0.463895</td>
      <td>-1.994145</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2000-01-23</td>
      <td>-4.081941</td>
      <td>2.106146</td>
      <td>-1.613711</td>
      <td>-2.449944</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2000-01-24</td>
      <td>-2.285756</td>
      <td>1.945990</td>
      <td>-2.187394</td>
      <td>-2.801139</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2000-01-25</td>
      <td>-2.085719</td>
      <td>2.229759</td>
      <td>-2.346547</td>
      <td>-3.920321</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2000-01-26</td>
      <td>-0.867196</td>
      <td>1.256995</td>
      <td>-2.348731</td>
      <td>-4.894784</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2000-01-27</td>
      <td>-1.962681</td>
      <td>0.384689</td>
      <td>-2.006307</td>
      <td>-4.085241</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2000-01-28</td>
      <td>-3.830575</td>
      <td>1.400387</td>
      <td>-3.188981</td>
      <td>-4.886687</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2000-01-29</td>
      <td>-3.475645</td>
      <td>-0.814179</td>
      <td>-4.267174</td>
      <td>-3.770801</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2000-01-30</td>
      <td>-3.442232</td>
      <td>-1.119295</td>
      <td>-4.582616</td>
      <td>-3.962757</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>970</th>
      <td>2002-08-28</td>
      <td>-5.132694</td>
      <td>8.864309</td>
      <td>70.104002</td>
      <td>-15.664375</td>
    </tr>
    <tr>
      <th>971</th>
      <td>2002-08-29</td>
      <td>-5.269573</td>
      <td>9.502246</td>
      <td>71.219606</td>
      <td>-16.914990</td>
    </tr>
    <tr>
      <th>972</th>
      <td>2002-08-30</td>
      <td>-4.423638</td>
      <td>10.013103</td>
      <td>72.816075</td>
      <td>-17.643128</td>
    </tr>
    <tr>
      <th>973</th>
      <td>2002-08-31</td>
      <td>-4.985483</td>
      <td>10.264684</td>
      <td>72.169692</td>
      <td>-18.856110</td>
    </tr>
    <tr>
      <th>974</th>
      <td>2002-09-01</td>
      <td>-4.341870</td>
      <td>11.387308</td>
      <td>71.740208</td>
      <td>-19.103484</td>
    </tr>
    <tr>
      <th>975</th>
      <td>2002-09-02</td>
      <td>-5.294424</td>
      <td>12.020717</td>
      <td>72.066551</td>
      <td>-20.015673</td>
    </tr>
    <tr>
      <th>976</th>
      <td>2002-09-03</td>
      <td>-4.895574</td>
      <td>11.769237</td>
      <td>72.213428</td>
      <td>-19.201418</td>
    </tr>
    <tr>
      <th>977</th>
      <td>2002-09-04</td>
      <td>-3.930532</td>
      <td>11.907623</td>
      <td>75.197546</td>
      <td>-19.282245</td>
    </tr>
    <tr>
      <th>978</th>
      <td>2002-09-05</td>
      <td>-4.272679</td>
      <td>11.077299</td>
      <td>76.613244</td>
      <td>-20.121468</td>
    </tr>
    <tr>
      <th>979</th>
      <td>2002-09-06</td>
      <td>-4.208707</td>
      <td>11.615586</td>
      <td>79.266410</td>
      <td>-21.861092</td>
    </tr>
    <tr>
      <th>980</th>
      <td>2002-09-07</td>
      <td>-4.352115</td>
      <td>10.307904</td>
      <td>78.097516</td>
      <td>-22.247174</td>
    </tr>
    <tr>
      <th>981</th>
      <td>2002-09-08</td>
      <td>-5.581701</td>
      <td>9.987265</td>
      <td>78.940391</td>
      <td>-23.531324</td>
    </tr>
    <tr>
      <th>982</th>
      <td>2002-09-09</td>
      <td>-5.583394</td>
      <td>9.695317</td>
      <td>80.562698</td>
      <td>-24.487811</td>
    </tr>
    <tr>
      <th>983</th>
      <td>2002-09-10</td>
      <td>-2.483232</td>
      <td>10.151229</td>
      <td>80.729409</td>
      <td>-25.283733</td>
    </tr>
    <tr>
      <th>984</th>
      <td>2002-09-11</td>
      <td>-2.297916</td>
      <td>11.389913</td>
      <td>83.334174</td>
      <td>-25.116505</td>
    </tr>
    <tr>
      <th>985</th>
      <td>2002-09-12</td>
      <td>-1.660984</td>
      <td>13.623364</td>
      <td>83.144139</td>
      <td>-24.521016</td>
    </tr>
    <tr>
      <th>986</th>
      <td>2002-09-13</td>
      <td>-1.505412</td>
      <td>10.830599</td>
      <td>83.124773</td>
      <td>-25.460171</td>
    </tr>
    <tr>
      <th>987</th>
      <td>2002-09-14</td>
      <td>-2.433196</td>
      <td>10.805600</td>
      <td>83.844334</td>
      <td>-25.373814</td>
    </tr>
    <tr>
      <th>988</th>
      <td>2002-09-15</td>
      <td>-1.779919</td>
      <td>11.096351</td>
      <td>83.621240</td>
      <td>-24.451086</td>
    </tr>
    <tr>
      <th>989</th>
      <td>2002-09-16</td>
      <td>-1.503576</td>
      <td>11.070637</td>
      <td>82.421186</td>
      <td>-25.070960</td>
    </tr>
    <tr>
      <th>990</th>
      <td>2002-09-17</td>
      <td>-2.327083</td>
      <td>11.475285</td>
      <td>82.061435</td>
      <td>-24.766335</td>
    </tr>
    <tr>
      <th>991</th>
      <td>2002-09-18</td>
      <td>-2.543023</td>
      <td>11.417301</td>
      <td>81.516890</td>
      <td>-24.147998</td>
    </tr>
    <tr>
      <th>992</th>
      <td>2002-09-19</td>
      <td>-3.008511</td>
      <td>10.647488</td>
      <td>81.077977</td>
      <td>-22.992137</td>
    </tr>
    <tr>
      <th>993</th>
      <td>2002-09-20</td>
      <td>-4.022455</td>
      <td>9.182600</td>
      <td>83.436909</td>
      <td>-23.370880</td>
    </tr>
    <tr>
      <th>994</th>
      <td>2002-09-21</td>
      <td>-3.591459</td>
      <td>11.162237</td>
      <td>82.588241</td>
      <td>-22.373426</td>
    </tr>
    <tr>
      <th>995</th>
      <td>2002-09-22</td>
      <td>-2.328329</td>
      <td>12.019868</td>
      <td>82.263235</td>
      <td>-23.012892</td>
    </tr>
    <tr>
      <th>996</th>
      <td>2002-09-23</td>
      <td>-2.250216</td>
      <td>10.879810</td>
      <td>81.145897</td>
      <td>-21.759539</td>
    </tr>
    <tr>
      <th>997</th>
      <td>2002-09-24</td>
      <td>-2.242817</td>
      <td>9.373741</td>
      <td>81.275277</td>
      <td>-21.625180</td>
    </tr>
    <tr>
      <th>998</th>
      <td>2002-09-25</td>
      <td>-0.773354</td>
      <td>8.846909</td>
      <td>82.058127</td>
      <td>-21.870115</td>
    </tr>
    <tr>
      <th>999</th>
      <td>2002-09-26</td>
      <td>1.514245</td>
      <td>9.453139</td>
      <td>81.847091</td>
      <td>-21.015344</td>
    </tr>
  </tbody>
</table>
<p>1000 rows × 5 columns</p>
</div>



#### Excel

依赖openpyxl


```python
try:
    import openpyxl
except:
    print("Please install openpyxl")
else:
    df.to_excel('./pandas/foo.xlsx', sheet_name='Sheet1')
    pd.read_excel('./pandas/foo.xlsx', 'Sheet1', index_col=None, na_values=['NA'])
```

    Please install openpyxl
    

