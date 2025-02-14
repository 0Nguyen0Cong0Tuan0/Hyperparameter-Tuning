<center><strong><p style="font-size: 35px;">Hyperparameter Tuning</p></strong></center>

### **Random Search**

**Random Search** is a method of hyperparameter tuning to find optimal hyperparameter that involves randomly sampling a combination of hyperparameters which is used to control the training process from a predefined set (a search space) and training a model using those hyperparameter.

We need to define the set of possibles value for each hyperparameter and then the algorithm randomly selects a combination of these values.

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

Source: <p><a href='https://www.run.ai/guides/hyperparameter-tuning#grid'>Hyperparameter Tuning (RUN.AI)</a></p>