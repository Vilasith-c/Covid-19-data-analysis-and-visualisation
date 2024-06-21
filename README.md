# Covid-19-data-analysis-and-visualisation
This is a basic python project using python libraries (Pandas , Plotly.express)
import pandas as pd
import plotly.express as px

def load_data(file_path):
    # Load data from CSV file
    df = pd.read_csv(file_path)
    return df

def clean_data(df):
    # Clean data: convert data types and handle missing values
    numeric_columns = ['total_cases', 'total_deaths', 'total_tests_per_million', 'total_vaccines_per_thousand',
                       'total_boosters_per_thousand', 'tests_per_case', 'total_deaths_per_million',
                       'icu_patients_per_million', 'positive_rate', 'population', 'population_density',
                       'life_expectancy', 'stringency_index', 'human_development_index']
    df[numeric_columns] = df[numeric_columns].apply(pd.to_numeric, errors='coerce')
    df.dropna(inplace=True)
    return df

def plot_total_cases_by_continent(df):
    # Plot total cases by continent using Plotly
    fig = px.bar(df, x='continent', y='total_cases', title='Total COVID-19 Cases by Continent',
                 labels={'total_cases': 'Total Cases', 'continent': 'Continent'})
    fig.show()

def plot_vaccination_vs_life_expectancy(df):
    # Plot vaccination vs life expectancy using Plotly
    fig = px.scatter(df, x='total_vaccines_per_thousand', y='life_expectancy', color='continent', size='population',
                     hover_name='country', log_x=True, title='Vaccination vs Life Expectancy by Continent')
    fig.update_xaxes(title_text='Total Vaccines per Thousand People')
    fig.update_yaxes(title_text='Life Expectancy')
    fig.show()

def main():
    # Load data
    file_path = 'file_path.csv'  # Adjust the file path as per your directory structure
    df = load_data(file_path)

    # Clean data
    df = clean_data(df)

    # Plotting examples using Plotly
    plot_total_cases_by_continent(df)
    plot_vaccination_vs_life_expectancy(df)

if __name__ == "__main__":
    main()
