
- [How to use reduce, lamda, map, sum, filter function ](#how_to_use_reduce_map_sum_filter_function)


## How to use **reduce**, **lamda**, **map**, **sum**, **filter** function 

```
# reduce function

from functools import reduce
from timeit import timeit

nums = [1,2,3,4]
products = reduce(lambda x, y: x+y, nums)
print(products)
# 10

# lamda, map

def f1(x):
     return x*x

f2 = lambda x:x*x

for i in range(10):
    assert f1(i) == f2(i)

nums = [1, 2, 3, 4]
nums_squared = [num * num for num in nums]
print(nums_squared)

# the num in nums is applied to f1
nums_squared_1 = map(f1, nums)
nums_squared_2 = map(lambda x: x*x, nums)

print(list(nums_squared_1))
# [1, 4, 9, 16]
print(list(nums_squared_2))
# [1, 4, 9, 16]

# lamda, map, sum

a, b = 3, -0.5
xs = [2,3,4,5]
labels = [6.4, 8.0, 10.9, 15.3]

# method 1
errors = []
for i, x in enumerate(xs):
    errors.append((a*x + b - labels[i]) ** 2)
results1 = sum(errors)** 0.5 / len(xs)
print("Results 1 ", results1)
# Results 1  0.3588175023601832

# method 2
diffs = map(lambda x, y: (a*x + b - y)**2, xs, labels)
result2 = sum(diffs)** 0.5 / len(xs)
print("Results 2 ", result2)
# Results 2  0.3588175023601832

# filter funtion

bad_preds = filter(lambda x: x > 0.5, errors)
print(list(bad_preds))

-  There's no difference in calling a *lambda* versus a *function*

print(timeit('a()', setup="def a():return 222*333"))
# 0.07061290740966797

print(timeit('a()', setup="a=lambda: 222*333"))
# 0.06967616081237793

```
