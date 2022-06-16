# 人臉辨識系統
* Code來源於[faceScore.py](https://gitlab.com/ccc109/ai/-/blob/master/09-image/02-face/face1/faceScore.py)，加上註解並加以說明。

* 參考資料<br>
[實作及時人臉偵測教學](https://blog.gtwang.org/programming/python-opencv-dlib-face-detection-implementation-tutorial/#google_vignette)<br>
[老師的程式碼](https://gitlab.com/ccc109/ai/-/blob/master/09-image/02-face/face1/faceScore.py)<br>
[dlib安裝心得](https://ithelp.ithome.com.tw/articles/10231535)<br>

## 介紹
人臉偵測是一項相當成熟的技術，不管是數位相機或是手機在拍照時，都可以自動偵測人臉並對焦，而在自行開發的程式當中，若要加入人臉偵測的功能也非常容易，只要串接相關的模組即可實作出相當專業的程式。

人臉偵測的實作方式有很多種，這裡我們選擇使用 Dlib 這套機器學習函式庫所提供的人臉偵測。

## 開發環境及運用模組
* 主要環境為python
* 輔助環境
    * CUDA TOOLKIT ---> 神經網路
    * CuDNN         
    * 安裝說明參考[CUDA TOOLKIT](https://developer.nvidia.com/cuda-toolkit)
* 運用模組 
    * dlib
    * cv2
    * imutils
### 模組應用範圍
* Cv2
    * CV :   主要OpenCV函式，即：核心函式庫
    * CVAUX ：  輔助函式庫
    * CXCORE ：  資料結構與線性代數庫(包含CvPoint、CvRect、CvSize、CvMat及lpiImage等常用資料結構)；
    * HIGHUI ： GUI函式庫(使用者互動介面，如影象顯示、接受滑鼠鍵盤事件等。已經包含視訊、攝像頭簡單操作)；
    * ML ：  機器學習函式庫，包含模式分類和迴歸分析等；
    * CVCAM ：視訊影象處理模組(一般還需要安裝DirectShow。此模組在2.0之後的版本好像不再包含，而直接使用highgui)。
    * 架構
    
    ![Pic](https://github.com/brian891005/ai109b/blob/main/Note/%E5%9C%96%E7%89%87/cv2.jpg)

* dlib --->神經網路
    * 介紹
    Dlib是一個現代化的C ++工具箱，其中包含用於在C ++中建立複雜軟體以解決實際問題的機器學習演算法和工具。它廣泛應用於工業界和學術界，包括機器人，嵌入式裝置，行動電話和大型高效能運算環境。Dlib的開源許可證 允許您在任何應用程式中免費使用它。
    * 特點
        * 高質量的廣泛相容的程式碼
        * 機器學習演算法
        * 數值計算演算法
        * 圖形模型推理演算法
        * 影象處理
        * 執行緒
        * 網路通訊
        * 圖形使用者介面
        * 資料壓縮和完整性檢查演算法
* [安裝步驟](https://ithelp.ithome.com.tw/articles/10231535)

* imutils
    * 介紹
    imutils是Adrian Rosebrock開發的一個python工具包，它整合了opencv、numpy和matplotlib的相關操作，主要是用來進行圖形圖像的處理，如圖像的平移、旋轉、縮放、骨架提取、顯示等等，後期又加入了針對視頻的處理，如攝像頭、本地文件等。
    * 圖片處理
    * 安裝
    ```
    pip install imutils
    ```

* 測試程式碼
test.py
```
# pip install imutils
import dlib
import cv2
import imutils

# 讀取照片圖檔
img = cv2.imread('image.jpg')

# 縮小圖片
img = imutils.resize(img, width=640)

# Dlib 的人臉偵測器
detector = dlib.get_frontal_face_detector()

# 偵測人臉
face_rects = detector(img, 0)

# 取出所有偵測的結果
for i, d in enumerate(face_rects):
  x1 = d.left()
  y1 = d.top()
  x2 = d.right()
  y2 = d.bottom()

  # 以方框標示偵測的人臉
  cv2.rectangle(img, (x1, y1), (x2, y2), (0, 255, 0), 4, cv2.LINE_AA)

# 顯示結果
cv2.imshow("Face Detection", img)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

* 呈現結果

![Pic](https://github.com/brian891005/ai109b/blob/main/Note/%E5%9C%96%E7%89%87/test.jpg)


* 主程式碼
[faceScore.py](https://gitlab.com/ccc109/ai/-/blob/master/09-image/02-face/face1/faceScore.py)
```
import dlib   # 神經網路
import cv2
import imutils

img = cv2.imread('image.jpg')
img = imutils.resize(img, width=1280)
detector = dlib.get_frontal_face_detector()

# 偵測人臉，輸出分數
face_rects, scores, idx = detector.run(img, 0, -1) # 超過 -1 分的人臉都算 
---------------------列出辨識圖片，並顯示分數-------------------------------
for i, d in enumerate(face_rects):
  x1 = d.left()
  y1 = d.top()
  x2 = d.right()
  y2 = d.bottom()
  text = "%2.2f(%d)" % (scores[i], idx[i])

  cv2.rectangle(img, (x1, y1), (x2, y2), (0, 255, 0), 4, cv2.LINE_AA)

  # 標示分數
  cv2.putText(img, text, (x1, y1), cv2.FONT_HERSHEY_DUPLEX,
          0.7, (255, 255, 255), 1, cv2.LINE_AA)

cv2.imshow("Face Detection", img) # 顯示影像

cv2.waitKey(0)
cv2.destroyAllWindows()
```

* 顯示結果
    * test1:
    ![Pic](https://github.com/brian891005/ai109b/blob/main/Note/%E5%9C%96%E7%89%87/result1.jpg)
    * test2:
    當圖片過度模糊式，正確率會降低

    ![Pic](https://github.com/brian891005/ai109b/blob/main/Note/%E5%9C%96%E7%89%87/test2.jpg)

## 本專案只用於學習所用
* [LICENSE](https://github.com/brian891005/sp109b/blob/main/Note/授權聲明/README.md)
