## 爬山演算法
* 概念
    * 一種優化算法
    * 往高的地方爬
    * 以左右高度來做判斷，比較高度來持續攀升

* 演算法(框架)
反覆的作這樣的動作，直到旁邊的解都比現在的更差時，程式就停止。

```
Algorithm HillClimbing(f, x)
  x = 隨意設定一個解。
  while (x 有鄰居 x' 比 x 更高)
    x = x';
  end
  return x;
end
```

* 程式碼
>>HillClimbingSimple.py
```
def hillClimbing(f, x, dx=0.01):
    while (True):
        print('x={0:.3f} f(x)={1:.3f}'.format(x, f(x)))
        if f(x+dx)>f(x):
            x = x + dx
        elif f(x-dx)>f(x):
            x = x - dx
        else:
            break
    return x

def f(x):
    return -1*(x*x+3*x+5)

hillClimbing(f, 0)
```
* 執行結果
以-1*(x*x-2*x+1)為函數
```
user@LAPTOP-8K49E37L MINGW64 ~/Desktop/人工智慧/teaching/ai/02-optimize/01-hillclimbing/02-var1 (master)
$ python hillClimbing1.py
x=0.00000 f(x)=-1.00000
x=0.01000 f(x)=-0.98010
x=0.02000 f(x)=-0.96040
x=0.03000 f(x)=-0.94090
x=0.04000 f(x)=-0.92160
x=0.05000 f(x)=-0.90250
x=0.06000 f(x)=-0.88360
x=0.07000 f(x)=-0.86490
x=0.08000 f(x)=-0.84640
x=0.09000 f(x)=-0.82810
x=0.10000 f(x)=-0.81000
x=0.11000 f(x)=-0.79210
x=0.12000 f(x)=-0.77440
x=0.13000 f(x)=-0.75690
x=0.14000 f(x)=-0.73960
x=0.15000 f(x)=-0.72250
x=0.16000 f(x)=-0.70560
x=0.17000 f(x)=-0.68890
x=0.18000 f(x)=-0.67240
x=0.19000 f(x)=-0.65610
x=0.20000 f(x)=-0.64000
x=0.21000 f(x)=-0.62410
x=0.22000 f(x)=-0.60840
x=0.23000 f(x)=-0.59290
x=0.24000 f(x)=-0.57760
x=0.25000 f(x)=-0.56250
x=0.26000 f(x)=-0.54760
x=0.27000 f(x)=-0.53290
x=0.28000 f(x)=-0.51840
x=0.29000 f(x)=-0.50410
x=0.30000 f(x)=-0.49000
x=0.31000 f(x)=-0.47610
x=0.32000 f(x)=-0.46240
x=0.33000 f(x)=-0.44890
x=0.34000 f(x)=-0.43560
x=0.35000 f(x)=-0.42250
x=0.36000 f(x)=-0.40960
x=0.37000 f(x)=-0.39690
x=0.38000 f(x)=-0.38440
x=0.39000 f(x)=-0.37210
x=0.40000 f(x)=-0.36000
x=0.41000 f(x)=-0.34810
x=0.42000 f(x)=-0.33640
x=0.43000 f(x)=-0.32490
x=0.44000 f(x)=-0.31360
x=0.45000 f(x)=-0.30250
x=0.46000 f(x)=-0.29160
x=0.47000 f(x)=-0.28090
x=0.48000 f(x)=-0.27040
x=0.49000 f(x)=-0.26010
x=0.50000 f(x)=-0.25000
x=0.51000 f(x)=-0.24010
x=0.52000 f(x)=-0.23040
x=0.53000 f(x)=-0.22090
x=0.54000 f(x)=-0.21160
x=0.55000 f(x)=-0.20250
x=0.56000 f(x)=-0.19360
x=0.57000 f(x)=-0.18490
x=0.58000 f(x)=-0.17640
x=0.59000 f(x)=-0.16810
x=0.60000 f(x)=-0.16000
x=0.61000 f(x)=-0.15210
x=0.62000 f(x)=-0.14440
x=0.63000 f(x)=-0.13690
x=0.64000 f(x)=-0.12960
x=0.65000 f(x)=-0.12250
x=0.66000 f(x)=-0.11560
x=0.67000 f(x)=-0.10890
x=0.68000 f(x)=-0.10240
x=0.69000 f(x)=-0.09610
x=0.70000 f(x)=-0.09000
x=0.71000 f(x)=-0.08410
x=0.72000 f(x)=-0.07840
x=0.73000 f(x)=-0.07290
x=0.74000 f(x)=-0.06760
x=0.75000 f(x)=-0.06250
x=0.76000 f(x)=-0.05760
x=0.77000 f(x)=-0.05290
x=0.78000 f(x)=-0.04840
x=0.79000 f(x)=-0.04410
x=0.80000 f(x)=-0.04000
x=0.81000 f(x)=-0.03610
x=0.82000 f(x)=-0.03240
x=0.83000 f(x)=-0.02890
x=0.84000 f(x)=-0.02560
x=0.85000 f(x)=-0.02250
x=0.86000 f(x)=-0.01960
x=0.87000 f(x)=-0.01690
x=0.88000 f(x)=-0.01440
x=0.89000 f(x)=-0.01210
x=0.90000 f(x)=-0.01000
x=0.91000 f(x)=-0.00810
x=0.92000 f(x)=-0.00640
x=0.93000 f(x)=-0.00490
x=0.94000 f(x)=-0.00360
x=0.95000 f(x)=-0.00250
x=0.96000 f(x)=-0.00160
x=0.97000 f(x)=-0.00090
x=0.98000 f(x)=-0.00040
x=0.99000 f(x)=-0.00010
x=1.00000 f(x)=-0.00000
```
![Pic](https://github.com/hung890202/ai110b/blob/master/note/%E5%9C%96%E7%89%87/function.jpg)

* 程式碼
>二維爬山演算法
>HillClimbingSimple2.py
```
import random

def hillClimbing(f, x, y, h=0.01):
    failCount = 0                    # 失敗次數歸零
    while (failCount < 10000):       # 如果失敗次數小於一萬次就繼續執行
        fxy = f(x, y)                # fxy 為目前高度
        dx = random.uniform(-h, h)   # dx 為左右偏移量
        dy = random.uniform(-h, h)   # dy 為前後偏移量
        if f(x+dx, y+dy) >= fxy:     # 如果移動後高度比現在高
            x = x + dx               #   就移過去
            y = y + dy
            print('x={:.3f} y={:.3f} f(x,y)={:.3f}'.format(x, y, fxy))
            failCount = 0            # 失敗次數歸零
        else:                        # 若沒有更高
            failCount = failCount + 1#   那就又失敗一次
    return (x,y,fxy)                 # 結束傳回 （已經失敗超過一萬次了）

def f(x, y):
    return -1 * ( x*x -2*x + y*y +2*y - 8 )

hillClimbing(f, 0, 0)

```
* 執行結果

```
PS D:\ccc\course\ai\python\02-optimize> python hillClimbing2r.py
x=0.009 y=0.003 f(x,y)=8.000
x=0.011 y=-0.004 f(x,y)=8.012
x=0.018 y=-0.008 f(x,y)=8.031
x=0.020 y=-0.016 f(x,y)=8.051
x=0.019 y=-0.022 f(x,y)=8.071
x=0.017 y=-0.027 f(x,y)=8.081
...
x=1.000 y=-1.001 f(x,y)=10.000
x=1.000 y=-0.999 f(x,y)=10.000
x=1.000 y=-1.000 f(x,y)=10.000
x=1.000 y=-1.000 f(x,y)=10.000
```
* 框架化 -----> 通用函數
以後只要帶入from hillClimbing import hillClimbing  引入爬山演算法類別
```
def hillClimbing(s, maxGens, maxFails):   # 爬山演算法的主體函數
    print("start: ", s.str())             # 印出初始解
    fails = 0                             # 失敗次數設為 0
    # 當代數 gen<maxGen，且連續失敗次數 fails < maxFails 時，就持續嘗試尋找更好的解。
    for gens in range(maxGens):
        snew = s.neighbor()               #  取得鄰近的解
        sheight = s.height()              #  sheight=目前解的高度
        nheight = snew.height()           #  nheight=鄰近解的高度
        if (nheight >= sheight):          #  如果鄰近解比目前解更好
            print(gens, ':', snew.str())  #    印出新的解
            s = snew                      #    就移動過去
            fails = 0                     #    移動成功，將連續失敗次數歸零
        else:                             #  否則
            fails = fails + 1             #    將連續失敗次數加一
        if (fails >= maxFails):
            break
    print("solution: ", s.str())          #  印出最後找到的那個解
    return s                              #    然後傳回。

```
* solution物件模組板
    * 定義鄰邊、改變值、能量or高度(將問題框架化)
```
class Solution: # 解答的物件模版 (類別)
    def __init__(self, v, step = 0.01):
        self.v = v       # 參數 v 為解答的資料結構
        self.step = step # 每一小步預設走的距離

    # 以下兩個函數至少需要覆蓋掉一個，否則會無窮遞迴
    def height(self): # 爬山演算法的高度函數
        return -1*self.energy()               # 高度 = -1 * 能量

    def energy(self): # 尋找最低點的能量函數
        return -1*self.height()               # 能量 = -1 * 高度
```
>>energy取最低點
>>height取最高點

* 引入答案值
```
from hillClimbing import hillClimbing # 引入解答類別
from solution import Solution
import random

class SolutionNumber(Solution):
    def neighbor(self): # 單變數解答的鄰居函數。
        x = self.v
        dx= self.step               # x:解答 , dx : 移動步伐大小
        xnew = x+dx if random.random() > 0.5 else x-dx # 用亂數決定向左或向右移動
        return SolutionNumber(xnew) # 建立新解答並傳回。

    def energy(self):               # 能量函數
        x = self.v                  # x:解答
        return abs(x*x-4)           # 能量函數為 |x^2-4|

    def str(self): # 將解答轉為字串，以供印出觀察。
        return "energy({:.3f})={:.3f}".format(self.v, self.energy())

```
* 執行結果
    * 設好能量
    * 鄰邊
    * 字串設定
>>hillClimbingNumber.py
```
$ python hillClimbingNumber.py
start:  energy(0.000)=4.000
0 : energy(0.010)=4.000 
2 : energy(0.020)=4.000 
4 : energy(0.030)=3.999 
5 : energy(0.040)=3.998 
        .
        .
        .
364 : energy(1.950)=0.197
365 : energy(1.960)=0.158
366 : energy(1.970)=0.119
367 : energy(1.980)=0.080
371 : energy(1.990)=0.040
373 : energy(2.000)=0.000
solution:  energy(2.000)=0.000
```
>>以亂數決定其值
* 圖例
![Pic](https://github.com/hung890202/ai110b/blob/master/note/%E5%9C%96%E7%89%87/height.jpg)

#### 技術
* 物件導向技巧----->self的應用
* 資料結構化------->串聯各結構


* solutionArray.py
多變數函式
```
from solution import Solution
from random import random, randint

class SolutionArray(Solution):
    def neighbor(self):           #  多變數解答的鄰居函數。
        nv = self.v.copy()        #  nv=v.clone()=目前解答的複製品
        i = randint(0, len(nv)-1) #  隨機選取一個變數
        if (random() > 0.5):      #  擲骰子決定要往左或往右移
            nv[i] += self.step
        else:
            nv[i] -= self.step
        return SolutionArray(nv)  #  傳回新建的鄰居解答。

    def energy(self): #  能量函數
        x, y, z =self.v
        return x*x+3*y*y+z*z-4*x-3*y-5*z+8 #  (x^2+3y^2+z^2-4x-3y-5z+8)

    def str(self):    #  將解答轉為字串的函數，以供列印用。
        return "energy({:s})={:f}".format(str(self.v), self.energy())


```

* 結果

```
user@LAPTOP-8K49E37L MINGW64 ~/Desktop/人工智慧/teaching/ai/02-optimize/01-hillclimbing/04-framework (master)
$ python hillClimbingArray.py
start:  energy([1, 1, 1])=1.000000
2 : energy([1, 1, 1.01])=0.970100
3 : energy([1.01, 1, 1.01])=0.950200
6 : energy([1.01, 0.99, 1.01])=0.920500
9 : energy([1.01, 0.98, 1.01])=0.891400
                        .
                        .
                        .
911 : energy([2.000000000000001, 0.49999999999999956, 2.469999999999991])=-2.999100
916 : energy([2.000000000000001, 0.49999999999999956, 2.4799999999999907])=-2.999600
919 : energy([2.000000000000001, 0.49999999999999956, 2.4899999999999904])=-2.999900
920 : energy([2.000000000000001, 0.49999999999999956, 2.4999999999999902])=-3.000000
solution:  energy([2.000000000000001, 0.49999999999999956, 2.4999999999999902])=-3.000000
```

* solutionEquation.py