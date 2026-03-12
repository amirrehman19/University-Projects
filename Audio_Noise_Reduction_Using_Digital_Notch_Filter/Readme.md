# 🔊 Noise Reduction in Audio Signal Using Digital Filtering

> 🎙️ *Eliminating narrowband interference while preserving the natural clarity of speech — through precision digital filter design.*

[![Domain](https://img.shields.io/badge/Domain-Signal%20Processing-blue?style=flat-square)]()
[![Tool](https://img.shields.io/badge/Tool-MATLAB-orange?style=flat-square&logo=mathworks)]()
[![Filter](https://img.shields.io/badge/Filter-IIR%20Notch-purple?style=flat-square)]()
[![Noise](https://img.shields.io/badge/Noise%20Frequency-6%20kHz-red?style=flat-square)]()
[![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)]()

---

## 📌 Problem Statement

Modern audio recordings often suffer from degradation caused by unwanted electronic interference. This project targets a **6 kHz high-frequency tone** contaminating a voice signal and removes it using a precisely tuned **IIR Notch Filter** in MATLAB — without affecting the speech spectrum.

> 🎯 **Goal:** Remove a 6 kHz interference tone using a digital notch filter while maintaining full speech integrity.

---

## 📖 Introduction

Digital filtering is a core technique in signal processing for improving audio quality. A **Notch Filter (Band-Stop Filter)** is ideal when noise exists at a known frequency — it removes a very narrow band while leaving the rest of the signal completely unaffected.

---

## 🧠 Theory & Background

### 🎙️ Voice Frequency Range

| Parameter | Value |
|-----------|-------|
| Speech Band | 300 Hz – 3400 Hz |
| Safe Filter Zone | Above 4 kHz |
| Interference Frequency | **6000 Hz** |

> Since most critical speech content exists below 4 kHz, the 6 kHz region can be safely targeted without affecting intelligibility.

### 🔴 Nature of Interference

The 6 kHz noise is a narrowband tone commonly caused by:
- ⚡ Electronic interference
- 🔌 Hardware coupling
- 🔋 Power supply noise
- 🎙️ Recording system artifacts

### 🔧 Notch Filter Parameters

| Parameter | Value |
|-----------|-------|
| Filter Type | IIR Notch (Band-Stop) |
| Noise Frequency | 6000 Hz |
| Quality Factor (Q) | **60** |

> 💡 A **high Q = 60** produces an extremely narrow notch — surgically removing only the interference frequency with negligible impact on neighboring content.

---

## ⚙️ Methodology

```
┌──────────────────────────────────────────────────────────┐
│                   PROCESSING PIPELINE                    │
│                                                          │
│  Load Audio → Identify 6kHz Noise → Design IIR Filter   │
│       ↓                                                  │
│  Apply filtfilt() → FFT Analysis → Compare Spectra       │
│       ↓                                                  │
│  Save Cleaned Audio → Playback Comparison                │
└──────────────────────────────────────────────────────────┘
```

---

## 💻 MATLAB Code Breakdown

### Workspace Setup
```matlab
clear;       % Clean workspace
close all;   % Close all figures
clc;         % Clear command window
```

### Load & Define Parameters
```matlab
[noisy_voice, Fs] = audioread('audio_with_noise.wav');
NOISE_FREQ = 6000;           % Target interference frequency
Wo = NOISE_FREQ / (Fs/2);   % Normalize to Nyquist frequency
Q  = 60;                     % Quality factor — narrow notch
```

### Design & Apply Filter
```matlab
[b, a] = iirnotch(Wo, Wo/Q);              % Design notch filter
cleaned_voice = filtfilt(b, a, noisy_voice); % Zero-phase filtering
```

### Frequency Analysis
```matlab
Y_noisy   = fft(noisy_voice, N);
P_noisy   = abs(Y_noisy(1:N/2+1) / N);   % Magnitude spectrum
```

### Save Output
```matlab
audiowrite('cleaned_audio.wav', cleaned_voice, Fs);
```

---

## 📊 Key MATLAB Functions

| Function | Purpose |
|----------|---------|
| `audioread()` | Load noisy .wav audio file |
| `iirnotch()` | Design IIR notch filter coefficients |
| `filtfilt()` | Apply zero-phase forward-backward filtering |
| `fft()` | Convert signal to frequency domain |
| `abs()` | Extract magnitude spectrum |
| `audiowrite()` | Save cleaned output as .wav |
| `subplot()` / `plot()` | Visualize spectra before & after |

---

## 📈 Results

| Measurement | Before Filtering | After Filtering |
|------------|-----------------|----------------|
| 6 kHz Spike | 🔴 Strong peak visible | ✅ Peak eliminated |
| Speech Band (300–3400 Hz) | ✅ Intact | ✅ Fully preserved |
| Phase Distortion | — | ✅ Zero (`filtfilt` used) |
| Audio Clarity | ⚠️ Noisy | ✅ Clean & natural |

### Spectral Plots Generated:
- 📉 **Before Filtering** — strong 6 kHz spike clearly visible
- 📉 **After Filtering** — spike eliminated, speech band untouched
- 📉 **Difference Spectrum** — isolated removed noise component

---

## ✅ Conclusion

The IIR notch filter effectively **removed the 6 kHz interference** while fully preserving the speech signal. This experiment validates the power of frequency-selective digital filtering for practical audio enhancement applications.

> 🔮 *Future improvements may include adaptive filtering, spectral subtraction, or ML-based noise reduction for complex noise environments.*

---

## 📚 References

- Ahlstrom & Tompkins (1985) — *Digital Filters for Real-Time ECG Signal Processing*, IEEE
- Chicharo & Ng (1990) — *Gradient-Based Adaptive IIR Notch Filtering*, IEEE
- Mojiri et al. (2007) — *Time-Domain Signal Analysis Using Adaptive Notch Filter*, IEEE

---

## 🛠️ Tools & Technologies

`MATLAB` · `IIR Notch Filter` · `FFT Analysis` · `filtfilt()` · `Digital Signal Processing` · `Audio Processing`

---

## 👤 About

| | |
|-|---|
| 👨‍💻 **Student** | Amir Rehman |
| 🏛️ **Institution** | NUST — PNEC, Karachi |
| 🌐 **GitHub** | [@amirrehman19](https://github.com/amirrehman19) |

---

⬅️ *Back to [University Projects Portfolio](../README.md)*
