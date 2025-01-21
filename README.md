# Life Expectancy vs GDP Data Visualization

This project visualizes the relationship between life expectancy and GDP per capita over time (1950-2018) using an interactive scatter plot. The dataset includes information about GDP, life expectancy, population, and continent for multiple countries.

---

## Prerequisites

Install the required libraries:

```bash
pip install kaggle plotly pandas
```

---

## Steps to Run the Project

### Step 1: Upload Kaggle API Key

1. Download your Kaggle API key (`kaggle.json`) from [Kaggle](https://www.kaggle.com/account).
2. Upload the `kaggle.json` file to your environment:

```python
from google.colab import files
files.upload()
```

### Step 2: Configure Kaggle

Set up the Kaggle API credentials:

```bash
!mkdir -p ~/.kaggle
!cp kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json
```

### Step 3: Download the Dataset

Download the dataset using the Kaggle API:

```bash
!kaggle datasets download -d luxoloshilofunde/life-expectancy-vs-gdp-19502018
```

Unzip the dataset:

```bash
!unzip life-expectancy-vs-gdp-19502018.zip
```

### Step 4: Load and Explore the Dataset

Load the dataset using pandas:

```python
import pandas as pd

df = pd.read_csv('Life Expectancy vs GDP 1950-2018.csv')
print(df.head())
```

Check for missing values and handle them:

```python
df['Population (historical estimates)'] = df['Population (historical estimates)'].fillna(0)
```

---

## Data Visualization

### Create an Interactive Scatter Plot

Use Plotly to create an animated scatter plot:

```python
import plotly.express as px

fig = px.scatter(
    df,
    x='GDP per capita',
    y='Life expectancy',
    animation_frame='Year',
    animation_group='Country',
    size='Population (historical estimates)',
    color='Continent',
    hover_name='Country',
    log_x=True,
    size_max=55,
    range_x=[100, 100000],
    range_y=[30, 90]
)

fig.update_layout(
    title='Life Expectancy vs GDP per Capita (1950-2018)',
    xaxis_title='GDP per Capita (log scale)',
    yaxis_title='Life Expectancy (years)'
)

fig.show()
```

---

## Key Features

- **Animated Scatter Plot**: Shows changes in life expectancy and GDP per capita over time.
- **Interactive Elements**: Hover over points to view detailed information for each country.
- **Color-Coded by Continent**: Makes it easier to identify regional patterns.
- **Logarithmic Scale for GDP**: Improves visualization of variations across countries with large GDP differences.

---

## Dataset Details

- **Source**: [Kaggle - Life Expectancy vs GDP 1950-2018](https://www.kaggle.com/datasets/luxoloshilofunde/life-expectancy-vs-gdp-19502018)
- **Columns**:
  - `Country`: Name of the country
  - `Year`: Year of the data
  - `Life expectancy`: Average life expectancy in years
  - `GDP per capita`: Gross Domestic Product per capita in USD
  - `Population (historical estimates)`: Population of the country
  - `Continent`: Continent of the country

---

## Notes

- Ensure the Kaggle API key is uploaded correctly to access the dataset.
- The dataset contains some missing values, which are filled with 0 for population.
- You can modify the `size_max` parameter in the Plotly scatter plot for better visualization.

---

## License

This project is open-source and available under the MIT License.

