# Automatic Number Plate Recognition

車牌辨識專案工作內容

## 技術：

```
OpenCV, Machine Learning, Object Detection, Image Process, C++, Node.JS, MongoDB.
```

## 專利：

因此專案本人申請了車牌歪斜矯正方法的[專利](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/%E8%BB%8A%E7%89%8C%E6%AD%AA%E6%96%9C%E7%9F%AF%E6%AD%A3%E6%96%B9%E6%B3%95%202016-9-12.pdf)：

* 本發明係關於一種車牌辨識演算法，特別是車牌顏色與車身顏色相近的車牌歪斜矯正方法。
* 車牌形狀雖為矩形，但若因拍攝角度造成車牌歪斜，會降低車牌辨識之識別率；此時，可藉由Hough轉換偵測出車牌框線進行車牌之歪斜矯正；但，若車牌與車身顏色相近時，不易偵測出車牌框線，此時必須借助車牌號碼本身。
* 已知技術之文字傾斜矯正方法，例如2012年8月21日公告之美國專利公報第8249391B2號中公開的方法，係偵測水平歪斜之角度做矯正。此類水平方向矯正方法只能用於正面歪斜之車牌，無法矯正側面歪斜之車牌，因為正面歪斜之車牌，垂直方向與水平方向仍可視為垂直關係；但側面歪斜之車牌，則不一定有此關係。
* 本發明的目的在於提供一種估算垂直方向歪斜角度之演算法，以提高車牌辨識之識別率。
* 雖然車牌與車身顏色可能會相近，但車牌若無汙損，基本上車牌號碼本身顏色與背景顏色對比強烈，且所有字符幾乎皆呈高度大於寬度的長方體，因此可藉由此特性，估算出垂直方向歪斜的角度。

## 車牌辨識主要演算法：

### Plate Detection

```
以 Local binary patterns (LBP) 演算法找出潛在車牌位置；篩選兩千多張車牌作訓練
```

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/plates.png)

### Char Analysis

```
找出及分析車牌區域內的字元:
```

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/char-analysis.jpg)

###	Plate Edges, Deskew

```
找出車牌邊緣， Plate Detection 只能找出車牌可能區域，還需找出車牌確切的上、下、左、右邊緣；並進一步做歪斜矯正。
```

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/plate-lines.JPG)

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/deskew.png)

###	Character Segmentation:

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/after_cleaning_AAB3010_1.jpg)

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/clean_filters_cleaning_AAB3010_1.jpg)

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/histograms_AAB3010_1.jpg)

###	Optical Character Recognition (OCR):

```
使用 Tesseract Open Source OCR Engine
```

## 網站重要功能介紹：

```
ANPR Daemon 與 HTTP Server 之架構圖
```

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/architecture.png)

### 即時影像辨識

* 提供即時影像顯示(最多支援4個車道影像顯示)，表格中提供車輛即時出入資料以及車牌縮圖

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/live.png)

### 紀錄查詢

* 可快速查詢近3小時、本日、本周、本月出入紀錄
* 可設定車號及日期區間進行進階查詢
* 可由右方查看縮圖，或點擊車號link以顯示完整辨識圖片

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/record-1.png)

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/record-2.png)

### 收費管理

* 收費管理頁面分為左邊編輯區及右邊檢視區

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/fee-1.png)

* 『一般設定』可設定一般周日~周六收費，收費方式可分為計時、計次
* 『特別週期設定』可設定特別日期區間收費
*	『特別日期設定』可設定特別日期收費

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/fee-2.png)

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/fee-3.png)

* 拖拉檢視區左上角『特別日期』至月曆上特定日期可設定為該特別日期，設定完成後，該月曆上之日期背景色會與該特定日期一樣。

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/fee-4.png)

*	點選檢視區右上角『週』按鈕，可檢視每周每天各時段之詳細設定

![](https://github.com/hulanpei/Automatic-Number-Plate-Recognition/blob/master/resources/fee-5.png)
