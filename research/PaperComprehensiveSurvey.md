# Smartphone based human activity monitoring and recognition using ML and DL: a comprehensive survey

## Paper Details

**Published**: 2020

**Link**: https://doi.org/10.1007/s12652-020-01899-y

## 1. Proposed Solution

### What is the proposed solution?
- Comparing different approaches to the HAR problem

## 2. Methodology

### What methodology was used to evaluate the proposed solution?
- Studies are compared

### What data sets were used?
- Provides a long list of open source datasets with HAR data ![image](https://user-images.githubusercontent.com/22744751/224630097-611c7da3-3788-40c7-a350-41fa77cf63ab.png)

### How was the performance of the proposed solution measured?
- N/A

### What hyperparameters were used in the proposed solution?
- N/A

### What interesting models were used in the proposed solution?
- N/A

## 3. Results

### What were the main findings of the study?
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

### How well did the proposed solution perform?
- N/A

### Were there any limitations or challenges encountered during the study?
- N/A

## 4. Insights

### How can these insights be used to inform your own solution for sensor-based activity recognition?

Deep Learnung: Two interesting approaches towards time series data using CNN's are discussed
- Option 1 utilizes a time-frequency-spectral map which is fed into a 2D-CNN. In a mentioned study this was calcualted using "Short-time Discrete Fourier Transform (STDFT)". As I undertsand this approach, the interesting thing here is that the time series data is downsampled to different frequencies, making this map hold information on shorter- and longer time scales <img width="377" alt="image" src="https://user-images.githubusercontent.com/22744751/224633873-969c50e2-5822-4096-b995-233b6623c17b.png">
- Option 2 feeds the raw time series data into a 1D-CNN. This in turn also means only one frequency is considered. <img width="377" alt="image" src="https://user-images.githubusercontent.com/22744751/224633916-9bcc94cb-7167-4ce4-8244-1b77942606b6.png">
- Alternative to Option 2: This interesting [article](https://towardsdatascience.com/how-to-use-convolutional-neural-networks-for-time-series-classification-56b1b0a07a57) explains a more complex multi stage 1D-CNN approach, where it also becomes possible to consider different frequencies (downsampling) and other preprocessing like smoothing using moving averages.
