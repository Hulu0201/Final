---
output:
  pdf_document: default
  html_document: default
---
# 期末專題報告

## 題目: 勵志書暢銷的背後，吸引讀者的關鍵為何？

## 分析議題背景:
在這出版業人人喊苦,書店一間接著一間熄燈(如女書店)的時代,勵志書籍卻能和工具書並駕齊驅甚至高居排行榜不下 
  Peter Su 是近年暢銷書作家,在百花齊放的社群上有著高人氣而出版的著作有著驚人的銷量           現今出書一刷2000本能賣完是萬幸的,十萬本的銷量更是遙不可及
  文字雲是關鍵詞的視覺化描述，用於匯總用戶生成的標籤或一個網站的文字內容。標籤一般是獨立的詞彙，常常按字母順 序排列，其重要程度又能通過改變字體大小或顏色來表現

## 分析動機:
[話題》勵志散文：在暢銷的背後，讀者追尋的是什麼？](http://www.openbook.org.tw/article/20170225-249) 看到這篇文章覺得很有意思,也想到今年於台北國際書展看到許多勵志書放置在顯眼的平台上,走過去總會忍不住拿起來翻個幾頁或是將封面書腰上的文字快速閱讀過 
網路上對於此類的書籍評價正反兩極 (正方認為能夠帶來舒緩;反方持無病呻吟的看法) 
Peter Su能夠在短短一個月55刷衝破10萬本的銷量,不論內容是什麼,總是讓人很好奇,並想一探究竟

## 資料介紹與來源
假設:因為Peter Su是先由FB貼文引起關注而逐漸擁有許多粉絲,才得以出書.所以這裡並非分析他的著作,而是想透過其臉書內容來了解其為何能有極大的影響力,甚至是商機.
  -資料為暢銷作家Peter Su的臉書貼文

```r
#install.packages("Rfacebook")  
token<-"EAACEdEose0cBAHZCmmPg8AZAE4VpI2ayMdeAQJTHM3wagNkFAaBDXZCVb9WZBSDAKwBZC3NlDPCiZCJYmYBaDhz9PlaKpqdJU4YEoZCwnJrtBSv8dJy3tiVqsfPM7UBF9Mltmw2s5kharJrtHefE94DJOzNne2QMMHUsx6YjJJf5tRov9lSvWEywmSuRUmj1lsZD" #access token 
library(Rfacebook) 
```

```
## Loading required package: httr
```

```
## Warning: package 'httr' was built under R version 3.3.3
```

```
## Loading required package: rjson
```

```
## Loading required package: httpuv
```

```
## Warning: package 'httpuv' was built under R version 3.3.3
```

```
## 
## Attaching package: 'Rfacebook'
```

```
## The following object is masked from 'package:methods':
## 
##     getGroup
```

```r
lastDate<-Sys.Date() 
DateVector<-seq(as.Date("2017-01-21"),lastDate,by="7 days")  
DateVectorStr<-as.character(DateVector)
totalPage<-NULL
for(i in 1:(length(DateVectorStr)-1)){
    tempPage<-getPage("petesonline", token,
                since = DateVectorStr[i],
                until = DateVectorStr[i+1])
    totalPage<-rbind(totalPage,tempPage)
     Sys.sleep(2)
}
```

```
## 9 posts 2 posts 3 posts 7 posts 5 posts 6 posts 4 posts 1 posts 7 posts 6 posts 4 posts 10 posts 2 posts 9 posts 5 posts 5 posts 4 posts 4 posts 4 posts 3 posts 5 posts
```


```r
nrow(totalPage) #有幾筆資料
```

```
## [1] 105
```

## 格式
data.frame 

```r
#先將不需要的欄位清除
totalPage$id <- NULL
totalPage$from_id <- NULL
totalPage$from_name <- NULL
totalPage$link <- NULL
#抓出發文時間
totalPage$time <- substr(totalPage$created_time, start=12, stop=13) 
str(totalPage)
```

```
## 'data.frame':	105 obs. of  8 variables:
##  $ message       : chr  "這次我和愛玩客到了日本山形為大家祈福，還沒看過的朋友現在可以在Youtube 上看到啦！\n\n祝大家雞年行大運\xed<U+00A0><U+00BD>\xed<U+"| __truncated__ "愛玩客首播！" "愛玩客首播！" "飛出雲海的那刻，我就把那些自己不喜歡卻還是犯賤放在心裡的事情拋開了，隨著水分子凝結化成了雪留在那沒人認識我的山谷裡。\n\n山形的"| __truncated__ ...
##  $ created_time  : chr  "2017-01-27T15:00:11+0000" "2017-01-25T14:49:30+0000" "2017-01-25T13:44:37+0000" "2017-01-25T13:00:06+0000" ...
##  $ type          : chr  "video" "video" "video" "photo" ...
##  $ story         : chr  NA "Peter Su was live." "Peter Su was live." "Peter Su added 2 new photos." ...
##  $ likes_count   : num  693 1052 912 1949 13206 ...
##  $ comments_count: num  7 375 205 8 161 30 0 8 67 76 ...
##  $ shares_count  : num  9 2 8 20 1285 ...
##  $ time          : chr  "15" "14" "13" "13" ...
```

## 分析議題&結果
假設:按讚數.分享數.留言數量越多表示有較高的互動,能帶來的商機.關注也越高
### 1.發文附圖的重要性
"發文不附圖 此風不可長"就算圖文不符,發文附圖才能引起關注
風靡全球的Instagram,其特色就是先以圖片引人注意接著看到下方的文字內容.

```r
#install.packages("ggplot2")
library(ggplot2)
```

```
## Warning: package 'ggplot2' was built under R version 3.3.3
```

```r
ggplot(totalPage,aes(x=type,y=likes_count))+geom_boxplot()+theme_bw() 
```

![](README_files/figure-html/unnamed-chunk-4-1.png)<!-- -->
![](https://drive.google.com/open?id=0Bwv7NFD7P2fyWXVGaXJDSzJ2bzQ)

### 2.發文好時機
12-14多半是大家午休時間,此時發文是個聰明的選擇

```r
library(ggplot2)
dotchart(as.numeric(totalPage$time))
```

![](README_files/figure-html/unnamed-chunk-5-1.png)<!-- -->
![](https://drive.google.com/open?id=0Bwv7NFD7P2fyZDhMMmJnVVZoUEE)

### 不同發文類型的關注度

```r
mean(totalPage$likes_count)  #平均每篇貼文的讚數
```

```
## [1] 7144.438
```

```r
mean(totalPage$comments_count) #下方留言平均數
```

```
## [1] 57.54286
```

```r
mean(totalPage$shares_count) # 分享次篇貼文的次數
```

```
## [1] 354.1048
```

```r
range(totalPage$shares_count)
```

```
## [1]    0 1589
```

```r
library(dplyr)
```

```
## Warning: package 'dplyr' was built under R version 3.3.3
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
totalpage_test <- NULL
totalpage_test <- totalPage
totalpage_test %>% 
  group_by(type) %>%   
          summarize(num_likes = mean(likes_count),
                    num_comment = mean(comments_count),
                    num_share  = mean(shares_count)) %>%
                  arrange(desc(num_likes))
```

```
## # A tibble: 3 × 4
##    type num_likes num_comment num_share
##   <chr>     <dbl>       <dbl>     <dbl>
## 1 photo  8090.628    58.92308  381.8974
## 2  link  6986.182    49.36364  545.6364
## 3 video  2640.562    56.43750   86.9375
```

##  什麼詞彙會刺激大家的額葉? 正能量或負能量?
"旅行" "夢想" "出發"" 等傳遞正能量的字眼,或許這些詞彙(故事)能減少生活的厭世感

```r
#install.packages("rJava")
#install.packages("Rwordseg", repos="http://R-Forge.R-project.org")
#install.packages("tm")
#install.packages("tmcn", repos="http://R-Forge.R-project.org", type="source")
#install.packages("wordcloud")
#install.packages("XML")
#install.packages("RCurl")
#install.packages("RPostgreSQL")
#devtools::install_github("lchiffon/wordcloud2")
#install.packages("htmlwidgets")
#devtools::install_github('ramnathv/htmlwidgets')
options(java.home="C:\\Program Files\\Java\\jre1.8.0_60")
#Sys.setenv(JAVA_HOME="C:\\Program Files\\Java\\jre1.8.0_60\\bin")
library(tm)
```

```
## Warning: package 'tm' was built under R version 3.3.3
```

```
## Loading required package: NLP
```

```
## 
## Attaching package: 'NLP'
```

```
## The following object is masked from 'package:ggplot2':
## 
##     annotate
```

```
## The following object is masked from 'package:httr':
## 
##     content
```

```r
library(tmcn)
```

```
## # tmcn Version: 0.1-4
```

```r
library(rJava)
library(Rwordseg) # 斷詞工具
```

```
## # Version: 0.2-1
```

```r
library(wordcloud)
```

```
## Warning: package 'wordcloud' was built under R version 3.3.3
```

```
## Loading required package: RColorBrewer
```

```r
# 過濾器設定
library(XML)
```

```
## Warning: package 'XML' was built under R version 3.3.3
```

```r
library(wordcloud2)
# 建立文本物件
insertWords(toTrad(iconv(c("有一天","並不是","點個頭","不一定","那一年","花了","不喜歡","一開始"),
                         "big5", "UTF-8"), rev=TRUE))
db.stopwords<-data.frame(V1=c("了","的","https","goo","gl","peter","825","30","要","那就","com","tw","00"))
db.stopwords$V1<-as.character(db.stopwords$V1)
if (length(colnames(db.stopwords)) > 0) {
  my.stopwords <- c(stopwordsCN(), stopwords("english"), db.stopwords[,1])
} else {
  my.stopwords <- c(stopwordsCN(), stopwords("english"))
}
totalPage$message<- enc2utf8(totalPage$message)
totalPage$message<- totalPage$message[Encoding(totalPage$message)!='unknown']
head(segmentCN(totalPage$message))
```

```
## [[1]]
##  [1] "這次"    "我"      "和"      "愛"      "玩"      "客"      "到"     
##  [8] "了"      "日本"    "山"      "形"      "為"      "大家"    "祈福"   
## [15] "還"      "沒"      "看"      "過"      "的"      "朋友"    "現在"   
## [22] "可以"    "在"      "Youtube" "上"      "看到"    "啦"      "祝"     
## [29] "大家"    "雞年"    "行"      "大"      "運"      "<U+653C>" "<U+613C>"
## [36] "<U+623C>" "<U+653C>" "<U+623C>" "大"      "雞"      "大"      "利"     
## [43] "<U+653C>" "<U+613C>" "<U+623C>" "<U+653C>" "<U+623C>" "印"      "鈔"     
## [50] "雞"      "<U+653C>" "<U+613C>" "<U+623C>" "<U+653C>" "<U+623C>" "https"  
## [57] "www"     "youtube" "com"     "watch"   "v"       "FcxAIog" "5"      
## [64] "cEw"     "feature" "youtu"   "be"     
## 
## [[2]]
## [1] "愛"   "玩"   "客"   "首播"
## 
## [[3]]
## [1] "愛"   "玩"   "客"   "首播"
## 
## [[4]]
##  [1] "飛"        "出"        "雲海"      "的"        "那"       
##  [6] "刻"        "我"        "就"        "把"        "那些"     
## [11] "自己"      "不喜歡"    "卻"        "還"        "是"       
## [16] "犯"        "賤"        "放在"      "心裡"      "的"       
## [21] "事情"      "拋開"      "了"        "隨"        "著"       
## [26] "水"        "分子"      "凝結"      "化"        "成"       
## [31] "了"        "雪"        "留"        "在"        "那"       
## [36] "沒"        "人"        "認識"      "我"        "的"       
## [41] "山谷"      "裡"        "山"        "形"        "的"       
## [46] "大地"      "有"        "著"        "無限"      "的"       
## [51] "寬容"      "讓"        "人"        "可以"      "將"       
## [56] "一些"      "東西"      "滯留"      "在"        "那"       
## [61] "希望"      "這"        "一輩子"    "都"        "不用"     
## [66] "再"        "贖回"      "我們"      "等等"      "十點"     
## [71] "愛"        "玩"        "客"        "見"        "Instagram"
## [76] "peter"     "825"      
## 
## [[5]]
##   [1] "我"        "在"        "書"        "裡"        "有"       
##   [6] "句"        "話"        "是"        "這麼"      "說"       
##  [11] "的"        "朋友"      "忽略"      "你"        "時"       
##  [16] "不要"      "傷心"      "每個"      "人"        "都"       
##  [21] "有"        "自己"      "的"        "生活"      "誰"       
##  [26] "都"        "不"        "可能"      "一直"      "陪"       
##  [31] "著"        "你"        "不要"      "過"        "份"       
##  [36] "地"        "去"        "猜測"      "身邊"      "的"       
##  [41] "人"        "對"        "你"        "是否"      "真心"     
##  [46] "也"        "不要"      "過"        "份"        "地"       
##  [51] "去"        "預設"      "對方"      "的"        "立場"     
##  [56] "想"        "得"        "太"        "多只"      "會"       
##  [61] "毀"        "了"        "自己"      "嚴重"      "的"       
##  [66] "更"        "可能"      "破壞"      "掉"        "彼此"     
##  [71] "辛苦"      "建立"      "的"        "感情"      "每個"     
##  [76] "人"        "都"        "有"        "自己"      "的"       
##  [81] "人生"      "要"        "過"        "有時候"    "不"       
##  [86] "是"        "對方"      "忽略"      "了"        "你"       
##  [91] "或許"      "是"        "自己"      "太"        "閒"       
##  [96] "了"        "今天"      "晚上"      "9"         "45"       
## [101] "我們"      "直播"      "見"        "囉"        "Instagram"
## [106] "peter"     "825"      
## 
## [[6]]
##  [1] "沒有"        "缺陷"        "的"          "朋友"        "是"         
##  [6] "很"          "難"          "找"          "到"          "的"         
## [11] "但"          "也"          "正"          "因為"        "如此"       
## [16] "我們"        "看透"        "了"          "彼此"        "卻"         
## [21] "依然"        "站"          "在"          "對方"        "身旁"       
## [26] "我"          "想"          "這"          "就"          "是"         
## [31] "最"          "溫柔"        "的"          "陪伴"        "明天"       
## [36] "晚上"        "10點"        "愛"          "玩"          "客"         
## [41] "首播"        "我"          "會"          "在"          "21"         
## [46] "45線"        "上"          "直播"        "和"          "大家"       
## [51] "先"          "來"          "聊聊"        "看"          "節目"       
## [56] "啊"          "明天"        "見"          "了"          "首集"       
## [61] "預告"        "https"       "youtu"       "be"          "PLapUNAsqEU"
## [66] "Instagram"   "peter"       "825"
```

```r
d<-data.frame(table(unlist(segmentCN(totalPage$message))),decreasing =T)
names(d)<-c("word","freq")
d$word<-as.character(d$word)
wordcloud2(d[!d$word %in% my.stopwords & d$freq>5 & nchar(d$word)>1,], 
           fontFamily = "Microsoft JhengHei", minRotation = -pi/2, maxRotation = -pi/2)
```

<!--html_preserve--><div id="htmlwidget-ed761f915be2105878b5" style="width:672px;height:480px;" class="wordcloud2 html-widget"></div>
<script type="application/json" data-for="htmlwidget-ed761f915be2105878b5">{"x":{"word":["bossini","Instagram","MO","PeterSu","Weibo","一段","一個","一起","一樣","十點","大家","不再","什麼","今天","日子","世界","出發","永遠","生命","生活","因為","地方","有人","你們","希望","快樂","我們","沒有","事情","其實","或許","朋友","狀態","知道","長大","很多","相信","看看","美好","美麗","面對","首播","旅行","時候","時間","海洋","真的","討厭","停止","晚上","現在","這次","這個","這樣","陪伴","喜歡","曾經","森林","無法","無論","發生","路上","夢想","對方","認識","需要","靜靜的","離開","關係","願意"],"freq":[9,69,9,8,7,8,21,41,7,7,11,9,16,12,6,32,13,14,7,7,15,7,6,8,8,6,33,20,7,7,12,13,7,7,8,9,6,9,6,6,8,6,30,10,9,6,7,6,7,13,7,9,7,9,9,22,6,7,9,9,7,7,6,7,7,6,6,9,9,6],"fontFamily":"Microsoft JhengHei","fontWeight":"bold","color":"random-dark","minSize":0,"weightFactor":2.60869565217391,"backgroundColor":"white","gridSize":0,"minRotation":-1.5707963267949,"maxRotation":-1.5707963267949,"shuffle":true,"rotateRatio":0.4,"shape":"circle","ellipticity":0.65,"figBase64":null,"hover":null},"evals":[],"jsHooks":{"render":[{"code":"function(el,x){\n                        console.log(123);\n                        if(!iii){\n                          window.location.reload();\n                          iii = False;\n\n                        }\n  }","data":null}]}}</script><!--/html_preserve-->
![wordcloud2](https://drive.google.com/open?id=0Bwv7NFD7P2fyUzZOSkVCWDJKaEU)

## 分析結果可能解決的問題
  -究竟是甚麼題材內容能夠讓大眾深深被吸引,造成一股旋風.
  -或許就如"看到的人會幸福吧"的概念,勵志書以作者真實的經驗來幫讀者找到抒發情緒的出口，陪同讀者走過低潮
  -一眼抓住讀者目光的詞彙
  -從中可以察覺到出書代言葉配的商機並非偶然 


## 組員名單與分工
胡茹芳—— 滷得很入味的魯蛇
