Readme
================
2026-04-07

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

## 🚀 Usage

1.  Place your grantee text file in the project folder (e.g.,
    `jus2026adult.txt`).

2.  Run the pipeline R scripts in order:

    - Extract author names
    - Search OpenAlex IDs
    - Retrieve papers
    - Build the coauthorship network
    - Compute network metrics
    - Visualize results

## 📊 Output

- Weighted coauthorship network (`.gml`) for Gephi
- Network metrics per author (`netSummary`)
- Visualizations of network structure and centrality

Top 10 Researchers (by weighted degree):

|  | author | degree | wdegree | betweenness | community | primary_neighbor_MaxW |
|:---|:---|---:|---:|---:|---:|:---|
| 193 | Tammela Teuvo | 33 | 4897 | 0.0006030 | 2 | Auvinen Anssi |
| 88 | Knip Mikael | 51 | 4574 | 0.0297573 | 13 | Toppari Jorma |
| 6 | Aittokallio Tero | 55 | 4097 | 0.0152286 | 6 | Kontro Mika |
| 165 | Ristimäki Ari | 62 | 3973 | 0.0156645 | 6 | Haglund Caj |
| 199 | Toppari Jorma | 52 | 3795 | 0.0267586 | 13 | Knip Mikael |
| 213 | Visakorpi Tapio | 44 | 3774 | 0.0185478 | 2 | Nykter Matti |
| 33 | Haglund Caj | 49 | 3681 | 0.0164748 | 6 | Ristimäki Ari |
| 19 | Carpen Olli | 76 | 3613 | 0.0279969 | 12 | Hautaniemi Sampsa |
| 147 | Palotie Aarno | 103 | 3493 | 0.0462684 | 1 | Pirinen Matti |
| 182 | Schleutker Johanna | 39 | 3291 | 0.0000411 | 2 | Tammela Teuvo |

Top 3 Researchers per Community:

| author                  | wdegree | community |
|:------------------------|--------:|----------:|
| Palotie Aarno           |    3493 |         1 |
| Hiltunen Mikko          |    2320 |         1 |
| Rinne Juha              |    2090 |         1 |
| Tammela Teuvo           |    4897 |         2 |
| Visakorpi Tapio         |    3774 |         2 |
| Schleutker Johanna      |    3291 |         2 |
| Töyräs Juha             |    1442 |         3 |
| Korhonen Rami           |    1246 |         3 |
| Saarakkala Simo         |     951 |         3 |
| Jalkanen Sirpa          |    2748 |         4 |
| Salmi Marko             |    2182 |         4 |
| Roivainen Anne          |    1763 |         4 |
| Saarma Mart             |     627 |         5 |
| Palva Matias            |     572 |         5 |
| Palva Satu              |     456 |         5 |
| Aittokallio Tero        |    4097 |         6 |
| Ristimäki Ari           |    3973 |         6 |
| Haglund Caj             |    3681 |         6 |
| Alitalo Kari            |    2618 |         7 |
| Yla Herttuala           |    2052 |         7 |
| Malm Tarja              |    1599 |         7 |
| Hallman Mikko           |     667 |         8 |
| Rämet Mika              |     556 |         8 |
| Ashorn Per              |     276 |         8 |
| Groop Per-Henrik        |    1810 |         9 |
| Pietiläinen Kirsi       |    1150 |         9 |
| Sandholm-Lafferre Niina |     873 |         9 |
| Belogurov Georgi        |      80 |        10 |
| Malinen Anssi           |      48 |        10 |
| Metsä-Ketelä Mikko      |      44 |        10 |
| Vapalahti Olli          |    2251 |        11 |
| Varjosalo Markku        |    1830 |        11 |
| Kere Juha               |    1722 |        11 |
| Carpen Olli             |    3613 |        12 |
| Hautaniemi Sampsa       |    3236 |        12 |
| Kauppi Liisa            |    1576 |        12 |
| Knip Mikael             |    4574 |        13 |
| Toppari Jorma           |    3795 |        13 |
| Hyöty Heikki            |    3224 |        13 |

## [View Interactive Co-authorship Network](https://jafarilab.github.io/Juselius_backdoor/network.html)

## ⚠️ Notes & Limitations

- Author matching is based on name search and may introduce minor errors
- OpenAlex data is continuously updated → results may vary between runs
- API rate limits and connectivity can affect data retrieval
- Some manual validation was performed, but results are not error-free

## 📌 Interpretation Notes

- High degree + low wdegree → broad but shallow collaboration
- Low degree + high wdegree → deep collaboration with few partners
- Primary neighbor → strongest collaboration link (potential entry point
  into a research cluster)

## License

MIT License – free to use and modify.


    This is a fully self-contained **R Markdown README**.  

    If you want, I can also add a **“Quick Start” code chunk** at the top so users can generate the scatter plot in **one go**, which is very handy for GitHub. Do you want me to do that?
