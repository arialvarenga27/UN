# UN Development Indicators: Country Clustering

## Project overview

This project uses country-level United Nations development indicators to
explore whether countries can be meaningfully grouped into broad
development categories.

The analysis applies **K-means clustering** to numerical development
indicators and uses the **Elbow Method** to assess the number of
clusters suggested by the data. It considers the broader argument in
*Factfulness* that global development is more nuanced than a simple
developed-versus-developing division.

## Research questions

1.  Can the world be meaningfully divided into only two clusters
    (developed vs. developing)?
2.  How many clusters are suggested by the data according to the Elbow
    Rule?
3.  How much of the data structure is explained by two clusters compared
    with other cluster solutions?
4.  Does the evidence support the *Factfulness* claim that the world
    cannot be divided into only two groups, but rather into four?

## Dataset

The notebook loads a CSV file named `UN.csv`:

``` python
df = pd.read_csv('/content/UN.csv')
```

The analysis covers **207 countries**. The dataset includes country and
region identifiers, as well as numerical development indicators.
Indicators discussed in the notebook include GDP per capita, life
expectancy, education, infant mortality, and economic activity.

**Data requirement:** `UN.csv` is not embedded in the notebook. You must
provide this file separately before running the analysis. If you are not
using Google Colab, update the file path in the loading cell to match
where you have saved the CSV.

## Methodology

The notebook follows these steps:

1.  **Load and inspect the data** --- read `UN.csv`, inspect data types
    and missing values, and calculate descriptive statistics for
    numerical variables.
2.  **Handle missing values** --- replace missing values in numerical
    columns with each column's median.
3.  **Prepare the features** --- exclude the non-numerical `country` and
    `region` columns from the clustering input.
4.  **Standardize the indicators** --- apply `StandardScaler` so
    numerical features are placed on a comparable scale before
    clustering.
5.  **Explore a three-cluster solution** --- fit K-means with three
    clusters and inspect cluster sizes and example countries.
6.  **Apply the Elbow Method** --- calculate K-means inertia for values
    of K from 1 to 10 and plot the resulting curve.
7.  **Select and fit the two-cluster solution** --- the notebook's Elbow
    Rule calculation identifies K = 2, and a final K-means model is
    fitted with two clusters.
8.  **Interpret the results** --- compare the groups and consider what
    the clustering suggests about global development.

K-means uses `random_state=42` for reproducibility. The Elbow Method
evaluates within-cluster sum of squares (inertia): as the number of
clusters increases, inertia decreases, and the elbow is used to identify
a balance between fit and model complexity.

## Main findings

-   The notebook's Elbow Rule calculation recommends **two clusters (K =
    2)** for this dataset.
-   The notebook also explores a three-cluster solution to illustrate
    that countries can show different combinations of economic,
    educational, and demographic characteristics.
-   In the final two-cluster interpretation, **Albania** is used as an
    example of a country in Cluster 0, while **Bangladesh** is used as
    an example of a country in Cluster 1.
-   The interpretation notes that countries from different continents
    can be grouped together, suggesting that development patterns are
    not determined by geographical proximity alone.
-   The conclusion is nuanced: although two clusters are selected by the
    Elbow Rule, this does not establish that global development can be
    fully represented by only two categories. The analysis therefore
    supports the broader *Factfulness* argument that development is
    multidimensional, but it does **not** statistically establish that
    four clusters are optimal.

Cluster labels such as `0` and `1` are algorithm-generated identifiers;
they do not inherently mean "developed" or "developing."

## Requirements

The notebook uses Python and the following libraries:

-   `pandas`
-   `numpy`
-   `matplotlib`
-   `scikit-learn`

Install the dependencies with:

``` bash
pip install pandas numpy matplotlib scikit-learn jupyter
```

## How to run

### Option 1: Google Colab

1.  Open `UN_development_indicators.ipynb` in Google Colab.
2.  Upload `UN.csv` to the Colab runtime.
3.  Make sure the CSV is available at `/content/UN.csv`, or update the
    path in the first code cell.
4.  Run the notebook cells in order.

### Option 2: Local Jupyter environment

1.  Place `UN_development_indicators.ipynb` and `UN.csv` in your project
    directory.

2.  Install the requirements listed above.

3.  In the first code cell, change the data-loading path to:

    ``` python
    df = pd.read_csv('UN.csv')
    ```

4.  Start Jupyter:

    ``` bash
    jupyter notebook
    ```

5.  Open the notebook and run all cells from top to bottom.

## Project files

``` text
.
├── UN_development_indicators.ipynb
├── UN.csv
└── README.md
```

`UN.csv` is a required input file and must be obtained or supplied
separately; it is not included in the notebook itself.

## Limitations and interpretation notes

-   K-means identifies groups based on the numerical features and
    preprocessing choices used in the notebook. The resulting clusters
    are not definitive development classifications.
-   Median imputation is used for missing numerical values; this can
    affect distances between countries.
-   Standardization makes indicators comparable in scale, but it does
    not by itself eliminate outliers or skewness.
-   The Elbow Method is a heuristic. Its recommendation of K = 2 should
    be interpreted alongside the research question and the limitations
    of representing multidimensional development with a small number of
    clusters.
-   The notebook explores three clusters but uses two clusters for its
    final model, following the reported Elbow Rule result.

## Reproducibility

The K-means models use `random_state=42`. The notebook should be run
from top to bottom so that data cleaning, standardization, inertia
calculations, and cluster assignments are created before they are used
in later cells.
