# Exploring Socio-Economic Trends in England and Wales: A Visual Analytics Approach

This repository contains the coursework project **“Exploring Socio-Economic Trends in England and Wales: A Visual Analytics Approach”**, developed as part of the MSc programme at the **University of Bristol**.

The project investigates **health inequalities and socio-economic disadvantage across Local Authority Districts (LADs) in England and Wales** using 2011 and 2021 Census data. It combines data preparation, geographic harmonisation, dimensionality reduction, clustering and interactive Tableau dashboards to explore how poor health relates to unemployment, qualifications, housing and other socio-economic factors.

## Project Objectives

The project addresses five main questions:

1. Which LADs have the highest levels of bad or very bad health?
2. Do areas with poorer health also show higher unemployment, lower education or poorer housing?
3. How did health-related disadvantage change between 2011 and 2021?
4. Which LADs appear as outliers?
5. Can dimensionality-reduction methods identify groups of LADs with similar health and socio-economic profiles?

The dashboards are designed for **public health analysts, local authority decision-makers and policy researchers**.

## Data

The project uses LAD-level Census data for England and Wales.

### 2011 data

The 2011 analysis uses data relating to:

- General health
- Economic activity
- Highest qualification
- Housing tenure

After cleaning and merging, the main 2011 dataset contained:

- **348 LADs**
- **89 columns**

A smaller health-economic dataset with **348 rows and 47 columns** was also created for comparison with 2021.

### 2021 data

The 2021 data includes general health and economic activity measures, with percentage measures calculated during preprocessing.

The cleaned 2021 dataset contained:

- **331 LADs**
- **41 columns**
- No missing values

### Geographic harmonisation

Because LAD boundaries and codes changed between the 2011 and 2021 Censuses, a harmonisation step was required.

Where older LADs had been merged into newer authorities, count variables were aggregated first and percentages were recalculated from the new totals.

The final comparison dataset contained:

- **331 comparable LADs per year**
- **662 LAD-year records in total**

Eight newer successor LADs were retained in the analysis but excluded from filled-map views where Tableau could not recognise their newer geographic boundaries.

## Data Preparation

The cleaning workflow included:

- Removing metadata rows and unnecessary headers
- Filtering to England and Wales LAD codes
- Standardising column names
- Cleaning numeric fields
- Merging count and percentage datasets
- Calculating percentage measures where required
- Harmonising LAD codes between census years
- Adding Tableau-compatible geographic fields
- Preparing modelling and projection datasets

Counts were retained to show the **absolute scale of affected populations**, while percentages were used for **fair comparison between LADs of different sizes**.

## Visual Analytics

The Tableau workbook contains four main dashboards.

### Dashboard 1 — 2011 Baseline

Explores spatial patterns in health inequality and related socio-economic conditions in 2011.

Key views include:

- Choropleth map
- Top 15 LAD bar chart
- Scatterplot
- Selected LAD profile
- Percentage/count selector

The dashboard allows users to compare poor health with socio-economic measures such as unemployment, low qualifications and housing tenure.

### Dashboard 2 — 2011 vs 2021 Comparison

Shows how selected health and socio-economic measures changed between 2011 and 2021.

Key features include:

- Change maps
- Top 15 change rankings
- Scatterplots of health change versus socio-economic change
- Selected LAD comparison
- Percentage/count switching
- Separate handling of LADs not recognised by Tableau geocoding

### Dashboard 3 — PCA and BGMM

Uses **Principal Component Analysis (PCA)** to reduce the dimensionality of the socio-economic data.

For the 2011 projection:

- 39 percentage-based features were standardised using `StandardScaler`
- PC1 and PC2 explained **53.4%** of the variance
- The first six principal components explained **82.36%**
- Six PCA components were used for Bayesian Gaussian Mixture Model clustering
- PC1 and PC2 were visualised in Tableau

The dashboard also includes:

- BGMM cluster labels
- BGMM confidence values
- Cluster profiles
- Selected LAD profiles
- Lowest-confidence LADs

### Dashboard 4 — UMAP and BGMM

Uses **Uniform Manifold Approximation and Projection (UMAP)** to identify non-linear local structure and neighbourhoods in the LAD data.

UMAP is combined with **Bayesian Gaussian Mixture Modelling (BGMM)** to identify clusters and uncertain assignments.

The dashboard includes:

- UMAP projection
- BGMM clusters
- Confidence-based point sizing
- Uncertain LAD assignments
- Cluster profiles
- Selected LAD profiles

## Methods

The project uses the following methods:

- Data cleaning and preprocessing
- Geographic harmonisation
- Percentage and count-based comparison
- Exploratory visual analytics
- Principal Component Analysis (PCA)
- Uniform Manifold Approximation and Projection (UMAP)
- Bayesian Gaussian Mixture Modelling (BGMM)
- Interactive Tableau dashboard design
- User evaluation

## Key Findings

The analysis found that health inequality is not evenly distributed across England and Wales.

In the 2011 percentage view:

- **Merthyr Tydfil** had the highest rate of bad or very bad health at **11.17%**
- **Blaenau Gwent** followed at **10.69%**
- **Neath Port Talbot** followed at **10.46%**

The count view produced a different picture, with larger authorities such as **Birmingham** having the highest absolute number of residents reporting bad or very bad health.

Relationships between poor health and other variables also differed in strength:

- Long-term sickness/disability showed the strongest relationship with poor health
- No qualifications also showed a strong positive relationship
- Unemployment showed a moderate relationship
- Social rented housing showed a weaker relationship
- Private renting showed very little relationship

For the 2011–2021 comparison, changes in long-term sickness/disability showed the clearest association with changes in poor health.

PCA and UMAP also revealed broader groups of LADs with similar socio-economic and health profiles, while BGMM confidence values helped identify uncertain or boundary cases.

## Evaluation

The visualisation was evaluated with three students from the discussion group.

Feedback led to several improvements, including:

- Adding a percentage/count selector
- Improving explanations of dashboard controls
- Clarifying why some LADs appear outside the main map
- Refining the target audience
- Improving interpretation of geographic and comparison views

## Technologies

- **Python**
- **Pandas**
- **NumPy**
- **Scikit-learn**
- **UMAP**
- **Bayesian Gaussian Mixture Models**
- **Tableau**
- **Jupyter Notebook**

## Repository Structure

```text
MSc-Visual-Analytics-UOB/
│
├── datasets/
│   └── Source, cleaned and derived datasets
│
├── VISA_cleaning.ipynb
│   └── Data cleaning, transformation and LAD harmonisation
│
├── VISA_modelling.ipynb
│   └── PCA, UMAP and BGMM modelling
│
├── Visual Analytics Coursework.twb
│   └── Tableau workbook containing the dashboards
│
├── SnehSaphalaReport.pdf
│   └── Final project report
│
├── VISA Coursework Specification.pdf
│   └── Coursework brief
│
└── README.md
```

## Running the Project

Clone the repository:

```bash
git clone https://github.com/saphala2712sneha/MSc-Visual-Analytics-UOB.git
cd MSc-Visual-Analytics-UOB
```

Open the notebooks in Jupyter:

```bash
jupyter notebook
```

Recommended order:

1. `VISA_cleaning.ipynb`
2. `VISA_modelling.ipynb`
3. Open `Visual Analytics Coursework.twb` in Tableau Desktop

## Limitations

Important limitations include:

- LAD boundaries changed between 2011 and 2021
- Tableau could not recognise some newer LAD boundaries
- Census data provides snapshots rather than continuous annual measurements
- Scatterplot trend lines show association, not causation
- PCA captures linear structure, while UMAP focuses on local non-linear structure
- BGMM cluster assignments should be interpreted alongside confidence values

## Author

**Sneha Saphala Ram Prasad**  
MSc, University of Bristol

GitHub: [saphala2712sneha](https://github.com/saphala2712sneha)

## Academic Use

This repository was created for academic coursework at the **University of Bristol**.

The project is intended for educational and portfolio purposes.
