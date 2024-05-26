---
layout: archive
# title: "Quick Start"
permalink: /quickstart/
author_profile: true
redirect_from:
  - /quickstart
---
{% include base_path %}

### Here is a basic usage example of **ERTool**.

Consider a medical scenario. 
There are three medical experts (weighted 10, 8, and 5). For one patient, the three experts rated the different likelihood of the diagnosis of cold, common pneumonia and COVID-19. As shown in the table.

| Experts & Diseases | Cold | Common Pneumonia | COVID-19 |
| :---:        |    :----:   |  :---: |  :---: |
| Expert 1 | 90% | 10% | 0 |
| Expert 2 | 20% | 70% | 10% |
| Expert 3 | 30% | 60% | 0 |

In this case, the ***numOfEvidence*** is 3 (the number of experts) and the ***numOfPropositions*** is 3 (cold, common pneumonia and COVID-19).

The ***W*** array is the weights array of every expert and the **ERTool** package can normalize them automatically.

We can write the code using the **ERTool** package:

```python
from ertool import er
import numpy as np

W = np.array([10,8,5])
DBF = np.array([[0.9, 0.1, 0], 
                [0.2, 0.7, 0.1], 
                [0.3, 0.6, 0]])

# List or numpy array are both OK.
# W = [10,8,5]
# DBF = [[0.9, 0.1, 0], 
#         [0.2, 0.7, 0.1], 
#         [0.3, 0.6, 0]])

numOfEvidence = 3
numOfPropositions = 3
B = er.er_algorithm(W, DBF, numOfEvidence, numOfPropositions)
print("The result: ", B)

P = ['Cold', 'Common Pneumonia', 'COVID-19']
er.show_er_result(B, P)
```
With the code, we can calculate the probability that the patient will be diagnosed with each disease using evidential reasoning.

```
The result:  [0.56182081 0.39411809 0.02924234 0.01481876]
```
The calculation results show that the probability of the patient being diagnosed with a cold, common pneumonia, and COVID-19 are 0.56182081, 0.39411809 and 0.02924234, respectively. The last member of B represents global uncertainty, and it is 0.01481876 in this example.

### How to do multi-level multi-source evidence fusion?

#### Step 1: Define the evaluation framework of the multi-level multi-attribute assessment problem.
First, we define the above two-level multi-attribute assessment problem using the ER framework.

#### Step 2: Build the “Objects” folder and store the data files in corresponding subfolders.
Secondly, we build the “Objects” folder and its subfolders according to the evaluation framework. Save the survey data about each attribute (research funding, research outcomes, teaching materials, teaching methods) of the three institutes from surveyed students and faculties together with corresponding weight to different CSV files, respectively. Put different evidence data files (Evidence1_Student.csv and Evidence2_Faculty.csv) and the data files for storing evidence combined results (Objects_combined.csv, Research_combined.csv, Research_Funding_combined.csv, Reseach_Outcomes_combined.csv, Teaching_combined.csv, Teaching_Materials_combined.csv, Teaching_Methods_combined.csv) to their corresponding subfolders.

#### Step 3: Call the function to get evidence fusion results.
Finally, we can call the multi_level_multi_source()function using the path of the “Objects” folder as input, and the output results will be written to “Objects_combined.csv” file by running the following codes:
```
from ertool import er
er.multi_level_multi_source(*)
```
Here, “*” represents the path of “Objects” folder. For example, it can be "/Users/pkuer/Documents/Objects".