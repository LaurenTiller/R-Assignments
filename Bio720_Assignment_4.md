---
title: "Bio720 Assignment_4"
author: "Lauren"
date: "November 16, 2018"
output: 
  html_document: 
    keep_md: yes
---



```r
library(dplyr)
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
library(tidyr)
```

#Introduction to ggplot2

##Exploratory vs Explanatory Visualizations

Exploratory visulaization is meant for a specialist audience and generally uses large data sets that are presented in a way to better analyze the data. Explanatory visualizations are intended for a broader audience, such as in a publication, and are designed to prove a point.

##Working with ggplot2


```r
# Load the ggplot2 package
library(ggplot2)

# Explore the mtcars data frame with str()
str(mtcars)
```

```
## 'data.frame':	32 obs. of  11 variables:
##  $ mpg : num  21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
##  $ cyl : num  6 6 4 6 8 6 8 4 4 6 ...
##  $ disp: num  160 160 108 258 360 ...
##  $ hp  : num  110 110 93 110 175 105 245 62 95 123 ...
##  $ drat: num  3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
##  $ wt  : num  2.62 2.88 2.32 3.21 3.44 ...
##  $ qsec: num  16.5 17 18.6 19.4 17 ...
##  $ vs  : num  0 0 1 1 0 1 0 1 1 1 ...
##  $ am  : num  1 1 1 0 0 0 0 0 0 0 ...
##  $ gear: num  4 4 4 3 3 3 3 4 4 4 ...
##  $ carb: num  4 4 1 1 2 1 4 2 2 4 ...
```

```r
# Execute the following command
ggplot(mtcars, aes(x = cyl, y = mpg)) +
  geom_point()
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
# Change the command below so that cyl is treated as factor
ggplot(mtcars, aes(x = factor(cyl), y = mpg)) +
  geom_point()
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-2-2.png)<!-- -->

##The Grammar of Graphics

A plotting framework was established by Leland Wilkinson in 1999. It consists of two key principles. The first being that graphics consists of gramatical element layers (eg. nouns and adjectives) and the second that meaningful plots are produced using aesthetics (eg. a set of grammatical rules for assembling the layers). There are 7 grammatical elements: data, aesthetics, geometries, facets, statistics, coordinates, and themes. Data, aesthetics, and geometries are the most essential. 

##Aesthetics

Some arguments for the aesthetics(aes) of the plot include, colour, size, and shape. See how they are used below to modify the data points based on a third variable (ie. not x or y), the displacement variable (disp). Colour applys a gradient based on the value of the disp variable of each data point. Size does the same as colour but changes the diameter of the point. Shape cannot be used on displacement because it is a continuous variable and there are a finite number of point shapes ggplot can use.


```r
# Colour
ggplot(mtcars, aes(x = wt, y = mpg, color = disp)) +
  geom_point()
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
# Size
ggplot(mtcars, aes(x = wt, y = mpg, size = disp)) +
  geom_point()
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-3-2.png)<!-- -->

```r
# Can't use shape with disp because it is a continuous variable
```

##Geometries


```r
# Example 1:
  
# 1 - Plot the diamonds dataset
ggplot(diamonds, aes(x = carat, y = price)) +
  geom_point() +
  geom_smooth()
```

```
## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
# 2 - Copy the above command but show only the smooth line
ggplot(diamonds, aes(x = carat, y = price)) +
  geom_smooth()
```

```
## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-4-2.png)<!-- -->

```r
# 3 - Copy the above command and assign the value of clarity to color in aes()
ggplot(diamonds, aes(x = carat, y = price, color = clarity)) +
  geom_smooth()
```

```
## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-4-3.png)<!-- -->

```r
# 4 - Keep the color settings from previous command. Plot only the points with argument alpha to make the points 60% transparent.
ggplot(diamonds, aes(x = carat, y = price, color = clarity)) +
  geom_point(alpha = 0.4)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-4-4.png)<!-- -->

```r
# Example 2:

# Create the object containing the data and aes layers: dia_plot
dia_plot <- ggplot(diamonds, aes(x = carat, y = price))

# Add a geom layer with + and geom_point()
dia_plot + geom_point()
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-4-5.png)<!-- -->

```r
# Add the same geom layer, but with aes() inside
dia_plot + geom_point(aes(color = clarity))
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-4-6.png)<!-- -->

```r
# Example 3:

# 1 - The dia_plot object has been created for you
dia_plot <- ggplot(diamonds, aes(x = carat, y = price))

# 2 - Expand dia_plot by adding geom_point() with alpha set to 0.2
dia_plot <- dia_plot + geom_point(alpha = 0.2)

# 3 - Plot dia_plot with additional geom_smooth() with se (error shading) set to FALSE
dia_plot + geom_smooth(se = F)
```

```
## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-4-7.png)<!-- -->

```r
# 4 - Copy the command from above and add aes() with the correct mapping to geom_smooth()
dia_plot + geom_smooth(aes(color = clarity), se = F)
```

```
## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-4-8.png)<!-- -->

#Data

##Base R vs ggplot

###Using Base R


```r
# Example 1: 
# Base R simple plot
plot(mtcars$wt, mtcars$mpg, col= mtcars$fcyl)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

###Limitations of Base R

Base R requires that the legend be set manually, while ggplot will automatically make a legend. ggplot also gives you a plot object that you can modify and when new data is layered on it can adapt to make the data fit more appropriately. This is not the case in base R as it acts as a static image that will not adapt to fit new data. ggplot also takes care of other aspects to make the plot "pretty". It is also more intuitive. However, ggplot has trouble with extremely large datasets and there are other aspects that are more easily manipulated using base R. 

```r
# Basic plot
mtcars$cyl <- as.factor(mtcars$cyl)
plot(mtcars$wt, mtcars$mpg, col = mtcars$cyl)

# Example from base R 
plot(mtcars$wt, mtcars$mpg, col = mtcars$cyl)
abline(lm(mpg ~ wt, data = mtcars), lty = 2)
lapply(mtcars$cyl, function(x) {
  abline(lm(mpg ~ wt, mtcars, subset = (cyl == x)), col = x)
  })
```

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
```

```r
legend(x = 5, y = 33, legend = levels(mtcars$cyl),
       col = 1:3, pch = 1, bty = "n")
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

```r
# Example from ggplot2
ggplot(mtcars, aes(x = wt, y = mpg, col = cyl)) +
  geom_point() + 
  geom_smooth(method = "lm", se = F)+
  geom_smooth(aes(group = 1), method = "lm" , se = F, linetype = 2)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-6-2.png)<!-- -->

##Formatting Data
Tidy data is useful for ggplot to have access to all data as it stores each data point observation seperately. This means that every row is an observation and every column is a variable. Wide format data can also be useful in other cases, depending on how you want to represent the data, as it can group together data into fewer columns.


```r
# Convert iris dataset to tidy format
iris.tidy <- iris %>%
  gather(key, Value, -Species) %>%
  separate(key, c("Part", "Measure"), "\\.")

# Example plotting tidy data
ggplot(iris.tidy, aes(x = Species, y = Value, col = Part)) +
  geom_jitter() +
  facet_grid(. ~ Measure)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

#Aesthetics

Shape can be modified to be solid circle (default, shape=19), hollow (shape=1), and solid with no outline (shape=16) as well as others but these are the most common. For example, shape=21 allows you to use an inside fill colour and an outside line colour. Shape values can go from 1-25 and 1-20 have only a colour aesthetic, but 21-25 also have a fill in addition to the colour aesthetic. Hex codes can be used to specify a specific colour. Note: aesthetics are set in the ggplot command and attributes are set in the geom layers.


```r
#Using colour aesthetic
ggplot(mtcars, aes(x=wt, y=mpg, col=cyl)) +
  geom_point()
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-8-1.png)<!-- -->

```r
#Changing the shape and size of the points
ggplot(mtcars, aes(x=wt, y=mpg, col=cyl)) +
  geom_point(shape=1, size=4)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-8-2.png)<!-- -->

```r
#Using shape=21
ggplot(mtcars, aes(x = wt, y = mpg, fill = cyl, col=am)) +
  geom_point(shape = 21, size = 4, alpha=0.6)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-8-3.png)<!-- -->

```r
#Using a hex code for colour
ggplot(mtcars, aes(x=wt, y=mpg, fill=cyl))+
geom_point(col="#4ABEFF", size=10, shape=23)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-8-4.png)<!-- -->

##Modifying Aesthetics

Different arguments can be added to modify the aesthetics of a plot. One example is modifying the positions of a bar graph (Example 1) and another is modying the axis to create a "fake"" y-axis (dummy aesthetic) (example 2).


```r
#Example 1:

cyl.am <- ggplot(mtcars, aes(x = factor(cyl), fill = factor(am)))

# Add geom (position = "stack" by default)
cyl.am + 
  geom_bar()
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

```r
# Fill - show proportion
cyl.am + 
  geom_bar(position = "fill")  
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-9-2.png)<!-- -->

```r
# Dodging - principles of similarity and proximity
cyl.am +
  geom_bar(position = "dodge") 
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-9-3.png)<!-- -->

```r
# Clean up the axes with scale_ functions
val = c("#E41A1C", "#377EB8")
lab = c("Manual", "Automatic")
cyl.am +
  geom_bar(position = "dodge") +
  scale_x_discrete("Cylinders") + 
  scale_y_continuous("Number") +
  scale_fill_manual("Transmission", 
                    values = val,
                    labels = lab) 
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-9-4.png)<!-- -->

```r
#Example 2:

ggplot(mtcars, aes(x = mpg, y = 0)) +
  geom_jitter()+
  scale_y_continuous(limits=c(-2,2))
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-9-5.png)<!-- -->

##Best Practises

Don't add unnescessary visual information and make the plot easy for the reader to decode. Colour scale can often be confusing and hard to interpret, but this is not always the case. Sequential colours can be useful to show something like an increase in the value of a variable. Aligning plots to a common y-axis can also make them easier to decode. Ways to improve the aesthetics of overplotting include using alpha blending and hollow shapes instead of filled ones. Jitter can be used to make random sctatering of points along the x-axis to show points more clearly where there is a lot. Jitter can be an argument, a geom layer, or a position function within geom_point.


```r
#Example 1:

cyl<- as.factor("cyl")

# Basic scatter plot: wt on x-axis and mpg on y-axis; map cyl to col
ggplot(mtcars, aes(x=wt, y=mpg, col=cyl))+
geom_point(size=4)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

```r
# Hollow circles - an improvement
ggplot(mtcars, aes(x=wt, y=mpg, col=cyl))+
geom_point(size=4, shape=1)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-10-2.png)<!-- -->

```r
# Add transparency - very nice
ggplot(mtcars, aes(x=wt, y=mpg, col=cyl))+
geom_point(size=4, shape=1, alpha=0.6)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-10-3.png)<!-- -->

```r
#Example 2:

# Without Jitter
ggplot(diamonds, aes(x=clarity, y=carat, col=price))+
geom_point(alpha=0.5)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-10-4.png)<!-- -->

```r
# Dot plot with jittering
ggplot(diamonds, aes(x=clarity, y=carat, col=price))+
geom_point(position="jitter", alpha=0.5)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-10-5.png)<!-- -->

#Bar plots

Histograms only require an x-axis aesthetic and no y. By default the data is split into several bins. Three position arguments used for bar plots include stack (bars are stacked on top of each other), fill(proportionate stacking), and dodge(bars side by side).


```r
#Example 1:

#Ploting a histogram with set binwidth and modified y-axis
ggplot(mtcars, aes(x = mpg, y=..density..)) +
  geom_histogram(aes(x = mpg, y=..density..), binwidth=1)
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

```r
#Example 2:

# Draw a bar plot of cyl, filled according to am
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar()
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-11-2.png)<!-- -->

```r
# Change the position argument to stack
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position="stack")
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-11-3.png)<!-- -->

```r
# Change the position argument to fill
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position="fill")
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-11-4.png)<!-- -->

```r
# Change the position argument to dodge
ggplot(mtcars, aes(x = cyl, fill = am)) +
  geom_bar(position="dodge")
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-11-5.png)<!-- -->

#Line Plots

```r
#Basic line plot
ggplot(economics, aes(x = date, y = unemploy)) +
geom_line()
```

![](Bio720_Assignment_4_files/figure-html/unnamed-chunk-12-1.png)<!-- -->























