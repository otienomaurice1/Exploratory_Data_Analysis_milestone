README
================

> Install the tidyverse library

``` r
if (!require(tidyverse)) install.packages("tidyverse")
```

    ## Loading required package: tidyverse

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.2     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.4     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(tidyverse)
```

> We’ll start our exploration by visualizing the distribution of weights
> (carat) of ~54,000 diamonds from the diamonds dataset. Since carat is
> a numerical variable, we can use a histogram:

<img src="figures/histo1-1.png" style="display: block; margin: auto;" />

> Let’s take a look at the distribution of carat for smaller diamonds.

<img src="figures/histo2-1.png" style="display: block; margin: auto;" />

## \>Unusual Values

> Outliers are observations that are unusual; data points that don’t
> seem to fit the pattern. Sometimes outliers are data entry errors,
> sometimes they are simply values at the extremes that happened to be
> observed in this data collection, and other times they suggest
> important new discoveries. When you have a lot of data, outliers are
> sometimes difficult to see in a histogram. For example, take the
> distribution of the y variable from the diamonds dataset. The only
> evidence of outliers is the unusually wide limits on the x-axis.

<img src="figures/histo3-1.png" style="display: block; margin: auto;" />

> There are so many observations in the common bins that the rare bins
> are very short, making it very difficult to see them (although maybe
> if you stare intently at 0 you’ll spot something). To make it easy to
> see the unusual values, we need to zoom to small values of the y-axis
> with coord_cartesian():

<img src="figures/histo4-1.png" style="display: block; margin: auto;" />

> This allows us to see that there are three unusual values: 0, ~30, and
> ~60. We pluck them out with dplyr:

    ## # A tibble: 9 × 4
    ##   price     x     y     z
    ##   <int> <dbl> <dbl> <dbl>
    ## 1  5139  0      0    0   
    ## 2  6381  0      0    0   
    ## 3 12800  0      0    0   
    ## 4 15686  0      0    0   
    ## 5 18034  0      0    0   
    ## 6  2130  0      0    0   
    ## 7  2130  0      0    0   
    ## 8  2075  5.15  31.8  5.12
    ## 9 12210  8.09  58.9  8.06

## \>EXCERCISES

> Exercise 10.3.3

> 1.Explore the distribution of each of the x, y, and z variables in
> diamonds. What do you learn? Think about a diamond and how you might
> decide which dimension is the length, width, and depth.

`To explore distributions between x,y and z , we are going to plot histograms for each of the variables`
<img src="figures/histo6-1.png" style="display: block; margin: auto;" />
\>Most values for x and y fall between 3 mm and 10 mm, suggesting they
represent the length and width. The z values are generally smaller,
typically between 2 mm and 6 mm, which aligns with the depth of a
diamond (top to bottom). \>Also notice that there are outliers in the
data set with some diamonds having dimensions of 0 which is impractical
—

<img src="figures/box-plots-1.png" style="display: block; margin: auto;" />

> 2.  Explore the distribution of price. Do you discover anything
>     unusual or surprising? (Hint: Carefully think about the binwidth
>     and make sure you try a wide range of values.)

------------------------------------------------------------------------

> Again we draw a histogram to visualize the distribution

<img src="figures/histo7 -1.png" style="display: block; margin: auto;" />

> The plot is highly right-skewed distribution. We can see that Most
> diamonds are priced under \$5,000. A long tail extends toward
> high-priced diamonds, with some over \$15,000.

> Lets increase binwidth and see

<img src="figures/histo8-1.png" style="display: block; margin: auto;" />

> 3.How many diamonds are 0.99 carat? How many are 1 carat? What do you
> think is the cause of the difference?

    ## # A tibble: 2 × 2
    ##   carat     n
    ##   <dbl> <int>
    ## 1  0.99    23
    ## 2  1     1558

> There are far fewer diamonds listed as 0.99 carat than 1.00 carat.
> This sharp drop suggests market behavior.Jewelers and cutters might
> cut slightly heavier stones down to exactly 1.00 carat to fetch higher
> prices.As a result, diamonds just under 1 carat (like 0.99) are
> undervalued and therefore less common in inventories.

> 4.  Compare and contrast coord_cartesian() vs. xlim() or ylim() when
>     zooming in on a histogram. What happens if you leave binwidth
>     unset? What happens if you try and zoom so only half a bar shows?

    ## Warning: Removed 14714 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

    ## Warning: Removed 2 rows containing missing values or values outside the scale range
    ## (`geom_bar()`).

<img src="figures/histo9 -1.png" style="display: block; margin: auto;" />

> xlim()/ylim() filters data before plotting .Only the data within the
> limits is used to calculate bins. If only part of a bar shows, the
> entire bar is dropped, because the data outside the limit is excluded
> Binning is re-calculated — no partial bars allowed

<img src="figures/histo10-1.png" style="display: block; margin: auto;" />

> EXCERCISE 10.4.1

> 1.  What happens to missing values in a histogram? What happens to
>     missing values in a bar chart? Why is there a difference in how
>     missing values are handled in histograms and bar charts?

> Missing values are automatically dropped for a histogram.For a bar
> chart, if the factor variable itself has NA, the bar is plotted unless
> you explicitly remove it

> 2.  What does na.rm = TRUE do in mean() and sum()?

> Removes NA values before computing the statistic.

> 3.  Recreate the frequency plot of scheduled_dep_time colored by
>     whether the flight was cancelled or not. Also facet by the
>     cancelled variable. Experiment with different values of the scales
>     variable in the faceting function to mitigate the effect of more
>     non-cancelled flights than cancelled flights.

> Load the dataset

``` r
library(nycflights13)
```

> Now lets plot the frequency plot with scales set to “free”

<img src="figures/histo11-1.png" style="display: block; margin: auto;" />

> Now lets plot the frequency plot with scales set to “free_y”

<img src="figures/histo12 -1.png" style="display: block; margin: auto;" />

> Now lets plot the frequency plot with scales set to “free_x”

<img src="figures/histo13 -1.png" style="display: block; margin: auto;" />
\>Now lets plot the frequency plot with scales set to “fixed”

<img src="figures/histo14 -1.png" style="display: block; margin: auto;" />
