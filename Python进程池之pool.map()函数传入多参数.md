## 一 定义与解释

对于python代码，多线程其实是个假的，因为每次计算的时候，实质上只有一个线程计算。使用多线程时，是几个线程之间切换计算，就像轮班工作一下，适合处理I/O密集型的任务。
对于python代码，多进程才是真正意义上的多个进程在同一时间同时计算，就像几个人同时工作，适合处理计算（CPU）密集型的任务
进程池就是我们将所要运行的东西，放到池子里，Python会自行解决多进程的问题
## 二 代码实现
### 1 调用函数传入单个参数
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


### 2 调用函数传入一对参数
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


### 3 调用函数传入多个参数
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


## tqdm 

### autonotebook自动切换进度条风格

用过tqdm的朋友们大都知道它可以在常规的终端以及jupyter风格的各种编辑器中使用，且在后者中会以更美观的形式进行渲染，而以往我们通常需要在常规的终端里使用```from tqdm import tqdm```，在jupyter风格的编辑器中使用```from tqdm.notebook import tqdm```来分别导入。

而tqdm最近几个版本中引入了实验性质的新特性，使得我们只需要统一通过```from tqdm.autonotebook import tqdm```导入tqdm，就可以自适应检测不同的运行环境从而自动控制显示：
### 延迟渲染进度条

有时候我们希望当循环过程很快就执行完时，可以不打印进度条，毕竟进度条的主要目的是监控长时间运行过程，这时我们就可以给tqdm()添加参数delay来设置延时的秒数，当循环过程实际运行时长低于delay则无需打印多余的迭代过程：
### 自定义进度条色彩

通过为tqdm()设置参数colour，可以传入多种常见色彩格式值，这在jupyter类编辑器中效果尤为明显：
### 自主控制的进度上限

有些情况下，我们传入tqdm()的对象在迭代过程中是无法预先计算得到进度上限轮次的，典型如pandas中数据框的itertuples()，这种时候我们就可以利用total参数自行预设上限：
### 针对enumerate、zip和map的替代

Python中除了常规的循环过程以外，还有几种内置函数也具有迭代循环的属性，而tqdm为了方便我们对这些非典型的循环过程添加进度条，也单独开发了tenumerate、tzip以及tmap这三个API，用于替代enumerate、zip和map：
### 设置进度条“用完即逝”

当我们希望为多层循环过程添加进度条监视时，常规的为每一层都直接使用tqdm()，会导致打印出过多的进度条，反而不利于我们观察进度过程。

而通过使用tqdm.auto中的trange()，我们可以通过设置参数leave=False，来让我们对应的进度条加载到头就自动消失掉


