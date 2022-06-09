## 電腦下棋

 * 兩個主要關鍵算法
    * 盤面評估函數(不僅自己的,對方的也很重要)
    * 搜尋很多層對局 - 尋找最不容易被打敗的下法

* 例子:AlphaGo
於2014年開始由英國倫敦Google DeepMind開發的人工智慧圍棋軟體

其演算法:

AlphaGo使用蒙地卡羅樹搜尋（Monte Carlo tree search），藉助估值網路（value network）與走棋網路（policy network）這兩種深度神經網路，通過估值網路來評估大量選點，並通過走棋網路選擇落點。

## 如何提升電腦的棋力
* Min-Max 對局搜尋法
    * 搜尋每一層對方的打法以及我方的應對打法
    * 要小心組合爆炸
    * 用Alpha-Beta修剪

![Pic](https://github.com/hung890202/ai110b/blob/master/note/%E5%9C%96%E7%89%87/Min-Max.jpg)

* Alpha-Beta修剪法
Alpha-Beta 修剪法 其實是「Min-Max 對局搜尋法」的一個修改版，主要是在 Min-Max 當中加入了 α 與 β 兩個紀錄值，用來做為是否要修剪的參考標準。

![Pic](https://github.com/hung890202/ai110b/blob/master/note/%E5%9C%96%E7%89%87/Alpha-Beta.jpg)

## 恐怖谷理論
* 定義
人類過於非擬人物體或者人的會帶有喜愛的情感,但似人非人的物體會讓人帶有恐懼。

畫成圖表(非擬人~人)就會呈現成一條深的谷,稱作恐怖谷。

* 圖例

![Pic](https://github.com/hung890202/ai110b/blob/master/note/%E5%9C%96%E7%89%87/恐怖谷.jpg)