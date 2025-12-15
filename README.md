Project: Avatar: Fire and Ash - Box Office Prediction
Overview
This Jupyter Notebook contains a machine learning pipeline designed to predict the opening week box office performance of the movie Avatar: Fire and Ash.

The project evolves through two main phases:

Phase 1 (Global Estimation): Uses a synthetic "workaround" strategy to estimate opening weeks from lifetime gross data.

Phase 2 (Domestic Precision): Implements a web scraper to fetch real-world "Domestic Opening" data from Box Office Mojo, merges it with production metadata, and retrains the models for higher accuracy.

Dependencies
pandas (Data manipulation)

numpy (Numerical operations)

matplotlib & seaborn (Data visualization)

sklearn (Random Forest, Grid Search, Preprocessing)

lightgbm (Gradient Boosting)

beautifulsoup4 & requests (Web scraping)

Notebook Workflow
1. Data Loading & Synthetic Labeling (Phase 1)
Goal: Create a training dataset from movies.csv (which contained only lifetime revenue).

Logic: Applied a heuristic function to estimate opening revenue:

Standard Blockbusters: Assumed ~35% of lifetime gross.

James Cameron Movies: Assumed ~13% of lifetime gross (due to historical "long legs").

2. Feature Engineering
Preprocessing:

Parsed genre strings (e.g., "['Action', 'Sci-Fi']") into Python lists.

Applied One-Hot Encoding using MultiLabelBinarizer to convert genres into numerical features.

Features Used: Budget, Genres.

3. Model Training & Comparison
Algorithms: Trained two regressors to compare performance:

Random Forest Regressor: A robust bagging ensemble.

LightGBM Regressor: A high-performance gradient boosting framework.

Validation: Compared predictions for Avatar: Fire and Ash side-by-side.

4. Visualizations
Prediction Bar Chart: Visualized the dollar-amount gap between the two models.

Feature Importance: Plotted which features (Budget vs. Specific Genres) drove the decision-making process for each algorithm.

5. Real-World Data Scraping (Phase 2)
Tool: Custom web scraper using requests and pd.read_html.

Source: Box Office Mojo - All Time Domestic Openings.

Process:

Scraped the table to get real "Opening Weekend" and "Total Gross" figures.

Cleaned currency formatting (removed $ and ,).

Saved to domestic_openings.csv.

6. Data Merging
Merged the original metadata (movies.csv) with the scraped targets (domestic_openings.csv) using an Inner Join on clean movie titles.

Resulted in a high-quality dataset (training_data_final.csv) with verified ground-truth targets.

7. Optimization & Final Prediction
Cross-Validation: Ran 5-Fold Cross-Validation (MAE) to determine the most stable model.

Hyperparameter Tuning: Used GridSearchCV to optimize settings (e.g., n_estimators, learning_rate) for the winning algorithm.

Result: Generated a final, scientifically rigorous prediction for the domestic opening of Avatar: Fire and Ash.
