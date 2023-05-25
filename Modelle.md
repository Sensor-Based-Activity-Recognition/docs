# CNN
The CNN is based on the paper by [Chen 2021](./recherche/Chen_2021.md). As described in the paper, we created spectrograms from the sensor data using the Short-Time Fourier Transform. We implemented the CNN using PyTorch and customized it a bit.

## DAG/Stages
```
     +----------------------+
     | pull_data_calibrated |
     +----------------------+
                 *
                 *
                 *
        +---------------+
        | resample_50Hz |
        +---------------+
                 *
                 *
                 *
        +---------------+
        | segmentate_5s |
        +---------------+
          **           **
        **               **
      **                   **
+------+        +--------------------------+
| stft |        | train_test_split_ratio02 |
+------+**      +--------------------------+
          **           **
            **       **
              **   **
            +---------+
            | dvclive |
            +---------+
                 *
                 *
                 *
           +----------+
           | evaluate |
           +----------+
```
The data is pulled from the database and then resampled to 50Hz. After that, it is split into 5 second windows. Then the train_test_split_ration02 marks 20% of the segments for testing and keeps the other 80% for the training. In the stft stage, the Spectrograms are created as described in the next section. The dvclive stage trains the model and the evaluate stage creates a confusion matrix to analyze the types errors the CNN makes. 

## Spectograms
The spectograms were created using `scipy.signal.stft`. The parameters are as follows:
- `fs`: Sampling rate we set to 50Hz (The same as it was set in the resample stage)
- `nperseg`: We have set the length of the segments to 100. This corresponds exactly to 2 seconds. 
- `noverlap`: We set the overlap of the segments to 95. This corresponds to an overlap of 95% or 1.9 seconds.

A spectogram then looks like this:

![Spectogramm](./images/rennen_spectrogram.png)

## CNN
The model architecture consists of four convolutional layers each followed by pooling layers. After the convolution part, a global average pooling layer and two fully connected layers follow. Here's a breakdown of the model:

- Convolutional Layer 1: Takes input with 9 channels, applies 32 filters of size 5x5.
- Pooling Layer 1: Performs max pooling with a kernel size of 2x2 and stride of 2.
- Convolutional Layer 2: Takes the output of the previous layer (32 channels) and applies 64 filters of size 4x4.
- Pooling Layer 2: Performs max pooling with a kernel size of 2x2 and stride of 2.
- Convolutional Layer 3: Takes the output of the previous layer (64 channels) and applies 128 filters of size 3x3.
- Pooling Layer 3: Performs max pooling with a kernel size of 2x2 and stride of 2.
- Convolutional Layer 4: Takes the output of the previous layer (128 channels) and applies 256 filters of size 2x2.
- Global Average Pooling Layer: Computes the average value of each channel across the spatial dimensions, resulting in a single value per channel.
- Fully Connected Layer 1: Takes the output of the global average pooling layer (128 features) and maps it to 64 features.
- Fully Connected Layer 2: Takes the output of the previous layer (64 features) and applies a softmax function to produce the final output.

### Model Parameters
Here's a summary of the trainable parameters in the model:

|  Name  |      Type          | Params |
|--------|:-----------------:|-------:|
| conv1             |  Conv2d             |  7.2 K |
| conv2             |  Conv2d             | 32.8 K |
| conv3             |  Conv2d             | 73.9 K |
| fc1               |  Linear             |  8.3 K |
| fc2               |  Sequential         |   390  |

Total params: 122 K

## Results
The model achieves a Performance of over 90% on the test set on the Accuracy. Here are the results:

|     Test metric    |        DataLoader 0         |
|:------------------:|----------------------------:|
|  test_acc_epoch    |     0.922       |
|  test_f1_epoch     |     0.915       |
