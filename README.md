# SIMULATION-OF-FREQUENCY-DIVISION-MULTIPLEXING-FDM-AND-DEMULTIPLEXING-USING-SCILAB
## AIM:

To write a Scilab program to simulate frequency division multiplexing and demultiplexing for six different frequencies, and verify the demultiplexed outputs correspond to the original signals.

## EQUIPMENTS Needed

Computer with Scilab installed

## ALGORITHM

1.Define six different frequencies to generate six sine wave signals.
2.Generate the time vector to represent time samples.
3.Compute six sine signals for each frequency over the time vector.
4.Frequency Division Multiplexing: sum all six sine signals to make one multiplexed signal.
5.Frequency Division Demultiplexing: for each frequency, multiply the multiplexed signal by a sine wave of that frequency (mixing), then apply a lowpass filter to extract the baseband (original) signal.
6.Plot original signals, multiplexed signal, and demultiplexed signals for verification.

## PROCEDURE

Refer Algorithms and write code for the experiment.
• Open SCILAB in System
• Type your code in New Editor
• Save the file
• Execute the code
• If any Error, correct it in code and execute again
• Verify the generated waveform using Tabulation and Model Waveform

## PROGRAM
```
Fs = 56300;
t = 0:1/Fs:0.02;

m1 = sin(2*%pi*200*t);
m2 = sin(2*%pi*300*t);
m3 = sin(2*%pi*400*t);
m4 = sin(2*%pi*500*t);
m5 = sin(2*%pi*600*t);
m6 = sin(2*%pi*700*t);

c1 = 3000; c2 = 6000; c3 = 9000; c4 = 12000; c5 = 15000; c6 = 18000;

carrier1 = cos(2*%pi*c1*t);
carrier2 = cos(2*%pi*c2*t);
carrier3 = cos(2*%pi*c3*t);
carrier4 = cos(2*%pi*c4*t);
carrier5 = cos(2*%pi*c5*t);
carrier6 = cos(2*%pi*c6*t);

s1 = m1 .* carrier1;
s2 = m2 .* carrier2;
s3 = m3 .* carrier3;
s4 = m4 .* carrier4;
s5 = m5 .* carrier5;
s6 = m6 .* carrier6;

s_total = s1 + s2 + s3 + s4 + s5 + s6;

// Demultiplex: multiply by carriers to shift each band back to baseband
r1 = s_total .* carrier1;
r2 = s_total .* carrier2;
r3 = s_total .* carrier3;
r4 = s_total .* carrier4;
r5 = s_total .* carrier5;
r6 = s_total .* carrier6;

// Simple FFT-based ideal low-pass filter (avoids butter/toolbox issues)
function y = ideal_lowpass_fft(x, Fs, fc)
    N = length(x);
    X = fft(x);
    f = Fs*(0:N-1)/N;
    mask = (f <= fc) | (f >= Fs-fc);
    Y = X .* mask;
    y = real(ifft(Y));
endfunction

fc = 1000;
dm1 = ideal_lowpass_fft(r1, Fs, fc);
dm2 = ideal_lowpass_fft(r2, Fs, fc);
dm3 = ideal_lowpass_fft(r3, Fs, fc);
dm4 = ideal_lowpass_fft(r4, Fs, fc);
dm5 = ideal_lowpass_fft(r5, Fs, fc);
dm6 = ideal_lowpass_fft(r6, Fs, fc);

figure(1);
subplot(3,2,1); plot(t,m1); title("Message Signal 1");
subplot(3,2,2); plot(t,m2); title("Message Signal 2");
subplot(3,2,3); plot(t,m3); title("Message Signal 3");
subplot(3,2,4); plot(t,m4); title("Message Signal 4");
subplot(3,2,5); plot(t,m5); title("Message Signal 5");
subplot(3,2,6); plot(t,m6); title("Message Signal 6");

figure(2);
plot(t, s_total); title("Multiplexed FDM Signal");

figure(3);
subplot(3,2,1); plot(t,dm1); title("Recovered Signal 1");
subplot(3,2,2); plot(t,dm2); title("Recovered Signal 2");
subplot(3,2,3); plot(t,dm3); title("Recovered Signal 3");
subplot(3,2,4); plot(t,dm4); title("Recovered Signal 4");
subplot(3,2,5); plot(t,dm5); title("Recovered Signal 5");
subplot(3,2,6); plot(t,dm6); title("Recovered Signal 6");
```

## OUTPUT:

<img width="757" height="727" alt="image" src="https://github.com/user-attachments/assets/1e1946e9-eb2b-48fb-9d38-d19adb8e97d7" />
<img width="759" height="722" alt="image" src="https://github.com/user-attachments/assets/a624f06b-bde1-470b-b3d6-3c7f023d09b6" />
<img width="761" height="721" alt="image" src="https://github.com/user-attachments/assets/039343e4-2bdf-4a7c-a72f-6f91010d181d" />



## RESULT:
Thus,Frequency division multiplexing is done experimentally and output is verified
