# TKI-RCC-delta-radiomics

## introduction

Heterogeneous radiologic responses were reported in renal cell carcinoma (RCC) patients under tyrosine kinase inhibitors (TKI) treatment. Specifically, the term refers to the fact that the responses of lesions fall into at least two response categories, which reflects different drug sensitivity between lesions. 

According to the relative size change between pre-treatment image and post-treatment image, each lesion can be classified into one of three response categories: responding lesions (RLs) decreased in size by 30% or more compared to baseline, progressing lesions (PLs) increased in size by 20% or more, and all other lesions were classified as stable lesions (SLs).

Our models are binary classification decision tree models. The RLs/SLs are classified as negative sample while the PLs are classified as positive sample. Through the stratification by lesion level predictive model, metastasectomy can be performed on some lesions with high risk of progressing while the majority of lesions with model-predicted preferable response remain TKI therapy.



## Environment

The environment is as follows:

+ Windows 10
+ Python
+ scikit-learn
+ pickle



## code example for using the models

load the model:

```python
from sklearn.tree import DecisionTreeClassifier
import pickle

with open('delta.pickle', 'rb') as f:
    clf = pickle.load(f)
```

view the feature names and feature importance:

```python
print(clf.feature_names_in_)
print(clf.feature_importances_)
```

make predictions (see more in the scikit-learn [documentation](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html#sklearn.tree.DecisionTreeClassifier))

```python
samples = [
    [1.777, 1.626, 1.825, 0.166, -0.771, 0.685], 
    [0.107, -0.963, -0.668, -1.455, 0.652, -0.118]
    ]
pred_label = clf.predict(samples)
pred_prob = clf.predict_proba(samples)
print(pred_label) # the predicted labels of each sample, 0 for RLs/SLs and 1 for PLs
print(pred_prob[:, 1]) # the predicted probabilities of being PLs
```



## Citation

The associated article will be updated after publication.

