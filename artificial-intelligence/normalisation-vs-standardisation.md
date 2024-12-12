# Normalisation vs Standardisation
Machine learning algorithms are often trained with the assumption that all features contribute equally to the final prediction, which fails when the features differ in range and unit, hence affecting their importance.

Normalisation and standardisation are essential [[feature-scaling|feature scaling]] techniques that can be used in preprocessing to adjust data for better performance or help in the interpretation of results.
## Normalisation 
The process of scaling/adjusting values measured on different scales to a common scale.
### Min-max 
Transforms features to a specified range, typically between 0 and 1. 
$$x'=\frac{x-max(x)}{max(x)-min(max))}$$

When:
- approx. upper and lower bounds of the dataset is known and it has few or no outliers 
- unknown/non-gaussian distribution and feature is uniformly distributed across a fixed range
- maintaining the distribution’s original shape is essential

![[normalised_data.jpg|center|500]]

### Decimal scaling 
Scales the feature values by a power of 10, ensuring that the largest absolute value in each feature becomes less than 1. $$x' = \frac{x}{10^{d}}$$
When
- range of values in a dataset is known, but the range varies across features
- datasets where the absolute magnitude of values matters more than their specific scale
### Log scaling 
Converts data into a logarithmic scale, by taking the log of each data point. $$x'=\log{x}$$
When:
- data spans several orders of magnitude
- data follows an exponential growth or decay pattern
## Standardisation
Transforms data to have a mean of 0 and a standard deviation of 1 i.e., it simply represents features in terms of the number of standard deviations that lie away from the mean. $$z=\frac{x-\mu}{\sigma}$$

When:
- gradient-based algorithms like SVM requires standardised data for optimal performance.
- algorithms that are sensitive to data with zero mean and unit variance e.g., SVM, Logistic Regression, Linear Regression, PCA, k-Means.
- In dimensionality reduction techniques like PCA because it considers both the mean and variance.

![[standardised_data.jpg|center|500]]


## Summary
Normalisation:
- Objective is to bring the values of a feature within a specific range, often between 0 and 1.
- Sensitive to outliers and the range of the data.
- Useful when maintaining the original range is essential.
- No assumption about the distribution of data is made.
- Suitable for algorithms where the absolute values and their relations are important (e.g., k-nearest neighbours, neural networks).
- Maintains the interpretability of the original values within the specified range.
- Can lead to faster convergence, especially in algorithms that rely on gradient descent.
- Use cases: Image processing, neural networks, algorithms sensitive to feature scales.

Standardisation:
- Objective is to transform the values of a feature to have a mean of 0 and a standard deviation of 1.
- Less sensitive to outliers due to the use of the mean and standard deviation.
- Effective when algorithms assume a standard normal distribution.
- Assumes a normal distribution or close approximation.
- Particularly useful for algorithms that assume normally distributed data, such as linear regression and support vector machines.
- Alters the original values, making interpretation more challenging due to the shift in scale and units.
- Also contributes to faster convergence, particularly in algorithms sensitive to the scale of input features.
- Use cases: Linear regression, support vector machines, algorithms assuming normal distribution.

_Sources:_
- [https://www.datacamp.com/tutorial/normalization-vs-standardization](https://www.datacamp.com/tutorial/normalization-vs-standardization)
- [https://www.datacamp.com/tutorial/normalization-in-machine-learning](https://www.datacamp.com/tutorial/normalization-in-machine-learning)