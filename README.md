# Model-Interpretability


## Difference in calculate Feature Importance

**LightBGM feature importance**: based on information gain/tree splits/ 

**SHAP value**: The essence of Shapley value is to measure the contributions to the final outcome from each player separately among the coalition. **to explain the prediction of an instance x by computing the contribution of each feature to the prediction. The SHAP explanation method computes Shapley values from coalitional game theory.**

- Paper for reference: [https://arxiv.org/pdf/1706.06060.pdf](https://arxiv.org/pdf/1706.06060.pdf)  
- Introduction for reference: [https://christophm.github.io/interpretable-ml-book/shapley.html#the-shapley-value-in-detail](https://christophm.github.io/interpretable-ml-book/shapley.html#the-shapley-value-in-detail)

**Permutation Feature Importance:** measure the importance of a feature by **calculating** the increase in the **model’s prediction error** after permuting the feature.
***Important feature***: if shuffling its values increases the model error, because in this case the model relied on the feature for the prediction

<img src='https://github.com/zhang-yuyi/Model-Interpretability/blob/master/images/PFI.png' width=90%>

- Paper for reference:  [https://arxiv.org/pdf/1801.01489.pdf](https://arxiv.org/pdf/1801.01489.pdf) ()

**Feature Shapley Value shows how much each feature contribute to the model’s output value, while PFI measures the feature’s impact on the
error of the model**

### Label Encoding VS One-hot Encoding:

- no much difference on model performance
- feature explanation
    - By one-hot encoding, we can pay more attention to a specific feature value

**Calculate on Training data VS on test data** 

one-hot encoding


### **PDP:** for global feature behavior

1D PDP measures the expected prediction for this value by averaging over the prediction of all observations pretending the feature of interest is that value.

A flat PDP indicates that the feature is not important, and the more the PDP varies, the more important the feature is.

Assume features are independent.

> **It captures only the main effect of the feature and ignores possible feature interactions. A feature could be very important based on other methods such as [permutation feature importance](https://christophm.github.io/interpretable-ml-book/feature-importance.html#feature-importance), but the PDP could be flat as the feature affects the prediction mainly through interactions with other features.**
> 

[https://christophm.github.io/interpretable-ml-book/pdp.html](https://christophm.github.io/interpretable-ml-book/pdp.html)

Paper for reference: 

[https://arxiv.org/pdf/1805.04755.pdf](https://arxiv.org/pdf/1805.04755.pdf)

### ALE

change the feature value a liitle, average the changes of predictions, not the predictions itself.

> **Partial Dependence Plots: “Let me show you what the model predicts on average when each data instance has the value v for that feature. I ignore whether the value v makes sense for all data instances.”
ALE plots: “Let me show you how the model predictions change in a small”window" of the feature around v for data instances in that window."**
> 

### Comparison & Recommendation:

|  | Pros | Cons | Use Case |
| --- | --- | --- | --- |
| SHAP value | -have solid theory -The feature contributions must add up to the difference of prediction for x and the average. -addictive | - suffers from inclusion of unrealistic data instances when features are correlated - computing consuming (can use TreeShap) |  |
| PFI | -good interpretation -take into account interactions with other features | -If features are correlated, the permutation feature importance can be biased by unrealistic data instances. -Adding a correlated feature can decrease the importance of the associated feature by splitting the importance between both features. |  |
| LightBGM feature importance |  |  |  |
| PDP | intuitive / stright-forward  -can show the combined effects of two features  * show the average prediction | PDP with one or two feature variables may produce unrealistic datapoint | 1. want to see the total effect of the two feature 2. suitable for one-hot encoded categorical features |
| ALE | not biased in case of correlated features *show the effects on prediction change (zero-centered) | can also fails when when features are strongly correlated. - it only makes sense to analyze the effect of changing both features together and not in isolation. | 1. want to describe how one feature influence the prediction
2. suitable for numerical and label-encoded categorical features |

## Some **insights:**

- The order/rank of feature importance generated from PFI can be changed by with or without sampling methods ( this might be resulted from changes in data distribution after sampling thus changing the effect brought by permutation.)
- Main issues:
    - Compute on training data or test data?
    - whether do sampling?
    - how to encode variables? what are you caring about?
- For categorial/ordinal feature, shap.dependence_plot can give better interpretation. For numerical features,

## Local interpretation: LIME VS SHAP

|  | Pros | Cons | Use Case |
| --- | --- | --- | --- |
| SHAP value |  |  |  |
| LIME |  |  |  |