## NP完全或NP完備(縮寫為NP-C或NPC）
NP完備是NP與NP困難的交集，是NP中最難的決定性問題，所有NP問題都可以被快速歸化為NP完備問題。

* bigO
    * 泡沫排序法:時間複雜度 = n的2次方
    * 循序搜尋法:時間複雜度 = n

* 深度優先搜尋法
![Pic](https://github.com/hung890202/ai110b/blob/master/note/%E5%9C%96%E7%89%87/深度優先搜尋法.jpg)

* 廣度優先搜尋法
![Pic](https://github.com/hung890202/ai110b/blob/master/note/%E5%9C%96%E7%89%87/廣度優先.jpg)

## 八皇后問題
* 題目
一個以西洋棋為背景的問題：如何能夠在8×8的西洋棋棋盤上放置八個皇后，使得任何一個皇后都無法直接吃掉其他的皇后？為了達到此目的，任兩個皇后都不能處於同一條橫行、縱行或斜線上。

* 圖例
![Pic](https://github.com/hung890202/ai110b/blob/master/note/%E5%9C%96%E7%89%87/八皇后.jpg)

* 程式碼
```
def queen(n): # n 皇后主函數
	q = [] # q 代表已經排下去的皇后，一開始還沒排，所以是空的
	return queenNext(n, q) # 呼叫 queenNext 遞迴下去排出所有可能

# 思考：排到一半 q=[1,3] 繼續排下去
#      對 [1,3,0..], [1,3,1..], [1,3,2..], [1,3,3..] 全部試一遍
def queenNext(n, q): # 已經排好 q[0..y2-1], 繼續排下去 [y2...n-1]
	y2 = qlen = len(q)
	if qlen == n: # 全部排好了
		print(q)  # 印出盤面
		return
	# 還沒排滿，繼續排下去
	for x2 in range(n): # 對本列的每一個 x2 去嘗試
		isConflict = False
		for y in range(qlen): # 前面已經排下去的舊皇后，座標為 (x,y)
			x = q[y]
			if conflict(x,y,x2,y2): # 檢查新排的皇后(x2,y2)，和前面的有沒有衝突
				isConflict = True
		if not isConflict:  # 如果沒有衝突，就繼續排下去
			q.append(x2)    # 把 (x2,y2) 放進盤面
			queenNext(n, q) # 繼續遞迴尋找下一個皇后位置
			q.pop()         # 把 (x2,y2) 移出盤面
		
def conflict(x1,y1,x2,y2): # 判斷 (x1,y1), (x2,y2) 兩個位置有沒有衝突
	if x1==x2: return True
	if y1==y2: return True
	if x1+y1==x2+y2: return True
	if x1-y1==x2-y2: return True
	return False

queen(4) # 列出四皇后的解答
queen(8) # 列出八皇后的解答

```

## TruthTable
真值表是使用於邏輯中（特別是在連結邏輯代數、布林函數和命題邏輯上）的一類數學用表，用來計算邏輯表示式在每種論證（即每種邏輯變數取值的組合）上的值。

尤其是，真值表可以用來判斷一個命題表示式是否對所有允許的輸入值皆為真，亦即是否為邏輯有效的。

* code
```
def truthTable(n): # 列出 n 變數的所有可能 0,1 排列
	p = [] # p 代表已經排下去的，一開始還沒排，所以是空的
	return tableNext(n, p) # 呼叫 tableNext 遞迴下去排出所有可能

def tableNext(n, p):
	i = len(p)      # i 是下一個排列的位置
	if i == n:		# 全部排好了
		print(p)	# 印出排列
		return      # 返回上層
	for x in [0,1]:     # x 是 0 或 1
		p.append(x)		# 把 x 放進表
		tableNext(n, p)	# 繼續遞迴尋找下一個排列
		p.pop()			# 把 x 移出表

truthTable(2) # 印出 2 變數的真值表
truthTable(3) # 印出 3 變數的真值表

```

* result
```
$ python truthtable2.py
[x, y, z] f
[0, 0, 0] 0
[0, 0, 1] 0
[0, 1, 0] 0
[0, 1, 1] 1
[1, 0, 0] 1
[1, 0, 1] 1
[1, 1, 0] 1
[1, 1, 1] 1
```