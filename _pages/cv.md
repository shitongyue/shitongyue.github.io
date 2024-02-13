---
layout: archive
title: "Instruction"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

### er_algorithm

```python
ertool.er.er_algorithm(W, DBF, numOfEvidence, numOfPropositions)
```
<kbd>er_algorithm()</kbd> can implement the Evidential Reasoning (ER) algorithm.

#### Input Variables
- ***W***: A one-dimensional array of floats. It represents the weights of each piece of evidence. These weights are used in the algorithm to adjust the influence of each evidence.
- ***DBF***: A two-dimensional array of floats. It stands for "Degrees of Belief" and is one of the main inputs to the algorithm, used to represent the initial belief degree of each proposition supported by each evidence.
- ***numOfEvidence***: An integer. It indicates the number of evidence to be combined. In the DBF array, this typically corresponds to the number of rows.
- ***numOfPropositions***: An integer. It indicates the number of propositions or evidential grades. In the DBF array, this typically corresponds to the number of columns.

#### Output Values
- ***B Array***: Upon completion of the algorithm, the B array is updated with the final calculation results. It reflects the degree of belief of each proposition or evidential grades for the object being assessed after combining all availble evidence. The pre-Numofproposition values in the B represent the belief degree of each proposition after evidence fusion. The last value of the B represents the belief degree of the global uncertainty.
- ***False (Boolean)***: It returns True if the algorithm successfully executes and completes all computations. If any error is encountered during execution (e.g., division by zero), it returns False.


### dempster_shafer
```python
ertool.er.dempster_shafer(DBF, numOfEvidence, numOfPropositions)
```

<kbd>dempster_shafer()</kbd> can implement the original Dempster-Shafer evidence theory.

#### Input Variables
- ***DBF***: A two-dimensional array of floats. It stands for "Degrees of Belief" and is one of the main inputs to the algorithm, used to represent the initial belief degree of each proposition supported by each evidence. The pre-Numofproposition values in the B represent the belief degree of each proposition after evidence fusion. The last value of the B represents the belief degree of the global uncertainty.
- ***numOfEvidence***: An integer. It indicates the number of evidence to be combined. In the DBF array, this typically corresponds to the number of rows.
- ***numOfPropositions***: An integer. It indicates the number of propositions or evidential grades. In the DBF array, this typically corresponds to the number of columns.

#### Output Values
- ***B Array***: Upon completion of the algorithm, the B array is updated with the final calculation results. It reflects the degree of belief of each proposition or evidential grades for the object being assessed after combining all availble evidence.
- ***False (Boolean)***: It returns True if the algorithm successfully executes and completes all computations. If any error is encountered during execution (e.g., division by zero), it returns False.


### show_er_result

```python
ertool.er.show_er_result(B, P = None)
```
<kbd>er.show_er_result()</kbd> can visualize the result of evidential reasoning algorithm.

#### Input Variables
- ***B***: The ER result of belief degree.
- ***P***: The name array of propositions.

### run_algorithm_from_file
```python
ertool.er.run_algorithm_from_file(file_path, algorithm = ’ER’)
```

<kbd>run_algorithm_from_file()</kbd> reads CSV or XLSX files and performs multi-source evidence fusion on the data using ER approach or Dempster-Shafer’s theory.

#### Input Variables
- ***file_path***: A string. The location of the CSV or XLSX file. Note that the format of data strictly follows the format of the provided template.
- ***algorithm***: ’ER’ or ’DS’. ‘ER’ stands for using the ER approach, and ’DS’ stands for using the Dempster-Shafer theory.

#### Output
- ***B Array***: Upon completion of the algorithm, the B array is updated with the final calculation results. It reflects the degree of belief in each proposition or evaluation grade for the object being assessed after combining all available evidence. The first numofPropositions members in the B represent the belief degree in each proposition after evidence fusion. The last member of the B represents the belief degree in the global uncertainty.
- ***False (Boolean)***: It returns True if the algorithm successfully executes and completes all computations. If any error is encountered during execution (e.g., division by zero), it returns False.

