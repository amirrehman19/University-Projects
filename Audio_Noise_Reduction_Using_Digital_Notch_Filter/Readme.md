# Noise Reduction in Audio Signal Using Digital Filtering

## Project Report

---

# 1. Problem Statement

Modern audio recordings often suffer from degradation due to unwanted electronic interference. The objective of this project is to enhance a noisy audio signal in which the desired voice signal is contaminated by high-frequency electronic noise.

The challenge is to design a filtering technique that removes the interference while preserving the natural characteristics of the speech signal.

### Goal

Reduce a **6 kHz interference tone** using a **digital notch filter** while maintaining the integrity of the speech spectrum.

---

# 2. Introduction

Digital filtering plays an important role in signal processing for improving the quality of audio recordings. By analyzing the characteristics of both the noise and the speech signal, it becomes possible to design filters that suppress specific unwanted frequency components.

A **notch filter** is particularly useful when the noise exists at a known frequency. It removes a very narrow frequency band while leaving the rest of the signal unaffected.

In this project, a **6 kHz narrowband interference** is removed using an **IIR notch filter implemented in MATLAB**. The effectiveness of the filtering process is evaluated using frequency spectrum analysis before and after filtering.

---

# 3. Theory and Background

## 3.1 Voice Frequency Range

Typical speech signals occupy the following frequency range:

• **300 Hz – 3400 Hz**

Most important speech information exists below **4 kHz**, which allows higher frequencies to be filtered without significantly affecting speech clarity.

---

## 3.2 Nature of Interference Noise

The noise present in the recording appears as a high-frequency tone around **6000 Hz**. This type of interference is commonly caused by:

• Electronic interference
• Hardware coupling
• Power supply noise
• Recording system artifacts

---

## 3.3 Notch Filtering

A **Notch Filter**, also known as a **Band-Stop Filter**, removes a very narrow frequency band while allowing the remaining frequencies to pass through.

### Advantages

1. Precisely removes a specific interfering frequency
2. Causes minimal distortion to the original signal
3. Simple and computationally efficient

### Filter Parameters Used

Noise Frequency: **6000 Hz**

Quality Factor (Q): **60**

The **Q factor** controls the sharpness of the notch. A higher value produces a narrower filter that removes only the unwanted frequency.

---

# 4. Methodology

The following procedure was used to reduce the noise in the audio signal:

1. Load the noisy audio file into MATLAB.
2. Identify the interference frequency (6 kHz).
3. Design an **IIR notch filter** using MATLAB’s `iirnotch()` function.
4. Apply **zero-phase filtering** using `filtfilt()` to avoid phase distortion.
5. Perform **frequency domain analysis** using Fast Fourier Transform (FFT).
6. Compare the spectrum before and after filtering.
7. Save and playback the cleaned audio signal.

---

# 5. MATLAB Code Explanation

## Workspace Preparation

**clear;**

Removes all variables from the workspace so the program starts with a clean environment.

**close all;**

Closes any previously opened figure windows.

**clc;**

Clears the command window.

---

## Loading the Audio File

`noisy_file = 'audio_with_noise.wav';`

Specifies the audio file to be processed.

`[noisy_voice, Fs] = audioread(noisy_file);`

Loads the audio signal.

• `noisy_voice` represents the audio data
• `Fs` represents the sampling rate

---

## Defining the Noise Frequency

`NOISE_FREQ = 6000;`

Defines the unwanted noise frequency at **6 kHz**.

---

## Frequency Normalization

`Wo = NOISE_FREQ / (Fs/2);`

MATLAB requires frequencies to be normalized between **0 and 1** relative to the Nyquist frequency.

---

## Quality Factor Selection

`Q = 60;`

The quality factor determines the width of the notch filter.

• High Q → narrow and precise filtering
• Low Q → wider frequency removal

---

## Notch Filter Design

`[b, a] = iirnotch(Wo, Wo/Q);`

Generates the filter coefficients used to remove the interference frequency.

---

## Applying the Filter

`cleaned_voice = filtfilt(b, a, noisy_voice);`

The `filtfilt()` function applies the filter forward and backward, resulting in **zero phase distortion** and preserving the natural sound of the voice.

---

## Frequency Domain Analysis

Fast Fourier Transform (FFT) is used to analyze the signal in the frequency domain.

`Y_noisy = fft(noisy_voice, N);`

Converts the noisy signal from the time domain into the frequency domain.

`P_noisy = abs(Y_noisy(1:N/2+1)/N);`

Extracts the magnitude spectrum of the positive frequencies.

The same process is applied to the filtered signal and the difference signal to observe the removed noise.

---

## Visualization

Several MATLAB plotting functions are used:

**subplot()** – divides the figure window into multiple plots
**plot()** – generates the frequency spectrum graphs
**xlabel() and ylabel()** – label the graph axes
**xlim()** – controls the displayed frequency range
**legend()** – identifies plotted signals
**sgtitle()** – adds an overall title for the figure

---

## Saving the Cleaned Audio

`audiowrite(output_file, cleaned_voice, Fs);`

Stores the filtered audio signal as a new `.wav` file.

The program can also playback the original and cleaned audio signals to allow direct comparison.

---

# 6. Results and Discussion

## Spectral Analysis

Three plots were used to evaluate the effectiveness of the filtering process.

### Before Filtering

A strong peak appears at **6000 Hz**, indicating the presence of interference noise.

### After Filtering

The peak at **6 kHz** is significantly reduced, confirming successful noise suppression.

### Difference Spectrum

The difference signal represents the removed noise component, demonstrating that the filter selectively eliminated the interference frequency.

---

## Audio Quality Observation

• The cleaned audio shows significantly reduced high-frequency noise.
• Speech clarity remains preserved.
• The filtering process introduces minimal distortion.

---

# 7. Conclusion

The digital notch filter effectively removed the **6 kHz interference noise** from the audio signal while preserving the important speech components.

This experiment demonstrates the effectiveness of **frequency-selective digital filtering** for improving audio quality in practical signal processing applications.

Future improvements may include the use of **adaptive filtering**, **spectral subtraction**, or **machine learning based noise reduction techniques** to handle more complex noise environments.

---

# 8. References

Ahlstrom, M.L. and Tompkins, W.J. (1985).
Digital Filters for Real-Time ECG Signal Processing Using Microprocessors. IEEE Transactions on Biomedical Engineering.

Chicharo, J.F. and Ng, T.S. (1990).
Gradient-Based Adaptive IIR Notch Filtering for Frequency Estimation. IEEE Transactions on Acoustics, Speech, and Signal Processing.

Mojiri, M., Karimi-Ghartemani, M. and Bakhshai, A. (2007).
Time-Domain Signal Analysis Using Adaptive Notch Filter. IEEE Transactions on Signal Processing.
