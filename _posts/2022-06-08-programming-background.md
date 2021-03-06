Programming Background
================
Mark Gordon
2022-06-08

## R as a programming language

R and SAS are both great statistical tools and they both have their
pluses and minuses. SAS I’ve found tends to have a lot better default
tools for the statistics themselves. However, R is much easier to
customize the output for things like plots. One of my previous
professors said he’ll often do the statistical calculations using SAS
but generate plots in R. This feels like something I might do myself as
SAS plots are customizable, but less intuitively so.

The parts I missed about SAS were things like the ease of doing an
iterative finding of which variables to use. While there is a package
for this in R, it didn’t really do it in the same way and didn’t follow
the rules of analysis (such as requiring the linear term for quadratic
or interaction terms). I didn’t find R particularly difficult to learn.
At least, not base R. Some of the packages such as ggplot2 have a good
bit of a learning curve, at least when I tried to teach it to myself
during ST503.

## R Markdown output

``` r
plot(iris)
```

![](../images/unnamed-chunk-1-1.png)<!-- -->

<!-- render("_Rmd/2022-06-08-programming-background.Rmd", output_format = "github_document", output_dir = "_posts", output_options = list(html_preview = "false")) -->
