# Our "Masterplan" 🚀

1. Pick preprocessing methods we want to use.
3. Implement our data pipeline in a way that we can dynamically define **used methods** and **order of appliance** 
  - (e.g. array-like Pipeline[LowPass, MA, FFT...])
4. Pick models we want to train. Based on paper research:
  - ML: KNN/SVM as Baseline, Random Forest, Adaboost Stump
  - DL: 2D-CNN (optionally RNN)
5. Continous Iteration:
  - Define several pipelines and train our ML/DL models on the data
  - Evaluate model performance (W&B) and tune hyperparams
6. Have some great performing models :)

# Proposed preprocessing

## Resampling

Resample the signals at a consistent sampling rate, accounting for differences in sensor sample rates to make the data more uniform for training. Resampling can involve upsampling (increasing the number of samples) or downsampling (decreasing the number of samples), depending on the desired target sampling rate.

Python libraries and functions: Pandas (`pandas.DataFrame.resample`, `pandas.DataFrame.interpolate`) and SciPy (`scipy.signal.resample`, `scipy.signal.resample_poly`)

## Filtering

Apply filters like low-pass, high-pass, or band-pass filters to remove noise from the raw accelerometer and gyroscope data. Common filters include Butterworth or Chebyshev filters.

- low-pass/high-pass: Low/high-pass filters allow low/high-frequency signals to pass through while attenuating high/low-frequency signals, effectively reducing high/low-frequency noise in the data. / Python libraries and functions: SciPy (`scipy.signal.butter`, `scipy.signal.lfilter`)
- Butterworth: Butterworth filters are a type of frequency-domain filter that provide a smooth frequency response with no ripples. These filters are designed to have a maximally flat frequency response in the passband and a sharp roll-off in the stopband. / Python libraries and functions: SciPy (`scipy.signal.butter`, `scipy.signal.lfilter`, `scipy.signal.filtfilt`)
- Chebyshev filters: Chebyshev filters are a type of frequency-domain filter characterized by their sharper roll-off compared to Butterworth filters but with ripples in the passband or stopband. There are two types of Chebyshev filters: Type I (ripples in the passband) and Type II (ripples in the stopband). These filters provide a faster transition between the passband and stopband at the expense of ripples. / Python libraries and functions: SciPy (`scipy.signal.cheby1`, `scipy.signal.cheby2`, `scipy.signal.lfilter`, `scipy.signal.filtfilt`)

## Segmentation

Segmentation, also known as windowing, involves dividing the continuous time-series data into smaller, fixed-length segments or sliding windows. This process captures the characteristics of different activities by isolating the relevant data portions for analysis. Segmentation is crucial for machine learning models, as it enables them to recognize patterns and features specific to each activity.

Python libraries and functions: Custom functions using NumPy (`numpy.array`, `numpy.lib.stride_tricks.as_strided`) or using specialized libraries like tslearn (`tslearn.preprocessing.TimeSeriesResampler`, `tslearn.utils.sliding_window`).

## Smoothing

Smoothing techniques reduce fluctuations and noise in the signals, making it easier to extract meaningful features for activity recognition. / Python libraries and functions: Moving average - NumPy or Pandas (`numpy.convolve`, `pandas.DataFrame.rolling`), Gaussian smoothing - SciPy (`scipy.ndimage.gaussian_filter`), Savitzky-Golay filtering - SciPy (`scipy.signal.savgol_filter`)

## Time alignment

Time alignment synchronizes the time-stamps of accelerometer and gyroscope data coming from multiple sensors or different sources, ensuring that the corresponding data points are temporally aligned. / Python libraries and functions: Pandas (`pandas.DataFrame.merge`, `pandas.DataFrame.join`, `pandas.DataFrame.interpolate`)

## Data augmentation

- rotation: Rotation augmentation involves rotating the sensor data by a certain angle to simulate different orientations during data collection. / Python libraries and functions: NumPy (`numpy.dot`, rotation matrix calculation)
- flipping: Flipping augmentation involves flipping the sensor data along one or more axes to simulate different spatial orientations during data collection. / Python libraries and functions: NumPy (`numpy.flip`)
- interpolation: Interpolation augmentation involves creating new samples by interpolating between existing data points, increasing the size and diversity of the dataset. / Python libraries and functions: SciPy (`scipy.interpolate.interp1d`)
- adding noise: Adding noise augmentation involves injecting artificial noise (e.g., Gaussian noise) into the sensor data, simulating real-world noise and improving the model's robustness. / Python libraries and functions: NumPy (`numpy.random.normal`)

## Data fusion

Data fusion combines accelerometer and gyroscope data in various ways to create a more comprehensive representation of the motion or activity. This can involve using raw data directly, computing the **Euclidean norm**, or applying sensor fusion techniques like the Kalman filter. / Python libraries and functions: NumPy (`numpy.linalg.norm`, raw data concatenation), filterpy (`filterpy.kalman.KalmanFilter` for Kalman filter implementation)

Euclidean norm of x, y and z axis of a sensor
- Libraray numpy.linalg.norm

# Proposed features

## Machine learning:

### Feature extraction (e.g. FFT)

- mean/variance/sd: Calculate the mean, variance, and standard deviation of each segment to represent the central tendency, dispersion, and variability of the signal values. These features provide insights into the overall characteristics of a given activity. / Python libraries and functions: NumPy (`numpy.mean`, `numpy.var`, `numpy.std`)
- entropy: Calculate the entropy of each segment to quantify the randomness or disorder in the data. Higher entropy values indicate more complexity or less predictability in the signal. / Python libraries and functions: SciPy (`scipy.stats.entropy`) or scikit-learn (`sklearn.metrics.cluster.entropy`)
- correlation: Calculate the correlation between different axes of the accelerometer and gyroscope data to quantify the degree to which the signals are related. This can help identify coordinated movements in multiple dimensions. / Python libraries and functions: NumPy (`numpy.corrcoef`) or Pandas (`pandas.DataFrame.corr`)
- Fast Fourier Transform (FFT): Compute the FFT coefficients of each segment to transform the time-domain signal into the frequency domain. This reveals the dominant frequencies and their magnitudes, which can be useful for differentiating between activities with distinct frequency patterns. / Python libraries and functions: NumPy (`numpy.fft.fft`, `numpy.fft.fftfreq`) or SciPy (`scipy.fft.fft`, `scipy.fft.fftfreq`)
- Wavelet Coefficients: Compute the wavelet coefficients of each segment using a wavelet transform. This transformation captures both time and frequency information, which allows for better representation of non-stationary signals commonly found in human activities. Wavelet coefficients can be used to extract relevant features for activity classification. / Python libraries and functions: PyWavelets (`pywt.wavedec`, `pywt.coeffs_to_array`, `pywt.array_to_coeffs`)

### Feature scaling and normalization

- min-max: Scale the features by transforming their values to a specific range, usually [0, 1]. It ensures that all features have equal importance during model training. / Python libraries and functions: scikit-learn (`sklearn.preprocessing.MinMaxScaler`)
- z-score normalization: Z-score normalization (also called standardization) scales the features by transforming their values to have a mean of 0 and a standard deviation of 1. It ensures that all features have equal importance during model training. / Python libraries and functions: scikit-learn (`sklearn.preprocessing.StandardScaler`)

### Feature selection (e.g. PCA)

Decompose a signal into it's base frequencies - similar approach to GML-MC3. Feature selection aims to identify the most relevant features from the original feature set, reducing dimensionality and computational costs while maintaining the predictive power of the model. / Python libraries and functions: scikit-learn (`sklearn.decomposition.PCA`, `sklearn.feature_selection.RFE`, `sklearn.feature_selection.SelectKBest`)

### Peak detection

- Detect peaks from a signal / Python libraries and functions: SciPy (`scipy.signal.find_peaks`)

## Deep learning:

### Spectrogram

A time-frequency-spectral map is a promising approach for activity recognition using Convolutional Neural Networks (CNNs). In this approach, you transform the raw accelerometer and gyroscope data into a time-frequency representation, such as spectrograms, which capture both time and frequency information. This representation provides richer information about the signal patterns related to different activities and allows CNNs to exploit the spatial and temporal dependencies in the data.

See insights in paper [Chen_2021](https://github.com/Sensor-Based-Activity-Recognition/docs/blob/main/research/Chen_2021.md#4-insights)

https://en.wikipedia.org/wiki/Spectrogram / Library: `scipy.signal`

Here's why time-frequency-spectral maps can be effective for CNNs:

1. Local patterns: CNNs are capable of capturing local patterns in the input data through their convolutional layers. Time-frequency representations, like spectrograms, preserve local information about time and frequency, which can be effectively learned by CNNs.
2. Hierarchical features: CNNs learn hierarchical features from the input data through multiple layers, starting from simple patterns to more complex ones. Time-frequency-spectral maps provide a suitable input format for CNNs to extract such hierarchical features and detect activity-specific patterns.
3. Robustness to noise: Time-frequency representations can reduce the impact of noise in raw sensor data, making it easier for CNNs to discern relevant patterns for activity recognition.
4. Data augmentation: Time-frequency-spectral maps can be augmented using techniques like time-shifting, frequency-shifting, or time-stretching to increase the diversity of the training data and improve the generalization capabilities of the CNN.

To use time-frequency-spectral maps for CNNs, follow these steps:

1. Transform the raw accelerometer and gyroscope data into time-frequency representations, such as spectrograms or scalograms, using techniques like Short-Time Fourier Transform (STFT) or Wavelet Transform.
2. Use the time-frequency-spectral maps as input to the CNN, treating them as image-like data (2D arrays).
3. Design the CNN architecture with multiple convolutional and pooling layers, followed by fully connected layers for classification.
4. Train the CNN using the time-frequency-spectral maps and evaluate its performance on a test dataset.
5. Fine-tune the CNN architecture, the choice of time-frequency representation, and other hyperparameters to optimize the activity recognition performance.

## Pipelines (ideas courtesy of GPT-4)

Certainly! Here's a list of different data pipelines that you can try by combining various preprocessing techniques in different ways. The **order** of techniques applied in each pipeline **is crucial**, as it may impact the overall performance of the activity recognition models.

### Pipeline 1: Basic Preprocessing

1. Time alignment
2. Resampling
3. Segmentation
4. Feature extraction
5. Feature scaling and normalization
6. Model training and evaluation

_Traditional ML models like k-NN, SVM, or Decision Trees may work well with this pipeline, as it focuses on basic preprocessing and feature extraction._

### Pipeline 2: Filtering and Smoothing

1. Time alignment
2. Resampling
3. Filtering (e.g., Butterworth filter)
4. Smoothing (e.g., moving average)
5. Segmentation
6. Feature extraction
7. Feature scaling and normalization
8. Model training and evaluation

_As the pipeline focuses on noise reduction, both traditional ML models and deep learning models like MLP or CNN can be trained and compared._

### Pipeline 3: Feature Selection

1. Time alignment
2. Resampling
3. Segmentation
4. Feature extraction
5. Feature scaling and normalization
6. Feature selection (e.g., PCA or RFE)
7. Model training and evaluation

_Traditional ML models, such as SVM, Decision Trees, or Logistic Regression, may benefit more from this pipeline, as feature selection can help reduce the dimensionality and improve model interpretability._

### Pipeline 4: Data Fusion and Augmentation

1. Time alignment
2. Resampling
3. Data fusion (e.g., Euclidean norm or sensor fusion)
4. Data augmentation (e.g., rotation or noise addition
5. Segmentation
6. Feature extraction
7. Feature scaling and normalization
8. Model training and evaluation

_Deep learning models, such as CNN, RNN, or TCN, might work well with this pipeline, as they can handle large amounts of data and capture complex patterns._

### Pipeline 5: Comprehensive Preprocessing

1. Time alignment
2. Resampling
3. Filtering (e.g., Butterworth filter)
4. Smoothing (e.g., moving average)
5. Data fusion (e.g., Euclidean norm or sensor fusion)
6. Data augmentation (e.g., rotation or noise addition)
7. Segmentation
8. Feature extraction
9. Feature scaling and normalization
10. Feature selection (e.g., PCA or RFE)
11. Model training and evaluation

_Both traditional ML and deep learning models can be trained and compared using this pipeline, as it combines multiple preprocessing techniques to optimize the input data._

### Pipeline 6: Frequency-domain Features

1. Time alignment
2. Resampling
3. Filtering (e.g., Butterworth filter)
4. Segmentation
5. Feature extraction (including frequency-domain features, e.g., FFT coefficients or wavelet coefficients)
6. Feature scaling and normalization
7. Model training and evaluation

_This pipeline focuses on frequency-domain features, which can be effective with traditional ML models like SVM or Decision Trees as well as deep learning models like MLP or CNN._

### Pipeline 7: Time-frequency-spectral Map for CNN

1. Time alignment: Align the time-stamps of accelerometer and gyroscope data when using multiple sensors or different sources.
2. Resampling: Resample the signals at a consistent sampling rate to make the data more uniform for further processing.
3. Filtering (optional): Apply filters like low-pass, high-pass, or band-pass filters to remove noise from the raw accelerometer and gyroscope data, if necessary.
4. Data fusion (optional): Combine accelerometer and gyroscope data in different ways, such as using the raw data directly, computing the Euclidean norm, or applying sensor fusion techniques (e.g., Kalman filter) to merge the data for more accurate activity recognition.
5. Time-frequency transformation: Transform the time-domain accelerometer and gyroscope data into time-frequency representations (e.g., spectrograms) using techniques like Short-Time Fourier Transform (STFT) or Wavelet Transform.
6. Data augmentation (optional): Enhance the training data by generating new examples through techniques like time-shifting, frequency-shifting, or time-stretching.
7. Segmentation: Divide the time-frequency-spectral maps into smaller, fixed-length segments or sliding windows, which capture the characteristics of different activities.
8. CNN input preparation: Format the segmented time-frequency-spectral maps as input data for the CNN, treating them as 2D arrays (image-like data).
9. Model training and evaluation: Train the CNN using the prepared time-frequency-spectral map data and evaluate its performance on a test dataset.
10. Fine-tuning: Optimize the CNN architecture, choice of time-frequency representation, and other hyperparameters to achieve the best activity recognition performance.
