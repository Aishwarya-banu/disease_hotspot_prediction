# US Disease Hotspot & Pollutant Dashboard

## 🌡️ Overview

This project is an interactive web application built with Streamlit for visualizing and analyzing disease hotspots across the United States, with an integrated layer of pollutant data. It allows users to explore disease hotspot predictions, track trends over time, and investigate potential correlations with various environmental pollutants at the county level.

The dashboard provides county-level insights, enabling users to filter data by year, state, and specific counties. It features an interactive map for geospatial analysis, trend charts, and detailed statistics for selected pollutants.

## ✨ Features

* **Interactive Hotspot Map:** Visualize disease hotspot prediction scores across US counties using an interactive map. Marker size and color intensity reflect hotspot status and prediction scores.
* **Dynamic Filtering:** Filter data by year, state, and select multiple counties for focused analysis.
* **Trend Analysis:** View trends in hotspot counts over several years for the selected geographical scope.
* **Pollutant Integration:**
    * Load and merge pollutant data with hotspot information.
    * Select specific pollutants from a dynamic list for detailed analysis.
    * View key statistics (min, max, mean, median, std. dev) for the selected pollutant.
    * Analyze pollutant distribution and average levels in hotspot vs. non-hotspot areas.
    * Explore potential correlations between pollutant levels and hotspot prediction scores via scatter plots.
    * Visualize average monthly trends for pollutants if monthly data is available.
* **Top County/State Analysis:** Identify top hotspot counties and states with the most hotspots for a given year.
* **Data Export:** Download the filtered dataset as a CSV file for offline analysis.
* **Responsive UI:** The dashboard is designed to be responsive and accessible on various screen sizes.

## 📊 Data Sources

The application utilizes two main CSV data files:

1.  **Hotspot Data (`all_years_gnn_predictions_semi_supervised.csv`):**
    * Contains information on disease hotspots, including year, state, county, latitude, longitude, a binary hotspot indicator, and a hotspot prediction score (expected as `Predicted_Hotspot_GNN`).
    * _Note: The application expects specific column names like 'Year', 'State Name', 'County Name', 'Predicted_Latitude', 'Longitude', 'Hotspot', and 'Predicted_Hotspot_GNN'. These are renamed internally to standardized names like 'State', 'County', etc._

2.  **Pollutant Data (`all_pollutants_merged_inner.csv`):**
    * Contains pollutant measurements for various US counties.
    * Expected to have a `Date Local` column from which the 'Year' is extracted.
    * Should contain 'State Name' and 'County Name' for merging with hotspot data.
    * Includes various pollutant measurement columns (e.g., `PM25`, `O3`, `NO2`, `SO2`, `CO`).
    * Can also include monthly pollutant data (e.g., `PM25_Jan`, `PM25_Feb`, etc.) which the app will attempt to parse for monthly trend analysis.

## ⚙️ Setup and Installation

To run this application locally, follow these steps:

1.  **Clone the Repository (if applicable):**
    ```bash
    git clone <your-repository-url>
    cd <your-repository-directory>
    ```

2.  **Create a Virtual Environment (Recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install Required Libraries:**
    The application primarily uses Streamlit, Pandas, and Plotly Express.
    ```bash
    pip install streamlit pandas plotly-express
    ```

4.  **Prepare Data Files:**
    * Ensure you have the two required CSV files:
        * `all_years_gnn_predictions_semi_supervised.csv` (for hotspot data)
        * `all_pollutants_merged_inner.csv` (for pollutant data)
    * Place these files in the same directory as the main Python script (e.g., `main.py`), or update the `HOTSPOT_DATA_PATH` and `POLLUTANT_DATA_PATH` constants at the beginning of the script with the correct file paths.

## 🚀 Running the Application

1.  Navigate to the directory containing the main Python script (e.g., `main.py`) and your data files.
2.  Run the Streamlit application from your terminal:
    ```bash
    streamlit run main.py
    ```
3.  Streamlit will open the application in your default web browser.

## 📈 Usage

* **Sidebar Filters:**
    * **Select Year:** Choose the year for which you want to view data.
    * **Select State:** Filter data by a specific US state or view data for "All States."
    * **Select Counties:** Further refine your analysis by selecting one or more counties within the chosen state and year.
    * **Select Pollutant for General Analysis:** If pollutant data is loaded, choose a specific pollutant from this dropdown to see its statistics and visualizations in the "Pollutant Analysis" tab and on the map hover.
* **Main Dashboard Tabs:**
    * **🗺️ Hotspot Intensity Map:** Displays an interactive map of US counties. The color intensity and size of markers indicate hotspot prediction scores and binary hotspot status. Hover over counties for more details, including the selected pollutant's value if available.
    * **📈 Trends & Predictions:** Shows line charts illustrating the trend of hotspot counts over the available years for the selected scope.
    * **🏆 Top Counties:** Presents bar charts of the top hotspot counties (based on prediction score or binary status) and states with the most hotspots for the selected year and scope.
    * **🏭 Pollutant Analysis (Conditional):** This tab appears if pollutant data is successfully loaded and a pollutant is selected in the sidebar.
        * **Key Statistics:** Displays a table with min, max, mean, median, and standard deviation for the selected pollutant within the filtered scope.
        * **Distribution:** Shows a histogram of the selected pollutant's values, colored by hotspot status.
        * **Average Levels:** A bar chart comparing average pollutant levels in hotspot vs. non-hotspot counties.
        * **Pollutant vs. Prediction Score:** A scatter plot to explore the relationship between the selected pollutant and hotspot prediction scores.
        * **Monthly Trends:** If monthly pollutant data (e.g., `PM25_Jan`, `PM25_Feb`) is detected in your pollutant CSV, you can select a "base pollutant" (e.g., PM25) to see its average monthly trend and identify the peak month.
    * **💾 Data View & Download:** Displays the filtered (and merged) data in a table and provides a button to download it as a CSV file.

## 🔮 Potential Future Enhancements

* More advanced statistical analysis options (e.g., correlation matrices, regression analysis).
* User-configurable thresholds for defining hotspots.
* Ability to compare multiple pollutants side-by-side.
* Integration of additional demographic or socio-economic data.
* Time-series forecasting for pollutant levels and hotspot occurrences.
* User accounts for saving preferences or analyses.
