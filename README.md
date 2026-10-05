# MSCS 634 - Lab 3: Clustering Analysis Using K-Means and K-Medoids Algorithms

## Purpose
This lab explores clustering on the Wine dataset from scikit-learn (178 wines, 13 chemical features, 3 true wine types). I applied K-Means and K-Medoids with k = 3, then compared them using visualizations and two metrics:
- **Silhouette Score:** how tight and well separated the clusters are (higher is better).
- **Adjusted Rand Index (ARI):** how well the clusters match the true wine types (1 = perfect, about 0 = random).

## Files
- `Lab3.ipynb` - the full notebook (data prep, K-Means, K-Medoids, plots, analysis)
- `README.md` - this file

## Results

| Method | Cluster sizes | Silhouette Score | ARI |
|---|---|---|---|
| K-Means | 65 / 51 / 62 | 0.285 | 0.897 |
| K-Medoids | 74 / 49 / 55 | 0.268 | 0.741 |

## Key Insights
- K-Means produced better-defined clusters and matched the real wine types much better (ARI 0.897 vs. 0.741).
- Both methods found nearly the same cluster in the upper left of the PCA plot. They differed in the border between the other two clusters, where K-Medoids shifted the boundary and assigned several middle wines differently.
- K-Means ARI is high, but the Silhouette Score is modest (0.285). The clusters match the real wine types well, but they overlap somewhat at the edges.
- K-Means centroids are averages and can fall between data points. K-Medoids centers are always real wines.
- K-Means is a good fit for clean, roughly round clusters. K-Medoids is better when the data has outliers or when the center needs to be a real example.

## Challenges and Decisions
- **Scaling:** Features have very different ranges (proline averages about 747, hue about 0.96), so I standardized all features with z-score normalization before clustering.
- **K-Medoids package:** `scikit-learn-extra` failed to install on my Windows machine because it needs the Microsoft C++ build tools. Instead of installing them, I implemented the PAM (Partitioning Around Medoids) algorithm myself with numpy.
- **Visualization:** The data has 13 dimensions, so I used PCA to reduce it to 2 dimensions for plotting only. The clustering used all 13 features.
- **Choice of k:** I used k = 3 because the dataset has 3 known wine types.
- **Reproducibility:** I set `random_state=42` so the results can be repeated.

## How to Run
1. Install: `pip install numpy pandas scikit-learn matplotlib`
2. Open the notebook in Jupyter and choose Restart & Run All.
