# Design-of-FIR-Filters-using-rectangular-window
DESIGN OF LOW PASS FIR DIGITAL FILTER
AIM:
To generate design of low pass FIR digital filter using SCILAB

APPARATUS REQUIRED:
PC Installed with SCILAB

PROGRAM
clc;
clear;
close;

// Filter specifications
N = 25;              // Filter order (changed from 21)
wc = 0.4 * %pi;      // Cutoff frequency in radians (changed from 0.5π)
alpha = (N - 1) / 2; // Midpoint of filter

// Ideal impulse response (sinc function)
hd = zeros(1, N);
for n = 0:N-1
    if (n - alpha) == 0 then
        hd(n+1) = wc / %pi;
    else
        hd(n+1) = sin(wc * (n - alpha)) / (%pi * (n - alpha));
    end
end

// Rectangular window
w = ones(1, N);

// Apply window
h = hd .* w;

// Compute frequency response using fft with padding
Nfft = 1024;              // Increased FFT size for smoother plot
H = fft(h, -1);           
H = [H, zeros(1, Nfft - N)];
H = fft(H, -1);           

// Frequency vector (normalized)
f = (0:Nfft-1) / Nfft;

// Plot magnitude response
plot(f, abs(H));
xlabel('Normalized Frequency');
ylabel('Magnitude');
title('Low Pass FIR Filter using Rectangular Window');
xgrid();

// Display coefficients
disp("Filter Coefficients:");
disp(h);



OUTPUT


<img width="1917" height="1078" alt="image" src="https://github.com/user-attachments/assets/092ed8cd-51ca-459e-a6e1-15bafd53fd84" />




RESULT
The Low Pass FIR digital filter was successfully designed using the rectangular window method, and its impulse and frequency responses were plotted and observed to exhibit proper low-pass characteristics.
