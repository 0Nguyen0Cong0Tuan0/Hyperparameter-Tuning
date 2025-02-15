<center><strong><p style="font-size: 35px;">Hyperparameter Tuning</p></strong></center>

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