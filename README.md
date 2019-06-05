# CVFX HW6 Report - Team 16

### 1. Take videos by ourselves
以下為我們所拍攝的測試影片:

[![Orignal video](http://img.youtube.com/vi/3TmlKczMQds/0.jpg)](https://youtu.be/3TmlKczMQds)

### 2. Make these visual effects with ORB-SLAM2

[![Orignal video](http://img.youtube.com/vi/C8XTWXcMIWc/0.jpg)](https://youtu.be/C8XTWXcMIWc)

我們使用的方法非常單純，首先我們直接將影片根據frame rate進行切割，切割成許多圖片，並且生成每個frame所對應的time stamp，然後輸出成一個文字檔讓ORB-SLAM2可以進行讀取。

接著將上述所提到的圖片與文字檔傳入ORB-SLAM2進行運算，我們使用的模式是Monocular，所以他只能將KeyFrame相機的旋轉與位置進行輸出。

最後我們將圖片檔與剛剛輸出KeyFrame相機的旋轉與位置丟到unity之中去模擬3D，我們使用的方法是將KeyFrame的資訊通通餵給unity中的camera，讓camera可以跟著ORB-SLAM2輸出的軌跡移動，然後再camera前面簡單加上一個3D object，這樣就可以很簡單達到一個類似AR的效果。

### 3. Make these visual effects with any post-production software

為了讓影片能配合我們所要的特效，因此我們重新拍攝了一段短片來製作我們的最終結果影片。

這次選擇了用After Effect這套軟體來進行後製，利用不同的影片及拍攝手法去凸顯兩者能做到事情的不同

原始影片如下：

[![Orignal video](http://img.youtube.com/vi/IpXLfVhbmdY/0.jpg)](https://youtu.be/IpXLfVhbmdY)

這裡大致用上了兩種方法：Track Camera & Animation，前者抓出跟蹤的目標影片物件、其在影片中移動的軌跡，套用到我們想要固定的物件─紙飛機上，再利用多標示幾個Keyframe做細部的Animation，微調使得物件看起來更加固定
另外我們這裡用了兩種物件來呈現Visual effect，一個是2D Text，提示鏡頭拉近，隨著Zooming in變更提示文字，並盡量維持在固定位置而不會隨鏡頭拉近而偏移，另一個則是3D object紙飛機，在Zooming in後出現在燈籠上頭，並且跟著彈指動作飛出窗外。

結果影片如下：

[![After video](http://img.youtube.com/vi/vIIGvNa-YIc/0.jpg)](https://youtu.be/vIIGvNa-YIc)

### 4. Compare above methods
* ORB-SLAM2 method:
ORB-SLAM2使用的方法很單純，他是將影像中的feature進行對位、比較之後，再配合time stamp的時間差，進行計算而推估出相機的行動軌跡。
在進行運算時看起來是非常準確的，視窗看到的相機軌跡都跟實際的情況很貼近，但是他無法將所有frame的旋轉與位置進行輸出，只能輸出KeyFrame的位置，而其他的Frame只能透過很簡單的內插法補齊，所以跑出來的效果才會比較差。
* After Effect method:
After Effect的優點在於強大的追蹤能力，並提供多種適用於不同狀態下的模式供選擇，能夠一次放置多個參考平面，且使用Animation進行微調，圖形化的介面也更容易操作，至於缺點也很明顯，畢竟本身歸類在"後製"軟體，自然不會考慮到Real-time processing，無論是使用Track Camera or Track Motion都必須等待一定時間 

### 5. Make some special effects based on the pose information, such as rotating, zooming in or out

如3.說明，一開始我們製造鏡頭Zooming in的畫面，隨著鏡頭拉近去改變標題文字和紙飛機出現等Visual effect
![](https://i.imgur.com/m9bSQxZ.png)

![](https://i.imgur.com/PtGQPYO.png)

![](https://i.imgur.com/QiFE0LA.png)


### 6. Insert a 3D model to your video

如3.說明，我們於畫面中加入了3D model─紙飛機，由於After Effect預設不支援直接匯入3D model file，我們是先透過匯入Photoshop生成.psd file，再匯入psd檔來達到插入特效。

![](https://i.imgur.com/xJDrKz6.png)

由於3D model本身多了旋轉要考慮，我們有特別透過Animation，隨著中間鏡頭左右橫移去微調Rotation，好讓物件看起來更穩定，之後為了凸顯3D model的特性，最後設計了彈指後紙飛機飛出的場景，為了呈現真實感，我們一共設置了超過10個Keyframe，藉由Easy ease & Roving的交互搭配完成直線加速、轉彎漸緩同時機身擺正、最後加速飛離的逼真特效。


