**What does `make_classification` do?**

**`make_classification`** is a function from the **scikit-learn (sklearn.datasets)** that generates a synthetic classification dataset. 

It allows for detailed control over the dataset structure, such as the number of features, informative/redundant/repeated features, class separation, noise level, and cluster distribution.

This is particularly useful for testing and benchmarking classification algorithms as we can create datasets with specific properties to evaluate model performance under controlled conditions.

<center>

| **Parameters** | **Description** |
| ------- | -----|
|  `n_samples=300` | Generates **300 samples (rows)** in the dataset. Each sample belongs to a class (binary by default) |
| `n_features=50` | The dataset has **50 total features (columns). These include informative, redundant and repeated features. | 
| `n_informative=10` | **10 features** contain real, meaningful information that helps differentiate classes. These are **linearly combined** to create the target variable ( `y` ) | 
|`n_redundant=25` | **25 features** are generated as **linear combinations** of the informative features. These features do not add new information but are correlated with informative features. |
| `n_repeated=15` | **15 features** are **duplicates** of previous features (either informative or redundant). These do not add new information to the dataset |
| `n_clusters_per_class=5` | Each class is formed by **5 clusters** in feature space, meaning data points belonging to the same class are grouped into multiple sub-clusters. This increases complexity. |
| `flip_y=0.05` | **5% of labels are randomly flipped** to introduce some label noise.  This simulates real-world data, which often has mislabeled instances $\rightarrow$ making the classification problem more realistic. | 
| `class_sep=0.5` | Controls the **separability between classes**. A lower value (like **0.5**) makes classes overlap more or classes are close together, making classification harder. A higher value (e.g., 2.0) would create well-separated classes or makes classes more distinct. |
| `random_state=0` | Sets a random seed to ensure reproducibility. Using the same seed will always generate the same dataset. |  

</center>

---

**How the Generated Dataset Looks?**

$\quad X: A(n\_samples, n\_features) = A(300, 50)$ - **Numpy array where each row represents a sample with 50 features**.
$\quad Y: A(n\_samples,) = A(300,)$ - **Numpy array containing class labels (0 or 1)**.

---

**What happens internally?**
1. The function first generates **10 informative features**, which contribute to the class labels.
2. It then create **25 redundant features**, which are linear combinations of the **informative features**.
3. Next, **15 repeated features** are created by duplicating some existing features.
4. The function groups data into **5 clusters per class**, adding complexity.
5. Finally, it **randomly flips 5% of the labels** to simulate noisy real-word data.

--- 

**When use `make_classification`?**
- When testing different classification algorithms in a controlled environment.
- When analyzing feature importance and how redundant/repeated features affect performance.
- When experimenting with class separability and noise to evaluate model robustness. 


----

**What is `loguniform`?**

**`loguniform(a, b)`** is a distribution that samples values exponentially between `a` and `b`.

- Unlike a **uniform distribution**, which **gives equal weight to all values**, **`loguniform`** is useful when hyperparameters span multiple orders of magnitude.

- It **avoids biasing the search towards larger numbers** and ensures a balanced selection across different scales.

<center>

![Log uniform](https://www.mathworks.com/help/examples/stats/win64/ComputeAndPlotLoguniformDistributionPdfExample_01.png)

</center>

**Example:**

If use **`loguniform(1, 1000)`**, instead of selecting numbers linearly like **`[1, 100, 200, ... , 1000]`**, it samples values logarithmically, favoring lower and mid-range values like **`[1, 10, 100, 500, 1000]`**
