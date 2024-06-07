---
layout: archive
# title: "Quick Start"
permalink: /quickstart/
author_profile: true
redirect_from:
  - /quickstart
---
{% include base_path %}

## Here are some basic usage examples of **ERTool**.

### Example 1: a medical scenario

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

### Example 2: a car brand selection scenario

Consider a car brand selection scenario.

We have now invited a car evaluator to evaluate cars from five brands, including Ford, Tesla, Audi, Volkswagen and BMW, based on four aspects: Acceleration, Braking, Horsepower and Powertrain. Assume that the four aspects are equally weighted.

We can write the following code to use ERTool to integrate the four aspects of evidence.

```python
from ertool import er
import numpy as np

W = np.array([1,1,1,1])
DBF = np.array([
 [0.173, 0.118, 0.054, 0.356, 0.298],
 [0.174, 0.207, 0.181, 0.427, 0.011],
 [0.160, 0.211, 0.283, 0.093, 0.253],
 [0.367, 0.325, 0.179, 0.017, 0.012]
])

numOfEvidence = 4
numOfPropositions = 5
B = er.er_algorithm(W, DBF, numOfEvidence, numOfPropositions)
print("The result: ", B)

car_brands = ["Ford", "Tesla", "Audi", "Volkswagen", "BMW"]

er.show_er_result(B, P=car_brands, fig_name="Car Selection on Performance", xlabel_name="Car Brands")
```

We can get the following results in the figure below.

![Figure](https://ertool.online/images/output4.png)

At the same time, we used IDS software to perform the same operation and obtained the same results as shown in the figure below.

![Figure](https://ertool.online/images/output4o.jpg)

This above example not only demonstrates the usage of ERTool, but also verifies ERTool's correctness.

### Example 3: a quality assessment scenario

Consider a quality assessment scenario.

We used both ERTool and IDS software to do evidence fusion for combining Expert judgments about the medical quality of three hospitals from medical facilities (MF), medical staff (MS), medical processes (MP), and medical outcomes (MO) perspectives. The summary statistics of patient feedback on the medical quality of Hospitals A, B, and C from the four different perspectives.

This example is from a published paper: Kong, Guilan, et al. "Combined medical quality assessment using the evidential reasoning approach." *Expert Systems with Applications* 42.13 (2015): 5522-5530.

Here are expert judgments about medical quality of Hospitals A, B, and C in the table below:
![Figure](https://ertool.online/images/table4.png)

We can calculate the three hospitals separately, and the code is as follows.

Use ERTool for Hospital A:

```python
from ertool import er
import numpy as np

W = np.array([1,1,1,1])
DBF = np.array([[1,0,0,0,0], 
                [0,0.5,0.5,0,0], 
                [0,0.6,0.4,0,0], 
                [0,0.9,0,0.1,0]])

numOfEvidence = 4
numOfPropositions = 5
B = er.er_algorithm(W, DBF, numOfEvidence, numOfPropositions)
print("The result: ", B)

P = ['Excellent', 'Good', 'Average','Poor','Worst']
er.show_er_result(B, P=P, fig_name="Hospital A on Medical Quality", xlabel_name="Evalution grades")
```

Use ERTool for Hospital B:

```python
from ertool import er
import numpy as np

W = np.array([1,1,1,1])
DBF = np.array([[0,0.7,0.3,0,0], 
                [0,0.8,0.2,0,0], 
                [0,0.5,0.5,0,0], 
                [0,0.6,0.4,0,0]])

numOfEvidence = 4
numOfPropositions = 5
B = er.er_algorithm(W, DBF, numOfEvidence, numOfPropositions)
print("The result: ", B)

P = ['Excellent', 'Good', 'Average','Poor','Worst']
er.show_er_result(B, P=P, fig_name="Hospital B on Medical Quality", xlabel_name="Evalution grades")
```

Use ERTool for Hospital C:

```python
from ertool import er
import numpy as np

W = np.array([1,1,1,1])
DBF = np.array([[0.5,0.3,0.2,0,0], 
                [0,0.6,0.4,0,0], 
                [0,0.5,0.4,0.1,0], 
                [0,0.4,0.5,0.1,0]])

numOfEvidence = 4
numOfPropositions = 5
B = er.er_algorithm(W, DBF, numOfEvidence, numOfPropositions)
print("The result: ", B)

P = ['Excellent', 'Good', 'Average','Poor','Worst']
er.show_er_result(B, P=P, fig_name="Hospital C on Medical Quality", xlabel_name="Evalution grades")
```

After calculation, we successfully obtained the fusion results of the quality assessment evidence of different experts for each hospital. At the same time, we can also compare the results with those generated by IDS software in the below figure and find that the results are exactly the same, which also verifies the correctness of ERTool.

![Figure](https://ertool.online/images/example.png)

## How to do multi-level multi-source evidence fusion?

### Step 1: Define the evaluation framework of the multi-level multi-attribute assessment problem.

First, we define the above two-level multi-attribute assessment problem using the ER framework.

### Step 2: Build the “Objects” folder and store the data files in corresponding subfolders.

Secondly, we build the “Objects” folder and its subfolders according to the evaluation framework. Save the survey data about each attribute (research funding, research outcomes, teaching materials, teaching methods) of the three institutes from surveyed students and faculties together with corresponding weight to different CSV files, respectively. Put different evidence data files (Evidence1_Student.csv and Evidence2_Faculty.csv) and the data files for storing evidence combined results (Objects_combined.csv, Research_combined.csv, Research_Funding_combined.csv, Reseach_Outcomes_combined.csv, Teaching_combined.csv, Teaching_Materials_combined.csv, Teaching_Methods_combined.csv) to their corresponding subfolders.

### Step 3: Call the function to get evidence fusion results.

Finally, we can call the multi_level_multi_source()function using the path of the “Objects” folder as input, and the output results will be written to “Objects_combined.csv” file by running the following codes:

```
from ertool import er
er.multi_level_multi_source(*)
```

Here, “*” represents the path of “Objects” folder. For example, it can be "/Users/Documents/Objects".

![Figure](https://ertool.online/images/fig6.png)