## Week_2 作業 ： 實作「content-based」的推薦系統
###### tags: `alphacamp data course`, `recommendation system`

### 專案目的
* 建立一個推薦系統，目的在以美妝電商資料中過去的商品銷售狀況，以內容為基礎的過濾(Content-based)的方式。並透過計算推薦商品與消費者實際購買商品狀況，評估推薦成果(Recall Score)。

### 使用資料集&欄位
* 資料集：http://deepyeti.ucsd.edu/jianmo/amazon/categoryFilesSmall/All_Beauty.csv http://deepyeti.ucsd.edu/jianmo/amazon/metaFiles2/meta_All_Beauty.json.gz
* 使用欄位：asin(商品ID)、reviewerID(評論者ID)、overall(商品評分)、unixReviewTime(評分時間)、rank(商品排名)、price(商品價格)、description(商品描述)、title(商品名稱)、brand(商品品牌)

### 資料切割方式
* Training data：日期在2017-01-01~2018-09-01之前的用戶評分資料。
* Testing data：日期介於2018-09-01及2018-09-30的用戶評分資料。

### 資料整理
* 觀察商品資料空值狀況，留下可運用的欄位：`asin`、`description`、`title`、`brand`、`rank`、`price`
* 清洗`rank`欄位，拆出純數字排名與子分類
* 新增欄位`features`，將所有文字欄位加入其中，轉為小寫，供後續斷詞使用
* 以nltk的word_tokenize進行斷詞，使用pos_tag篩選詞性(選取名詞、形容詞、副詞為主)，同時用stopword過濾不重要字詞。
* 以TfidfVectorizer計算tf-idf數值
* 使用cosine_similarity計算相似度矩陣

### 推薦邏輯
* 本次推薦分兩層邏輯
	* content-based: 以9月份資料計算推薦成效，584位使用者中以前曾購買過的僅僅只佔38位，此38位有過往商品購買的歷史資料，故套用content-based推薦，嘗試以推薦不同K個類似商品。
	
	* rule-based: 除了38位之外，其餘新使用者皆無過往商品的購買紀錄，故採用rule-based推薦，推薦其最熱銷商品。

### 推薦結果評分

* 在50個推薦，且時間區間為近30天時，表現最好(recall:0.342373)。

### 結果發現

* 在測試過程中發現，由於測試集中與訓練集的用戶重合度過低(僅38位)，使用content-based進行推薦的有效人數不高，但相比於上個星期的rule-based(0.0966)來說進步不少。

### 使用工具及平台
* Python

	* package: gzip, json, pandas, nltk, numpy, datetime
* Colab
* Github
