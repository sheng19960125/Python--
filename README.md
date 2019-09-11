# Python-OpenCV 膨脹與侵蝕
## 首先介紹 影像處理中 侵蝕原理
* 侵蝕的基本概念：腐蝕景物的邊界(在測試時，我們用白色為圖黑色為底來做測試)；在圖中每一個像素點為1吋，原始圖像中的像素(1或0)才會被認為1，否則皆被侵蝕，變為0。  
* 簡單來說，在邊界所有像素都將被丟棄，具體取決於內核(內主圖)的大小，因此前景對象的厚度或大小減小，或是圖像中的白色區域減少，將有助於消除小的白噪音，並分離兩個連接對象。
```
import cv2
import numpy as np

img = cv2.imread('your_photo',0)

kernel = np.ones((7,7),np.uint8)
erosion = cv2.erode(img,kernel,iterations = 1)

cv2.imshow('base',img)
cv2.imshow('last',erosion)
cv2.waitKey()
```
![](https://github.com/sheng19960125/Python--/edit/master/01.png)  
  
## 接著介紹 影像處理中 膨脹原理
* 與侵蝕正好相反。如果內圖至少為一個像素為"1"，則像素元素為"1"，增加在圖像中白色區域或前景對象的大小增加。  
* 通常在去除操音的情況下，侵蝕之後是膨脹，因為，侵蝕會消除白噪音，但他也會縮小我們本身的物體站面輛，所以我們要膨脹他，由於噪音的消失在膨脹後並不會回來所以他可以用來復原破碎的部分。
```
import cv2
import numpy as np

img = cv2.imread('your_photo',0)

kernel = np.ones((5,5),np.uint8)
dilation = cv2.dilate(img,kernel,iterations = 1)

cv2.imshow('src',img)
cv2.imshow('show',dilation)
cv2.waitKey()
```
![](https://github.com/sheng19960125/Python--/edit/master/02.png)  
  
## 開運算 利用先侵蝕接著膨脹 *cv2.morphologyEx() - cv2.MORPH_OPEN
```
import cv2
import numpy as np
import matplotlib.pylab  as plt

img = cv2.imread('03.png',0)

kernel = np.ones((5,5),np.uint8)
opening = cv2.morphologyEx(img, cv2.MORPH_OPEN, kernel)

cv2.imshow('src',img)
cv2.imshow('show',opening)
cv2.waitKey()
```
![](https://github.com/sheng19960125/Python--/edit/master/03.png)  
  
## 閉運算 利用先膨脹接著侵蝕 *cv2.morphologyEx() - cv2.MORPH_CLOSE
```
import cv2
import numpy as np

img = cv2.imread('img9.png',0)

kernel = np.ones((5,5),np.uint8)
closing = cv2.morphologyEx(img, cv2.MORPH_CLOSE, kernel)

cv2.imshow('src',img)
cv2.imshow('show',closing)
cv2.waitKey()
```
![](https://github.com/sheng19960125/Python--/edit/master/04.png)  
  
