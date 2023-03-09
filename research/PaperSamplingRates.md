# Smartphone Sensor-based Human Activity Recognition Robust to Different Sampling Rates

## Paper Details

**Published**: 2021

## 1. Proposed Solution

### What is the proposed solution?
- The proposed
method applies an adversarial network and data augmentation by downsampling to a common activity recognition model
to achieve the acquisition of feature representations that make the sampling rate unspecifiable
- An activity recognition model that is robust to different sampling rates by applying an adversarial deep learning network

## 2. Methodology

### What methodology was used to evaluate the proposed solution?
- Data augmentation by downsampling
- Dataset split <img width="1093" alt="image" src="https://user-images.githubusercontent.com/22744751/224159194-4f74d7d7-34e0-4f04-9c1e-d2d2476534db.png">
- Training the models

### What data sets were used?
- HASC dataset

### How was the performance of the proposed solution measured?
- N/A

### What hyperparameters were used in the proposed solution?
- N/A

### What interesting models were used in the proposed solution?
- Multi modal model constisting of 3 elements

<img width="565" alt="image" src="https://user-images.githubusercontent.com/22744751/224158217-2aea0c86-cd95-4ee8-96d8-0557deed53a6.png">

## 3. Results

### What were the main findings of the study?
- the method combining the sampling-rate adversarial network and data augmentation by downsampling works better than conventional methods

### How well did the proposed solution perform?
- N/A

### Were there any limitations or challenges encountered during the study?
- Only compared on HASC dataset

## 4. Insights

### How can these insights be used to inform your own solution for sensor-based activity recognition?
- Check whether we get different results with/without when training the models
  - with all data transformed to specific sampling rate (expected to perform better)
  - with keep the sampling rates as they are

### What are the implications for our project in sensor-based activity recognition?
- TODO
