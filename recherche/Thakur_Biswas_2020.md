# Smartphone based human activity monitoring and recognition using ML and DL: a comprehensive survey

## Paper Details

**Published**: 2020
**Link**: [URL](https://doi.org/10.1007/s12652-020-01899-y)

## 1. Proposed Solution

### What is the proposed solution?
- N/A

## 2. Methodology

### What methodology was used to evaluate the proposed solution?
- N/A

### What data sets were used?
- N/A

### How was the performance of the proposed solution measured?
- N/A

### What hyperparameters were used in the proposed solution?
- N/A

### What interesting models were used in the proposed solution?

- Traditional ML/DL classifiers used:
There are a large number of classifier algorithms implemented for HAR. The classifier was generally one of the well-known methods such as 
Naive Bayesian (NB), k-Nearest Neighbors (KNN), Decision 
Tree (DT), Multilayer Perceptron (MP), Logistic Regression 
(LR), Support Vector Machines (SVM) (Cortes and Vap-
nik 1995), Extreme Learning Machine (ELM) (Huang et al. 
2006), ensemble learning algorithm of Random Forest (RF) 
(Breiman 2001), Artificial Neural Networks (ANN) (Lara 
and Labrador 2013) and deep learning approach of deep 
LSTM (Zhu et al. 2016)

## 3. Results

### What were the main findings of the study?

- Different classification methods give different accuracy to recognize various human activities
- Selection and location of the sensors are two important issues that are to take care off in the field of HAMR
- The sensor signals can differ significantly in distinct positions on the body of a user for the same physical activity.
- The benefit of DL techniques is automatic extraction of features compared to traditional techniques.
- Different smartphone has different hardware configuration such as sensor sampling rate, sensor accuracy. So device independent HAMR is required. The position and orientation of the smartphone cannot be fixed. Position and orientation of smartphone independent HAMR is required.

### How well did the proposed solution perform?

Measuring by phone in pocket and recognizing similar activities as we do, Adaboost-Stump and Random Forest (ML) and CNN's as well as RNN's (DL) seem to perform best.

![image](https://user-images.githubusercontent.com/22744751/224645926-9fd8abaf-0ca3-41ff-ba92-f62e2f8fbb15.png)

![image](https://user-images.githubusercontent.com/22744751/224647346-6bd3d712-0772-4bba-8a9a-c9e3ce974b0a.png)

### Were there any limitations or challenges encountered during the study?
- N/A

## 4. Insights

### How can these insights be used to inform your own solution for sensor-based activity recognition?

We should experiment with the following models:

- ML: Random Forest, Adaboost Stump
- DL: CNN (maybe RNN)
