# Terrorism Hotspots Analysis

## Project Overview

This project explores patterns in recorded terrorist incidents around the world between 1970 and 2017 using the Global Terrorism Database. The analysis looks at how incident counts changed over time, how trends differed by region, which attack methods were most common, how incident counts related to casualties, and where incidents were geographically concentrated.

The goal is to make a large historical dataset easier to understand through data analysis, statistical comparisons, and interactive visualizations. This is a descriptive analysis of the recorded data, not a model for predicting future incidents or establishing causes.

## Questions Explored

1. How did incident counts change over time, and how did regional patterns compare with the global trend?
2. How closely were incident counts and casualties related, and which country and year observations differed from the overall pattern?
3. Which attack methods were most common, and how did the mix vary across regions and time?
4. Where were incidents concentrated geographically, both by location and by country?

## Dataset

The notebook reads a compressed Global Terrorism Database extract named `globalterrorismdb_0718dist.tar.bz2`. The original dataset contains 181,691 incidents and 136 columns. The analysis selects 23 fields relevant to dates, country and region, location, attack type, targets, attributed groups, weapons, fatalities, and injuries.

A casualty count is derived by combining recorded deaths and injuries. A separate set of records with valid latitude and longitude values is used for mapping. The notebook expects the dataset file to be available locally with the expected filename.

## Tools and Technologies

* **Python** for the analysis workflow.
* **Pandas** for data loading, cleaning, grouping, aggregation, and summary tables.
* **NumPy** for numerical calculations, logarithmic transformations, and fitting a trend line.
* **Plotly Express and Plotly Graph Objects** for interactive charts and geographic visualizations.
* **Jupyter Notebook and IPython** for running the analysis and displaying results.
* **Matplotlib and Seaborn** are also imported in the notebook, although most visualizations are built with Plotly.

## Methodology

### 1. Data inspection and preparation

The notebook loads the compressed dataset, checks its structure, and reviews missing values. It then selects fields needed to answer the project questions. Special unknown codes in the perpetrator count field are converted to missing values. Deaths and injuries are combined to calculate casualties, while records without coordinates are kept out of the mapping dataset.

### 2. Trends over time and across regions

Incident counts are grouped by year and by region. Line charts compare yearly activity, area charts show each region's share of global incidents, and regional peak years are identified. Additional comparisons index each region to its own peak so that the timing of regional changes can be compared even when total volumes differ.

### 3. Incidents and casualties

The data is aggregated by country and year to compare incident counts with total casualties. Pearson correlation, Spearman rank correlation, and Pearson correlation after a logarithmic transformation are calculated. The same measures are recalculated after removing the ten country and year observations with the highest casualty totals to check whether the relationship depends heavily on extreme cases.

A fitted line on logarithmic axes is used to identify observations with substantially more or fewer casualties than the broader pattern would suggest. Those observations are then examined by attack type, target category, attributed group, and largest recorded incident. The analysis also compares incident counts with casualties per incident, which helps distinguish the frequency of attacks from their average impact.

### 4. Attack methods

Attack types are counted and compared as shares of all incidents. The notebook uses bar charts to show the most common methods, heatmaps to compare the mix across regions, and charts grouped into five year periods to examine how methods changed over time.

### 5. Geographic concentration

The notebook maps a random sample of 20,000 incidents with usable coordinates and separately maps the 2,000 incidents with the highest casualty counts. Country level choropleth maps compare incident and casualty totals using a logarithmic color scale. Country rankings are also calculated for total incidents and total casualties.

## Key Findings

### Historical and regional trends

* Global incident counts rose gradually from fewer than 1,000 per year in 1970 to around 5,000 by the early 1990s. Counts then declined before rising sharply after 2010.
* The global peak was about 17,000 incidents in 2014, followed by a decline to around 11,000 in 2017. Incident counts roughly tripled between 2011 and 2014.
* Regional trends differed substantially. The Middle East and North Africa and South Asia together accounted for roughly 70 percent of the 2014 global peak. Western Europe, South America, and Central America and the Caribbean reached their peaks decades earlier.

### Incident counts and casualties

* Across 3,762 country and year observations, incident counts and total casualties had a Spearman correlation of 0.761, indicating a strong positive association.
* The relationship remained almost unchanged after removing the ten country and year observations with the highest casualty totals. Spearman correlation changed from 0.761 to 0.759.
* The relationship between incident count and casualties per incident was much weaker, with a Spearman correlation of 0.32. A country can experience many incidents without having the highest average casualty count per incident, and a single major event can dominate a year's total.

### Attack methods

* Bombing and Explosion was the most common method, accounting for 48.6 percent of incidents.
* Armed Assault accounted for 23.5 percent and Assassination for 10.6 percent. Together, these three categories represented about 83 percent of recorded incidents.
* Bombing and Explosion led in most regions and in almost every year. Armed Assault was the leading method in Central America and the Caribbean, and its share was close to the share of bombings in Sub Saharan Africa.
* The increase after 2010 appeared across multiple attack methods, with bombings and armed assaults contributing the largest increases.

### Geographic concentration

* The ten countries with the most incidents accounted for 55 percent of all recorded incidents.
* Iraq, Pakistan, Afghanistan, and India together accounted for 35.1 percent of incidents.
* Iraq ranked first for both incident count and recorded casualties, with 24,636 incidents and 213,279 casualties in the dataset.
* The locations of incidents were concentrated in the Middle East and North Africa, South Asia, Sub Saharan Africa, Southeast Asia, the Andes, and Central America. The maps show raw counts rather than population adjusted rates.

## Visualizations Included

* Annual incident trends and regional comparisons.
* Regional shares of global incidents and regional peak year comparisons.
* Scatter plots comparing incidents with casualties, including a fitted trend line and observations far from the trend.
* Bar charts and heatmaps showing attack methods by region and time period.
* Geographic maps of a random sample of incidents and the incidents with the highest casualty counts.
* Country level maps and rankings for incidents and casualties.

## How to Run the Project

1. Place the compressed dataset `globalterrorismdb_0718dist.tar.bz2` in the same directory as the notebook. If the file has a different name or location, update the file path in the first code cell.
2. Install the required packages in your Python environment:

   ```text
   pip install pandas numpy matplotlib seaborn plotly jupyter
   ```

3. Start Jupyter Notebook:

   ```text
   jupyter notebook
   ```

4. Open `terrorism_hotspots.ipynb` and run the cells from top to bottom. Later sections reuse dataframes created earlier in the notebook.

## Limitations and Data Considerations

* The Global Terrorism Database has no records for 1993.
* The database's collection methods changed over time. Abrupt changes, including the large drop around 1998, may partly reflect changes in recording practices rather than changes in real world activity alone.
* Casualty totals are based on recorded deaths and injuries. Missing values mean the totals may be lower than the true numbers. The findings report also flags near identical, very large casualty counts in two New York records from 2001, which may overstate that country and year total.
* Some incidents have missing or approximate coordinates. The geographic maps omit incidents without usable coordinates, and coordinate coverage is lowest in Central America and the Caribbean.
* The country maps use raw counts rather than rates per person. They show where recorded incidents were most numerous, not the relative risk faced by people in each country.
* Some historical country names do not map cleanly to modern geographic boundaries. The notebook checks for possible unmatched names, but some locations may remain unshaded in the choropleth maps.
* The dataset ends in 2017, so the results describe the historical period covered by this extract and should not be treated as a picture of current conditions.

## Conclusion

The analysis shows that global incident counts changed markedly across the period, with the surge around 2014 concentrated in a few regions. Bombing and Explosion was the dominant recorded method, while the geography of incidents was concentrated in a relatively small number of countries. The casualty analysis adds an important distinction: the number of incidents is strongly associated with total casualties, but it is much less informative about the average impact of an individual incident. These findings are best read alongside the dataset's missing years, evolving collection methods, and incomplete casualty and location information.
