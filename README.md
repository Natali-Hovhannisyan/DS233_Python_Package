# myclustering package


## Description and Features

The MyClustering package is a Python library that provides implementations of various clustering algorithms, including K-means. It also includes utilities for visualizing clustering results and performing dimensionality reduction using PCA. The package aims to simplify the process of clustering and provide tools for analyzing and interpreting clustering results.

Key features of the myclustering package include:

- K-means clustering algorithm
- Silhouette score calculation and elbow method visualization
- PCA for dimensionality reduction
- Visualization of clustering results using scatter plots

## Installation

To install the myclustering package, you can use pip:

```bash
pip install myclustering
```

## Usage Examples

Here are some examples of how to use the myclustering package:

### K-means Clustering

```python
import numpy as np
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt
from myclustering.kmeans.kmeans import KMeans

X, y = make_blobs(centers=3, n_samples=500, n_features=2, shuffle=True, random_state=40)
print(X.shape)
    
clusters = len(np.unique(y))
print(clusters)
k = KMeans(K=clusters, max_iters=150, plot_steps=False)
y_pred = k.fit(X)

k.plot()

```
You can identify the best number of cluster for K-means by looking at the silhouette score and elbow method
visualization.

```python
from myclustering.kmeans.silhouette import silhouette_score
from myclustering.kmeans.elbow import elbow_method 

silhouette_score(X,k)
elbow_method(X)
```
### PCA for dimensionality reduction

```python
from sklearn import datasets
import matplotlib.pyplot as plt
import numpy as np
from myclustering.pca.pca import PCA


data = datasets.load_iris()
X = data.data
y = data.target

# Project the data onto the 2 primary principal components
pca = PCA(2)
pca.fit(X)
X_projected = pca.transform(X)

print('Shape of X:', X.shape)
print('Shape of transformed X:', X_projected.shape)

x1 = X_projected[:, 0]
x2 = X_projected[:, 1]

plt.scatter(x1, x2,
        c=y, edgecolor='none', alpha=0.8,
        cmap=plt.cm.get_cmap('viridis', 3))

plt.xlabel('Principal Component 1')
plt.ylabel('Principal Component 2')
plt.colorbar()
plt.show()
```
### DBSCAN visualization with the help of PCA

You can also visalize the results of your DBSCAN algorithm and identify the outliers in you data.

```python
from myclustering.dbscan.visualization import plot_dbscan_pca
plot_dbscan_pca(X, epsilon = 0.3, min_points = 5)
```
## Customer segmentation

One of the common applications of clustering is customer segmentation, where customers are grouped into distinct segments based on their behavior, preferences, or characteristics. The MyClustering package can be used for customer segmentation tasks.

Here's an example of how the myclustering package can be used for customer segmentation:

```python
import pandas as pd
from myclustering.kmeans.kmeans import KMeans
from myclustering.pca.pca import PCA

# Load customer data
data = pd.read_csv('customer_data.csv')

# Preprocess the data (e.g., remove missing values, scale features)

# Apply PCA for dimensionality reduction
pca = PCA(n_components=2)
pca.fit(data)
X_pca = pca.transform(data)

# Apply K-means clustering
kmeans = KMeans(K=3, max_iters=150, plot_steps=False)
kmeans.fit(data)

# Analyze the clustering results
# (e.g., visualize clusters, identify key features for each cluster)
kmeans.plot()

# Interpret and use the customer segments for targeted marketing, personalized recommendations, etc.
```
## Contributing

Contributions to the MyClustering package are welcome! If you find any issues, have suggestions for improvements, or would like to add new features, feel free to open an issue or submit a pull request on the GitHub repository.

## License

The myclustering package is licensed under the MIT License. See the [MIT](https://opensource.org/license/mit/) for more information.


Credits
-------

This package was created with Cookiecutter_ and the `audreyr/cookiecutter-pypackage`_ project template.

.. _Cookiecutter: https://github.com/audreyr/cookiecutter
.. _`audreyr/cookiecutter-pypackage`: https://github.com/audreyr/cookiecutter-pypackage
