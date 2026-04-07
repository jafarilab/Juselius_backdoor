Readme
================
2026-04-01

# Juselius_backdoor

![](coauthorship_plot.png)

**Juselius_backdoor** is an R pipeline for constructing and analyzing
coauthorship networks of **Sigrid Juselius Foundation** grantees using
**OpenAlex author IDs**. It extracts authors from a text file, resolves
their OpenAlex IDs, retrieves their publications, and builds a weighted
coauthorship network.

------------------------------------------------------------------------

## Features

- Extracts grantee names from text files.  
- Resolves authors to **OpenAlex IDs**.  
- Collects publication data for each author.  
- Builds a weighted coauthorship network.  
- Computes network metrics:
  - Degree (number of collaborators)  
  - Weighted degree  
  - Betweenness (key connectors)  
  - Eigenvector centrality (influence)  
- Detects communities using the **Louvain algorithm**.  
- Generates visualizations:
  - Network graph with community coloring  
  - **Scatter plot of one-time vs. total coauthorship**  
  - Histograms of centrality measures  
- Exports networks for **Gephi** analysis (`.gml` format).

------------------------------------------------------------------------

## Installation

``` r
# Install required packages
install.packages(c(
  "httr", "jsonlite", "dplyr", "igraph", "ggraph", 
  "tidygraph", "ggplot2", "ggrepel", "viridis"
))
```

------------------------------------------------------------------------

## Usage

1.  Place your grantee text file in the project folder (e.g.,
    `jus2026adult.txt`).

2.  Run the pipeline R scripts in order:

    - Extract author names
    - Search OpenAlex IDs
    - Retrieve papers
    - Build the coauthorship network
    - Compute network metrics
    - Visualize results

## Output

- Weighted coauthorship network (`.gml`) for Gephi
- Network metrics per author (`netSummary`)

``` r
library(knitr)
netSummary <- read.csv("netSummary.csv")
top10 <- netSummary[order(-netSummary$wdegree), ][1:10, ]
top10_display <- top10[, c("author", "degree", "wdegree", "betweenness", "community", "primary_neighbor_MaxW")]
kable(top10_display, format = "markdown")
```

|  | author | degree | wdegree | betweenness | community | primary_neighbor_MaxW |
|:---|:---|---:|---:|---:|---:|:---|
| 191 | Tammela Teuvo | 32 | 2448 | 0.0015354 | 2 | Auvinen Anssi |
| 87 | Knip Mikael | 51 | 2287 | 0.0318919 | 12 | Toppari Jorma |
| 6 | Aittokallio Tero | 55 | 2056 | 0.0120418 | 5 | Kontro Mika |
| 163 | Ristimäki Ari | 60 | 1932 | 0.0157585 | 5 | Haglund Caj |
| 197 | Toppari Jorma | 51 | 1899 | 0.0207606 | 12 | Knip Mikael |
| 211 | Visakorpi Tapio | 43 | 1876 | 0.0165469 | 2 | Nykter Matti |
| 33 | Haglund Caj | 47 | 1826 | 0.0172786 | 5 | Ristimäki Ari |
| 19 | Carpen Olli | 76 | 1809 | 0.0319828 | 10 | Hautaniemi Sampsa |
| 145 | Palotie Aarno | 103 | 1751 | 0.0487733 | 1 | Pirinen Matti |
| 180 | Schleutker Johanna | 39 | 1647 | 0.0000419 | 2 | Tammela Teuvo |

- Visualizations of network structure and centrality

## [View Interactive Co-authorship Network](https://jafarilab.github.io/Juselius_backdoor/network.html)

## License

MIT License – free to use and modify.


    This is a fully self-contained **R Markdown README**.  

    If you want, I can also add a **“Quick Start” code chunk** at the top so users can generate the scatter plot in **one go**, which is very handy for GitHub. Do you want me to do that?
