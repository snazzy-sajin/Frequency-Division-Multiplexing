# Frequency Division Multiplexing


## AIM
To implement Frequency Division Multiplexing (FDM) for six different message signals using Scilab, generate the multiplexed signal, and perform demultiplexing to recover all the original message signals. The experiment also includes plotting the message signals, multiplexed signal, and demultiplexed signals.

## APPARATUS REQUIRED

1. Computer System
2. Scilab Software

## ALGORITHM

1. Set sampling frequency, time duration, and time vector.
2. Generate six message signals with different frequencies.
3. Assign six different carrier frequencies.
4. Perform DSB-SC modulation by multiplying each message with its carrier.
5. Add all modulated signals to form the multiplexed FDM signal.
6. For each channel, multiply the multiplexed signal with the same carrier (demodulation).
7. Apply a low-pass filter to extract the recovered message.
8. Plot message signals, multiplexed signal, and recovered s  ignals.

## THEORY

Frequency Division Multiplexing (FDM) is a technique in which multiple message signals are transmitted simultaneously over a single communication channel by assigning each signal a different carrier frequency. Each message modulates its own carrier, and all modulated signals are added to form the multiplexed signal. Since the carrier frequencies are well separated, the signals do not overlap in the frequency domain.

At the receiver, each signal is recovered by multiplying the multiplexed signal with the corresponding carrier (coherent demodulation) and passing it through a low-pass filter to extract the original baseband message. FDM is widely used in radio broadcasting, telephone systems, and cable TV.

## PROGRAM
```
clc; 
clear; 
close;

fs = 50000;
t = 0:1/fs:0.05;

m1 = 6.5*sin(2*%pi*499*t);
m2 = 6.6*sin(2*%pi*509*t);
m3 = 6.7*sin(2*%pi*519*t);
m4 = 6.8*sin(2*%pi*529*t);
m5 = 6.9*sin(2*%pi*539*t);
m6 = 7*sin(2*%pi*549*t);

c1 = cos(2*%pi*2000*t);
c2 = cos(2*%pi*4000*t);
c3 = cos(2*%pi*6000*t);
c4 = cos(2*%pi*8000*t);
c5 = cos(2*%pi*10000*t);
c6 = cos(2*%pi*12000*t);

s1 = m1 .* c1;
s2 = m2 .* c2;
s3 = m3 .* c3;
s4 = m4 .* c4;
s5 = m5 .* c5;
s6 = m6 .* c6;

fdm = s1 + s2 + s3 + s4 + s5 + s6;

r1 = fdm .* c1;
r2 = fdm .* c2;
r3 = fdm .* c3;
r4 = fdm .* c4;
r5 = fdm .* c5;
r6 = fdm .* c6;


cutoff_hz = 400;
norm_cutoff = cutoff_hz/(fs/2);

M = 101; 

[h, w] = wfir('lp', M, [norm_cutoff, 0], 'hm', 0);  

d1 = conv(r1, h, 'same');
d2 = conv(r2, h, 'same');
d3 = conv(r3, h, 'same');
d4 = conv(r4, h, 'same');
d5 = conv(r5, h, 'same');
d6 = conv(r6, h, 'same');

d1 = 2 * d1;
d2 = 2 * d2;
d3 = 2 * d3;
d4 = 2 * d4;
d5 = 2 * d5;
d6 = 2 * d6;

figure(1);
subplot(3,2,1); plot(t,m1); title("Message 1");
subplot(3,2,2); plot(t,m2); title("Message 2");
subplot(3,2,3); plot(t,m3); title("Message 3");
subplot(3,2,4); plot(t,m4); title("Message 4");
subplot(3,2,5); plot(t,m5); title("Message 5");
subplot(3,2,6); plot(t,m6); title("Message 6");

figure(2);
plot(t,fdm); title("Multiplexed FDM");

figure(3);
subplot(3,2,1); plot(t,d1); title("Demod 1");
subplot(3,2,2); plot(t,d2); title("Demod 2");
subplot(3,2,3); plot(t,d3); title("Demod 3");
subplot(3,2,4); plot(t,d4); title("Demod 4");
subplot(3,2,5); plot(t,d5); title("Demod 5");
subplot(3,2,6); plot(t,d6); title("Demod 6");
```

## OUTPUT WAVEFORM
<img width="1855" height="990" alt="FDM message signals" src="https://github.com/user-attachments/assets/e4f4c65d-1d31-43a5-9554-d9afc5f2836d" />

<img width="1838" height="970" alt="FDM modulated signal" src="https://github.com/user-attachments/assets/31a7a8a5-b1fc-4305-b8e0-6f35e2eeca6f" />

<img width="1839" height="979" alt="FDM Demodulated signals" src="https://github.com/user-attachments/assets/6ddaba2b-97e2-44b2-9ecd-401f8c16775f" />

## CALCULATION


## RESULT
Six different message signals were generated and modulated using FDM. All modulated signals were added to form a multiplexed FDM signal. Each message was successfully recovered using coherent demodulation followed by low-pass filtering. The plots confirmed accurate multiplexing and demultiplexing.
