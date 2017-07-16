# R语言小技巧笔记

xiaoman 20170716

[TOC]

## 1.操作方面

### 1.1 快捷键

**RStudio 常用快捷键**

`Ctrl + L` # 清除控制台输出

`Ctrl + Enter` # 运行光标所在行的R代码 或者 当前选中行的R代码

`Ctrl + Shift + S` # 运行当前脚本文件

`Ctrl + D `# 删除整行

`Ctrl + F `# 查找、替换源程序中的指定字符串

`F3` # 查找下一个字符串

`Ctr + Shift + C `# 注释/取消行注释；可以选中整个代码块进行注释

`Ctrl + O `# 打开文件编辑页面

`Ctrl + W` # 关闭当前文件编辑页面

`Ctrl + Shift + W` # 关闭所有文件编辑页面

`Ctrl + S` # 保存当前文件编辑页面的文件

`Ctrl + Alt + S` # 保存所有文件编辑页面的文件

`Alt  + -`快捷插入“<-”

`rm()`可以清除加载的数据集

### 1.2 快捷处理方式

#### 1.2.1 启动预加载常用包

使用以下代码 插入到R安装目录的etc\Rprofile.site 中

```R
.First <- function(){
  # 加载程序包跟平常一样用library或require
  library(dplyr)
  library(ggplot2)
  library(tidyr)
  cat("xiaoman, you have done loading package: dplyr/tidyr/ggplot2. " )
}
```

#### 1.2.2更换源为国内镜像

```r
local({r <- getOption("repos")
       r["CRAN"] <- "http://mirrors.aliyun.com/CRAN/"
       r["CRANextra"] <- "http://mirrors.ustc.edu.cn/CRAN/"
       options(repos=r)})
```

### 1.3 快捷处理包

