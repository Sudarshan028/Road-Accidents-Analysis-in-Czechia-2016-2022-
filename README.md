Based on the provided content from the Jupyter Notebook, here's a draft for your GitHub repository's README file:

---

# Road Accidents Analysis in Czechia (2016-2022)

This project analyzes road accidents in Czechia from 2016 to 2022 using a dataset that includes various attributes about the accidents. The analysis focuses on understanding patterns and trends in road accidents, such as the number of accidents by day, month, and year, the conditions of the drivers, types of road surfaces, and more.

## Table of Contents

- [Data Overview](#data-overview)
- [Analysis](#analysis)
  - [Data Loading](#data-loading)
  - [Data Exploration](#data-exploration)
  - [Visualizations](#visualizations)
- [Contributing](#contributing)
- [License](#license)


## Data Overview

The dataset `road_accidents_czechia_2016_2022.csv` contains 707,027 entries and 46 columns, detailing various aspects of road accidents in Czechia. Key columns include:
- `date`, `time`, `accident_kind`, `crash_kind`, `injury`, `cause_of_accident`, `killed_persons`, `severely_injured_persons`, `slightly_injured_persons`, `road_surface_type`, `driver_condition`, and more.

## Analysis

### Data Loading

The data is loaded using pandas:
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

sheet = pd.read_csv('road_accidents_czechia_2016_2022.csv')
sheet.head()
```

### Data Exploration

Basic exploration includes checking the shape and information of the data:
```python
sheet.shape
sheet.info()
```

### Visualizations

#### Extracting Date Information

Extracting day, month, year, and day of the week from the `date` column:
```python
sheet['date'] = pd.to_datetime(sheet['date'])
sheet['day'] = sheet['date'].dt.day.fillna(0).astype(int)
sheet['day_of_week'] = sheet['date'].dt.dayofweek.fillna(0).astype(int) + 1
sheet['month'] = sheet['date'].dt.month.fillna(0).astype(int)
sheet['year'] = sheet['date'].dt.year.fillna(0).astype(int)
```

#### Number of Killed, Severely Injured, and Slightly Injured Persons per Day

```python
a = sheet[sheet['day'] != 0]
a.groupby('day')['killed_persons'].sum().plot.bar()
plt.title('Number of Killed Persons per Day')
plt.ylabel('Number of Killed Persons')
plt.show()

a.groupby('day')['severely_injured_persons'].sum().plot.bar()
plt.title('Number of Severely Injured Persons per Day')
plt.ylabel('Number of Severely Injured Persons')
plt.show()

a.groupby('day')['slightly_injured_persons'].sum().plot.bar()
plt.title('Number of Slightly Injured Persons per Day')
plt.ylabel('Number of Slightly Injured Persons')
plt.show()
```

#### Number of Killed, Severely Injured, and Slightly Injured Persons per Month

```python
a = sheet[sheet['month'] != 0]
a.groupby('month')['killed_persons'].sum().plot.bar(color='red')
plt.title('Number of Killed Persons per Month')
plt.ylabel('Number of Killed Persons')
plt.show()

a.groupby('month')['severely_injured_persons'].sum().plot.bar(color='red')
plt.title('Number of Severely Injured Persons per Month')
plt.ylabel('Number of Severely Injured Persons')
plt.show()

a.groupby('month')['slightly_injured_persons'].sum().plot.bar(color='red')
plt.title('Number of Slightly Injured Persons per Month')
plt.ylabel('Number of Slightly Injured Persons')
plt.show()
```

#### Number of Killed, Severely Injured, and Slightly Injured Persons per Year

```python
a = sheet[sheet['year'] != 0]
a.groupby('year')['killed_persons'].sum().plot.bar(color='green')
plt.title('Number of Killed Persons per Year')
plt.ylabel('Number of Killed Persons')
plt.show()

a.groupby('year')['severely_injured_persons'].sum().plot.bar(color='green')
plt.title('Number of Severely Injured Persons per Year')
plt.ylabel('Number of Severely Injured Persons')
plt.show()

a.groupby('year')['slightly_injured_persons'].sum().plot.bar(color='green')
plt.title('Number of Slightly Injured Persons per Year')
plt.ylabel('Number of Slightly Injured Persons')
plt.show()
```

#### Driver Condition at the Time of Accident

```python
a = sheet[sheet['driver_condition'] != 'undetected, driver drove off']
driver_condition_counts = a.groupby('driver_condition')['driver_condition'].count().sort_values(ascending=False)
print(driver_condition_counts)
```

#### Type of Road Surface

```python
a = sheet[sheet['year'] != 0]
road_surface_counts = a.groupby('road_surface_type')['road_surface_type'].count().sort_values(ascending=False)
print(road_surface_counts)
```

#### Road Type

```python
a = sheet[sheet['year'] != 0]
road_type_counts = a.groupby('road_type')['road_type'].count().sort_values(ascending=False).head(7)
print(road_type_counts)
```

#### Cause of Accident

```python
a = sheet[sheet['year'] != 0]
cause_of_accident_counts = a.groupby('cause_of_accident')['cause_of_accident'].count().sort_values(ascending=False)
print(cause_of_accident_counts)
```

#### Driver Category Involved in Accidents

```python
a = sheet[(sheet['driver_category'] != 'not detected (e.g. for foreigners)') & (sheet['driver_category'] != 'undetected, driver drove off')]
driver_category_counts = a.groupby('driver_category')['driver_category'].count().sort_values(ascending=False)
print(driver_category_counts)
```

#### Vehicle Type Involved in Accidents

```python
a = sheet[sheet['vehicle_type'] != 'undetected, driver drove off']
vehicle_type_counts = a.groupby('vehicle_type')['vehicle_type'].count().sort_values(ascending=False)
print(vehicle_type_counts)
vehicle_type_counts.head(5).plot.pie(autopct="%1.1f%%")
plt.title("Vehicle Type Distribution")
plt.show()
```

## Contributing

Contributions are welcome! Please follow these steps to contribute:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Make your changes.
4. Commit your changes (`git commit -am 'Add new feature'`).
5. Push to the branch (`git push origin feature/your-feature`).
6. Create a new Pull Request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.

---
