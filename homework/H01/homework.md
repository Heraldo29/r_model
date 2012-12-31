Week 1 Homework
==============
## 书面作业
### 2.2
将1,2,..20 构成两个4*5阶的矩阵, 其中矩阵A是按列输入,矩阵B按行输入,做如下运算:


#### (1) C=A+B

```r
C <- A + B
C
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    2    7   12   17   22
## [2,]    8   13   18   23   28
## [3,]   14   19   24   29   34
## [4,]   20   25   30   35   40
```

#### (2) D=AB

```r
D <- A %*% B
```

```
## Error: non-conformable arguments
```

#### (3) E=$(e_{ij})_{n \times n}$, 其中$e_{ij}=a_{ij}*b_{ij}$

```r
E <- A * B
E
```

```
##      [,1] [,2] [,3] [,4] [,5]
## [1,]    1   10   27   52   85
## [2,]   12   42   80  126  180
## [3,]   33   84  143  210  285
## [4,]   64  136  216  304  400
```

#### (4) F是由A的前3行和前3列构成的矩阵;

```r
F <- A[1:3, 1:3]
F
```

```
##      [,1] [,2] [,3]
## [1,]    1    5    9
## [2,]    2    6   10
## [3,]    3    7   11
```

#### (5) G是由矩阵B的各列构成的矩阵,但不含B的第三列.

```r
G <- B[, c(1:2, 4:ncol(B))]
G
```

```
##      [,1] [,2] [,3] [,4]
## [1,]    1    2    4    5
## [2,]    6    7    9   10
## [3,]   11   12   14   15
## [4,]   16   17   19   20
```


### 2.3 
构造一个向量x,向量是由5个1,3个2,4个3和2个4构成.

```r
x <- c(rep(1, 5), rep(2, 3), rep(3, 4), rep(4, 2))
x
```

```
##  [1] 1 1 1 1 1 2 2 2 3 3 3 3 4 4
```


### 2.4
生成一个5阶的Hilbert矩阵,
$H=(h_{ij})_{n \times n}$, $h_{ij}=\frac{1}{i+j-1}$,$i,j = 1,2, \ldots, n.$

```r
n <- 5
H <- matrix(0, n, n)
for (i in 1:n) {
    for (j in 1:n) {
        H[i, j] <- 1/(i + j - 1)
    }
}
H
```

```
##        [,1]   [,2]   [,3]   [,4]   [,5]
## [1,] 1.0000 0.5000 0.3333 0.2500 0.2000
## [2,] 0.5000 0.3333 0.2500 0.2000 0.1667
## [3,] 0.3333 0.2500 0.2000 0.1667 0.1429
## [4,] 0.2500 0.2000 0.1667 0.1429 0.1250
## [5,] 0.2000 0.1667 0.1429 0.1250 0.1111
```


#### (1) 计算Hilbert矩阵$H$的行列式.

```r
det(H)
```

```
## [1] 3.749e-12
```

#### (2) 求$H$的逆矩阵

```r
solve(H, diag(n))
```

```
##       [,1]   [,2]    [,3]    [,4]   [,5]
## [1,]    25   -300    1050   -1400    630
## [2,]  -300   4800  -18900   26880 -12600
## [3,]  1050 -18900   79380 -117600  56700
## [4,] -1400  26880 -117600  179200 -88200
## [5,]   630 -12600   56700  -88200  44100
```

#### (3) 求$H$的特征值和特征向量

```r
V = eigen(H)
```

特征值为1.5671, 0.2085, 0.0114, 3.059 &times; 10<sup>-4</sup>, 3.2879 &times; 10<sup>-6</sup>,特征向量为

```r
V$vectors
```

```
##         [,1]    [,2]    [,3]     [,4]      [,5]
## [1,] -0.7679  0.6019 -0.2142  0.04716  0.006174
## [2,] -0.4458 -0.2759  0.7241 -0.43267 -0.116693
## [3,] -0.3216 -0.4249  0.1205  0.66735  0.506164
## [4,] -0.2534 -0.4439 -0.3096  0.23302 -0.767191
## [5,] -0.2098 -0.4290 -0.5652 -0.55760  0.376246
```



### 2.5
有5名学生的数据,如表2.3所示.用数据框的形式读入数据.

```r
students <- data.frame(姓名 = c("张三", "李四", "王五", "赵六", "丁一"), 
    性别 = c("女", "男", "女", "男", "女"), 年龄 = c(14, 15, 16, 14, 
        15), 身高 = c(156, 165, 157, 162, 159), 体重 = c(42, 49, 41.5, 52, 
        45.5))
students
```

```
##   姓名 性别 年龄 身高 体重
## 1 张三   女   14  156 42.0
## 2 李四   男   15  165 49.0
## 3 王五   女   16  157 41.5
## 4 赵六   男   14  162 52.0
## 5 丁一   女   15  159 45.5
```

### 2.6
将题2.5中的数据表2.3的数据写成一个纯文本文件,用函数read.table()读该文件,然后再用函数write.csv()写成一个能用Excel表打开的文件,并用Excel表打开.

```r
students_loaded <- read.table("students.data", header = T)
students_loaded
```

```
##   姓名 性别 年龄 身高 体重
## 1 张三   女   14  156 42.0
## 2 李四   男   15  165 49.0
## 3 王五   女   16  157 41.5
## 4 赵六   男   14  162 52.0
## 5 丁一   女   15  159 45.5
```

```r
write.csv(students_loaded, file = "students.csv")
```
