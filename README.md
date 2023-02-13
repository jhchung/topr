
# *topr*: an R package for viewing and annotating genetic association results

<img src="man/figures/manhattan_wide_1080_high.gif" alt="topr GIF" width="100%">


## Installation
<hr>

Install from CRAN:

``` r
install.packages("topr")
```

Or from github:

``` r
devtools::install_github("totajuliusd/topr")
```

And then load the package:

``` r
library(topr)
```


## Main features and functionality
<hr>

### Example input datasets 

*See the <a href="https://totajuliusd.github.io/topr/articles/input_datasets.html">Input datasets vignette</a> for more detailed information.*

Input datasets must include least three columns (<code>CHROM,
POS</code> and <code>P</code>), where naming of the columns is flexible
(i.e the chr label can be either chr or chrom and is case insensitive).

*topr* has 3 inbuilt GWAS results (<code>CD_UKBB, CD_FINNGEN</code> and <code>UC_UKBB</code>). To get information on them, do:

``` r
?CD_UKBB
?CD_FINNGEN
?UC_UKBB
```

The chromosome in the <code>CHROM</code> column can be represented with
our without the <i>chr</i> suffix, e.g (chr1 or 1)



### Basic usage 
<hr>

*topr's* two main plotting functions are <code>manhattan()</code> and <code>regionplot()</code>



#### Manhattan
<hr>

*See the <a href="https:///totajuliusd.github.io/topr/articles/manhattan.html">Manhattan vignette</a> for more detailed examples of how to use the manhattan plot function.*

View the whole genome association results on a Manhattan plot:

``` r
manhattan(CD_UKBB)
```

Annotate the lead/index variants (with p-values below 5e-9) with their nearest gene:

``` r
manhattan(CD_UKBB, annotate=5e-9)
```

View multiple GWAS results on the same plot

``` r
manhattan(list(CD_UKBB, CD_FINNGEN), legend_labels = c("UKBB", FinnGen"))
```


#### Regionplot
<hr>
*See the <a href="https:///totajuliusd.github.io/topr/articles/regionplot.html">Regionplot vignette</a> for more detailed examples of how to use the regionplot function.*

Further zoom-in on a genetic region by gene name (*IL23R*):

``` r
regionplot(CD_UKBB, gene="IL23R")
```

View the correlation pattern between the variants within the region in a locuszoom like plot.
Note that the variant correlation (<code>R2</code>) has to be pre-calculated and included in the input dataframe.

``` r
locuszoom(R2_CD_UKBB)
```

Display multiple GWAS results zoomed in on the *IL23R* gene

``` r
regionplot(list(UC_UKBB, CD_UKBB), gene="IL23R")
```

<br>

#### Useful functions
<hr>

Extract lead/index variants from the GWAS dataset (<code>CD_UKBB</code>):

```{r}
get_lead_snps(CD_UKBB)
```

Annotate the lead/index variants with their nearest gene:

```{r}
get_lead_snps(CD_UKBB) %>% annotate_with_nearest_gene()
```

Get genomic coordinates for a gene (*topr* uses genome build GRCh38.p13 by default):

```{r}
get_gene_coords("IL23R")
```
Get genomic coordinates for a gene using genome build GRCh37 instead.

```{r}
get_gene_coords("IL23R", build="37")
```

Get snps within a region:

```{r}
get_snps_within_region(CD_UKBB, region = "chr1:67138906-67259979")
```

Get the top variant on a chromosome:
```{r}
get_top_snp(CD_UKBB, chr="chr1")

```

<br>

#### Get help:

``` r
?manhattan()
?regionplot()
?locuszoom()
```
