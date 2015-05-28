---
layout: post
tagline: ""
tags : [tutorial, statistics]
---
{% include JB/setup %}

### Measuring and Describing Relationships
* A correlation is a statistical method used to measure and describe the relationship between two variables.
* A relationship exists when changes in one variable tend to be accompanied by consistent and predictable changes in the other variable.
* There is no assumption of causality

### Graphical Method

#### Positive Correlation
X increases with Y

![Positive Correlation]({{ site.url }}/assets/img/positive-cor.png  "Positive Correlation")

#### Negative Correlation
X decreases with Y

![Negative Correlation]({{ site.url }}/assets/img/negative-cor.png  "Negative Correlation")

#### Zero Correlation
No relationship between X & Y

![Zero Correlation]({{ site.url }}/assets/img/zero-cor.png  "Zero Correlation")

#### Exponential Relationship

![Exponential Relationship]({{ site.url }}/assets/img/exp-cor.png  "Exponential Relationship")


### Measuring Correlation

* Pearson's Coefficient of Correlation
* Spearman's Rank Correlation

#### Pearson's Coefficient Of Correlation
* Represented by \` r \`.
* Measures the strength and the direction of linear relationship between two variables.
* The direction of the relationship is measured by the sign of the correlation (`+` or `-`).
    + A positive correlation means that the two variables tend to change in the same direction; as one increases, the other also tends to increase.
    + A negative correlation means that the two variables tend to change in opposite directions; as one increases, the other tends to decrease.
* Assumes both variables to be normally distributed.
* Its value vary between (`-1` to `1`)
    + `-1` indicates perfect negative relationship,
    + `+1` indicates perfect positive relationship,
    + `0` implies no relationship in data.
* It is not a measure of causality.

##### __Measuring Correlation__

~~~ R
  > x <- rnorm(20, mean=300, sd=5)
  > y <- rnorm(20, mean=12, sd=4)
  > plot(x, y,
      main="Imperfect linear relationship between x & y",
      sub="Correlation between -1 to 0",
      xlab="Price(in Thousands)", ylab="Km/L")
  > abline(lm(y ~ x))
  > cor(x, y, method="pearson")
  [1] -0.06129544
  >
~~~

![Pearson]({{ site.url }}/assets/img/pearson-cor.png  "pearson")

\` r = (n sum xy - sum x sum y) / ( sqrt(n sum x^2 - (sum x)^2) sqrt(n sum y^2 - (sum y)^2))\`

##### __Example__

* Relationship between age of a car and the distance it covers before stopping.

  Car | Age (in Months) | Distance covered during 40 km/h to 0 (in Meters)
  ----|:-----------:|:------------------------:
   A  |  9          |  28.4
   B  | 15          |  29.3
   C  | 24          |  37.6
   D  | 30          |  36.2
   E  | 38          |  36.5
   F  | 46          |  35.3
   G  | 53          |  36.2
   H  | 60          |  44.1
   I  | 64          |  44.8
   J  | 66          |  47.2
  {:.table-bordered}

* Calculating pearson's correlation coefficient

  | | \` X \` | \` Y \` | \` X^2 \` | \` Y^2 \` | \` XY \`
  |-|---:|-------:|------:|---------:|---------:|---------:
  | | 9  |  28.4  |   81  |  805.56  |  255.6
  | |15  |  29.3  |  225  |  858.49  |  439.5
  | |24  |  37.6  |  576  | 1413.76  |  902.4
  | |30  |  36.2  |  900  | 1310.44  |  1086.0
  | |38  |  36.5  | 1444  | 1332.25  |  1387.0
  | |46  |  35.3  | 2116  | 1246.05  |  1623.8
  | |53  |  36.2  | 2809  | 1310.44  |  1918.6
  | |60  |  44.1  | 3600  | 1944.81  |  2646.0
  | |64  |  44.8  | 4096  | 2007.04  |  2867.2
  | |66  |  47.2  | 4356  | 2227.84  |  3115.2
  | \` sum \` |405 | 375.6 | 20203 | 14457.72 | 16241.3
  {:.table-bordered}

* Plugging the values into the forumla

\` r = (10 * 16241.3 - 405 * 375.6) / ( sqrt(10 * 20203 - (405)^2) sqrt(10 * 14457.72 - (375.6)^2) ) \`

\` r = .89 \`

* Plot of the data

~~~R
  > x <- c(9,15,24,30,38,46,53,60,64,66)
  > y <- c(28.4,29.3,37.6,36.2,36.5,35.3,36.2,44.1,44.8,47.2)
  > plot(x,y)
  > abline(lm(y ~ x))
  > cor(x, y, method="pearson")
  [1] 0.8923964
~~~

![Pearson Example]({{ site.url }}/assets/img/pearson-example-1.png  "pearson-example-1")

#### The Spearman's Rank Correlation
* Represented by \` rho \`.
* Measures the strength and the direction of monotonic relationship between two variables.
* Unlike Pearson's coefficient both variables don't have to be normally distributed.
* Its value vary between (`-1` to `1`).
    - `-1` indicates perfect negative relationship
    - `+1` indicates perfect positive relationship
    - `0` implies no relationship in data.
* It is not a measure of causality.
* It is generally used to measure the rank relationship, not the actual relationship. e.g percent measures actual marks while percentile measures rank.
* It can't be used if the ranks are tied.

##### __Monotonic Relationship__
A monotonic relationship is a relationship that does one of the following:
  1. as the value of one variable increases, so does the value of the other variable
  2. as the value of one variable increases, the other variable value decreases

~~~~R
> x <- 1:10
> f <- function(x) x^3
> y <- f(x)
> par(mfrow=c(1,2))
> plot(x, y, type="o", ylab="y=x^3")
> grid()
> f <- function(x) 1/x
> y <- f(x)
> plot(x, y, type="o", ylab="y=1/x")
> grid()
~~~~

![Monotonic Relationship]({{ site.url }}/assets/img/monotonic-rel.png  "monotonic-rel")

~~~~R
> x <- 0:10
> y <- (x-6)^2 + 5
> plot(x, (x-6)^2 + 5, type="o")
> grid()
~~~~

![Non-Monotonic Relationship]({{ site.url }}/assets/img/non-monotonic-rel.png  "non-monotonic-rel")

##### Testing whether `X` and `Y` follow Normal Distribution
  1. Draw a histogram of `X` values, i.e. x values on X-axis and frequency on Y-axis. Connect the middle points of the bars with a smooth curve
  2. Draw Mean of `X` on the same plot.
  3. `X` is normal if the the curve is symmetrical around mean and has a bell shaped curved
  4. Repeat steps 1 to 3 for `Y` values

> Important - Pearson's correlation coefficient can be used if and only if both `X` and `Y` follow normal distribution.

* __Example 1__

  + A study was conducted on 303 people to find a relationship between rest blood pressure and cholesterol level.
    Can we calculate Pearson's coefficient of correlation between the two?

      Rest BP  |   Frequency
      --------:|-----------:
      91-100   |      2
      101-110  |     18
      111-120  |     40
      121-130  |     75
      131-140  |     70
      141-150  |     46
      151-160  |     26
      161-170  |     13
      171-180  |      8
      181-190  |      3
      191-200  |      1
      201-210  |      1
      =========|===========
      {:.table-bordered}

      
      Cholesterol Level| Frequency
      ----------:|----------:
      126-150    |      5
      151-175    |     11
      176-200    |     34
      201-225    |     58
      225-250    |     68
      251-275    |     52
      276-300    |     31
      301-325    |     27
      326-350    |      9
      351-375    |      3
      376-400    |      1
      401-425    |      3
      426-450    |      0
      451-475    |      0
      476-500    |      0
      501-525    |      0
      526-550    |      0
      551-575    |      1
      ===========|==========
      {:.table-bordered}

    ![Rest BP]({{ site.url }}/assets/img/restbp-norm.png  "restbp-norm")
    ![Cholesterol Level]({{ site.url }}/assets/img/cholesterollevel-norm.png  "cholesterollevel-norm")

    In this example we can see both `X` and `Y` follow normal distribution, therefore Pearson's correlation coefficient can be calculated.

* __Example 2__

  + A study was conducted on 99,000 facebook users to find a relationship between friend count and time on facebook(tenure).
    Can we calculate Pearson's coefficient of correlation between the two?

   ![Friends Count Frequency Curve]({{ site.url }}/assets/img/facebook-friendscount-freq.png  "facebook-friendscount-freq")
   ![Time On Facebook Frequency Curve]({{ site.url }}/assets/img/facebook-time-freq.png  "facebook-time-freq")

   We can see neither "Friends Count" nor "Time on Facebook" follow a normal distribution therefore
   we can't calculate Pearson's Coefficient of Correlation for the given data.

##### The Spearman Correlation

* Scores of students in English and Maths in GMAT

~~~~
  English 56  75  45  71  62  64  58  80  76  61
  Maths   66  70  40  60  65  56  59  77  67  63
~~~~

* Calculating Spearman's rank correlation coefficient

  1. Calculate ranks of \` x \` and \` y \`, \` d \` and \` d^2 \`

  \` X  \` | \` Y\` | \` rank(x) \` | \` rank(y) \` | \` d = rank(x) - rank(y) \` | \` d^2 \`
  -:|--:|:--------:|:-------:|:--------:|--------:
  56  | 66  | 9 | 4 | 5 | 25
  75  | 70  | 3 | 2 | 1 | 1
  45  | 40  | 10  | 10  | 0 | 0
  71  | 60  | 4 | 7 | -3  | 9
  62  | 65  | 6 | 5 | 1 | 1
  64  | 56  | 5 | 9 | -4  | 16
  58  | 59  | 8 | 8 | 0 | 0
  80  | 77  | 1 | 1 | 0 | 0
  76  | 67  | 2 | 3 | -1  | 1
  61  | 63  | 7 | 6 | 1 | 1
  {:.table-bordered}

  \` sum d^2 = 54 \`

* Spearman's Rank Correlation formula

  \` rho = 1 - ( (6 xx d^2) / (n xx (n^2 -1)) ) \`

  \` rho = 1 - ( (6 xx 54) / (10 xx (10^2 -1)) ) = 1 - (324/990) = 0.67 \`

### Rank correlation for tied Ranks

        EMP                  1  2    3   4   5   6   7   8   9  10
        Height (in inches)  62  68  66  70  74  61  70  70  65  64
        Weight (in kgs)     55  62  66  68  80  57  67  75  64  63

  1. write down the ranks of Height and Weight in usual manner. You can assign ranks 2,3, & 4 to 70 in any order.

Height| Weight| rank(\` x \`)| rank(\` y \`)
------|-------|-----------------
62    | 55    |  9     |  10
68    | 62    |  5     |   8
66    | 66    |  6     |   5
**70**   | 68    |  2     |   3     # tie
77    | 80    |  1     |   1
61    | 57    | 10     |   9
**70**   | 67    |  3     |   4     # tie
**70**   | 75    |  4     |   2     # tie
65    | 64    |  7     |   6
64    | 63    |  8     |   7
{:.table-bordered}

  2. take mean of ranks of `70`. e.g. in our example the mean would be \` (2+3+4)/3 = 3 \`. we are dividing by `3` because `70` happens to be three times.

Height| Weight| rank(\` x \`)| rank(\` y \`)
------|------|-------------|-----
62    | 55   |  9    |  10
68    | 62   |  5    |   8
66    | 66   |  6    |   5
70    | 68   | **3** |   3     # tie
77    | 80   |  1    |   1
61    | 57   | 10    |   9
70    | 67   | **3** |   4     # tie
70    | 75   | **3** |   2     # tie
65    | 64   |  7    |   6
64    | 63   |  8    |   7
{:.table-bordered}

Rank Correlation formula for Tied Ranks

\` rho = (n sum x_r y_r - sum x_r y_r) / ( sqrt(n sum x_r^2 - (sum x_r)^2) sqrt(n sum y_r^2 - (sum y_r)^2) ) \`

\` rho = (10 ** 376 - 55 ** 55) / (sqrt(10 ** 383 - 55^2) sqrt(10 ** 385 - 55^2)) = 0.90 \`

> Note - \` x_r \` and \` y_r \` are the ranks of \` X \` and \` Y \`

### Comparison of correlation coefficients

Pearson | Spearman| Rank For Tied Ranks 
----|----|----|----
1. Variables \` (x, y) \` have to be normally distributed | Variables \` (x, y) \` don't have to be normally distributed | Variables \` (x, y) \` don't have to be normally distributed
2. Linear relationship between variables \` (x, y) \` | Monotonic relationship between variables \` (x, y) \` | Monotonic relationship between variables \` (x, y) \`
3. Measures relationship between actual values | Measures relationship between Ranks | Measures relationship between Ranks
4. | Cant be used if ranks are tied. | Is used when ranks are tied.
{:.table}