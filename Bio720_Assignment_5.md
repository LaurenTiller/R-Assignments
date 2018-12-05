---
title: "Bio720 Assignment 5"
author: "Lauren"
date: "November 29, 2018"
output: 
  html_document: 
    keep_md: yes
---
2.

```r
diploid_selection <- function(p0, w_AA, w_Aa, w_aa, n = 100) {
# Initialize vectors 
  p <- rep(NA,n)  
  w_bar <- rep(NA, n)
  
  # starting conditions
  p[1] <- p0
  w_bar[1] <- ((p[1]^2)*w_AA) + (2*p[1]*(1-p[1])*w_Aa) + (((1-p[1])^2)*w_aa)
  
  # loop from generation to generation
  for ( i in 2:n) {
    w_bar[i-1] <- ((p[i-1]^2)*w_AA) + (2*p[i-1]*(1-p[i-1])*w_Aa) + (((1-p[i-1])^2)*w_aa) 
    p[i] <- ((p[i-1]^2)*(w_AA/w_bar[i-1]) + ((p[i-1]*(1-p[i-1]))*(w_Aa/w_bar[i-1])))
             }
  if (any(p > 0.9999)) {
    fixation_A <- min(which.max(p > 0.9999))
    cat("fixation for A occurs approximately at generation:", fixation_A) 
  } else if (any(p < 0.0001)) {
    fixation_a <- min(which.max(p < 0.0001))
    cat("fixation for a occurs approximately at generation:", fixation_a)
    } else {
      maxAlleleFreq <- max(p)
      cat("fixation of A1 does not occur, max. allele frequency is:", print(maxAlleleFreq, digits=2))
    }
  plot(x = 1:n, y = p, xlab="Generations", ylab="Allele frequency (p)",
     pch = 20, col = "black", cex.lab = 1.0)
}
diploid_selection(p0=0.3, w_AA=1, w_Aa=0.9, w_aa=0.8, n=100)
```

```
## fixation for A occurs approximately at generation: 96
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-1-1.png)<!-- -->

```r
diploid_selection(p0=0.5, w_AA=0.9, w_Aa=0.7, w_aa=0.6, n=100)
```

```
## fixation for A occurs approximately at generation: 39
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-1-2.png)<!-- -->

```r
diploid_selection(p0=0.4, w_AA=0.8, w_Aa=0.9, w_aa=0.6, n=100)
```

```
## [1] 0.75
## fixation of A1 does not occur, max. allele frequency is: 0.7499841
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-1-3.png)<!-- -->

3.

```r
allele_plot <- function(startfreq, allele_number, generations) {
  
allele_freq_A <- rep(NA, generations)
allele_freq_A[1] <- startfreq

for (i in 2:generations) {
allele_counts <- sample(c("A", "a"), size = allele_number, replace = TRUE, prob = c(allele_freq_A[i-1], 1 - (allele_freq_A[i-1])))
allele_freq_A[i] <- sum(allele_counts=="A")/(allele_number)
}
plot(x = 1:generations, y = allele_freq_A, xlab="Generations", ylab="Allele frequency (A)", pch = 20, col = "black", cex.lab = 1.0, type="l")
allele_freq_A
}
allele_plot(0.6, 100, 100)
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```
##   [1] 0.60 0.53 0.56 0.57 0.54 0.71 0.65 0.63 0.63 0.63 0.58 0.49 0.50 0.50
##  [15] 0.54 0.52 0.53 0.54 0.53 0.50 0.53 0.52 0.54 0.56 0.49 0.55 0.56 0.54
##  [29] 0.57 0.54 0.50 0.51 0.42 0.45 0.42 0.38 0.41 0.41 0.43 0.48 0.55 0.57
##  [43] 0.56 0.51 0.51 0.49 0.52 0.56 0.58 0.60 0.59 0.56 0.61 0.56 0.45 0.39
##  [57] 0.36 0.29 0.28 0.34 0.35 0.39 0.38 0.40 0.37 0.38 0.38 0.42 0.34 0.34
##  [71] 0.34 0.18 0.18 0.14 0.23 0.25 0.23 0.27 0.33 0.29 0.37 0.39 0.33 0.33
##  [85] 0.21 0.16 0.10 0.07 0.07 0.08 0.08 0.07 0.07 0.05 0.04 0.06 0.09 0.09
##  [99] 0.12 0.13
```

```r
allele_plot(0.6, 200, 100)
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-2-2.png)<!-- -->

```
##   [1] 0.600 0.525 0.505 0.530 0.505 0.495 0.515 0.535 0.490 0.450 0.440
##  [12] 0.490 0.575 0.580 0.565 0.545 0.560 0.540 0.520 0.545 0.575 0.590
##  [23] 0.615 0.625 0.600 0.615 0.615 0.590 0.650 0.625 0.595 0.650 0.680
##  [34] 0.705 0.690 0.700 0.745 0.755 0.755 0.710 0.730 0.690 0.670 0.635
##  [45] 0.675 0.650 0.610 0.615 0.670 0.650 0.695 0.755 0.730 0.725 0.790
##  [56] 0.775 0.750 0.755 0.715 0.745 0.725 0.735 0.765 0.780 0.740 0.720
##  [67] 0.730 0.685 0.695 0.680 0.735 0.770 0.760 0.745 0.710 0.760 0.745
##  [78] 0.715 0.705 0.680 0.640 0.640 0.620 0.665 0.595 0.595 0.570 0.585
##  [89] 0.610 0.625 0.610 0.565 0.520 0.565 0.560 0.505 0.490 0.455 0.450
## [100] 0.390
```

```r
allele_plot(0.6, 500, 100)
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-2-3.png)<!-- -->

```
##   [1] 0.600 0.604 0.638 0.622 0.622 0.664 0.670 0.690 0.676 0.666 0.678
##  [12] 0.688 0.698 0.668 0.674 0.662 0.684 0.684 0.674 0.652 0.674 0.702
##  [23] 0.712 0.732 0.746 0.784 0.784 0.810 0.786 0.760 0.776 0.760 0.770
##  [34] 0.770 0.810 0.782 0.772 0.788 0.794 0.796 0.800 0.780 0.788 0.810
##  [45] 0.828 0.788 0.796 0.818 0.806 0.816 0.832 0.844 0.844 0.850 0.872
##  [56] 0.878 0.884 0.904 0.914 0.922 0.934 0.960 0.942 0.946 0.952 0.948
##  [67] 0.938 0.944 0.954 0.944 0.958 0.966 0.958 0.964 0.962 0.964 0.964
##  [78] 0.966 0.954 0.950 0.948 0.936 0.924 0.916 0.898 0.902 0.890 0.886
##  [89] 0.878 0.882 0.874 0.902 0.918 0.910 0.912 0.894 0.864 0.870 0.860
## [100] 0.852
```

4.

```r
allele <- function(startfreq, allele_number, generations) {
  
allele_freq_A <- rep(NA, generations)
allele_freq_A[1] <- startfreq

for (i in 2:generations) {
allele_counts <- sample(c("A", "a"), size = allele_number, replace = TRUE, prob = c(allele_freq_A[i-1], 1 - (allele_freq_A[i-1])))
allele_freq_A[i] <- sum(allele_counts=="A")/(allele_number)
}
return(allele_freq_A)
}

replicate_allele <- function(fun=allele, startfreq, allele_number, generations=100, n=1000) {
freq <- replicate(n, fun(startfreq, allele_number, generations))
    return(sum((freq[100,]==0)/n))
}
replicate_allele(fun=allele, startfreq=0.5, allele_number=400)
```

```
## [1] 0.005
```

```r
replicate_allele(fun=allele, startfreq=0.25, allele_number=400)
```

```
## [1] 0.115
```

```r
replicate_allele(fun=allele, startfreq=0.1, allele_number=400)
```

```
## [1] 0.447
```

5.

```r
plot(x = 1, y = 0, type="n",
     xlab="Generations", 
     ylab="Allele frequency (A)", 
     xlim=c(1, 100), 
     ylim=c(0,1),
     main = "The influence of genetic drfit on allele frequencies")
allele <- function(startfreq, allele_number, generations, x) {
allele_freq_A <- rep(NA, generations)
allele_freq_A[1] <- startfreq
for (i in 2:generations) {
allele_counts <- sample(c("A", "a"), size = allele_number, replace = TRUE, prob = c(allele_freq_A[i-1], 1 - (allele_freq_A[i-1])))
allele_freq_A[i] <- sum(allele_counts=="A")/(allele_number)
}
lines(allele_freq_A ~ c(1:x), col=sample(rainbow(6), 1), type="l")
}
replicate(100, allele(0.5, 400, 100, 100))
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```
## [[1]]
## NULL
## 
## [[2]]
## NULL
## 
## [[3]]
## NULL
## 
## [[4]]
## NULL
## 
## [[5]]
## NULL
## 
## [[6]]
## NULL
## 
## [[7]]
## NULL
## 
## [[8]]
## NULL
## 
## [[9]]
## NULL
## 
## [[10]]
## NULL
## 
## [[11]]
## NULL
## 
## [[12]]
## NULL
## 
## [[13]]
## NULL
## 
## [[14]]
## NULL
## 
## [[15]]
## NULL
## 
## [[16]]
## NULL
## 
## [[17]]
## NULL
## 
## [[18]]
## NULL
## 
## [[19]]
## NULL
## 
## [[20]]
## NULL
## 
## [[21]]
## NULL
## 
## [[22]]
## NULL
## 
## [[23]]
## NULL
## 
## [[24]]
## NULL
## 
## [[25]]
## NULL
## 
## [[26]]
## NULL
## 
## [[27]]
## NULL
## 
## [[28]]
## NULL
## 
## [[29]]
## NULL
## 
## [[30]]
## NULL
## 
## [[31]]
## NULL
## 
## [[32]]
## NULL
## 
## [[33]]
## NULL
## 
## [[34]]
## NULL
## 
## [[35]]
## NULL
## 
## [[36]]
## NULL
## 
## [[37]]
## NULL
## 
## [[38]]
## NULL
## 
## [[39]]
## NULL
## 
## [[40]]
## NULL
## 
## [[41]]
## NULL
## 
## [[42]]
## NULL
## 
## [[43]]
## NULL
## 
## [[44]]
## NULL
## 
## [[45]]
## NULL
## 
## [[46]]
## NULL
## 
## [[47]]
## NULL
## 
## [[48]]
## NULL
## 
## [[49]]
## NULL
## 
## [[50]]
## NULL
## 
## [[51]]
## NULL
## 
## [[52]]
## NULL
## 
## [[53]]
## NULL
## 
## [[54]]
## NULL
## 
## [[55]]
## NULL
## 
## [[56]]
## NULL
## 
## [[57]]
## NULL
## 
## [[58]]
## NULL
## 
## [[59]]
## NULL
## 
## [[60]]
## NULL
## 
## [[61]]
## NULL
## 
## [[62]]
## NULL
## 
## [[63]]
## NULL
## 
## [[64]]
## NULL
## 
## [[65]]
## NULL
## 
## [[66]]
## NULL
## 
## [[67]]
## NULL
## 
## [[68]]
## NULL
## 
## [[69]]
## NULL
## 
## [[70]]
## NULL
## 
## [[71]]
## NULL
## 
## [[72]]
## NULL
## 
## [[73]]
## NULL
## 
## [[74]]
## NULL
## 
## [[75]]
## NULL
## 
## [[76]]
## NULL
## 
## [[77]]
## NULL
## 
## [[78]]
## NULL
## 
## [[79]]
## NULL
## 
## [[80]]
## NULL
## 
## [[81]]
## NULL
## 
## [[82]]
## NULL
## 
## [[83]]
## NULL
## 
## [[84]]
## NULL
## 
## [[85]]
## NULL
## 
## [[86]]
## NULL
## 
## [[87]]
## NULL
## 
## [[88]]
## NULL
## 
## [[89]]
## NULL
## 
## [[90]]
## NULL
## 
## [[91]]
## NULL
## 
## [[92]]
## NULL
## 
## [[93]]
## NULL
## 
## [[94]]
## NULL
## 
## [[95]]
## NULL
## 
## [[96]]
## NULL
## 
## [[97]]
## NULL
## 
## [[98]]
## NULL
## 
## [[99]]
## NULL
## 
## [[100]]
## NULL
```

6. 

```r
#Use set.seed to keep it the same across users
set.seed(720)
significant <- function(intercept, slope, sd, samplesize) {
x <- seq(from=1, to=10, length.out = samplesize)
y_deterministic <- intercept + (slope*x)
y_simulated <- rnorm(length(x), mean=y_deterministic, sd)
mod_sim <- lm(y_simulated ~ x)
p_val_slope <- summary(mod_sim)$coef[2,4]
p_val_slope
}

significant(intercept = 0.5, slope = 0.1, sd = 2, samplesize = 20)
```

```
## [1] 0.3620625
```

```r
replicate_significant<-replicate(1000, significant(intercept = 0.5, slope = 0.1, sd = 2, samplesize = 20))

hist(replicate_significant, xlab = "p-value", main = "Frequency of p-values over replicates")
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
#Proportion of p<0.05
sum(replicate_significant<0.05)/length(replicate_significant)
```

```
## [1] 0.107
```

```r
#Change slope to 0
significant(intercept = 0.5, slope = 0, sd = 2, samplesize = 20)
```

```
## [1] 0.2654518
```

```r
replicate_significant_2 <- replicate(1000, significant(intercept = 0.5, slope = 0, sd = 2, samplesize = 20))
hist(replicate_significant_2, xlab = "p-value", main = "Frequency of p-values over replicates")
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-5-2.png)<!-- -->

```r
#Proportion of p<0.05
sum(replicate_significant_2<0.05)/length(replicate_significant_2)
```

```
## [1] 0.048
```

```r
#Proportion of p<0.05 increases as sample size increases
seq1 <- seq(from=10, to=100, by=5)
replicate_significant_3 <- rep(NA, 100)
proportion <- rep(NA, length(seq1))

for (i in 1:length(seq1)) {
replicate_significant_3 <- replicate(100, significant(intercept=0.5, slope=0.1, sd=1.5, samplesize = seq1[i]))
proportion[i]<-sum(replicate_significant_3<0.05)/length(replicate_significant_3)
}
plot(x=seq1, y=proportion, xlab="Sample Size", ylab="Proportion with p<0.05", main = "Proportion of p<0.05 with variation in sample size")
```

![](Bio720_Assignment_5_files/figure-html/unnamed-chunk-5-3.png)<!-- -->


