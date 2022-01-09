## Week_3 作業 ： 實作「Collaborative-filtering」的推薦系統
###### tags: `alphacamp data course`, `recommendation system`

### 專案目的
* 建立一個推薦系統，目的在以美妝電商資料中過去的商品銷售狀況，以使用者評分及商品銷售過往資料為基礎的過濾(Collaborative-filtering)的方式。並透過計算推薦商品與消費者實際購買商品狀況，評估推薦成果(Recall Score)。

### 使用資料集&欄位
* 資料集：http://deepyeti.ucsd.edu/jianmo/amazon/categoryFilesSmall/All_Beauty.csv http://deepyeti.ucsd.edu/jianmo/amazon/metaFiles2/meta_All_Beauty.json.gz
* 使用欄位：asin(商品ID)、reviewerID(評論者ID)、overall(商品評分)、unixReviewTime(評分時間)、rank(商品排名)、price(商品價格)

### 資料切割方式
* Training data：日期在2017-01-01~2018-09-01之前的用戶評分資料。
* Testing data：日期介於2018-09-01及2018-09-30的用戶評分資料。

### 資料整理
* 觀察商品資料空值狀況，留下可運用的欄位：`asin`、`description`、`title`、`brand`、`rank`、`price`
* 清洗`rank`欄位，拆出純數字排名
* 清洗`price`欄位，拆出純數字價格
* 將`rank`、`price`欄位合併到training data以供後續EDA使用
* 以`asin`欄位groupby，做出`overall_mean`、`sales`兩個欄位，並合併回training data，供後續EDA使用

### EDA
* 以pairplot觀察數值型資料兩兩之間的關係
* 深入畫出各數值型資料與`sales`之間的關係
* 同時查看用戶的購買次數分佈

### 推薦邏輯
* 本次推薦分兩層邏輯
	* collaborative-filtering: 以9月份資料計算推薦成效，584位使用者中以前曾購買過的僅僅只佔38位，此38位有過往商品購買的歷史資料，故套用collaborative-filtering推薦，嘗試以改變training data時間區間及推薦不同K個類似商品測試。
	
	* rule-based: 除了38位之外，其餘新使用者皆無過往商品的購買紀錄，故採用rule-based推薦，推薦其最熱銷商品；同時若使用collaborative-filtering推薦的個數未達K個，亦使用rule-based填補。

### 推薦結果評分

* 在未使用rule-based狀況下，user-based的分數為0
* item-based分數為0.169
* surprise則需篩選天數(跑不動)篩選180天則與item-based結果一致分數為0.169

### 結果發現

* 在測試過程中發現，由於測試集中與訓練集的用戶重合度過低(僅38位)，且其中只有9位用戶過去購買商品次數>1，基本上collaborative-filtering的結果不怎麼好，分數的提升也都是由於結合rule-based的緣故。
