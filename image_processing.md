# Applications of Hilbert Space-Filling Curves to Image Processing

## Euclidean Distances of Flyback and Hilbert Matrices
These are heatmaps of the Euclidean difference between all pairs of cells in the Flyback-ordered and Hilbert-ordered matrices, along the Flyback and Hilbert paths. On the left, Euclidean distances for the conventionally numbered matrix. On the right, the Euclidean distance between all pairs following the sequence of the space-filling curve. That is, on the left are the Euclidean distances for standard row order, and on the right are the Euclidean distances between two cells on the Hilbert path.
![](images/hilbert_explainer_B_1.png)

From the above right, we can see that the distance along the Hilbert path is (somewhat) correlated with the Euclidean distance between two points.

Next, we will divide the Flyback distances by the Hilbert distances.

![](images/hilbert_explainer_B_2.png)

The mean value of the above ratio grid is higher than 1.0 (medium purple), but the median is just under, meaning that the Euclidean distance grid has more outliers. But really they're still very close. The maximum (white) is around 5.

## Cluster Size Distributions
Now, let's take a look at the sizes of these sampled clusters. We're going to map sequences of cells from Flyback to Hilbert order, and analyze the sizes of the resulting cell clusters. This dataset is a portrait of the locality of these 2-dimensional neighborhood samples.

![](images/hilbert_explainer_B_3.png)

Let's take this row-by-row sampling of an 8x8 grid when mapped to Hilbert space, and:
* calculate the centroid of the sample cluster
* calculate the Euclidean distance from each cell to the centroid.

First, a simple plot of these distances, with a grid for reference.

![](images/hilbert_explainer_B_4.png)

This is a scatter plot of the distances, with 2D information preserved.

![](images/hilbert_explainer_B_5.png)

Next, we're going to march through the 8x8 cube one cell at a time, and collect the same measurements. That is, we're going to march a row of cells through the matrix in Flyback order, capture the positions of those cells in the Hilbert version of the matrix, and take the distance from the centroid of all 63 row-length. (Here are 6 examples of the 63 possible rows and their corresponding clusters. Black/dark blue squares are skipped)

![](images/hilbert_explainer_B_6.png)

Note that the row-wise walk of the matrix (above) always creates clustered neighborhoods, while the off-power-of-2 walk often generates larger, sparser neighborhoods.
As a result, the row-wise walk distances are limited to below 2.5, while the off-register walk distances range to 5.

![](images/hilbert_explainer_B_7.png)

Let's do a scatterplot of this larger dataset, and since the data has lot more variation, we will also also a KDE (kernel density estimation) plot. The scatterplot is good for seeing the structure of outliers, while the KDE plot is a portrait of the main structure.

![](images/hilbert_explainer_B_8.png)

![](images/hilbert_explainer_B_9.png)

## Appendix: More on space-filling curves
There are many kinds of space-filling curve.
Empirical research has shown that the Hilbert curve has the best locality. Here are two such investigations:

[Analysis_of_the_Clustering_Properties_of_Hilbert_Space-filling_Curve](https://www.researchgate.net/publication/3296936_Analysis_of_the_Clustering_Properties_of_Hilbert_Space-filling_Curve)

[The Performance of Space-Filling Curves for Dimension Reduction](https://people.csail.mit.edu/jaffer/CNS/PSFCDR)

These images were all generated in a Colab notebook.

[Colab](https://colab.research.google.com/github/LanceNorskog/deep-scurve/blob/master/notebooks/Hilbert_Mapping_in_Image_Processing.ipynb)
[github](https://github.com/LanceNorskog/deep-scurve/blob/master/notebooks/Hilbert_Mapping_in_Image_Processing.ipynb)
