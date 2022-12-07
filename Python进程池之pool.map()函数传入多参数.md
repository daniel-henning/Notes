##一 定义与解释

对于python代码，多线程其实是个假的，因为每次计算的时候，实质上只有一个线程计算。使用多线程时，是几个线程之间切换计算，就像轮班工作一下，适合处理I/O密集型的任务。
对于python代码，多进程才是真正意义上的多个进程在同一时间同时计算，就像几个人同时工作，适合处理计算（CPU）密集型的任务
进程池就是我们将所要运行的东西，放到池子里，Python会自行解决多进程的问题
##二 代码实现
###1 调用函数传入单个参数
```python
import multiprocessing as mp

def job(x):
    return x*x

def multicore():
    pool = mp.Pool() # 无参数时，使用所有cpu核
    # pool = mp.Pool(processes=3) # 有参数时，使用CPU核数量为3
    res = pool.map(job, range(10))
    print(res)
    
if __name__ == '__main__':
    multicore()
```
运行结果：
```[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]```


###2 调用函数传入一对参数
```python
import multiprocessing as mp
import itertools

def job(r, item):
    (x, y) = item
    return x * y 

def multicore(z):
    x_y = list(itertools.product(range(10), range(10)))
    pool = mp.Pool()  # 无参数时，使用所有cpu核
    # pool = mp.Pool(processes=3) # 有参数时，使用CPU核数量为3
    res = pool.map(func, x_y)
    return res

if __name__ == '__main__':
    res = multicore()
    print(res)
```


###3 调用函数传入多个参数
```python
import multiprocessing as mp
import itertools
from functools import partial

def job(z, r, item):
    (x, y) = item
    return x * y + z + r
    
def multicore(z):
    x_y = list(itertools.product(range(10), range(10)))
    r = 2
    func = partial(job, z, r)
    pool = mp.Pool()  # 无参数时，使用所有cpu核
    # pool = mp.Pool(processes=3) # 有参数时，使用CPU核数量为3
    res = pool.map(func, x_y)
    return res

if __name__ == '__main__':
    res = multicore(1)
    print(res)
```
