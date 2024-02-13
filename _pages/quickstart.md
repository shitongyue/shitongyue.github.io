---
layout: archive
title: "Quick Start"
permalink: /quickstart/
author_profile: true
redirect_from:
  - /quickstart
---
{% include base_path %}

## Quick Start
Here is a basic usage example of **ERTool**.

Consider a medical scenario. 
There are three medical experts (weights 10, 8, and 5). For one patient, the three experts rated the different likelihood of the diagnosis of cold, common pneumonia, COVID-19, and other diseases. As shown in the table.

| Experts & Diseases | Expert 1 | Expert 2 | Expert 3 |
| :---:        |    :----:   |  :---: |  :---: |
| Cold | 90% | 0 | 0 |
| Common Pneumonia |0 | 90% | 0|
| COVID-19 | 0 | 0 | 90% |

In this case, the ***numOfEvidence*** is 3 (the number of experts) and the ***numOfPropositions*** is 3 (cold, common pneumonia and COVID-19).

The ***W*** array is the weights array of every expert and the **ERTool** package can normalize them automatically.

We can write the code using the **ERTool** package:

```python
from ertool import er
import numpy as np

W = np.array([10,8,5])
DBF = np.array([[0.9, 0, 0], 
                [0, 0.9, 0], 
                [0, 0, 0.9]])

# List or numpy array are both OK.
# W = [10,8,5]
# DBF = [[0.9, 0, 0], 
#        [0, 0.9, 0], 
#        [0, 0, 0.9]]

numOfEvidence = 3
numOfPropositions = 3
B = er.er_algorithm(W, DBF, numOfEvidence, numOfPropositions)
print("The result: ", B)

P = ['Cold', 'Common Pneumonia', 'COVID-19']
er.show_er_result(B, P)
```
With the code, we can calculate the probability that the patient will be diagnosed with each disease using evidential reasoning.

```
The result: [0.43317251 0.307059 0.16390311 0.09586537]
```
The calculation results show that the probability of the patient being diagnosed with a cold, common pneumonia, and COVID-19 are 0.43317251, 0.307059, and 0.16390311, respectively. The last member of B represents global uncertainty, and it is 0.09586537 in this example.