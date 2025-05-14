# Supervised learning part 2

## Dense vs Sparse Feature Space

## Dense Feature Space
- A feature space is considered **dense** when most of the feature values are non-zero or meaningful.
- Common in datasets where features are continuous or categorical with limited unique values.
- Example: A dataset with numerical measurements like height, weight, or temperature.

### Advantages:
- Easier to process and analyze.
- Often leads to better model performance due to the richness of information, but for obvious reasons a dense feature space would need lots of data not always possible to include large number of features quickly, for example a feature space of Images having 32m pixels each. 

---

## Sparse Feature Space
- A feature space is considered **sparse** when most of the feature values are zero or missing.
- Common in datasets with high-dimensional data, such as text (e.g., bag-of-words) or one-hot encoded categorical variables.
- Example: A document-term matrix where most words do not appear in a given document, we usually check a document based on which word has occured and how many times it has occured now if its written in english it can have a 1m words but usually all document consists of only less than 1000 words repeating itself. 

### Challenges:
- Requires specialized algorithms to handle efficiently.

---

## Key Differences
| Aspect               | Dense Feature Space         | Sparse Feature Space        |
|-----------------------|-----------------------------|-----------------------------|
| **Feature Values**    | Mostly non-zero            | Mostly zero                 |
| **Dimensionality**    | Typically lower            | Typically higher            |
| **Processing**        | Easier                     | More complex                |
| **Examples**          | Numerical data             | Text data, one-hot encoding |

---

## Types and Categories of Feature Labels

### Types of Feature Labels
1. **Binary Labels**:
    - Represent two possible outcomes (e.g., yes/no, 0/1).
    - Example: Whether an email is spam or not.

2. **Multiclass Labels**:
    - Represent more than two categories.
    - Example: Classifying animals into cats, dogs, or birds.

3. **Continuous Labels**:
    - Represent numerical values on a continuous scale.
    - Example: Predicting house prices or temperatures.

### Categories of Feature Labels
1. **Nominal Labels**:
    - Represent categories without any inherent order.
    - Example: Colors (red, blue, green).

2. **Ordinal Labels**:
    - Represent categories with a meaningful order but no fixed interval.
    - Example: Ratings (poor, average, good).

3. **Interval Labels**:
    - Represent ordered categories with meaningful intervals but no true zero.
    - Example: Temperature in Celsius or Fahrenheit.

4. **Ratio Labels**:
    - Represent ordered categories with meaningful intervals and a true zero.
    - Example: Weight, height, or age.


## Hypothesis Function

A **hypothesis function** is a mathematical function that represents the relationship between input features and the target variable in a machine learning model. It is used to make predictions based on the input data, when we are training our model using sample Feature and Labels we are actually training or refining our **hypothesis function** (h), a lot depends on choosing the right type of **hypothiesis function**. 

### Types of Hypothesis Functions

1. **Linear Hypothesis**:
        - Assumes a linear relationship between input features and the target variable.
        - Example: $h(x) = w_1x_1 + w_2x_2 + \dots + w_nx_n + b$, where $ w $ are weights,  $x$ are features, and $b$ is the bias term.

2. **Non-Linear Hypothesis**:
        - Assumes a non-linear relationship between input features and the target variable.
        - Example: Polynomial functions, exponential functions, or functions involving activation functions in neural networks.

3. **Probabilistic Hypothesis**:
        - Outputs probabilities instead of deterministic values.
        - Example: Lets say you want to create a model where you can pridict probablity of a patient return in 1 month after discharge.

4. **Piecewise Hypothesis**:
        - Combines multiple functions to represent different regions of the input space.
        - Example: Decision trees where each branch represents a different hypothesis.

### Importance:
    - The choice of hypothesis function directly impacts the model's ability to learn and generalize from the data.
    - Selecting the right hypothesis depends on the nature of the problem and the underlying data distribution.
    - A good hypothesis function balances simplicity and accuracy to avoid overfitting or underfitting.

### NOTE
Hypothesis of your feature/label h ∈ H, where H is all possible functions your model could use. 

## Loss Function

A **loss function** quantifies the difference between the predicted values from the hypothesis function and the actual target values. It serves as a measure of how well the model's predictions align with the true outcomes. The goal of training a machine learning model is to minimize this loss.

For a given hypothesis function $ h(x) $, the error can be represented using the delta function \( \delta \), which evaluates to 1 when $h(x_i) \neq y_i $ and 0 otherwise. The equation is:

$$
\text{Error Rate} =  \frac{1}{n} \sum_{i=1}^{n} \delta(h(x_i) \neq y_i)
$$

where:
- $\ \delta(h(x_i) \neq y_i) $ is 1 if the prediction  $h(x_i)$ does not match the actual label $y_i$, and 0 otherwise.
- n is the total number of data points in the dataset.

### Squared Loss
The **squared loss function** measures the squared difference between the predicted and actual values. It is commonly used in regression tasks. The formula is:

$$
\text{Squared Loss} = \frac{1}{n} \sum_{i=1}^{n} (h(x_i) - y_i)^2
$$

#### Real-World Example:
Predicting house prices based on features like size, location, and number of rooms. Squared loss penalizes larger errors more heavily, making it suitable for scenarios where large deviations are undesirable.

### Absolute Loss
The **absolute loss function** measures the absolute difference between the predicted and actual values. It is robust to outliers compared to squared loss. The formula is:

$$
\text{Absolute Loss} = \frac{1}{n} \sum_{i=1}^{n} |h(x_i) - y_i|
$$

#### Real-World Example:
Predicting delivery times for a logistics company. Absolute loss is preferred when minimizing the impact of outliers, such as rare delays caused by extreme weather conditions.

### Importance:
- These loss functions help guide the optimization process during model training.
- The choice of loss function depends on the problem type and the desired sensitivity to outliers.
- Squared loss is more sensitive to large errors, while absolute loss provides a more robust alternative.


###
    Here is a example of bad sample, army requested to write a AI program which can tell which vehicle is military and which are civilian, it worked out perfectly and gave 0 error, but when they deployed it, they found it worked like 50% of time, when they tried to find out what went wrong, turned out they took picture of army vehicle in day time and evening time they brought in civilian, so Algorithm though that when its brighter its army vechicle else its civilian.

### Generalization

A memorization doesn't have any pridictibility hence even though it works perfectly on training data it doesn't work for complete distribution space.

One way is to break training data into two part, learn from part-1 and when H is ready you test it with second part for which you already have correct values of y. 