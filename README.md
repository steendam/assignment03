# Assignment 3
Patrick D. Schloss  
September 26, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 3 repository](http://www.github.com/microbialinformatics/assignment03).  Format this document appropriately using R markdown and knitr. For those cases where there are multiple outputs, make it clear in how you format the text and interweave the solution, what the solution is.

Your pull request should only include your *.Rmd and *.md files. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment and to any websites that you used along your way. You should not use any packages beyond the base R system and knitr.

This assignment is due on October 10th.

------

1.  Generate a plot that contains the different pch symbols. Investigate the knitr code chunk options to see whether you can have a pdf version of the image produced so you can print it off for your reference. It should look like this:

    <img src="pch.png", style="margin:0px auto;display:block" width="500">

```r
pchvalues <- 1:25
#To print the image as a pdf file, I simply un-comment the next code:
#pdf('rplot1.pdf')
plot1 <- plot(x=1, y=1, pch= pchvalues[1], xlim = c(1,25), xlab = "PCH Values", main = "PCH Symbols", yaxt='n', ylab="", cex = 2.3)
abline(v=1);
i = 1
repeat
{
i = i +1 
points(x=i, y=1, pch= pchvalues[i], cex = 2.3)
abline(v=i)
if (i > 25)
break;
}
```

![plot of chunk unnamed-chunk-1](./README_files/figure-html/unnamed-chunk-1.png) 

```r
rm(plot1, pchvalues)
```

The final result can also be seen in an attached .pdf file, named *rplot1.pdf*. 

2.  Using the `germfree.nmds.axes` data file available in this repository, generate a plot that looks like this. The points are connected in the order they were sampled with the circle representing the beginning and the square the end of the time course:

    <img src="beta.png", style="margin:0px auto;display:block" width="700">
      

```r
#To print the image as a pdf file, I simply un-comment the next code:
#pdf('rplot2.pdf')
germfree <- read.table(file="germfree.nmds.axes", header=T)
#The black line is the most in the back
plot(x=germfree$axis1[1:20], y=germfree$axis2[1:20], type = "l", xlim = c(-0.3, 0.7), ylim = c(-0.56, 0.41), lwd = 2, xlab = "NMDS Axis 1", ylab = "NMDS Axis 2")
#Then there is the blue line
points(x=germfree$axis1[21:41], y=germfree$axis2[21:41], type = "l", col = "blue", lwd = 2)
#Then there is the red line
points(x=germfree$axis1[42:61], y=germfree$axis2[42:61], type = "l", col = "red", lwd = 2)
#Then there is the green line
points(x=germfree$axis1[62:82], y=germfree$axis2[62:82], type = "l", col = "green", lwd = 2)
#Then there is the brown line
points(x=germfree$axis1[83:103], y=germfree$axis2[83:103], type = "l", col = "brown", lwd = 2)

#For the squares, the order is not important instead of for blue and red: the red square tops the blue one (so the blue one should be called upon first).
points(x=germfree$axis1[20], y=germfree$axis2[20], pch = 15, cex = 1.5)
points(x=germfree$axis1[41], y=germfree$axis2[41], pch = 15, cex = 1.5 ,col = "blue")
points(x=germfree$axis1[61], y=germfree$axis2[61], pch = 15, cex = 1.5,col = "red")
points(x=germfree$axis1[82], y=germfree$axis2[82], pch = 15, cex = 1.5,col = "green")
points(x=germfree$axis1[103], y=germfree$axis2[103], pch = 15, cex = 1.5,col = "brown")

#For the circles, the order is not important instead of for blue and red: the red square tops the blue one (so the blue one should be called upon first).
points(x=germfree$axis1[1], y=germfree$axis2[1], pch = 19, cex = 1.5)
points(x=germfree$axis1[21], y=germfree$axis2[21], pch = 19, cex = 1.5,  col = "blue")
points(x=germfree$axis1[42], y=germfree$axis2[42], pch = 19, cex = 1.5,col = "red")
points(x=germfree$axis1[62], y=germfree$axis2[62], pch = 19, cex = 1.5,col = "green")
points(x=germfree$axis1[83], y=germfree$axis2[83], pch = 19, cex = 1.5,col = "brown")

#Inserting a legend
legend(x = 0.0, y = -0.2, legend = c("Mouse 337", "Mouse 343", "Mouse 361", "Mouse 387", "Mouse 389"), col = c("black","blue", "red", "green", "brown"), lwd = 3.5, cex = 0.85)
```

![plot of chunk unnamed-chunk-2](./README_files/figure-html/unnamed-chunk-2.png) 
  
The final result can also be seen in an attached .pdf file, named *rplot2.pdf*.  

3.  On pg. 57 there is a formula for the probability of making x observations after n trials when there is a probability p of the observation.  For this exercise, assume x=2, n=10, and p=0.5.  Using R, calculate the probability of x using this formula and the appropriate built in function. Compare it to the results we obtained in class when discussing the sex ratios of mice.


```r
prob <- dbinom(x=2, size=10, p=0.5)
```
The probability of making x observations is equal to 0.0439. This value is exactly equal to the probability calculated in class, when we wanted to see if it was strange that one mice gave birth to 2 males and 8 females in one litter. 

4.  On pg. 59 there is a formula for the probability of observing a value, x, when there is a mean, mu, and standard deviation, sigma.  For this exercise, assume x=10.3, mu=5, and sigma=3.  Using R, calculate the probability of x using this formula and the appropriate built in function


```r
rm(prob)
prob <- dnorm(x=10.3, mean=5, sd=3)
```
The probability of observing the valule x is equal to 0.0279.

5.  One of my previous students, Joe Zackular, obtained stool samples from 89 people that underwent colonoscopies.  30 of these individuals had no signs of disease, 30 had non-cancerous ademonas, and 29 had cancer.  It was previously suggested that the bacterium *Fusobacterium nucleatum* was associated with cancer.  In these three pools of subjects, Joe determined that 4, 1, and 14 individuals harbored *F. nucleatum*, respectively. Create a matrix table to represent the number of individuals with and without _F. nucleatum_ as a function of disease state.  Then do the following:


```r
nobact <-c(26, 29, 15)
bact <- c(4, 1, 14)
table <- cbind(nobact, bact)
rownames(table) <- c("nodisease", "noncancerous", "cancer")
```

    * Run the three tests of proportions you learned about in class using built in R  functions to the 2x2 study design where normals and adenomas are pooled and compared to carcinomas.

```r
poolednobact <-c(55,15)
pooledbact <- c(5, 14)
pooledtable <- cbind(poolednobact, pooledbact)
rownames(pooledtable) <- c("nocancer", "cancer")
colnames(pooledtable) <- c("nobact", "bact")

#Test of proportion: Chi squared test. What is the difference between what we expected and what we observed?
chisq.test(pooledtable)

#Test of proportion: Fisher exact test. What is the difference between what we expected and what we observed?
fisher.test(pooledtable)

#Test of proportion. Null: the fraction of bacteria is greater in cancerous individuals.
cancer.sums <- margin.table(pooledtable, 1)
bact.sums <- margin.table(pooledtable, 2)
bact <- pooledtable[,2]
prop.test(bact, cancer.sums)
```
    * Without using the built in chi-squared test function, replicate the 2x2 study design in the last problem for the Chi-Squared Test...

      * Calculate the expected count matrix and calculate the Chi-Squared test statistics. Figure out how to get your test statistic to match Rs default statistic.

```r
frac.canc <- cancer.sums[[2]]/sum(cancer.sums)
frac.nocanc <- 1 - frac.canc
frac.health <- c(nocanc = frac.nocanc, canc = frac.canc)

frac.nobact <- bact.sums[[1]]/sum(bact.sums)
frac.bact <- 1 - frac.nobact
frac.infected <- c(nobact = frac.nobact, bact = frac.bact)

expected <- frac.health %*% t(frac.infected)
expected <- expected * sum(pooledtable)

# My test statistics for Chi-Squared
chi.sq <- sum((expected - pooledtable)^2/expected)

# Rs default statistic for Chi-Squared
chi.built.in.R <- chisq.test(pooledtable)
```
The expected count matrix is equal to 47.191, 22.809, 12.809, 6.191 (the first value shown is the seat on the first row, first column; second value = first column, second row; third value = second column, first row; fourth value = second column, second row). My Chi-sqared test statistic is equal to 18.5763.  

      *	Generate a Chi-Squared distributions with approporiate degrees of freedom by the method that was discussed in class

```r
df <- (nrow(pooledtable) - 1) * (ncol(pooledtable) - 1)
plot(seq(0, 20, 0.05), dchisq(seq(0, 20, 0.05), df = df), type = "l", xlab = "ChiSquared Statistic", ylab = "Probability with 1 degree of freedom")
```

![plot of chunk unnamed-chunk-8](./README_files/figure-html/unnamed-chunk-8.png) 
        
      * Compare your Chi-Squared distributions to what you might get from the appropriate built in R functions

```r
#My Chi-Squared value is shown on the graph
plot(seq(0, 20, 0.05), dchisq(seq(0, 20, 0.05), df = df), type = "l", xlab = "ChiSquared Statistic", ylab = "Probability with 1 degree of freedom")
arrows(x0 = chi.sq, x1 = chi.sq, y0 = 0.5, y1 = 0.1, lwd = 2, col = "red")
```

![plot of chunk unnamed-chunk-9](./README_files/figure-html/unnamed-chunk-9.png) 
  
My Chi-squared value is shown on the graph, and more precisely it  is equal to 18.5763. The value is slightly higher than what the built in R function gives (16.2736), but this also happens for the example given in class.

      * Based on your distribution calculate p-values

```r
chi.sq.distribution <- dchisq(seq(0, 20, 0.05), df = df)
#The distribution jumps with 0.05, and we have 20 such jumps for 'one unit' on the x-axis. 
p.value <- chi.sq.distribution[chi.sq*20]
```
My calculated p-value is equal to 8.9146 &times; 10<sup>-6</sup>.    

      * How does your p-value compare to what you saw using the built in functions? Explain your observations.
My p.value is *lower* than the one calculated by the built in function. This is logical since my chi-squared value is *higher* than the one of the built in function. 

6\.  Get a bag of Skittles or M&Ms.  Are the candies evenly distributed amongst the different colors?  Justify your conclusion.

```r
amount.blue <- 11
amount.yellow <- 22
amount.orange <- 15
amount.red <- 10
amount.green <- 10
amount.brown <- 24

groups <- c(rep("blue", length(amount.blue)), rep("yellow", length(amount.yellow)), rep("orange", length(amount.orange)), rep("red", length(amount.red)), rep("green", length(amount.green)), rep("brown", length(amount.brown)))
data <- c(amount.blue, amount.yellow, amount.orange, amount.red, amount.green, amount.brown)

#I now have multiple groups of a color and I want to know whether one of them is different =>  I perform a one-way ANOVA test.
anova(lm(data~groups))
```

```
## Warning: ANOVA F-tests on an essentially perfect fit are unreliable
```

```
## Analysis of Variance Table
## 
## Response: data
##           Df Sum Sq Mean Sq F value Pr(>F)
## groups     5    195    39.1               
## Residuals  0      0
```
R tells me that the MnM's are evenly distributed, because an error message is generated saying *ANOVA F-tests on an essentially perfect fit are unreliable* (which implies that my fit is perfect).
