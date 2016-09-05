---
title: 'Peer Graded Assignment: Course Project 1'
author: "Tomasz"
date: "August 31, 2016"
output: html_document
---



### **Loading and preprocessing the data**

<div class="chunk" id="loadtab"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">acttab</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">read.csv</span><span class="hl std">(</span><span class="hl kwc">file</span> <span class="hl std">=</span> <span class="hl str">&quot;activity.csv&quot;</span><span class="hl std">)</span>
    <span class="hl std">acttab</span><span class="hl opt">$</span><span class="hl std">date</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">as.Date</span><span class="hl std">(acttab</span><span class="hl opt">$</span><span class="hl std">date)</span>
    <span class="hl std">acthead</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">head</span><span class="hl std">(acttab)</span>
</pre></div>
</div></div>

First 5 rows look like this:

<div class="chunk" id="unnamed-chunk-1"><div class="rcode"><div class="output"><pre class="knitr r">##   steps       date interval
## 1    NA 2012-10-01        0
## 2    NA 2012-10-01        5
## 3    NA 2012-10-01       10
## 4    NA 2012-10-01       15
## 5    NA 2012-10-01       20
## 6    NA 2012-10-01       25
</pre></div>
</div></div>

### **What is mean total number of steps taken per day?**

1. Calculate the total number of steps taken per day

<div class="chunk" id="actcalculation1"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">actcalc</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">aggregate</span><span class="hl std">(acttab</span><span class="hl opt">$</span><span class="hl std">steps,</span> <span class="hl kwc">by</span> <span class="hl std">=</span> <span class="hl kwd">list</span><span class="hl std">(acttab</span><span class="hl opt">$</span><span class="hl std">date),</span> <span class="hl kwc">FUN</span> <span class="hl std">= mean)</span>
    <span class="hl std">actcalc</span><span class="hl opt">$</span><span class="hl std">median</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">aggregate</span><span class="hl std">(acttab</span><span class="hl opt">$</span><span class="hl std">steps,</span> <span class="hl kwc">by</span> <span class="hl std">=</span> <span class="hl kwd">list</span><span class="hl std">(acttab</span><span class="hl opt">$</span><span class="hl std">date),</span> <span class="hl kwc">FUN</span> <span class="hl std">= median)[,</span><span class="hl num">2</span><span class="hl std">]</span>
    <span class="hl kwd">names</span><span class="hl std">(actcalc)</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">c</span><span class="hl std">(</span><span class="hl str">&quot;date&quot;</span><span class="hl std">,</span> <span class="hl str">&quot;stepavg&quot;</span><span class="hl std">,</span> <span class="hl str">&quot;stepmedian&quot;</span><span class="hl std">)</span>
</pre></div>
</div></div>

2. If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day

<div class="chunk" id="actcalculation2"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">acttab.clean</span> <span class="hl kwb">&lt;-</span> <span class="hl std">acttab[</span><span class="hl opt">!</span><span class="hl kwd">is.na</span><span class="hl std">(acttab</span><span class="hl opt">$</span><span class="hl std">steps),]</span>
    <span class="hl std">tmp</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">aggregate</span><span class="hl std">( steps</span> <span class="hl opt">~</span> <span class="hl std">date, acttab.clean, sum )</span>
    <span class="hl kwd">hist</span><span class="hl std">(tmp</span><span class="hl opt">$</span><span class="hl std">steps,</span> <span class="hl kwc">main</span> <span class="hl std">=</span> <span class="hl str">&quot;Steps taken each day&quot;</span><span class="hl std">,</span> <span class="hl kwc">xlab</span> <span class="hl std">=</span> <span class="hl str">&quot;Steps / Day&quot;</span><span class="hl std">,</span> <span class="hl kwc">col</span><span class="hl std">=</span> <span class="hl num">3</span> <span class="hl std">)</span>
</pre></div>
<div class="rimage default"><img src="figure/actcalculation2-1.png" title="plot of chunk actcalculation2" alt="plot of chunk actcalculation2" class="plot" /></div>
</div></div>

3. Calculate and report the mean and median of the total number of steps taken per day

<div class="chunk" id="actcalculation3"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl kwd">names</span><span class="hl std">(actcalc)</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">c</span><span class="hl std">(</span><span class="hl str">&quot;date&quot;</span><span class="hl std">,</span> <span class="hl str">&quot;stepsmean&quot;</span><span class="hl std">,</span> <span class="hl str">&quot;stepsmedian&quot;</span><span class="hl std">)</span>
    <span class="hl kwd">head</span><span class="hl std">(actcalc)</span>
</pre></div>
<div class="output"><pre class="knitr r">##         date stepsmean stepsmedian
## 1 2012-10-01        NA          NA
## 2 2012-10-02   0.43750           0
## 3 2012-10-03  39.41667           0
## 4 2012-10-04  42.06944           0
## 5 2012-10-05  46.15972           0
## 6 2012-10-06  53.54167           0
</pre></div>
</div></div>

### **What is the average daily activity pattern?**

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


<div class="chunk" id="plot.int.steps"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">acttab.1</span> <span class="hl kwb">&lt;-</span> <span class="hl std">acttab[</span><span class="hl opt">!</span><span class="hl kwd">is.na</span><span class="hl std">(acttab</span><span class="hl opt">$</span><span class="hl std">steps),]</span> <span class="hl com">#remove all NA's</span>
    <span class="hl std">actavg</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">aggregate</span><span class="hl std">(acttab.1,</span> <span class="hl kwc">by</span> <span class="hl std">=</span> <span class="hl kwd">list</span><span class="hl std">(acttab.1</span><span class="hl opt">$</span><span class="hl std">interval),</span> <span class="hl kwc">FUN</span> <span class="hl std">= mean)</span>
    <span class="hl kwd">plot</span><span class="hl std">(actavg</span><span class="hl opt">$</span><span class="hl std">interval, actavg</span><span class="hl opt">$</span><span class="hl std">steps,</span> <span class="hl kwc">type</span> <span class="hl std">=</span> <span class="hl str">&quot;l&quot;</span><span class="hl std">,</span> <span class="hl kwc">xlab</span> <span class="hl std">=</span> <span class="hl str">&quot;Time (interval)&quot;</span><span class="hl std">,</span> <span class="hl kwc">ylab</span> <span class="hl std">=</span> <span class="hl str">&quot;Steps (average)&quot;</span><span class="hl std">,</span> <span class="hl kwc">main</span> <span class="hl std">=</span> <span class="hl str">&quot;Steps in time&quot;</span><span class="hl std">,</span> <span class="hl kwc">col</span> <span class="hl std">=</span> <span class="hl num">3</span><span class="hl std">)</span>
</pre></div>
<div class="rimage default"><img src="figure/plot.int.steps-1.png" title="plot of chunk plot.int.steps" alt="plot of chunk plot.int.steps" class="plot" /></div>
</div></div>

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

<div class="chunk" id="actgraphs"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">maxline</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">which.max</span><span class="hl std">(actavg</span><span class="hl opt">$</span><span class="hl std">steps)</span> <span class="hl com">#find max value</span>
    <span class="hl std">maxvalue</span> <span class="hl kwb">&lt;-</span> <span class="hl std">actavg[maxline,</span> <span class="hl num">2</span><span class="hl std">]</span> <span class="hl com">#show max value</span>
</pre></div>
</div></div>
That would be **<code class="knitr inline">206.1698113</code>** on line **<code class="knitr inline">104</code>**

### **Imputing missing values**

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

<div class="chunk" id="errorrep1"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">totalNAs</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">sum</span><span class="hl std">(</span><span class="hl kwd">colSums</span><span class="hl std">(</span><span class="hl kwd">is.na</span><span class="hl std">(acttab)))</span> <span class="hl com">#count all NA's</span>
</pre></div>
</div></div>

Total number of missing values in the dataset is **<code class="knitr inline">2304</code>**

2. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

Strategy: filling missing values with steps mean for the interval.

<div class="chunk" id="errorrep2"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">tmp</span> <span class="hl kwb">&lt;-</span> <span class="hl std">acttab</span>
    <span class="hl std">tmp[</span><span class="hl kwd">is.na</span><span class="hl std">(tmp</span><span class="hl opt">$</span><span class="hl std">steps),]</span><span class="hl opt">$</span><span class="hl std">steps</span> <span class="hl kwb">&lt;-</span> <span class="hl opt">-</span><span class="hl num">1</span>
    <span class="hl std">tmp</span><span class="hl opt">$</span><span class="hl std">steps2</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">round</span><span class="hl std">(actavg</span><span class="hl opt">$</span><span class="hl std">steps)</span>
    <span class="hl std">tmp</span><span class="hl opt">$</span><span class="hl std">steps</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">as.numeric</span><span class="hl std">(</span> <span class="hl kwd">apply</span><span class="hl std">(tmp,</span> <span class="hl num">1</span><span class="hl std">,</span> <span class="hl kwa">function</span><span class="hl std">(</span><span class="hl kwc">x</span><span class="hl std">)</span> <span class="hl kwd">max</span><span class="hl std">(x[[</span><span class="hl num">1</span><span class="hl std">]],x[[</span><span class="hl num">4</span><span class="hl std">]])))</span>
</pre></div>
</div></div>

3. Create a new dataset that is equal to the original dataset but with the missing data filled in.

<div class="chunk" id="errorrep3"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">acttab.filled</span> <span class="hl kwb">&lt;-</span> <span class="hl std">tmp[,</span> <span class="hl kwd">c</span><span class="hl std">(</span><span class="hl num">1</span><span class="hl opt">:</span><span class="hl num">3</span><span class="hl std">)]</span>
    <span class="hl kwd">head</span><span class="hl std">(acttab.filled,</span> <span class="hl num">10</span><span class="hl std">)</span>
</pre></div>
<div class="output"><pre class="knitr r">##    steps       date interval
## 1      2 2012-10-01        0
## 2      0 2012-10-01        5
## 3      0 2012-10-01       10
## 4      0 2012-10-01       15
## 5      0 2012-10-01       20
## 6      2 2012-10-01       25
## 7      1 2012-10-01       30
## 8      1 2012-10-01       35
## 9      0 2012-10-01       40
## 10     1 2012-10-01       45
</pre></div>
</div></div>
4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

<div class="chunk" id="unnamed-chunk-2"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">daysteps</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">aggregate</span><span class="hl std">(steps</span> <span class="hl opt">~</span> <span class="hl std">date, acttab.filled , sum)</span>
    <span class="hl kwd">hist</span><span class="hl std">(daysteps</span><span class="hl opt">$</span><span class="hl std">steps,</span> <span class="hl kwc">col</span> <span class="hl std">=</span> <span class="hl num">3</span><span class="hl std">,</span> <span class="hl kwc">xlab</span> <span class="hl std">=</span> <span class="hl str">&quot;Steps / Day&quot;</span><span class="hl std">,</span> <span class="hl kwc">main</span> <span class="hl std">=</span> <span class="hl str">&quot;Steps per day (avarage)&quot;</span><span class="hl std">,</span> <span class="hl kwc">breaks</span> <span class="hl std">=</span> <span class="hl num">5</span><span class="hl std">)</span>
</pre></div>
<div class="rimage default"><img src="figure/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" class="plot" /></div>
<div class="source"><pre class="knitr r">    <span class="hl std">smean</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">mean</span><span class="hl std">(daysteps</span><span class="hl opt">$</span><span class="hl std">steps)</span>
    <span class="hl std">smedian</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">median</span><span class="hl std">(daysteps</span><span class="hl opt">$</span><span class="hl std">steps)</span>
</pre></div>
</div></div>

Avarage: **<code class="knitr inline">17050.16</code>**

Median: **<code class="knitr inline">17350.00</code>**

### **Are there differences in activity patterns between weekdays and weekends?**

For this part the weekdays() function may be of some help here. Use the dataset with the filled-in missing values for this part.

1. Create a new factor variable in the dataset with two levels - "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.

<div class="chunk" id="weekact"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl std">acttab.filled</span><span class="hl opt">$</span><span class="hl std">weekday</span> <span class="hl kwb">&lt;-</span> <span class="hl str">&quot;week&quot;</span>
    <span class="hl std">acttab.filled[</span><span class="hl kwd">which</span><span class="hl std">(</span><span class="hl kwd">weekdays</span><span class="hl std">(acttab.filled</span><span class="hl opt">$</span><span class="hl std">date)</span> <span class="hl opt">==</span> <span class="hl str">&quot;Sunday&quot;</span> <span class="hl opt">|</span> <span class="hl kwd">weekdays</span><span class="hl std">(acttab.filled</span><span class="hl opt">$</span><span class="hl std">date)</span> <span class="hl opt">==</span> <span class="hl str">&quot;Saturday&quot;</span><span class="hl std">),]</span><span class="hl opt">$</span><span class="hl std">weekday</span> <span class="hl kwb">&lt;-</span> <span class="hl str">&quot;weekend&quot;</span>
    <span class="hl std">acttab.filled.avg</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">with</span><span class="hl std">( acttab.filled,</span> <span class="hl kwd">aggregate</span><span class="hl std">(steps,</span> <span class="hl kwc">by</span> <span class="hl std">=</span> <span class="hl kwd">list</span><span class="hl std">(interval, weekday),</span> <span class="hl kwc">FUN</span> <span class="hl std">= mean) )</span>
    <span class="hl kwd">names</span><span class="hl std">(acttab.filled.avg)</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">c</span><span class="hl std">(</span><span class="hl str">&quot;interval&quot;</span><span class="hl std">,</span> <span class="hl str">&quot;weekday&quot;</span><span class="hl std">,</span> <span class="hl str">&quot;steps&quot;</span><span class="hl std">)</span>
</pre></div>
</div></div>

2. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data

<div class="chunk" id="weekact2"><div class="rcode"><div class="source"><pre class="knitr r">    <span class="hl kwd">xyplot</span><span class="hl std">(steps</span> <span class="hl opt">~</span> <span class="hl std">interval</span> <span class="hl opt">|</span> <span class="hl std">weekday,</span> <span class="hl kwc">data</span> <span class="hl std">= acttab.filled.avg,</span> <span class="hl kwc">type</span> <span class="hl std">=</span> <span class="hl str">&quot;l&quot;</span><span class="hl std">,</span> <span class="hl kwc">layout</span> <span class="hl std">=</span> <span class="hl kwd">c</span><span class="hl std">(</span><span class="hl num">1</span><span class="hl std">,</span><span class="hl num">2</span><span class="hl std">),</span> <span class="hl kwc">col</span> <span class="hl std">=</span> <span class="hl num">3</span><span class="hl std">)</span>
</pre></div>
<div class="rimage default"><img src="figure/weekact2-1.png" title="plot of chunk weekact2" alt="plot of chunk weekact2" class="plot" /></div>
</div></div>
