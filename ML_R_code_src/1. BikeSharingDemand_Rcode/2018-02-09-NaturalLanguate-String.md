---
layout : post
title: "Natural Language Processing & Stringr"
author: "ooDoo"
date: 2018-03-03
categories : study
cover : /assets/article_images/title/instacode_sizedown.png
---




#1. stringr package

{% highlight r %}
#Examples
shopping_list <- c("apples x4", "bag of flour", "bag of sugar", "milk x2")
shopping_list
{% endhighlight %}



{% highlight text %}
## [1] "apples x4"    "bag of flour" "bag of sugar" "milk x2"
{% endhighlight %}


## 1) str_extract
: 특정 조건만을 *벡터로* 추출하는 함수

{% highlight r %}
str_extract(shopping_list, "\\d")              # extract number only as character type
{% endhighlight %}



{% highlight text %}
## [1] "4" NA  NA  "2"
{% endhighlight %}



{% highlight r %}
str_extract(shopping_list, "[a-z]+")           # extract word only 
{% endhighlight %}



{% highlight text %}
## [1] "apples" "bag"    "bag"    "milk"
{% endhighlight %}



{% highlight r %}
str_extract(shopping_list, "[a-z]{1,4}")       # extract first 4word mong character
{% endhighlight %}



{% highlight text %}
## [1] "appl" "bag"  "bag"  "milk"
{% endhighlight %}



{% highlight r %}
str_extract(shopping_list, "\\b[a-z]{1,4}\\b") # extract only under 4word among character
{% endhighlight %}



{% highlight text %}
## [1] NA     "bag"  "bag"  "milk"
{% endhighlight %}


## 2) str_extract_all
### (1) list
: 특정 조건만을 *리스트*로 추출하는 함수

{% highlight r %}
# Extract all matches
str_extract_all(shopping_list, "\\d")          # extract number only as list
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] "4"
## 
## [[2]]
## character(0)
## 
## [[3]]
## character(0)
## 
## [[4]]
## [1] "2"
{% endhighlight %}



{% highlight r %}
str_extract_all(shopping_list, "[a-z]+")       # extract all character only as list
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] "apples" "x"     
## 
## [[2]]
## [1] "bag"   "of"    "flour"
## 
## [[3]]
## [1] "bag"   "of"    "sugar"
## 
## [[4]]
## [1] "milk" "x"
{% endhighlight %}



{% highlight r %}
str_extract_all(shopping_list, "\\b[a-z]+\\b") # extract word only but execpt word pated with numbe r as list
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] "apples"
## 
## [[2]]
## [1] "bag"   "of"    "flour"
## 
## [[3]]
## [1] "bag"   "of"    "sugar"
## 
## [[4]]
## [1] "milk"
{% endhighlight %}


### (2) matrix
: 특정 조건만을 *메트릭스*로 추출하는 함수

{% highlight r %}
# Simplify results into character matrix
str_extract_all(shopping_list, "\\d", simplify = TRUE)
{% endhighlight %}



{% highlight text %}
##      [,1]
## [1,] "4" 
## [2,] ""  
## [3,] ""  
## [4,] "2"
{% endhighlight %}



{% highlight r %}
str_extract_all(shopping_list, "\\b[a-z]+\\b", simplify = TRUE)
{% endhighlight %}



{% highlight text %}
##      [,1]     [,2] [,3]   
## [1,] "apples" ""   ""     
## [2,] "bag"    "of" "flour"
## [3,] "bag"    "of" "sugar"
## [4,] "milk"   ""   ""
{% endhighlight %}


### (3) extract_all

{% highlight r %}
# Extract all words
str_extract_all("This is, suprisingly, a sentence.", boundary("word"))
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] "This"        "is"          "suprisingly" "a"           "sentence"
{% endhighlight %}

## 3) str_split  
: 특정 패턴을 기준으로 모든 단어를 쪼개는 방식

{% highlight r %}
# split by pattern
shopping <- "abc,ekq.qpwe*dfji"
str_split(shopping, "[ ]")
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] "abc,ekq.qpwe*dfji"
{% endhighlight %}



{% highlight r %}
str_split(shopping, "[*]")
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] "abc,ekq.qpwe" "dfji"
{% endhighlight %}



{% highlight r %}
str_split(shopping, "[,.]")
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] "abc"       "ekq"       "qpwe*dfji"
{% endhighlight %}



{% highlight r %}
str_split(shopping, "[,.]")[[1]][2]
{% endhighlight %}



{% highlight text %}
## [1] "ekq"
{% endhighlight %}


### (1) strsplit
 : 특정 패턴을 기준으로 단어를 쪼개는 기본 함수
 ※ apply 함수와 함께 사용하여, 모든 row에 일괄 적용 

{% highlight r %}
head(mtcars)
{% endhighlight %}



{% highlight text %}
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
##                     brand
## Mazda RX4           Mazda
## Mazda RX4 Wag       Mazda
## Datsun 710         Datsun
## Hornet 4 Drive     Hornet
## Hornet Sportabout  Hornet
## Valiant           Valiant
{% endhighlight %}



{% highlight r %}
head(strsplit(rownames(mtcars), split = " "))
{% endhighlight %}



{% highlight text %}
## [[1]]
## [1] "Mazda" "RX4"  
## 
## [[2]]
## [1] "Mazda" "RX4"   "Wag"  
## 
## [[3]]
## [1] "Datsun" "710"   
## 
## [[4]]
## [1] "Hornet" "4"      "Drive" 
## 
## [[5]]
## [1] "Hornet"     "Sportabout"
## 
## [[6]]
## [1] "Valiant"
{% endhighlight %}



{% highlight r %}
mtcars$brand <- sapply(strsplit(rownames(mtcars), split = " "), "[", 1)
{% endhighlight %}

  
