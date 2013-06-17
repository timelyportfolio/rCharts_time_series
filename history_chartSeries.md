---
title: R Charting of Time Series
subtitle: History from plot.default to rCharts
author: Timely Portfolio
github: {user: ramnathv, repo: rCharts, branch: "gh-pages"}
framework: minimal
mode: selfcontained
ext_widgets: {rCharts: ["libraries/morris","libraries/nvd3", "libraries/polycharts", "libraries/highcharts","libraries/xcharts", "libraries/rickshaw"]}
hitheme: solarized_light
logo: libraries/frameworks/minimal/images/rCharts.png
---

<style>
.rChart {
  height: 400px
}
</style>





```r
require(latticeExtra)
require(ggplot2)
require(reshape2)
require(quantmod)
require(PerformanceAnalytics)
require(xtsExtra)
require(rCharts)


# get S&P 500 data from FRED (St. Louis Fed)
sp500 <- na.omit( 
  getSymbols(
    "SP500",
    src = "FRED",
    from = "1949-12-31",
    auto.assign = FALSE
  )
)

# use monthly data
sp500.monthly <- sp500[endpoints(sp500, on ="months")]
```



- - -

---
### [quantmod/TTR chartSeries](https://r-forge.r-project.org/scm/viewvc.php/pkg/R/chartSeries.R?root=quantmod&view=log) 2007-10-07


```r
# 2007-10-17 then quantmod/TTR built on zoo
# to offer much better handling of financial time series
# notice the ease of adding pertinent financial information
chartSeries(
  sp500.monthly,
#  log = TRUE,
  theme = chartTheme("white"),
  TA = c(addBBands(),addTA(RSI(sp500.monthly)))
)
```

![plot of chunk unnamed-chunk-3](assets/fig/unnamed-chunk-31.png) ![plot of chunk unnamed-chunk-3](assets/fig/unnamed-chunk-32.png) 


Just look how easy it is to zoom.


```r
# also easy zooming
zoomChart("1990::")
```

![plot of chunk unnamed-chunk-4](assets/fig/unnamed-chunk-41.png) ![plot of chunk unnamed-chunk-4](assets/fig/unnamed-chunk-42.png) 

