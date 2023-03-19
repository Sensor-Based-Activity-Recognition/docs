# Proposed preprocessing

## Resampling

Resampling of a signal
- Library: pandas.DataFrame.resample, scipy.signal.resample

## Filtering

Cut off frequencies higher or lower than a certain threshold
- Librariy: scipy.signal.butter 

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