<p align="center"><strong><span style="font-size: 35px;">Hyperparameter Tuning</span></strong></p>

### **Grid Search**
**Grid Search** is a method of hyperparameter tuning that involves exhaustively searching through a predefined set of hyperparameter values. It systematically evaluates all possible combinations to find the optimal set of hyperparameters.

To perform **Grid Search**, we define a grid (a search space) containing specific values for each hyperparameter. The algorithm then trains and evaluates the model for every possible combination within this grid using a specified evaluation metric such as **accuracy** or **F1 score**.

Although **Grid Search** ensures a thorough exploration of the hyperparameter space, its main drawback is that it can be computationally expensive, especially when dealing with high-dimensional data and large search spaces. The number of evaluations grows exponentially with the number of hyperparameters, making it impractical in some cases.

$\Rightarrow$ As a result, so ideal when the search space is relatively small or when we have enough computational resources to evaluate all possible hyperparameter combinations. However, for larger search spaces, it may not be the most efficient approach.

**Pros**:
- Guarantees that the best hyperparameter combination (within the predefined gird) is found.
- Systematic and structured approach, ensuring full coverage of the search space

**Cons**:
- Computationally expensive, especially when dealing with multiple hyperparameters.
- May spend unnecessary time evaluating suboptimal hyperparameters instead of focusing on promising regions.

**When to use Grid Search**
- When the number of hyperparameters and their possible values are limited.
- When computational resources are sufficient to perform an exhaustive search.
- When precision is more important than efficiency, ensuring that the absolute best combination is found within the predefined grid.

-----

### **Random Search**
**Random Search** is a method of hyperparameter tuning to find optimal hyperparameter that involves randomly sampling a combination of hyperparameters which is used to control the training process from a predefined set (a search space) and training a model using those hyperparameter.

To perform **Random Search**, we need to define the set of possibles value for each hyperparameter and then instead of systematically testing all combinations (like Grid Search), Random Search selects a combination of these values at random.

The model is then trained and evaluate using a specified metric such as **accuracy** or **F1 score**. The process is repeated a predefined number of times, and the combination of hyperparameters that results in the best model performance is chosen as the optimal set.

It is particularly effective for high-dimensional data and is widely used in practice (But not now maybe : )). However, its main drawback is that it does not *utilize information* from **PREVIOUS TRIALS** to determine the next set of hyperparameters (not memorize) 

$\Rightarrow$ As a result, discovering the best hyperparameter with **Random Search** often relied on **LUCK** 🍀🍀🍀. While the selections are random **BUT THEY DO NOT CONSTITUTE A NAIVE SELECTION**. In fact, it functions as a statistical random sampling technique: The key idea is that by conducting a sufficient number of random trials, we increase the likelihood of finding optimal hyperparameters without excessively wasting computational resources.

**Pros**: 
- **Random Search** method is widely used due to its simplicity and ease of implementation.

**Cons**:
- Less systematic and may not be as effective at finding the optimal set of hyperparameters, particularly for larger and more complex models.


**When to use Random Search**
- When the search space is large and exhaustive search (like Grid Search) is computationally expensive
- When some hyperparameters are more impactful than others, as Random Search can still discover good configurations without testing every possibility
- When a simple yet effective approach is needed, especially as a baseline before exploring more complex tuning methods

----

### **Halving Search**

**Halving Search** (also called **Successive Halving**) is a hyperparameter tuning technique that efficiently finds the best hyperparameters by **gradually eliminating poor candidates** while allocating more computational resources to promising ones.

Traditional hyperparameter tuning methods like **Grid Search** and **Random Search** are very slow because they evaluate all hyperparameter combinations fully. This wastes time on bad hyperparameters.

Besides that, the common drawback of both is that they operate in an **uninformed** manner, meaning they do not take advantage of prior information during the search process. Suppose a few test runs reveal that certain hyperparamters do not significantly impact the results or that some value ranges are ineffective - this information **is not carried forward to subsequent searches**.

Because of this limitation, **Halving Search** was introduced, with **HalvingGridSearch** and **HalvingRandomSearch** being used to explore the parameter space by applying an experimental approach with successive halvings on **Grid Search** and **Random Search**.

**Halving Search speeds up the process** by:

👍 Starting with many configurations but using **limited resources** for each.
👍 **Eliminating bad performers early**, saving computational cost.
👍**Focusing resources on the best candidates** in later stages.

**How Halving Search Works?**

**Step 1: Define hyperparameter search space**

For example, we have a **Random Forest** model with several hyperparameter:

<center>

| Hyperparameter | Possible values | 
| --- | --- |
| **`n_estimators`** | `[10, 50, 100, 200, 500]` |
| **`max_depth`** | `[5, 10, 15, None]` | 
| **`min_samples_split`** | `[2, 5, 10]` |

</center>

These create a **search space** of hyperparameter combinations.

**Step 2: Choose initial candidates (N)**

Then randomly sample **N hyperparameter sets** from the search space. In this case, let's sa **`N = 16`** candidate configurations.

**Step 3: Allocate small computational resources**

Instead of fully training all 16 candidates, it **trains them with them with a small resource budget**.

- If we tune a **neural network**, the resource might the **number of training epochs**.
- If we tune a **Random Forest**, the resource might be **number of tree (**`n_estimators`**)**

Assign **only 10 epochs** (a small resource budget) to each configuration.

**Step 4: Evaluate performance and rand candidates**

After training each candidate for 10 epochs, it **evaluate them** using validation accuracy.

Example result:

| **Candidate** | **`n_estimators`** | **`max_depth`** | **`min_samples_split`** | **Accuracy (%)** | 
| --- | ---- | --- | ---- | --- |
|C1	 | 10	| 5	| 2 | 	60 |
|C2	 | 50	| 10 |	2 |	62 |
|C3	 | 100	| 15 |	5 |	59 |
|C4	 | 200	| None |	2 |	65 |
|C5	 | 500	| 10 |	10 |	57 |
|C6	 | 50	| None |	2 |	66 |
|C7	 | 100	| 5 |	10 |	54 |
|C8	 | 200	| 15 |	5 |	64 |
|C9	 | 500	| 5 |	2 |	55 | 
|C10 | 	10	| 15 |	10 |	52 |
|C11 | 	50	| 5 |	5 |	53 |
|C12 | 	100 | 	None |	10 |	61 |
|C13 | 	200 | 	10 |	5 |	63 |
|C14 | 	500 | 	None |	2 | 68 |
|C15 | 	10	| 10 |	5 |	50 |
|C16 | 	50	| 15 |	10 |	58 |

**Step 5: Keep the best candidates (top 50%)**

It **eliminate the worst half** and keep the **top-performing 8 candidates**.

**Step 6: Increase computational resources**

For the remaining 8 candidates, it double the training epochs (e.g., train them for 20 epochs instead of 10)
- Train **only the surviving candidates**, not the eliminated ones.
- This **saves computational cost** while focusing on **good configurations**.

**Step 7: Repeat the process**

**Again**, rank the remaining candidates based on performance.

**Keep the top half** and **increase the training budget again**.

Example reduction:

| **Round** | **Candidates** | **Epochs per candidates** |
| ---- | ---- | ----- |
| Round 1 |	16 |	10 |
| Round 2 |	8 |	20 |
| Round 3 |	4 |	40 |
| Round 4 |	2 |	80 |
| Round 5 |	1 (Best) |	160 |

Eventually, **only the best hyperparameter set remains** after all rounds.


**Mathematical Formulation**

Halving Search follows a **geometric reduction**:
1. **Initial candidates** $N$
2. **Number of Halving rounds**
$$r = \log_s(N)$$

where $s$ is the **reduction factor** (e.g., 2 means we keep 50% each round)
3. **Resources per round**
$$R_i = R_{\min} \times s^i$$

where $R_{\min}$ is the initial resource and $i$ is the round index
