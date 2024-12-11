Feature scaling is an important step in preparing data for machine learning models. It involves transforming the values of features in a dataset to a similar scale, ensuring that all features contribute equally to the model’s learning process.

When features are on vastly different scales e.g., $x_1$ ranging from 1 to 10 and $x_2$ from 1,000 to 10,000, models can prioritise the larger values, leading to bias in predictions. This can result in poor model performance and slower convergence during training. 

Feature scaling addresses these issues by adjusting the range of the data without distorting differences in the actual values.

_Source: [https://www.datacamp.com/tutorial/normalization-vs-standardization](https://www.datacamp.com/tutorial/normalization-vs-standardization)_