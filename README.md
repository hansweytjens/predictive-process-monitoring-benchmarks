### README 
This repository contains two files. 

"BPIC_scripts" is a notebook containing the scripts to convert the original BPIC (Business Process Intelligence Challenge) datasets into benchmark datasets as described in the paper "Creating Unbiased Public Benchmark Datasets with Data Leakage Prevention for Predictive Process Monitoring" (abstract below).

"create_benchmarks" is a python file with code for "BPIC_scripts". 

### Datasets
The BPIC datasets can be downloaded from:

- BPIC_2012: https://data.4tu.nl/articles/dataset/BPI\_Challenge\_2012/12689204
- BPIC_2015: https://data.4tu.nl/collections/BPI\_Challenge\_2015/5065424
- BPIC_2017: https://data.4tu.nl/articles/dataset/BPI\_Challenge\_2017/12696884
- BPIC_2019: https://data.4tu.nl/articles/dataset/BPI\_Challenge\_2019/12715853
- BPIC_2020: https://data.4tu.nl/collections/BPI\_Challenge\_2020/5065541

### pm4py
The scripts in this repository require the installation of PM4PY (https://pm4py.fit.fraunhofer.de/install).

Due to a built-in compression mechanism within the pm4py libary, converting the BPIC_2017 train and test sets is not feasible within a reasonable time frame. Users are recommended to save them as pickle or csv files instead, as shown in the script.

### Outputs
The scripts output two files: a training set and test set according to the principles laid out in the paper. The outputs can be found in the same directory (PATH) as where the original xes files were found, and will be in xes-format as well, unless otherwise specified (BPIC_2017). The suffices "_train" and "_test" (for remaining time and outcome prediction) and "_next_event_train and "_next_event_test" (for next event prediction) are added to the original filenames.

Since we concatenated five files corresponding to five municipalities into one BPIC_2015 dataset, we also added a "munic" column to identify the original municipality. The values in "case:concept:name" which identify the cases were slightly modified to avoid overlap.

### Using the test set for inference
Some events in the test set (red in Fig.2 in the paper) have the value "NAN" as their targets. These events belong to cases that start before the separation time (start time of the test set), but end after it (red/grey cases in Fig. 2). The events corresponding to prefixes ending after the separation time (in grey in Fig. 2) do carry a real target and belong to the test set. The prefixes corresponding to the events with "NAN" targets are not part of the test set and should not be used for inference. However, the researcher will use these events before the separation time to construct the prefixes that are part of the dataset.


### Paper abstract
Advances in AI, and especially machine learning, are increasingly drawing research interest and efforts towards predictive process monitoring, the subfield of process mining (PM) that concerns predicting next events, process outcomes and remaining execution times. Unfortunately, researchers use a variety of datasets and ways to split them into training and test sets. The documentation of these preprocessing steps is not always complete. Consequently, research results are hard or even impossible to reproduce and to compare between papers. At times, the use of non-public domain knowledge further hampers the fair competition of ideas. Often the training and test sets are not completely separated, a data leakage problem particular to predictive process monitoring. Moreover, test sets usually suffer from bias in terms of both the mix of case durations and the number of running cases. These obstacles pose a challenge to the  field's progress. The contribution of this paper is to identify and demonstrate the importance of these obstacles and to propose preprocessing steps to arrive at unbiased benchmark datasets in a principled way, thus creating representative test sets without data leakage with the aim of levelling the playing field, promoting open science and contributing to more rapid progress in predictive process monitoring.

### Remaining time prediction
Compared to the original datasets, a column "remain_time" is added. This column constitutes the target for remaining time prediction problems.

### Classification 
Additionnally, the scripts can also be used to add classification targets to the BPIC_2012 and BPIC_2017 datasets. Each dataset contains 3 binary (True/False) targets: "approved", "declined" and "canceled". Note that in the case of BPIC_2017, the targets are not mututally exclusive as sometimes "canceled" cases are restarted and "approved" or "declined" cases become "canceled" later.

### Next event prediction
Scripts for next event prediction were also added for BPIC_2012 and BPIC_2017, according to the guidelines laid out in the paper. The targets are found in the column "nextEvent".

### Caution
Make sure to NOT use targets from another prediction problem as features for your prediction problem!
