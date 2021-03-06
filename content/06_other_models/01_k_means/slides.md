---

marp: true

---

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>

# k-means

<!--
k-means clustering is an unsupervised machine learning algorithm that can be used to group items into clusters.

So far we have only worked with supervised algorithms. Supervised algorithms have training data with labels that identify the numeric value or class for each item. These algorithms train on labeled data to build a model that can be used to make predictions.

k-means clustering is different. The training data is not labeled. Unlabeled training data is fed into the model, which attempts to find relationships in the data and create clusters based on those relationships. Once these clusters are formed, predictions can be made about which cluster new data items belong to.

k-means is the most common clustering algorithm. You performed a k-means clustering during the screw/fastener exercise.

To bring this topic to life more, let's relate k-means back to what you did in the screw/fastener exercise.
-->

---

# k-means Mathematics
## Clustering Activity Review

All of the different fasteners == Your dataset: `(X1, X2, ..,  XN)`

Making different numbers of piles == Making clusters (`S1, S2, ..., SK)`

"Minimizing differences" == Minimizing variances (within-cluster sum of squares)

<!--
The pile of screws and other fasteners on your desk made up your dataset. You can think of labeling each screw as x_{1}, x_{2}, ... x_{n}. So the total number of items in your pile was n.

When you were asked to make 2, 4, or 6 clusters, this played the role of k. This is a hyperparameter of the model.

Finally, you tried to create clusters with "similar" items. That is, they shared some traits. You may have chosen a distance metric based on color (dark screw in one cluster, chrome screw in another, etc.) or based on shape (1-inch screws in one cluster, 2-inch screws in another, etc.). These choices played the role of your distance metric. When grouping similar items, you were attempting to minimize the variance within each cluster.

-->

---

# k-means Mathematics
## Within-cluster sum of squares

![center](res/kmeans02b.png)

<!--
More formally, this is the actual mathematical formula for minimizing the variance within each cluster.

$ arg\, \underset{s}min   \sum_{i=1}^{k} \sum_{x \in S_i} || X - \mu_i ||^2 $

* Image name: res/kmeans02b.png
  * Repo link: https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans02b.png
  * Source https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans02b.png by Author Google LLC under License Copyright [2020] Google LLC.
-->

---

# k-means Algorithm
## k Randomly generated points are generated

![center](res/kmeans03.png)
<!--
Let's take a closer look at each step in the k-means algorithm.

We choose our hyperparameter k (i.e., the number of clusters). In this case, k = 3. Then three points are randomly generated within the data. These are our initial "means" often called "centroids."


* Image name: res/kmeans03.png
  * Repo link: https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans03.png
  * Source https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans03.png by Author Google LLC under License Copyright [2020] Google LLC.
-->

---

# k-means Algorithm
## Clusters are created based on proximity to the points

![center](res/kmeans04.png)

<!--
Now, clusters are created around each of those three means. Every data point is put into a cluster based on which of the three centroids it's closest to, where close is defined by our distance metric. In this problem the distance metric is just Euclidean distance in the plane.


* Image name: res/kmeans04.png
  * Repo link: https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans04.png
  * Source https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans04.png by Author Google LLC under License Copyright [2020] Google LLC.
-->

---

# k-means Algorithm
## The centroid of the custer is determined
![center](res/kmeans05.png)

<!--
We now have three clusters. But if we just stopped here, then the model wouldn't be a "learning algorithm." The task now is to iteratively refine the model.

We compute the arithmetic mean of each of the three clusters.

* Image name: res/kmeans05.png
  * Repo link: https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans05.png
  * Source https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans05.png by Author Google LLC under License Copyright [2020] Google LLC.
-->

---

# k-means Algorithm
## The arithmetic means become the new centroids
![center](res/kmeans06.png)

<!--
The arithmetic means become the new centroids.

* Image name: res/kmeans06.png
  * Repo link: https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans06.png
  * Source https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans06.png by Author Google LLC under License Copyright [2020] Google LLC.
-->
---

# k-means Algorithm
## Data is reassigned to clusters
![center](res/kmeans07.png)

<!--
Again, every data point is put into a cluster based on which of the three centroids it's closest to.

* Image name: res/kmeans07.png
  * Repo link: https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans07.png
  * Source https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans07.png by Author Google LLC under License Copyright [2020] Google LLC.
-->

---

# k-means Algorithm
## Repeat until the clusters have stabilized

![center](res/kmeans08.png)

<!--
We repeat steps two and three, recalculating the centroids and re-clustering around those centroids, until convergence is reached. Convergence is typically measured by very little or no change in the centroids. In other words, the assignment of data points to clusters is not changing with more iterations.

* Image name: res/kmeans08.png
  * Repo link: https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans08.png
  * Source https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/kmeans08.png by Author Google LLC under License Copyright [2020] Google LLC.
-->

---

# Lab

Clustering mushrooms to determine whether they're edible or poisonous.

![center](res/mushrooms.jpg)

<!--
It can often be difficult to identify whether mushrooms are of an edible or poisonous species. Slight variations on a range of features (stalk size, cap color, odor, etc.) can mean the difference between a healthy snack and a mushroom of deadly toxicity. The University of California Irvine has a [dataset containing various attributes of mushrooms] (https://www.kaggle.com/uciml/mushroom-classification), including edibility.

In this lab we want to see if we can find clusters of mushroom attributes that can be used to determine if a mushroom is edible or not.

* Image name: res/mushrooms.jpg
  * Repo link: https://github.com/google/applied-machine-learning-intensive/tree/master/content/06_other_models/01_k_means/res/mushrooms.jpg
  * Source https://pixabay.com/photos/mushroom-mushrooms-agaric-3659165/ by Author Adege / Andreas https://pixabay.com/users/adege-4994132/ under License https://pixabay.com/service/license/.
-->

---

# Lab

```python
    from sklearn.cluster import KMeans

    model = KMeans(n_clusters=10)
```

<!--

There are many hyperparameters that we can set when using scikit-learn's k-means function. But n_clusters is the most important, as it denotes the number of clusters (i.e., centroids) we want.

You can see more details in scikit-learn's documentation.

https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html

-->
---

# Your Turn

<!--
Now let's explore the k-means lab.
-->
