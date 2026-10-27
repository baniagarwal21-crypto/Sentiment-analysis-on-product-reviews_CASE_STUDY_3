E-Commerce Customer Segmentation using RFM
A machine-learning case study that segments e-commerce customers based on their purchasing behaviour using RFM analysis, K-Means, and DBSCAN. It uses PCA and t-SNE to visualize customer groups and maps the resulting K-Means and DBSCAN segments to suggested marketing actions.
Project Overview
Businesses can use customer segmentation to understand which customers purchase frequently, spend more, have purchased recently, or may need re-engagement. This notebook converts transaction-level data into customer-level features and applies unsupervised learning to discover groups with similar behaviour.
Objectives
- Download and explore an online retail transaction dataset.
- Clean transaction data and calculate total line-item value.
- Build Recency, Frequency, and Monetary (RFM) features for each customer.
- Scale the features and compare clustering approaches.
- Visualize clusters using PCA and t-SNE.
- Assign descriptive customer personas and example marketing actions.
- Compare K-Means and DBSCAN cluster counts and DBSCAN noise points.
Techniques Used
- RFM analysis: Recency measures how recently a customer purchased; Frequency counts distinct invoices; Monetary sums transaction value.
- K-Means: partitions customers into a chosen number of clusters. The notebook evaluates values of k from 2 to 8 using inertia and silhouette score, then fits a 4-cluster model.
- DBSCAN: groups points in dense regions and labels points that do not belong to a dense group as noise (-1). Its result depends on eps and min_samples.
- PCA: reduces the three scaled RFM features to two dimensions for a cluster plot.
- t-SNE: creates a two-dimensional visualization of a sample of customers. It is for visualization, not a clustering algorithm.
- StandardScaler and log1p: log transformation reduces skew in positive-valued features; standardization puts features on comparable scales.
Dataset
The notebook downloads the carrie1/ecommerce-data dataset using kagglehub. The CSV is read with ISO-8859-1 encoding. The expected columns include InvoiceNo, InvoiceDate, CustomerID, Quantity, and UnitPrice.

The dataset is downloaded at runtime, so it is not necessary to commit the CSV to this repository. Review the dataset's Kaggle page and its terms before redistributing the data.
Workflow
1. Install and import Python libraries.
2. Download the dataset and load its CSV.
3. Inspect shape, columns, data types, summary statistics, and missing values.
4. Clean records: convert data types, remove rows missing required fields, exclude cancellation invoices, keep positive quantities and unit prices, remove duplicates, and calculate TotalPrice = Quantity × UnitPrice.
5. Aggregate transactions by customer to calculate RFM values. The reference date is one day after the latest invoice date in the cleaned data.
6. Apply log1p and StandardScaler to RFM features.
7. Evaluate K-Means cluster counts from 2 to 8, then assign customers to four clusters.
8. Summarize clusters and visualize them using PCA.
9. Run DBSCAN and visualize its clusters/noise using PCA.
10. Run t-SNE on a reproducible sample of up to 1,500 customers and plot both sets of labels.
11. Assign rule-based personas and suggested marketing actions, then compare the clustering methods.
Requirements
- Python 3.10+ (a compatible version supported by the installed packages)
- Jupyter Notebook or Google Colab
- Internet access for downloading the dataset
Libraries: kagglehub, pandas, numpy, matplotlib, seaborn, and scikit-learn.
How to Run
Option 1: Google Colab
1. Upload BaniAgarwal_202501100300082_CSE_AI_SEC_B.ipynb to Google Colab.
2. Run the notebook cells from top to bottom.
3. Allow the first cell to install dependencies and the dataset-download cell to fetch the data.
Option 2: Local Jupyter
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

python -m pip install kagglehub pandas numpy matplotlib seaborn scikit-learn jupyter
jupyter notebook
Open the notebook and run all cells in order. If the dataset download requires Kaggle authentication or configuration in your environment, follow kagglehub's current instructions.
Outputs
The notebook produces:
- Dataset quality and shape checks.
- RFM feature table and descriptive statistics.
- RFM distribution histograms.
- Elbow and silhouette plots for K-Means model selection.
- K-Means cluster sizes and customer-level averages.
- PCA plots for K-Means and DBSCAN.
- t-SNE plots coloured by K-Means and DBSCAN labels.
- Persona summaries with example marketing actions.
- A final comparison of cluster counts and DBSCAN noise customers.
Important Interpretation Notes
- Cluster IDs such as 0, 1, 2, and 3 are arbitrary labels; they do not inherently mean “best” or “worst.”
- The notebook fixes K-Means to four clusters after plotting model-selection metrics. Check the plots before treating four as the optimal choice.
- DBSCAN's eps=0.7 and min_samples=10 are chosen parameters, not guaranteed optimal values.
- PCA and t-SNE plots are projections; apparent visual separation does not by itself prove business value.
- Customer personas are assigned with median-based rules to cluster averages. They are heuristic labels, not trained predictions or validated customer categories.
- The dataset is historical, and campaign suggestions are illustrative. Validate any real marketing decisions against current business data and privacy requirements.
Repository Structure
.
├── BaniAgarwal_202501100300082_CSE_AI_SEC_B.ipynb
└── README.md
Future Improvements
- Add formal cluster validation and compare multiple values of eps for DBSCAN.
- Investigate outliers and the effects of cancelled invoices and returns.
- Add a clearer mapping from cluster profiles to personas at the customer level.
- Export the cleaned RFM table and cluster assignments.
- Add screenshots of plots and a concise results section with measured outputs from a completed notebook run.
License and Data
Add a license if you want others to reuse your code. Check the dataset owner's license/terms separately; a repository license for your code does not automatically license the dataset.
