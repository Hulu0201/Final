# 期末專題報告

## 題目: 勵志書暢銷的背後，吸引讀者的關鍵為何？

## 分析議題背景:
在這出版業人人喊苦,書店一間接著一間熄燈,勵志書籍為何能和工具書並駕齊驅甚至高居排行榜不下 
Peter Su 是近年暢銷書作家,在百花齊放的社群上有著高人氣而出版的著作有著驚人的銷量.能在這出版業哀聲載道, 一刷2000本能賣完是萬幸的寒冬 還能賣出十萬本的書籍究竟是深藏著何種功夫?
這些書暢銷的背後，讀者追尋的是什麼？

## 分析動機:
[話題》勵志散文：在暢銷的背後，讀者追尋的是什麼？](http://www.openbook.org.tw/article/20170225-249) 看到這篇文章覺得很有意思,也想到今年於台北國際書展看到許多勵志書放置在顯眼的平台上,走過去總會忍不住拿起來翻個幾頁或是將封面書腰上的文字快速閱讀過 
網路上對於此類的書籍評價正反兩極 (正方認為能夠帶來舒緩;反方持無病呻吟的看法) 
Peter Su能夠在短短一個月55刷衝破10萬本的銷量,不論內容是什麼,總是讓人很好奇,並想一探究竟

## 資料介紹與來源
假設:因為Peter Su是先由FB貼文引起關注而逐漸擁有許多粉絲,才得以出書.所以這裡並非分析他的著作,而是想透過其臉書內容來了解其為何能有極大的影響力,甚至是商機.
  -資料為暢銷作家Peter Su的臉書貼文(從2016六月至今)

```r
#install.packages("Rfacebook")  
token<-"EAACEdEose0cBAM71XohHnX6jqBQrskMGFbhJK1s6XN3OKIQMF5ZCOgU7vf98OnSqviFuZC5QdOGlejiIGD9TshvsRGiAhtUKSznTAfYSTECCaIgcsjYhkkKd4DE6NaXtPQTLKio7Wprg9ZAPeVnxlg4ag8QZA7tTUUogUJZCGGcN65gxpuhj7caiJeZAPYscUZD" #access token 
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
DateVector<-seq(as.Date("2017-05-01"),lastDate,by="1 days")  
DateVectorStr<-as.character(DateVector)
totalPage<-NULL
for(i in 1:(length(DateVectorStr)-1)){
    tempPage<-getPage("petesonline", token,
                since = DateVectorStr[i],
                until = DateVectorStr[i+1])
    totalPage<-rbind(totalPage,tempPage)
}
```

```
## 1 posts 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 1 posts 1 posts 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 1 posts 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 1 posts 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 1 posts 1 posts 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 0 posts
```

```
## No public posts were found : petesonline
```

```
## 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 1 posts 1 posts 1 posts 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 1 posts 2 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 0 posts
```

```
## No public posts were found : petesonline
```

```
## 1 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 2 posts 0 posts
```

```
## No public posts were found : petesonline
```

```
## 0 posts
```

```
## No public posts were found : petesonline
```

```
## 2 posts
```

```r
nrow(totalPage) #有幾筆資料
```

```
## [1] 33
```

## 格式

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
## 'data.frame':	33 obs. of  8 variables:
##  $ message       : chr  "夏天是讓人想要奮不顧身去旅行的季節，那藍天太美、世界太大，所以我一定要去看看，外面的世界或許沒有自己想像中的完美，我們都無法決"| __truncated__ "你走的那天，我開始旅行，從此四海為家，不再問有你的遠方。\n\nInstagram: peter825" "如果說愛你是需要練習的，那不愛也是，曾經因為你的加入而變得美好，但也會因為你的缺席而變得更好。\n\nInstagram: peter825" "小時候世界很大，認識的人很少，深交的人很多；長大後的世界很小，認識的人很多，深交的人很少，或許如此才明顯地感受到這世界，路過的"| __truncated__ ...
##  $ created_time  : chr  "2017-05-01T13:28:06+0000" "2017-05-02T13:53:12+0000" "2017-05-04T14:06:13+0000" "2017-05-05T13:37:05+0000" ...
##  $ type          : chr  "photo" "photo" "photo" "photo" ...
##  $ story         : chr  NA NA NA NA ...
##  $ likes_count   : num  3320 7168 7783 10154 6678 ...
##  $ comments_count: num  6 24 64 68 51 29 56 108 73 15 ...
##  $ shares_count  : num  50 135 245 732 331 ...
##  $ time          : chr  "13" "13" "14" "13" ...
```

## 分析議題&結果
假設:按讚數.分享數.留言數量越多表示有較高的互動,能帶來的商機.關注也越高
### 發文附圖的重要性
發文不附圖 此風不可長
風靡全球的Instagram,其特色就是圖片在搭配一些文字.

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

### 發文好時機
12-14多半是大家午休時間,此時發文是個聰明的選擇

```r
library(ggplot2)
dotchart(as.numeric(totalPage$time))
```

![](README_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

### 不同發文類型的關注度

```r
mean(totalPage$likes_count)  #平均每篇貼文的讚數
```

```
## [1] 7673.121
```

```r
mean(totalPage$comments_count) #下方留言平均數
```

```
## [1] 56.54545
```

```r
mean(totalPage$shares_count) # 分享次篇貼文的次數
```

```
## [1] 419.9394
```

```r
range(totalPage$shares_count)
```

```
## [1]    0 1194
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
## 1 photo  8649.174    60.78261  466.8261
## 2 video  5801.800    49.20000  252.6000
## 3  link  5054.600    44.40000  371.6000
```
##探索式資料分析

```r
#install.packages("jiebaR")
library(jiebaR)
```

```
## Warning: package 'jiebaR' was built under R version 3.3.3
```

```
## Loading required package: jiebaRD
```

```
## Warning: package 'jiebaRD' was built under R version 3.3.3
```

```r
cutter <- worker()
#新增詞彙
new_user_word(cutter,'並不是',"n")
```

```
## [1] TRUE
```

```r
new_user_word(cutter,'有一天',"n")
```

```
## [1] TRUE
```

```r
new_user_word(cutter,'點個頭',"n")
```

```
## [1] TRUE
```

```r
new_user_word(cutter,'不一定',"n")
```

```
## [1] TRUE
```

```r
new_user_word(cutter,'那一年',"n")
```

```
## [1] TRUE
```

```r
new_user_word(cutter,'花了',"n")
```

```
## [1] TRUE
```

```r
new_user_word(cutter,'不喜歡',"n")
```

```
## [1] TRUE
```

```r
new_user_word(cutter,'一開始',"n")
```

```
## [1] TRUE
```

```r
head(sort(table(cutter[totalPage$message]),decreasing = T))
```

```
## 
##  的  你  我  人  是  了 
## 147  46  31  24  24  21
```
##  什麼詞彙會刺激大家的額葉? 正能量或負能量?
旅行 夢想 出發 等傳遞正能量的字眼

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
library(Rwordseg) # 中文斷詞工具
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
head(segmentCN(totalPage$message))
```

```
## [[1]]
##   [1] "夏天"     "是"       "讓"       "人"       "想"       "要"      
##   [7] "奮不顧身" "去"       "旅行"     "的"       "季節"     "那"      
##  [13] "藍天"     "太"       "美"       "世界"     "太"       "大"      
##  [19] "所以"     "我"       "一定"     "要"       "去"       "看看"    
##  [25] "外面"     "的"       "世界"     "或許"     "沒有"     "自己"    
##  [31] "想像"     "中"       "的"       "完美"     "我們"     "都"      
##  [37] "無法"     "決定"     "這"       "段"       "旅程"     "的"      
##  [43] "好"       "與"       "壞"       "但"       "只要"     "我們"    
##  [49] "願意"     "輕柔"     "的"       "去"       "面對"     "世界"    
##  [55] "必然"     "會"       "給予"     "我們"     "一個"     "美好"    
##  [61] "的"       "溫度"     "喜歡"     "夏天"     "的"       "視野"    
##  [67] "想"       "要"       "帶"       "著"       "清爽"     "不"      
##  [73] "黏"       "膩"       "的"       "心情"     "去"       "旅行"    
##  [79] "我"       "的"       "清爽"     "女"       "力"       "水"      
##  [85] "潤"       "不"       "黏"       "膩"       "妮"       "維"      
##  [91] "雅"       "深層"     "修"       "護"       "乳"       "液"      
##  [97] "https"    "goo"      "gl"       "z"        "8"        "LDBU"    
## 
## [[2]]
##  [1] "你"        "走"        "的"        "那天"      "我"       
##  [6] "開始"      "旅行"      "從此"      "四海為家"  "不再"     
## [11] "問"        "有"        "你"        "的"        "遠方"     
## [16] "Instagram" "peter"     "825"      
## 
## [[3]]
##  [1] "如果"      "說"        "愛"        "你"        "是"       
##  [6] "需要"      "練習"      "的"        "那"        "不"       
## [11] "愛"        "也"        "是"        "曾經"      "因為"     
## [16] "你"        "的"        "加入"      "而"        "變"       
## [21] "得"        "美好"      "但"        "也"        "會"       
## [26] "因為"      "你"        "的"        "缺席"      "而"       
## [31] "變"        "得"        "更"        "好"        "Instagram"
## [36] "peter"     "825"      
## 
## [[4]]
##  [1] "小時候"    "世界"      "很"        "大"        "認識"     
##  [6] "的"        "人"        "很"        "少"        "深"       
## [11] "交"        "的"        "人"        "很"        "多"       
## [16] "長大"      "後"        "的"        "世界"      "很小"     
## [21] "認識"      "的"        "人"        "很"        "多"       
## [26] "深"        "交"        "的"        "人"        "很"       
## [31] "少"        "或許"      "如此"      "才"        "明顯"     
## [36] "地"        "感受"      "到"        "這"        "世界"     
## [41] "路過"      "的"        "人"        "很"        "多"       
## [46] "留"        "下"        "來"        "的"        "人"       
## [51] "很"        "重要"      "願"        "我們"      "在"       
## [56] "顛沛流離"  "的"        "世界"      "裡"        "找到"     
## [61] "屬"        "於"        "彼此"      "的"        "溫暖"     
## [66] "Instagram" "peter"     "825"      
## 
## [[5]]
##  [1] "之所以"    "還"        "有"        "勇氣"      "去"       
##  [6] "面對"      "這個"      "世界"      "是因為"    "無論"     
## [11] "再"        "遠"        "再"        "累"        "心裡"     
## [16] "還有"      "一些"      "人"        "陪"        "著"       
## [21] "那種"      "感覺"      "就"        "像"        "是"       
## [26] "即使"      "他們"      "都"        "不"        "在"       
## [31] "身邊"      "心裡"      "有"        "個"        "人"       
## [36] "陪"        "著"        "自己"      "面對"      "面對"     
## [41] "那些"      "說"        "不"        "出口"      "的"       
## [46] "秘密"      "Instagram" "peter"     "825"      
## 
## [[6]]
##  [1] "這次" "去"   "了"   "非常" "多"   "顛覆" "自己" "印象" "的"   "香港"
## [11] "讓"   "我"   "對"   "這"   "裡"   "又"   "多"   "了"   "更"   "多"  
## [21] "想"   "念"   "的"   "地方" "希望" "下次" "可以" "和"   "朋友" "一起"
## [31] "過來" "分享" "下次" "見"   "了"   "香港" "<U+653C>" "<U+613C>" "<U+623C>" "<U+653C>"
## [41] "<U+623C>" "<U+613C>" "<U+653C>" "<U+613C>" "<U+623C>" "<U+653C>" "<U+623C>" "<U+623C>" "<U+653C>" "<U+613C>"
## [51] "<U+623C>" "<U+653C>" "<U+623C>" "<U+653C>" "<U+613C>" "<U+623C>" "<U+653C>" "<U+623C>" "<U+623C>"
```

```r
d<-data.frame(table(unlist(segmentCN(totalPage$message))),decreasing =T)
names(d)<-c("word","freq")
d$word<-as.character(d$word)
wordcloud2(d[!d$word %in% my.stopwords & d$freq>5 & nchar(d$word)>1,], 
           fontFamily = "Microsoft JhengHei", minRotation = -pi/2, maxRotation = -pi/2)
```

<!--html_preserve--><div id="htmlwidget-1ad028d61640c69b091e" style="width:672px;height:480px;" class="wordcloud2 html-widget"></div>
<script type="application/json" data-for="htmlwidget-1ad028d61640c69b091e">{"x":{"word":["bossini","growup","Instagram","一個","一起","什麼","分享","世界","出發","永遠","因為","你們","我們","或許","美好","旅行","時候","時間","停止","無法","無論"],"freq":[9,7,20,12,21,11,6,18,6,7,6,7,14,7,7,19,8,6,7,6,6],"fontFamily":"Microsoft JhengHei","fontWeight":"bold","color":"random-dark","minSize":0,"weightFactor":8.57142857142857,"backgroundColor":"white","gridSize":0,"minRotation":-1.5707963267949,"maxRotation":-1.5707963267949,"shuffle":true,"rotateRatio":0.4,"shape":"circle","ellipticity":0.65,"figBase64":null,"hover":null},"evals":[],"jsHooks":{"render":[{"code":"function(el,x){\n                        console.log(123);\n                        if(!iii){\n                          window.location.reload();\n                          iii = False;\n\n                        }\n  }","data":null}]}}</script><!--/html_preserve-->


## 分析結果可能解決的問題
-究竟是甚麼題材內容能夠讓大眾深深被吸引,造成一股旋風.
  -或許就如"看到的人會幸福吧"的概念,勵志書以作者真實的經驗來幫讀者找到抒發情緒的出口，陪同讀者走過低潮
  -一眼抓住讀者目光的詞彙
  -出書代言葉配的商機 


## 組員名單與分工
胡茹芳—— 滷得很入味的魯蛇

# 感謝老師如buzzer beater的救援
