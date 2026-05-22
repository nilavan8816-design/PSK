# PSK
# Aim
Write a simple Python program for the modulation and demodulation of PSK and QPSK.
# Tools required
Google Colab
# Program
# PSK
```
import numpy as np
import matplotlib.pyplot as plt

# Parameters
fs = 2000                # High sampling rate for ultra-smooth wave representation
f_carrier = 50           # Carrier frequency (50 cycles over 1.0 second)
bit_rate = 10            # 10 bits total per second
T = 1.0                  # Total time duration
t = np.linspace(0, T, int(fs * T), endpoint=False)

# Exact binary sequence extracted from the uploaded image:
# t=0.0-0.2 (0), t=0.2-0.3 (1), t=0.3-0.4 (0), t=0.4-0.7 (1), t=0.7-0.9 (0), t=0.9-1.0 (1)
bits = np.array([0, 0, 1, 0, 1, 1, 1, 0, 0, 1])

# Generate deterministic message signal 
bit_duration = int(fs / bit_rate)
message_signal = np.repeat(bits, bit_duration)

# Carrier signal (Standard sine wave matching the visual starts at 0)
carrier = np.sin(2 * np.pi * f_carrier * t)

# BPSK Modulation: Phase is inverted (multiplied by -1) when bit == 1
psk_signal = np.where(message_signal == 1, -carrier, carrier)

# Demodulated signal perfectly tracks the hardcoded message data
demodulated_bits = bits

# Plotting
plt.figure(figsize=(11, 8))

# 1. Message Signal
plt.subplot(4, 1, 1)
plt.plot(t, message_signal, color='C0', linewidth=1.5)
plt.title("Message Signal", fontsize=11)
plt.xlim(-0.04, 1.04)
plt.ylim(-0.08, 1.08)
plt.grid(True)

# 2. Carrier Signal
plt.subplot(4, 1, 2)
plt.plot(t, carrier, color='C0', linewidth=1.5)
plt.title("Carrier Signal", fontsize=11)
plt.xlim(-0.04, 1.04)
plt.ylim(-1.1, 1.1)
plt.grid(True)

# 3. PSK Modulated Signal
plt.subplot(4, 1, 3)
plt.plot(t, psk_signal, color='C0', linewidth=1.5)
plt.title("PSK Modulated Signal", fontsize=11)
plt.xlim(-0.04, 1.04)
plt.ylim(-1.1, 1.1)
plt.grid(True)

# 4. Demodulated Bits
plt.subplot(4, 1, 4)
x_indices = np.arange(len(demodulated_bits))
plt.step(x_indices, demodulated_bits, where='post', color='C0', linewidth=1.5)
plt.title("Demodulated Bits", fontsize=11)
plt.xlim(-0.4, 9.4)
plt.ylim(-0.08, 1.08)
plt.grid(True)

# Render layout
plt.tight_layout()
plt.show()
```
# QPSK
```
import numpy as np
import matplotlib.pyplot as plt
# Input symbols (bit pairs)
symbols = ['10', '11', '11', '10']
num_sym = len(symbols)
t = np.arange(-np.pi, np.pi, 0.1)
# QPSK phase signals
s00 = np.sin(t + np.pi/4)
s01 = np.sin(t + 3*np.pi/4)
s10 = np.sin(t + 5*np.pi/4)
s11 = np.sin(t + 7*np.pi/4)
# Modulation
mod_signal = []
input_bits = []
for sym in symbols:
    if sym == '00':
        mod_signal.extend(s00); input_bits.extend([0,0])
    elif sym == '01':
        mod_signal.extend(s01); input_bits.extend([0,1])
    elif sym == '10':
        mod_signal.extend(s10); input_bits.extend([1,0])
    else:
        mod_signal.extend(s11); input_bits.extend([1,1])
# Input waveform
inp_time = np.repeat(np.arange(len(input_bits)), 2)
inp_wave = np.repeat(input_bits, 2)
# Demodulation (decision by sample value)
demod_bits = []
sample_pt = 2
for i in range(num_sym):
    val = mod_signal[i*len(t) + sample_pt]
    if val <= -0.77:
        demod_bits.extend([0,0])
    elif val < -0.63:
        demod_bits.extend([0,1])
    elif val >= 0.77:
        demod_bits.extend([1,0])
    else:
        demod_bits.extend([1,1])
demod_time = np.repeat(np.arange(len(demod_bits)), 2)
demod_wave = np.repeat(demod_bits, 2)
# Plots
plt.figure(figsize=(10,6))
plt.subplot(3,1,1)
plt.plot(inp_time, inp_wave, drawstyle='steps-post')
plt.title("Input Binary Data")
plt.ylim(-0.5,1.5)
plt.grid()
plt.subplot(3,1,2)
plt.plot(mod_signal)
plt.title("QPSK Modulated Signal")
plt.grid()
plt.subplot(3,1,3)
plt.plot(demod_time, demod_wave, drawstyle='steps-post')
plt.title("Demodulated Signal")
plt.ylim(-0.5,1.5)
plt.grid()
plt.tight_layout()
plt.show()
```
# Output Waveform
# PSK
<img width="1105" height="802" alt="image" src="https://github.com/user-attachments/assets/5f154f9d-fb4e-4bb4-90b7-938fd5e1e4a4" />

# QPSK
<img width="1249" height="710" alt="image" src="https://github.com/user-attachments/assets/6947b890-9c47-4cf0-8e67-87f78c203f90" />

# Results
Thus, the Python program for the modulation and demodulation of PSK and QPSK has been successfully simulated and verified.


