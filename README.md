# STC TV Data Analysis Project

## Task 1 – User Behavior Analysis

1. Introduction

This project aims to analyze user behavior on the Jawwy TV platform to understand:
 • The most-watched programs.
 • Viewing distribution by video quality (HD / SD).
 • User experience relationship by Program Class (Film / Series).

⸻

2. Dataset
 • File used: stc- Jawwy TV Data Set_T1.xlsb
 • Key columns:
 • program_name → Name of the program
 • program_class → Film or Series/Episodes
 • user_id_maped → User ID
 • duration_seconds → Viewing duration in seconds
 • season, episode → For Series episodes
 • hd → 1 = HD, 0 = SD

⸻

3. Data Preprocessing
 • Drop unnecessary columns (e.g., Column1) safely if exists.
 • Trim program names to remove extra spaces.
 • Convert data types:
 • Numeric columns: duration_seconds, season, episode
 • String columns: user_id_maped, program_name, program_class etc.
 • Convert dates from Excel serial to datetime format.

⸻

4. Analysis Performed

4.1 Most Watched Programs
 • Programs aggregated by program_name and program_class.
 • For Series, episode and season numbers concatenated to distinguish episodes.
 • Metrics calculated:
 • Number of unique users
 • Total number of watches
 • Total watch time in hours
 • Top programs sorted by total watch time, then number of watches, then number of users.
 • Visualizations:
 • Pie chart of Top 10 programs by total watch time.

4.2 User Experience by Program Class
 • Aggregated metrics by program_class:
 • Number of unique users
 • Number of watches
 • Total watch time in hours
 • Visualizations:
 • Pie chart for total watch time by Program Class
 • Pie chart for total users by Program Class

4.3 HD vs SD Analysis
 • Overall comparison:
 • Number of users watching HD vs SD
 • Number of watches HD vs SD
 • Total watch time HD vs SD
 • Comparison by Program Class:
 • Same metrics, split by Film and Series
 • Visualizations:
 • Pie chart for overall watch time by quality
 • Grouped Bar chart for watch time per Program Class and quality (HD vs SD)

⸻

5. Tools & Libraries
 • Python 3.x
 • Pandas → for data manipulation
 • NumPy → for numerical operations
 • Plotly → for interactive visualizations
 • pyxlsb → to read .xlsb files in Python

⸻

6. How to Run
 1. Open the Notebook in Google Colab or Jupyter.
 2. Upload the dataset (stc- Jawwy TV Data Set_T1.xlsb).
 3. Run cells sequentially:
 • Install libraries
 • Preprocessing
 • Analysis & visualizations
 4. Visualizations are interactive in Colab using Plotly.

⸻

7. Outputs
 • DataFrames containing:
 • Top programs and metrics
 • Program Class aggregation
 • HD vs SD comparison
 • Interactive charts:
 • Pie charts for overall watch time and user distribution
 • Bar charts for Program Class vs quality

⸻

8. Notes
 • All preprocessing is done safely using copies to preserve the original data.
 • Dates converted correctly from Excel serial numbers.
 • HD/SD analysis is based on hd column: 1 = HD, 0 = SD.

## Task 2 – Watch Time Forecasting

Overview

This project analyzes daily TV watch time data and builds a predictive model to forecast the expected watch time for the next two months. The dataset contains:
 • A serial number column (used as index)
 • A date column (date_)
 • Daily watch time in hours (Total_watch_time_in_houres)

⸻

Steps Performed
 1. Data Loading & Exploration
 • Loaded the dataset from Excel using pandas.
 • Explored the dataset using .head(), .shape(), and .describe() to understand the distribution of watch time.
 2. Data Visualization
 • Plotted the daily watch time using Plotly Line Chart to visualize trends.
 • Optional: Scatter plots can be used to identify outliers or anomalies in daily watch time.
 3. Forecasting
 • Prepared the dataset for time series forecasting (ds for date, y for watch time).
 • Built a forecast model using Prophet to predict the next 60 days (approx. two months).
 • Visualized forecasted watch time with confidence intervals.
 • Created a table displaying predicted watch time along with lower and upper confidence bounds.
 4. Focus on Predictions
 • Filtered the forecast to show only the two-month prediction period for clear reporting.
 • This allows stakeholders to focus on upcoming trends without confusion from historical data.

⸻

Key Points
 • The data is continuous (watch time can have fractional hours), not discrete.
 • Line charts are used for trend visualization; pie charts are not suitable for time series.
 • ARIMA or Prophet models are recommended for time series forecasting rather than clustering (K-means) or classification methods (Decision Tree, KNN).

⸻

Libraries Used
 • pandas & numpy – Data manipulation
 • matplotlib & plotly – Data visualization
 • prophet – Time series forecasting

⸻

Next Steps
 • Further fine-tune the Prophet model with weekly or monthly seasonality if longer-term predictions are needed.
 • Add more features (e.g., day of week, holidays) to improve forecast accuracy.
 • Integrate interactive dashboards for real-time monitoring.
 
## Task 3 – Recommendation System

1. Introduction

This project builds a user-based recommendation system using the STC TV dataset.
The goal is to suggest new programs to users based on their viewing ratings and similarity to other users.
By applying cosine similarity, the system identifies users with similar tastes and recommends top programs they haven’t watched yet.

⸻

2. Dataset
 • File used: stc TV Data Set_T3.xlsx
 • Key columns:
 • user_id_maped → Unique user identifier
 • program_name → Name of the program watched
 • rating → User rating for the program
 • date_ → Viewing date (converted to datetime format)

⸻

3. Data Preprocessing
 • Loaded the dataset using pandas and checked basic info: .shape, .head(), .describe().
 • Converted the date_ column to datetime type.
 • Verified missing values using .isnull().any().
 • Created a user–program rating matrix using pivot_table().
 • Filled missing ratings with 0 for similarity calculations.

⸻

4. Recommendation Logic

4.1 Similarity Computation
 • Used cosine similarity from sklearn.metrics.pairwise to measure similarity between users based on their program ratings.

4.2 Recommendation Function
 • Implemented recommend_programs_fast(user_id, user_program_matrix, user_similarity, top_n=5) which:
 • Finds users most similar to the target user.
 • Computes weighted average ratings of unseen programs.
 • Returns the top 5 recommended programs for that user.

4.3 Example Case
 • Selected users who watched “Moana” and generated top recommendations for one of them.

⸻

5. Visualization
 • Used Plotly Express to visualize the top 5 recommended programs.
 • Created a bar chart showing program names on the X-axis and recommendation strength on the Y-axis.
 • Labels displayed directly above bars for readability.

⸻

6. Tools & Libraries
 • Python 3.x
 • pandas → Data loading and transformation
 • numpy → Numerical operations
 • scikit-learn → Cosine similarity computation
 • plotly → Interactive bar chart visualization
 • pyxlsb → Read binary Excel files (if needed)

⸻

7. How to Run
 1. Open the script in Google Colab or Jupyter Notebook.
 2. Upload the dataset file (stc TV Data Set_T3.xlsx).
 3. Run the script sequentially:
 • Install dependencies
 • Preprocess data
 • Generate similarity matrix
 • Run the recommend_programs_fast() function
 • Display visualizations
 4. The output bar chart will appear interactively in Colab.

⸻

8. Outputs
 • User–program rating matrix (user_program_matrix_filled)
 • Cosine similarity matrix (user_similarity)
 • Recommended programs for a given user (recommended_series)
 • Interactive Plotly bar chart:
 • Top 5 recommended programs
 • Readable labels and angled X-axis for clarity

⸻

9. Notes
 • The recommender is user-based, not content-based.
 • Recommendations depend heavily on available ratings — sparse data may reduce accuracy.
 • Future enhancements can include:
 • Program-based similarity (Item-based CF)
 • Hybrid models combining both user and item similarities
 • Integration with watch history weights or recency factors
