# COVID-19-Data-Analysis
# This script performs a basic analysis of simulated COVID-19 data.
# It demonstrates skills in Python with libraries like pandas and matplotlib.

import pandas as pd
import matplotlib.pyplot as plt

def generate_sample_data():
    """Generates a sample DataFrame for COVID-19 cases and vaccinations."""
    data = {
        'region': ['North', 'South', 'East', 'West', 'North', 'South', 'East', 'West'],
        'date': pd.to_datetime(['2023-01-01', '2023-01-01', '2023-01-01', '2023-01-01',
                                '2023-02-01', '2023-02-01', '2023-02-01', '2023-02-01']),
        'cases': [15000, 25000, 10000, 18000, 12000, 22000, 9000, 16000],
        'vaccinations': [80000, 120000, 50000, 95000, 100000, 150000, 60000, 110000]
    }
    return pd.DataFrame(data)

def main():
    """Main function to perform analysis and generate visualizations."""
    # Step 1: Generate or load the dataset
    df = generate_sample_data()
    print("Simulated COVID-19 Data:")
    print(df.to_markdown(index=False))
    print("\n" + "="*50 + "\n")

    # Step 2: Perform data analysis
    # Calculate key metrics
    df['fatality_rate'] = (df['cases'] / (df['cases'] + df['vaccinations'])) * 100
    print("Analysis Results:")
    print(df[['region', 'fatality_rate']].to_markdown(index=False))
    print("\n" + "="*50 + "\n")

    # Group data by region to identify trends
    regional_summary = df.groupby('region')[['cases', 'vaccinations']].sum().reset_index()
    print("Regional Summary:")
    print(regional_summary.to_markdown(index=False))

    # Step 3: Create visualizations
    fig, axes = plt.subplots(1, 2, figsize=(14, 6))

    # Bar chart for total cases by region
    axes[0].bar(regional_summary['region'], regional_summary['cases'], color='skyblue')
    axes[0].set_title('Total Cases by Region')
    axes[0].set_xlabel('Region')
    axes[0].set_ylabel('Total Cases')

    # Bar chart for total vaccinations by region
    axes[1].bar(regional_summary['region'], regional_summary['vaccinations'], color='lightgreen')
    axes[1].set_title('Total Vaccinations by Region')
    axes[1].set_xlabel('Region')
    axes[1].set_ylabel('Total Vaccinations')

    plt.tight_layout()
    plt.show()

if __name__ == "__main__":
    main()
