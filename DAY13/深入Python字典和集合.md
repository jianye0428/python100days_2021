- [字典和集合](#字典和集合)
- [增删查找](#增删查找)
# 字典和集合
字典是一系列无序元素的组合，其长度大小可变，元素可以任意地删减和改变。不过要注意，这里的元素，是一对键（key）和值（value）

相比于列表和元组，字典的性能更优，特别是对于查找、添加和删除，字典都能在常数的时间复杂度内完成

而集合和字典基本相同，唯一的区别，就是集合没有键和值的配对是一系列无序的、唯一的元素组合。

```
d1 = {'name': 'jason', 'age': 20, 'gender': 'male'}
d2 = dict({'name': 'jason', 'age': 20, 'gender': 'male'})
d3 = dict([('name', 'jason'), ('age', 20), ('gender', 'male')])
d4 = dict(name='jason', age=20, gender='male') 
d1 == d2 == d3 ==d4
True

s1 = {1, 2, 3}
s2 = Set([1, 2, 3])
s1 == s2
True
```
集合并不支持索引操作，因为集合本质上是一个哈希表，和列表不一样
```
s = {1, 2, 3}
s[0]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'set' object does not support indexing
```

想要判断一个元素在不在字典或集合内，我们可以用 value in dict/set

```
s = {1, 2, 3}
1 in s
True
10 in s
False

d = {'name': 'Runsen', 'age': 20}
'name' in d
True
'location' in d
False
```

**字典的增删改**
```
In [1]: d = {'name': 'Runsen', 'age': 20}^M
   ...:

In [2]: d['gender'] = 'male'

In [3]: d['birthday'] = '1999-10-01'

In [4]: d
Out[4]: {'name': 'Runsen', 'age': 20, 'gender': 'male', 'birthday': '1999-10-01'}

In [5]: d['birthday'] = '1999/10/01'

In [6]: d.pop('birthday')
Out[6]: '1999/10/01'

In [8]: d
Out[8]: {'name': 'Runsen', 'age': 20, 'gender': 'male'}


In [9]: s = {1, 2, 3}^M
   ...:

In [10]: s.add(4)

In [11]: s
Out[11]: {1, 2, 3, 4}

In [12]: s.remove(4)

In [13]: s
Out[13]: {1, 2, 3}****
```

**字典的升序和降序排序**

~~~
d = {'b': 1, 'a': 2, 'c': 10}
d_sorted_by_key = sorted(d.items(), key=lambda x: x[0]) # 根据字典键的升序排序
d_sorted_by_value = sorted(d.items(), key=lambda x: x[1]) # 根据字典值的升序排序
d_sorted_by_key
[('a', 2), ('b', 1), ('c', 10)]
d_sorted_by_value
[('b', 1), ('a', 2), ('c', 10)]
~~~

# 增删查找
字典和集合是进行过性能高度优化的数据结构，特别是对于查找、添加和删除操作

**列表的做法**
```
# list version
def find_unique_price_using_list(products):
    unique_price_list = []
    for _, price in products: # A
        if price not in unique_price_list: #B
            unique_price_list.append(price)
    return len(unique_price_list)

# products id 和 price
products = [
    (143121312, 100), 
    (432314553, 30),
    (32421912367, 150),
    (937153201, 30)
]
print('number of unique price is: {}'.format(find_unique_price_using_list(products)))

# 输出
number of unique price is: 3
```

**集合的做法**
```
# set version
def find_unique_price_using_set(products):
    unique_price_set = set()
    for _, price in products:
        unique_price_set.add(price)
    return len(unique_price_set)        

products = [
    (143121312, 100), 
    (432314553, 30),
    (32421912367, 150),
    (937153201, 30)
]
print('number of unique price is: {}'.format(find_unique_price_using_set(products)))

# 输出
number of unique price is: 3
```

比较运行的时间，也就是性能

```
import time
id = [x for x in range(0, 100000)]
price = [x for x in range(200000, 300000)]
products = list(zip(id, price))

# 计算列表版本的时间
start_using_list = time.perf_counter()
find_unique_price_using_list(products)
end_using_list = time.perf_counter()
print("time elapse using list: {}".format(end_using_list - start_using_list))
## 输出
time elapse using list: 41.61519479751587


# 计算集合版本的时间
start_using_set = time.perf_counter()
find_unique_price_using_set(products)
end_using_set = time.perf_counter()
print("time elapse using set: {}".format(end_using_set - start_using_set))
# 输出
time elapse using set: 0.008238077163696289
```

在性能上, 集合完爆列表

对于字典，哈希表存储了哈希值，键和值这三个元素

字典和集合都是无序的数据结构，其内部的哈希表存储结构，保证了查找，插入，删除操作的高效性。所以，字典和集合通常运用在对元素的查找，去重

初始化字典的方式有两种方法，比较下哪一种更高效?

```
In [20]: timeit a ={'name':"runsen",'age':20}
127 ns ± 0.8 ns per loop (mean ± std. dev. of 7 runs, 10000000 loops each)

In [21]: timeit b =dict({'name':"runsen",'age':20})
438 ns ± 3.41 ns per loop (mean ± std. dev. of 7 runs, 1000000 loops each)
```

第一种，因为不用调用相关的函数。

![](https://camo.githubusercontent.com/c08539af01c206535eda0db5008e453a63b9e82ae70c757398adac33715279f7/68747470733a2f2f696d67636f6e766572742e6373646e696d672e636e2f6148523063484d364c793970625764726369356a62693169616935315a6d6c735a57397a4c6d4e76625338334e6a55784e6a4533597931684d574d304c54526a4d474574596a6b794e433034596d4d784d7a6b334e5441774f446b756347356e3f782d6f73732d70726f636573733d696d6167652f666f726d61742c706e67)

字典的键可以是一个列表吗？下面这段代码中，字典的初始化是否正确?

```
In [22]: d = {'name': 'Runsen', ['education']: [' primary school', 'junior middle school']}^M
    ...:
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-22-13cd196aef11> in <module>
----> 1 d = {'name': 'Runsen', ['education']: [' primary school', 'junior middle school']}

TypeError: unhashable type: 'list'

In [23]: d = {'name': 'Runsen', ('education'): [' primary school', 'junior middle school']}^M
    ...:
    ...:

In [24]: d
Out[24]: {'name': 'Runsen', 'education': [' primary school', 'junior middle school']}
```

用列表作为 Key 在这里是不被允许的，因为列表是一个动态变化的数据结构，字典当中的 key 要求是不可变的，原因也很好理解.

key 首先是不重复的，如果 Key 是可以变化的话，那么随着 Key 的变化，这里就有可能就会有重复的 Key，那么这就和字典的定义相违背；如果把这里的列表换成之前我们讲过的元组是可以的，因为元组不可变。
