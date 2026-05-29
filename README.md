# Brazil Real Estate Market Insights & Pipeline Optimization

An end-to-end exploratory data analysis (EDA) and data cleaning pipeline that processes and analyzes real estate sales and rental listings across Brazil using the Properati dataset. 

This project is explicitly engineered to handle large-scale data processing smoothly on **Google Colab's free tier**, incorporating advanced memory management principles to prevent system crashes while maintaining maximum data utility.

## 🚀 Key Features

* **Advanced Outlier Mitigation Engine**: 
  * Identifies and drops cross-listed international anomalies (e.g., properties in Miami or Orlando incorrectly grouped into Brazilian metrics).
  * Automatically filters out real estate agent placeholder entries (such as dummy values where price is $\$0$ or property sizes are listed as $\le 10\text{ m}^2$) to ensure true statistical representation.
* **Free-Tier Memory Optimization**: Cuts memory footprint by over $50\%$ to run comfortably under Colab's $\approx 12\text{ GB}$ RAM limit. Implemented via:
  * Upfront numeric downcasting (converting bulky `float64` and `int64` types into lightweight `float32`).
  * Instant variable deletion (`del`) of heavy intermediate data copies.
  * Active garbage collection invocations (`gc.collect()`) after intensive transformations.
* **Geospatial & Statistical Visualization Engine**: 
  * **Interactive Geospatial Density Map**: A custom Plotly Mapbox scatter map that segments properties by market category (Rent vs. Sell) across geographic coordinates.
  * **Before-vs-After Diagnostic Panels**: Uses Matplotlib boxplots and scatter plots to actively demonstrate how filtering 95th percentile limits and removing dummy micro-values unlocks clean, interpretable data distributions.
  * **Aggregated Market Trends**: Generates highly legible bar charts showing average valuation by state and room distribution, featuring clean numeric formatting labels (e.g., $\$1.5\text{M}$, $\$250\text{K}$).

## 🛠️ Tech Stack & Libraries
* **Language**: Python 3
* **Data Manipulation**: Pandas, NumPy
* **Visualization**: Matplotlib, Plotly Express
* **Data Sourcing**: data.world Python SDK & REST API streaming
* **System Utilities**: `gc` (Garbage Collector), `io`, `os`

## 📊 Pipeline Architecture

1. **Secure Authentication**: Connects safely to data.world using the Google Colab Secrets Manager (`DATAWORLD_API_TOKEN`).
2. **Streamed Ingestion**: Queries rental tables directly via the SDK and streams zipped sales records through a REST API connection to optimize local disk utilization.
3. **Feature Extraction**: Parses geographic coordinates from raw geometric data string formats and extracts state tokens safely.
4. **RAM Scrubbing**: Filters outliers, executes matrix type downcasting, slices a lightweight geographical dataframe for mapping, and purges parent data assets from memory.
5. **Insights Distribution**: Renders descriptive analytics tables alongside static and interactive graphic outputs.

## 📈 Visual Highlights
* **Outlier Visualizations**: Scatter charts are strictly filtered to remove unrealistic clusters hugging the $0$ boundaries (like $1\text{ m}^2$ or $2\text{ m}^2$ entries), revealing the authentic correlation between property area and pricing.
* **State & Room Analysis**: Pricing scales are automatically adjusted dynamically to display clean, professional currency abbreviations instead of unreadable scientific notation (e.g., `1.5e+06`).

## 💡 How to Run on Google Colab
1. Clone this repository or download the `.ipynb` file.
2. Upload the notebook to your Google Drive and open it via Google Colab.
3. Add your data.world token inside Colab's **Secrets (the 🔑 icon)** panel on the left sidebar with the name `DATAWORLD_API_TOKEN`.
4. Turn on "Notebook access" for the secret.
5. Run the cells sequentially from top to bottom.
