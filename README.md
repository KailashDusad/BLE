# Secure Voice Communication System over Bluetooth Low Energy

## Overview
This project implements a real-time encrypted voice transmission system using Bluetooth Low Energy (BLE) protocol. Two mobile devices communicate with each other, where one device encrypts audio signals using spectrum scrambling or noise masking techniques, transmits over BLE, and the receiving device decrypts and plays the audio. The project demonstrates signal processing, wireless communication, and embedded system design.

## Project Features

- **Dual Encryption Methods**: 
  - Method 1: Frequency-domain spectrum scrambling for audio obfuscation
  - Method 2: Additive noise masking using pure-tone injection
- **Real-Time Signal Processing**: Bidirectional encryption/decryption pipeline with minimal latency
- **Bluetooth Low Energy (BLE)**: Wireless communication protocol for IoT applications
- **Simulink-Based Implementation**: Hardware-software co-design for reliable system operation

## System Architecture

### Transmitter (Phone A)
```
Voice Input
    ↓
Encryption Module
    ↓
├── Method 1: Spectrum Scrambling
└── Method 2: Noise Masking
    ↓
BLE Transmission
```

### Receiver (Phone B)
```
BLE Reception
    ↓
Decryption Module
    ↓
├── Play Encrypted Audio
├── Play Decrypted Audio (Method 1: Spectrum Scrambling)
└── Play Decrypted Audio (Method 2: Noise Masking)
    ↓
Audio Playback
```


## Software Requirements

- **Simulink**: For application development and simulation
- **BLE Stack**: Standard Bluetooth Low Energy protocol implementation
- **Signal Processing Library**: MATLAB, DSP, or equivalent for filtering and transformation

## Encryption Methods

### Spectrum Scrambling (Frequency-Domain Encryption)
Rearranges frequency components of audio signals to make them unintelligible

** **
1. Apply Fast Fourier Transform (FFT) to audio signal
2. Scramble frequency bins using a pseudo-random permutation
3. Apply Inverse FFT to obtain encrypted time-domain signal
4. Transmit encrypted signal via BLE

**Decryption:**
1. Apply FFT to received encrypted signal
2. Apply inverse permutation (using same key) to unscramble frequency bins
3. Apply Inverse FFT to recover original audio


### Additive Noise Masking (Time-Domain Encryption)
Overlays pure-tone noise signals on audio to mask intelligibility

** **
1. Generate pure-tone noise signals at predefined frequencies
2. Add noise signals to original audio: Encrypted = Audio + Noise
3. Transmit encrypted signal via BLE

**Decryption:**
1. Generate identical noise signals using shared key
2. Subtract noise from received signal: Audio = Encrypted - Noise
3. Apply optional filtering to remove residual noise


### Signal Processing Pipeline

```
Input Audio
    ↓
[Sample Buffering]
    ↓
[Encryption Algorithm Selection]
    ↓
├─ Method 1: FFT → Scrambling → IFFT
└─ Method 2: Noise Generation → Addition
    ↓
[BLE Packetization]
    ↓
[Wireless Transmission]
    ↓
[Reception & Buffering]
    ↓
[BLE Depacketization]
    ↓
[Decryption]
    ↓
├─ Method 1: FFT → Unscrambling → IFFT
└─ Method 2: Noise Generation → Subtraction
    ↓
[Audio Playback / UI Display]
```
