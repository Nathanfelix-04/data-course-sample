## Week_1 作業 ： 實作「rule-based」的推薦系統
###### tags: `alphacamp data course`, `recommendation system`

### 專案目的
* 建立一個推薦系統，目的在以美妝電商資料中過去的商品銷售狀況，尋找其規則去推薦其他消費者商品。並透過計算推薦商品與消費者實際購買商品狀況，評估推薦成果。

### 使用資料集&欄位
* 資料集：http://deepyeti.ucsd.edu/jianmo/amazon/categoryFilesSmall/All_Beauty.csv http://deepyeti.ucsd.edu/jianmo/amazon/metaFiles2/meta_All_Beauty.json.gz
* 使用欄位：asin(商品ID)、reviewerID(評論者ID)、overall(商品評分)、unixReviewTime(評分時間)、also_buy(也買過什麼商品)、also_view(也看過什麼商品)

### 資料切割方式
* Training data：日期在2017-01-01~2018-09-01之前的用戶評分資料。
* Testing data：日期介於2018-09-01及2018-09-30的用戶評分資料。

### 推薦邏輯
* 此次推薦以用戶評論資料將消費者過往評論商品的次數排序，找出每一消費者各自評論過的所有品項，並推薦其他用戶購買其品項也購買、瀏覽過的商品(also_buy、also_view)，若過往無該用戶評論資料，則推薦其熱銷商品。


### 推薦結果評分

* 推薦準確率為9.66%

### 結果發現

* 在測試過程中發現，由於測試集中與訓練集的用戶重合度過低(僅38位)，使用also_buy和also_view欄位進行推薦的有效人數不高，導致從過往用戶紀錄進行推薦的效果不甚理想。
過往客戶在這個月購買意願不高(38/584)，而新客戶較多(或許有什麼新客戶優惠？)

### 使用工具及平台
* Python
	* package: gzip, json, pandas
* Colab
* Github
