# World Electricity Analysis EDA Project

This project focuses on the analysis of global electricity production, transmission, distribution losses, and access data. By aggregating data from various sources, cleaning and preprocessing it, and performing detailed analysis, we aim to provide insights into electricity trends and disparities across regions and income groups. The results are visualized through an interactive Power BI dashboard, and findings are summarized in a comprehensive report.

## Authors
- [Hashir Sheikh](https://github.com/hashir-sheikh-da)
- [Ghanshyam Jadhav](https://github.com/ghanshyamjadhav2125)
- [Saloni Gupta](https://github.com/SaloniGupta0956)
- [Ashish Agrahari](https://github.com/Ashish12122024)

## Key Objectives:
- 🔍 Data Collection: Aggregating data from multiple CSV files, which include details about electricity access (rural, urban, and total), electricity transmission and distribution losses, and electricity production from nuclear, oil, and renewable sources.
- 🛠️ Data Cleaning: Processing the data to handle missing values, ensure consistency, and integrate metadata for comprehensive analysis.
- 📊 Data Analysis: Utilizing Python for preprocessing and SQL for querying to generate meaningful insights. This stage involves aggregating data, calculating proportions, and summarizing key metrics.
- 📈 Visualization: Creating an interactive Power BI dashboard that presents the insights through various visualizations such as line charts, grouped bar charts, stacked bar charts, pie charts, donut charts, and filled maps. Each visualization aims to highlight different aspects of the data, making it easier to understand and interpret the findings.
- 📃 Reporting: Summarizing the analysis and insights in a detailed report, which includes PowerPoint presentations and interactive dashboard views, to communicate the findings effectively to stakeholders.

## Project Deliverables:
- 📝 Data Collection Scripts: Python scripts used to aggregate and preprocess data from multiple CSV files.
- 📂 Cleaned Data: A cleaned dataset saved in CSV format, integrated with metadata for comprehensive analysis.
- 📑 SQL/NoSQL Queries: SQL scripts to analyze the cleaned data and generate insights.
- 📊 Power BI Dashboard: An interactive dashboard for visualizing data, including trends in electricity production, distribution losses, and access across different regions and income groups.
- 📋 PowerPoint Presentation: Slides summarizing the project, data insights, and key findings to communicate the results effectively to stakeholders.

## Table of Contents 
    1. Introduction
    2. Data Collection
    3. Data Cleaning
    4. Data Analysis
    5. Dashboard Creation
    6. Conclusion

### 1. Introduction
This project focuses on the comprehensive analysis of global electricity data, covering production, transmission, distribution losses, and access. The goal is to collect, clean, and analyze this data to provide meaningful insights into electricity trends and disparities across regions and income groups. The findings will be visualized through an interactive Power BI dashboard and summarized in a detailed report, including a PowerPoint presentation for stakeholders.
    
### 2. Data Collection
We collected data from multiple JSON files, each containing information on different aspects of electricity access and production. The datasets include:

- Access to electricity (rural, urban, and total)
- Electricity transmission and distribution losses
- Electricity production from nuclear, oil, and renewable sources

### 3. Data Cleaning

#### Deployment

Data cleaning involved handling missing values, ensuring consistency, and integrating metadata for comprehensive analysis.

#### Libraries Nedded
- pandas for data manipulation and analysis
- numpy for numerical operations

#### Import libraries, Load the JSON files, Cleaned the Data and Converted to CSV files for further Analysis
```bash
import pandas as pd
import numpy as np

def load_json_data(file_path):
    """
    Load JSON data, set correct headers, replace empty strings with NaN, 
    convert columns to numeric types, and eliminate year columns from 1960 to 1999.
    
    Parameters:
    file_path (str): The path to the JSON file.
    
    Returns:
    pd.DataFrame: The cleaned and processed DataFrame.
    """
    # Load JSON data into a DataFrame
    data_df = pd.read_json(file_path)
    
    # Drop the first row
    data_df = data_df.drop(index=0)
    
    # Set the second row as the header
    data_df.columns = data_df.iloc[0]
    data_df = data_df.drop(index=1)
    
    # Reset the index to remove the old index and reindex starting from 1
    data_df = data_df.reset_index(drop=True)
    data_df.index = data_df.index + 1
    
    # Drop the empty column if it exists
    if '' in data_df.columns:
        data_df = data_df.drop(columns=[''])
    
    # Replace empty strings with NaN
    data_df.replace('', 0, inplace=True)
    data_df.fillna(0, inplace=True)
    
    # Convert year columns to numeric types
    for col in data_df.columns:
        if col not in ['Country Name', 'Country Code', 'Indicator Name', 'Indicator Code']:
            data_df[col] = pd.to_numeric(data_df[col], errors='coerce')
    
    # Round all column values to 2 decimal places
    data_df = data_df.round(2)
    
    # Rename columns
    new_columns = {}
    for col in data_df.columns:
        try:
            new_columns[col] = int(float(col))  # Convert to int if possible
        except ValueError:
            new_columns[col] = col.replace('.0', '')  # Remove '.0' if present
    
    data_df.rename(columns=new_columns, inplace=True)
    
    # Drop columns from 1960 to 1999
    columns_to_drop = [year for year in range(1960, 2000)]
    data_df = data_df.drop(columns=columns_to_drop, errors='ignore')

    # Inspect the modified DataFrame
    print("Modified DataFrame:")
    print(data_df.head())
    
    return data_df

# Example usage
json_data_file = 'electricity_production_renewable_sources.json'
df = load_json_data(json_data_file)

```

### 4. Data Analysis
After collecting and cleaning the data, we proceeded to analyze it to extract meaningful insights. The primary focus of our analysis was to understand global electricity trends and disparities across regions and income groups. Here are the key steps and techniques we used in our data analysis:

### Descriptive Statistics:
- Electricity Access Analysis: We calculated the average, minimum, and maximum electricity access percentages for each country and region.
- Production Analysis: We analyzed the average production values from nuclear, oil, and renewable sources for each country to identify key producers and their contributions.
- Loss Analysis: We examined the transmission and distribution losses across different countries and regions.

### Grouping and Aggregation:
- Regional Analysis: We grouped the data by region to identify trends in electricity access and production across different geographical areas.
- Income Group Analysis: We analyzed electricity access and production data based on income groups to understand disparities and identify areas needing improvement.

### Trend Analysis:
- Yearly Trends: We looked at the trends over the years for electricity access, production, and losses to identify significant changes and patterns.
- Source Analysis: We analyzed the proportions of electricity production from nuclear, oil, and renewable sources to understand the energy mix of different countries and regions.
Here, I'm including the document with the detailed insights we derived from our data analysis.

[Detailed Insights](https://github.com/hashir-sheikh-da/Preamble_PyTorch_048/blob/main/Data_Analysis_Report/world_electricity_analysis.pdf)

### 6. Dashboard Creation
To make our analysis accessible and user-friendly, we created an interactive Power BI dashboard. The dashboard provides a comprehensive view of global electricity trends, production, and access. Key features of the dashboard include:

- Interactive Filters: Allow users to filter data by region, income group, year, and other criteria for a customized view.
- Visual Representations: Includes various visualizations such as line charts, bar charts, pie charts, and maps to represent different aspects of the data.
- Detailed Tables: Provides tables with aggregated data for in-depth analysis.
- Insights: Highlights key findings and trends from the data.

Here is a screenshot of the dashboard:

![Dashboard](https://github.com/hashir-sheikh-da/Preamble_PyTorch_048/blob/main/Data_PowerBI_Assets/dashboard_world_electricity_analysis.png)

The dashboard is designed to be an invaluable tool for stakeholders, allowing them to explore the data dynamically and make informed decisions.

[Link to Interactive Dashboard](https://github.com/hashir-sheikh-da/Preamble_PyTorch_048/blob/main/Data_PowerBI_Assets/dashboard_world_electricity_analysis.pbix)


### 7. Conclusion
Our project successfully demonstrates the comprehensive process of collecting, cleaning, analyzing, and visualizing global electricity data. By leveraging Python for data preprocessing, SQL for querying, and Power BI for interactive visualization, we have created a detailed and insightful overview of electricity trends, production, and access across different regions and income groups.

This project not only provides valuable insights into global electricity dynamics but also highlights the importance of data analysis and visualization in understanding and addressing energy-related challenges.

We hope our work serves as a valuable resource for stakeholders, policymakers, and researchers interested in exploring electricity data. Thank you for your interest in our project. We welcome any feedback or questions you may have.
