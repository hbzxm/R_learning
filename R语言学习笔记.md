---
typora-copy-images-to: pic
---

# R 语言学习笔记

[xiaoman 2017暑假]
[TOC]

## 1. R语言的基本特性

* R 语言是一种统计学语言，在R环境下运行，因有许多功能包而著名。

* R 语言是 **区分大小写 **的解释型语言。

* R 使用` <- `  符号来赋值，快捷键是Alt + -

* R 使用 ` # ` 号 作为注释起始

* 查看帮助使用 ` help("ggplot2") `或 `?ggplot2 `

  r语言能绘制很多酷炫的科学图表

  ![聚类热图](pic\Rplot11.png)



## 2. R 语言常见操作

### 2.1 设置工作目录以及目录相关操作

养成良好的习惯设定工作目录十分重要，你懂的！

设定工作目录 ` setwd() `  查看工作目录 ` getwd() `  ，目录中使用**正斜杠**或者**双反斜杠** 

`file.choose()` 函数比较有用，能弹出选择框手动选择路径

### 2.2 管理空间操作

![常见管理函数](pic\17.png)
### 2.3 关于package 的操作

`install.package("name")` 安装package

`library("name")` 索引package

### 2.4 数据类型

![R语言数库类型](pic\18.png)

不同的行业对于数据集的行和列叫法不同。统计学家称它们为观测（observation）和变量
（variable），数据库分析师则称其为记录（record）和字段（field），数据挖掘和机器学习学科的研
究者则把它们叫作示例（example）和属性（attribute） 。

#### 2.4.1 向量

**向量（Vector）** 是用于存储数值型、字符型或逻辑型数据的一维数组。执行组合功能的函数c()可用来
创建向量 

``` R
a <- c(1, 2, 5, 3, 6, -2, 4)
b <- c("one", "two", "three")
c <- c(TRUE, TRUE, TRUE, FALSE, TRUE, FALSE) 
```

* 单个向量中的数据必须拥有相同的类型或模式 

* **标量**是只含一个元素的向量 
#### 2.4.2  矩阵

**矩阵（matrix）**是一个二维数组，只是每个元素都拥有**相同的模式**（数值型、字符型或逻辑型） 。可通
过函数``matrix()``创建矩阵

``` R
myymatrix <- matrix(vector, 
                    nrow=number_of_rows, 
                    ncol=number_of_columns,
                    byrow=logical_value, 
                    dimnames=list(char_vector_rownames, char_vector_colnames)
                   )
```

#### 2.4.3 数据框

**数据框（Data Frame）** 是一个由向量组构成的数据，类似数据库结构。数据框是在R语言中最为常见的数据结构。

```R
ID <- c(1,2,3,4)
age <- c(25,34,28,52)
status <- c("Pool" , "Improved" , "Excellent", "Poor")
patient.data <- data.frame(ID, age, status)
```

运行结果

![22](pic\22.png)



数据框的操作：

* 选取数据框中的变量（列）： ` patient.data[2]`  

  > patient.data[2]
  >
  >    age
  > 1  25
  > 2  34
  > 3  28
  > 4  52

* 选取特定变量：` patient.data[c("ID","status")] `

  > patient.data[c("ID","status" )]
  >    ID    status
  > 1  1      Pool
  > 2  2  Improved
  > 3  3 Excellent
  > 4  4      Poor

* 将变量添加到索引 `atttach()` 和 取消索引`detach()`   如果attach后的变量名称与已经存在的变量冲突，则以之前存在的变量为准。 养成习惯局部使用，及时解除。

* `with()`函数可以局部执行命令 

  ```R
  with(patient.data,{
    summary(age)
  })
  ```


> with(patient.data,{
>
> ​				summary(age)
>
> ​				})
> 花括号{}之间的语句都针对数据框执行，这样就无需担心名称冲突了。如果仅有一条语句，那么花括号{}可以省略。函数with()的局限性在于，**赋值仅在此函数的括号内生效**。如果你需要创建在with()结构以外存在的对象，使用特殊赋值符`<<-`替代标准赋值符`<-`即可，它可将对象保存到with()之外的全局环境中


#### 2.4.5 因子

变量可归结为名义型、有序型或连续型变量。 名义型变量是没有顺序之分的类别变量。 有序型变量表示一种顺序关系，而非数量关系。 

#### 2.4.6 列表

列表（list）是R的数据类型中最为复杂的一种。一般来说， 列表就是一些对象（或成分， component）的有序集合。可以组合任意多的对象，并将它们保存为一个列表 

### 2.5 需要注意的地方

* R语言中的“ . ” 没有特殊含义，但是 “ $ ” 是提取子集的符号
* R不提供多行注释，可以用if (false){ ......   } 来设定调试开关
* R下标从0开始
* R严格区分大小写

### 2.6 数据的输入 

#### 2.6.1数据手动导入

Rstudio 有手动数据导入功能 支持常用数据集

![0009](pic\0009-9135761748.png)

 



#### 2.6.2 数据自动导入



``mydataframe <- read.table(file, options) ``

![010](pic\010.png)
例如
```R
grades <- read.table("studentgrades.csv",
					header=TRUE,
					row.names="StudentID", 	
					sep=",") 
```

#### 2.6.3 数据包的移除

使用rm() 可以移除不需要的数据集以节省内存占用 ，rm=**r**elease **m**emory

## 3 数据的基本操

### 3.1 变量的增减

* 增加变量 可以用新赋值方式 

`` new.data <- data+ data2``

* 直接在数据框中增加变量

```R
mydata<-data.frame(x1 = c(2, 2, 6, 4),
				 x2 = c(3, 4, 2, 8)
				 )
mydata$sumx <- mydata$x1 + mydata$x2
mydata$meanx <- (mydata$x1 + mydata$x2)/2
# or
mydata <- transform(mydata,
		  		   sumx = x1 + x2,
		            meanx = (x1 + x2)/2
                    )
```

> \>mydata
>  x1 x2
> 1  2  3
> 2  2  4
> 3  6  2
> 4  4  8
>
> \>mydata\$sumx <- mydata\$x1 + mydata\$x2
>
> \>mydata\$meanx <- (mydata\$x2)/2
>
> \>mydata
>
>   x1 x2 sumx meanx
> 1  2  3    5   2.5
> 2  2  4    6   3.0
> 3  6  2    8   4.0
> 4  4  8   12   6.0

* 按照变量归类 

  重编码涉及根据同一个变量和/或其他变量的现有值创建新值的过程。
   将一个连续型变量修改为一组类别值；
   将误编码的值替换为正确值；
   基于一组分数线创建一个表示及格/不及格的变量。

逻辑符号如下表

![011](pic\011.png)

例如 

案例数据

>mydata
>   ID mRNA   pval  fc
>1 pd1   10 0.0001 2.5
>2 pd2    8 0.0500 1.0
>3 pd3    6 0.2000 0.2
>4 pd4    8 0.0040 0.1
>5 pd5    3 0.0120 0.3
>6 pd6    4 0.5000 2.0
>7 pd7    1 0.0300 1.5
>8 pd8    7 0.3500 1.8



```R
mydata$diff[mydata$fc > 1.5] <- "Up"
mydata$diff[mydata$fc < 0.6] <- "Down"
mydata$diff[mydata$fc <= 1.5 & mydata$fc >= 0.6] <- "ns"
```

运行结果 

![12](pic\12.png)

另外一种写法 

```r
mydata <- within(mydata,{
 					 diff <- NA
 					 diff[fc > 1.5] <- "Up"
  					 diff[fc < 0.6] <- "Down"
 					 diff[fc <= 1.5 & mydata$fc >= 0.6] <- "ns"
  					})
mydata$diff <- factor(mydata$diff) # 转化成因子便于后续处理数据
```

### 3.2 数据的简单手动编辑

**可以使用``edit(mydata)``函数修改数据集中的内容，如果是另存为其他数据则使用**``mydata <- edit(mydata) ``

直接修改并保存 使用 `fix(...)`

## 4 数据的清洗与处理

使用dplyr包对数据进行清洗和预处理

在清理数据之前，建议使用`tbl_df()`函数进行数据转换预处理，可以提高处理速度。如果处理更庞大的数据，dplyr建议使用tibble类型数据集，转换方式为 as_tibble().



### 4.1 单表操作命令

单表操作的基本函数和参数

`filter()` 根据参数的值来选择列表的内容

`arrange()` 根据指定参数来排序

`select()`选择列`rename()`重命名参数

`mutate()`计算结果生成新列

`summarise()` 将多个值汇总到一个值

`sample_n()` 和`sample_frac()` 随机抽样函数



下面是具体的用法

#### 4.1.1 filter()

![filter](pic\16.png)

`filter()` 函数可以按值来筛选变量，语法相对简单

例如，筛选TCGA膀胱样本中的实体瘤样本 并保存为Bladder.T

```r
Bladder.T <- filter(Bladder,sample_type == "Primary solid Tumor")
```

跟帅气的写法是这样的 

``` r
Bladder %>% 
filter(sample_type == "Primary solid Tumor") -> Bladder.T
```

运行结果完全一样 

![15](pic\15.png)

如果没有高大上的dplyr包 我们需要这样写才能实现以上功能

```r
Bladder.T <- Bladder[sample_type == "Primary solid Tumor",] # 注意最后的逗号以及用法 
```

当筛选条件很多的情况，可以用到``%in%`` 符号

例如需要选出CTSA基因表达值在11.8 和11 这两个值时 代码可以这样写 

```r
filter(bla,CTSA %in% c(10.8,11))
```

注意： 这里需要提醒的是，对于多条件的选择，需要完整条件的，然后使用集合运算符将条件拼接起来。集合运算符有 !、|、&、xor(交补)。条件的判断符有>(=)、<(=)、==、!=、%in% (判断元素是否在集合或者列表内，返回逻辑值)。

需要注意的是 `filter()` 函数筛选的是正则表达式为true 的行**

表达式符号

![表达式符号](pic\14.png)

#### 4.1.2 arrange()

![arrange](pic\17-9702513596.png)

`arrange()`用于对变量排序，函数与filter()语法类似 

`arrange(data,rule1,rule2,... )` 

降序叠加使用desc()，如`arrange(data,rule1,desc(rule2),... )`



#### 4.1.3 select()

![seclect](pic\18-9702577977.png)

`select()`函数用于选择感兴趣的列 ，

用法`select(data, colname1, colname2, ...)`  

也可以用排除的方法`select(data, -colname1, -colname2, ...)`

当然也可以用选择函数`select(data, contains(...), ends_with(...), ...)`

#### 4.1.4 mutate()

mutate 用于添加新的变量，直接使用列名进行计算得到新变量即可。而且它很有特色地方是，可以使用刚添加的变量，也就是在一个语句中可以多个变量，而且变量可以来源于刚新建的变量

`mutate(.data, average=(x1+x2+x3)/3 )`

#### 4.1.5 summarize()

summarise 可以用于“分类汇总”，但不是传统意义上的分类汇总，它还能做更多。

　　实际上它是把我们现有的完整 data frame 依据分组依据（这里是 color）拆分成多个data frame，然后对每个 data frame 分别计算，类似于ddply。

　　使用经历：分组依据可以多个，比如根据城市、月份、年份，我们对数据进行分类汇总，可以得到每个城市每一年每月的情况。

summarise 可以使用的函数有：

- min(x), median(x), max(x), quantile(x, p),IQR()等统计量
- n()返回观测个数, n_distinct()返回不同的观测个数, sum(x), mean(x)
- sum(x > 10), mean(x > 10)
- sd(x)标准差, var(x)方差, iqr(x), mad(x)
- first()返回第一个观测
- last()返回最后一个观测
- nth(x,n)返回第n个观测

#### 4.1.6 rename()

#### 4.1.7 sample_n() 和 sample_frac()

抽样函数，使用方式相同 sample_n(.data, size )















