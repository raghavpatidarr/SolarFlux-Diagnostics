# SolarFlux-Diagnostics

## 💡 Project Overview
This repository documents a complete data science pipeline from exploratory analysis to machine learning classification to assess the operational health of solar power generation channels. The assignment required three core phases:
1. Exploratory Data Analysis (EDA): Analyze feature relationships (e.g., Power vs. Sunlight, Current, and Voltage) to derive key physical insights.
2. Anomaly Detection: Visualize daily generation curves to identify and flag operational anomalies like flat-lines or sudden power drops.
3. Channel Classification: Build a robust Machine Learning Classification Model to use time-series telemetry data and categorize each channel's operational state as 'Excellent,' 'Good,' or 'Poor.'

---

## 🎯 Goal and Classification Criteria

The primary objective is to build a robust model to categorize the operational status of each energy channel based on its average performance metric.

| Raw Performance | Performance Category |
| :--- | :--- |
| **$> 80$** | **Excellent** |
| **$60 \le \text{performance} < 80$** | **Good** |
| **$< 60$** | **Poor** |

---

## 🛠️ Setup and Installation

### Dependencies

The following Python libraries are required: `pandas`, `numpy`, `matplotlib`, `seaborn`, and `scikit-learn`.

## Install via `pip`

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```


## Running the Code
1. Clone the repository and open the SolarFlux_Diagnostics.ipynb notebook.
2. Upload Data: Ensure you have your input data (a CSV file containing the time, channel, current, voltage, power, sunlight, and performance columns) uploaded to the environment.
3. Execute all cells sequentially to perform the full pipeline from EDA to classification.
4. ** Note ** : All the plots for 28 channels are being saved into each individual folders for easy access ( plz open respective files to see all the visualizations)

## 🔍 Data Analysis and Insights
The core of this project lies in Exploratory Data Analysis (EDA) to understand the relationships between key variables before building the predictive model.

1. EDA Phase: Feature Correlation
We focused on two key correlation studies, visualized using a Heatmap and Regplots.

     A. Power vs. Sunlight
   
     Finding: The correlation coefficient between power and sunlight was found to be closer to 1.
   
     Visualization: The Regplot showed a strong, linear relationship, confirming that sunlight is positively correlated to power. As sunlight increases, power generation increases, as expected.

     B. Power, Current, and Voltage Relationship
     Analysis of the electrical parameters revealed critical insights:

     Current is the Primary Driver of Power: The correlation between Power and Current was an almost perfect 1.00. This confirms that for this dataset, the total power output is almost perfectly determined by the current. This is the most significant finding.

     Voltage's Lesser Role: The correlations involving Voltage (e.g., Power/Voltage and Current/Voltage) were significantly lower, around 0.65. This indicates that Voltage is the more stable variable and only has a moderate impact on power, while current has an almost absolute impact.

     All Positive Relationships: The color scale of the heatmap confirmed that all relationships are positive, meaning the variables move in the same direction.

3. Anomaly Detection Phase
We implemented a step to visualize the daily power generation curve for each channel and identify anomalies.
The logic primarily focused on detecting flat-lines or sudden drops by comparing the power output to the maximum (MAX) expected generation for a given time window.

4. Classification Phase (The Crucial Fix)
The goal was to categorize each channel using the final performance metric: Excellent (> 80), Good (60-80), or Poor (< 60).

     Initial Failure: The initial attempt failed because the classification was based on the overall average performance/power. Including the zero-power nighttime hours (which are non-generating hours) significantly dragged the average down, resulting in every channel incorrectly being marked as "Poor".

     The Fix: The approach was corrected to calculate the daytime-only average performance/power. By filtering the data to exclude non-generation periods (i.e., when sunlight and power are zero), we obtained appropriate, representative results, allowing for accurate categorization of the channels.
