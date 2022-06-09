## 遺傳演算法

* 概念
遺傳演算法是模仿兩性生殖的演化機制，使用交配、突變等機制，不斷改進群體適應的一種演算法。

此方法廣泛被用在各個人工智慧領域，尤其是在最佳化問題上，遺傳演算法是經常使用的方法之一。

分數高機會大，分數低機會小

* 原理
傳演算法具有保存良好基因的特性 (良好基因 (父) + 良好基因 (母) = 更好的個體)在某些問題上，公式不成立時，遺傳演算法也就失效了，因此將無法具有良好的表現。

![Pic](https://github.com/brian891005/ai109b/blob/main/Note/%E5%9C%96%E7%89%87/遺傳.jpg)

*  keyGa.py
```
from geneticAlgorithm import GeneticAlgorithm
import random
 
class KeyGA(GeneticAlgorithm):
   def __init__(self, key):
       super().__init__()
       self.key = key
 
   def randomChromosome(self): # 隨機產生一個染色體 (一個 16 位元的 01 字串)
       bits=[]
       for _ in range(len(self.key)):
           bit = str(random.randint(0,1))
           bits.append(bit)
       return ''.join(bits)
 
   def calcFitness(self, c): # 分數是和 key 一致的位元個數
       fitness=0
       for i in range(len(self.key)):
           fitness += 1 if c[i]==self.key[i] else 0
       return fitness
 
   def crossover(self, c1, c2):
       cutIdx = random.randint(0, len(c1)-1)
       head   = c1[0:cutIdx]
       tail   = c2[cutIdx:]
       return head + tail
   
   def mutate(self, chromosome): # 突變運算
       i=random.randint(0, len(chromosome)-1) # 選擇突變點
       cMutate = chromosome[0:i]+random.choice(['0','1'])+chromosome[i+1:] # 在突變點上隨機選取 0 或 1
       return cMutate # 傳回突變後的染色體
```

* 執行
執行遺傳演算法，企圖找到 key，最多執行一百代，每代族群都是一百人
kga = KeyGA("1010101010101010")

## 加密技術

* 凱撒密碼 -- 字母位移法

凱撒密碼簡單來說就是將字母移動k位。

對英文加密時 k 會介於0到25之間，因為k=26等於沒有移位。比如attackatdawn 取位移量1 = bubdlbuebxo

* 維吉尼亞密碼 (Vigenère_cipher)
    * 維吉尼亞密碼是凱薩密碼的進化版，其方法是將位移量從單一數字變成一連串的位移，讓金鑰變成金鑰陣列。方法是將位移量從單一數字變成一連串的位移，也就是讓金鑰變成金鑰陣列時， 加密方法就從「凱撒密碼」進化成了「維吉尼亞密碼」。
    * 舉例而言，假如用 0 2 4 當位移，那麼 attackatdawn這句話，就會被加密成。
    ```
    a + 0 = a
    t + 2 = v
    t + 4 = x
    a + 0 = a
    c + 2 = e
    k + 4 = m
    a + 0 = a
    t + 2 = v
    d + 4 = h
    w + 0 = w
    n + 2 = p
    ```

* XOR 密碼
    * XOR 用來作加解密的好處是當我們對某位元連續與某樣式位元連續作兩次 XOR 運算時，就會得到原來的位元。
    * 用XOR加密且解密,利用邏輯閘相同位元輸出1,不同位元輸出1,相同位元輸出0的特性讓位元做兩次XOR還是能輸出成原本的樣貌
    * 例子 M XOR K XOR K = M
    

## 線性規劃

在數學中，線性規劃（Linear Programming，簡稱LP）特指目標函數和約束條件皆為線性的最佳化問題。

* 種類
    * 標準型
    * 增廣矩陣 - [單純形法](https://zh.wikipedia.org/wiki/%E5%8D%95%E7%BA%AF%E5%BD%A2%E6%B3%95)
    * 對偶
* 特性
    * 可加性 : L(x+t) = L(x) + L (t)
    * 一次齊次性 : L(mx) = mL(x)

## 整數規劃
要求所有的未知量都為整數的線性規劃問題。

相對於即使在最壞情況下也能有效率地解出的線性規劃問題，整數規劃問題的最壞情況是不確定的，在某些實際情況中（有約束變量的那些）為NP困難問題。

## NP完全或NP完備(縮寫為NP-C或NPC）
NP完備是NP與NP困難的交集，是NP中最難的決定性問題，所有NP問題都可以被快速歸化為NP完備問題。

* bigO
    * 泡沫排序法:時間複雜度 = n的2次方
    * 循序搜尋法:時間複雜度 = n

* 深度優先搜尋法
![Pic](https://github.com/brian891005/ai109b/blob/main/Note/%E5%9C%96%E7%89%87/深度優先搜尋法.jpg)

* 廣度優先搜尋法
![Pic](https://github.com/brian891005/ai109b/blob/main/Note/%E5%9C%96%E7%89%87/廣度優先.jpg)

