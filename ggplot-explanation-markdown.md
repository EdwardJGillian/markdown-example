## ggplot2 - Explanation of some features

### This brief guide explains some of the features of gpplot2 which are not always clear in the documentation.

 It explains how to create a simple barplot using R software and ggplot2 package.  It includes detailed comments on different options to create a barplot.  The data are sourced from the **chickwts** data set.  The dataset **chickwts** describes Chicken Weights by Feed Type.

```ggdf <- filter(chickwts, weight > 100 & weight < 200)``` 

A data set is created from **chickwts** to select:
chicks with a weight > 100 and < 200 

```head(ggdf)```

```
     weight     feed
1    179        horsebean
2    160        horsebean
3    136        horsebean
4    168        horsebean
5    108        horsebean
6    124        horsebean
```
* weight - Weight of the chicks
* feed - type of feed the chicks received

### Create a basic barplot

```
p <- ggplot(data=ggdf, aes(x=weight, y=feed)) +
  geom_bar(stat="identity") +
  ggtitle(" Chicken Weights by feed types") +
  theme(plot.title = element_text(hjust = 0.5))
p
```

![Barplot-basic](ggplot%20images/barplot-basic.png)


### ggplot options explained

* geom_bar() makes the height of the bar proportional to the number of cases in each group
* stat - gives the statistical transformation to use on the data for this layer.
  * stat="identity" - ensures the heights of the bars to represent values in the data
* ggtitle() - adds a title to the plot
* theme(plot.title = element_text(hjust = 0.5)) - ensures title will be centred

### Change the width of bars

```
p <- ggplot(data=ggdf, aes(x=weight, y=feed)) +
  geom_bar(stat="identity", width=0.5) +
  ggtitle(" Chicken Weights by feed types") +
  theme(plot.title = element_text(hjust = 0.5))
p
```
![Bar-Plot-change-width](https://github.com/EdwardJGillian/markdown-example/blob/master/barplot-change-width.png)

* width - changes the width of the bars
  * width value < 1 - means gaps between the bars

### Change the colours of the bars
```
p <- ggplot(data=ggdf, aes(x=weight, y=feed)) +
  geom_bar(stat="identity", width=0.5, color="blue", fill="white") 
p + ggtitle(" Chicken Weights by feed types") +
  theme(plot.title = element_text(hjust = 0.5))
```
* color - changes the borders of the bars
* fill - changes the fill-in color of the bars

![Bar-plot-change-colors](ggplot%20images/barplot-white-fill.png)

### Set a minimal theme + blue fill color
```
p<-ggplot(data=ggdf, aes(x=weight, y=feed)) +
  geom_bar(stat="identity", fill="steelblue")+
  theme_minimal()
p + ggtitle(" Chicken Weights by feed types") +
  theme(plot.title = element_text(hjust = 0.5))
```
![Bar-plot-minimal-theme](ggplot%20images/barplot-minimal-theme.png)
* theme_minimal - A minimalistic theme with no background annotations.

### Set a classic theme + blue fill color
```
p<-ggplot(data=ggdf, aes(x=weight, y=feed)) +
  geom_bar(stat="identity", fill="steelblue")+
  theme_classic()
p + ggtitle(" Chicken Weights by feed types") +
  theme(plot.title = element_text(hjust = 0.5))
```

![Bar-plot-theme-classic](ggplot%20images/barplot-classic-theme.png)

* theme_classic - a classic-looking theme, with x and y axis lines and no gridlines.

### creating bar plots with labels
#### create labels outside bars
```
p <- ggplot(data=ggdf, aes(x=weight, y=feed, fill=feed)) +
     geom_bar(stat="identity", fill="steelblue")+
     geom_text(aes(label=weight), vjust=-0.3, size=3.5)+
     theme_classic()
p + ggtitle(" Chicken Weights by feed types") +
  theme(plot.title = element_text(hjust = 0.5))
```
![Bar-plot-labels-outside](ggplot%20images/barplot-labels-outside.png)

* geom_text - adds text directly to the plot
* aes - describes how variables in the data are mapped to visual properties (aesthetics) of geoms
* vjust -  controls vertical justification - a value of 0.5 centers the text vertically
* hjust - controls horizontal justification - a value of 0.5 centers the text horizontally
   * hjust and vjust are only defined between 0 and 1
* size - size in the geom_text changes the size of the geom_text labels. 
   * This will be different if size is included as an option in the theme()
