# Proposed preprocessing

## Resampling

Resample the signals at a consistent sampling rate, accounting for differences in sensor sample rates to make the data more uniform for training. Resampling can involve upsampling (increasing the number of samples) or downsampling (decreasing the number of samples), depending on the desired target sampling rate.

Python libraries and functions: Pandas (`pandas.DataFrame.resample`, `pandas.DataFrame.interpolate`) and SciPy (`scipy.signal.resample`, `scipy.signal.resample_poly`)

## Filtering

Apply filters like low-pass, high-pass, or band-pass filters to remove noise from the raw accelerometer and gyroscope data. Common filters include Butterworth or Chebyshev filters.

- low-pass/high-pass: Low/high-pass filters allow low/high-frequency signals to pass through while attenuating high/low-frequency signals, effectively reducing high/low-frequency noise in the data. / Python libraries and functions: SciPy (`scipy.signal.butter`, `scipy.signal.lfilter`)
- Butterworth: Butterworth filters are a type of frequency-domain filter that provide a smooth frequency response with no ripples. These filters are designed to have a maximally flat frequency response in the passband and a sharp roll-off in the stopband. / Python libraries and functions: SciPy (`scipy.signal.butter`, `scipy.signal.lfilter`, `scipy.signal.filtfilt`)
- Chebyshev filters: Chebyshev filters are a type of frequency-domain filter characterized by their sharper roll-off compared to Butterworth filters but with ripples in the passband or stopband. There are two types of Chebyshev filters: Type I (ripples in the passband) and Type II (ripples in the stopband). These filters provide a faster transition between the passband and stopband at the expense of ripples. / Python libraries and functions: SciPy (`scipy.signal.cheby1`, `scipy.signal.cheby2`, `scipy.signal.lfilter`, `scipy.signal.filtfilt`)

## L2 Norm

Euclidean norm of x, y and z axis of a sensor
- Libraray numpy.linalg.norm

# Proposed features

## Machine learning:

### FFT / PCA

Decompose a signal into its base frequencies
- Similar approach to GML-MC3
- Library: scipy.fft, sklearn.decomposition.PCA

### Peak detection

Detect peaks from a signal
- Library: scipy.signal.find_peaks

### Mean

Mean value of an axis
- numpy.mean

### Standard deviation

Standard deviation of an axis
- numpy.std

## Deep learning:

### Spectrogram

A spectrogram is a visual representation of frequency with respect to time.
- https://en.wikipedia.org/wiki/Spectrogram
- Library: scipy.signal
