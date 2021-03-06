## Task 1-2 Signal Processing II
**Name:** Tianyi Yu  
**Degree:** BA  
**ID:** 20550150

### Problem 1
---
##### (a)
![](Prob1a.jpg)

##### (b)

```matlab
close all
clearvars

A = 1;
a = 1;
t = -a*2:0.01:a*2;

f= A*(a>abs(t)); 
g= A*(a>abs(t)); 

% convolution
m=length(f);
n=length(g);
X=[f,zeros(1,n)];
H=[g,zeros(1,m)];
for i=1:n+m-1
    Y(i)=0;
    for j=1:m
        if(i-j+1>0)
            Y(i)=Y(i)+X(j)*H(i-j+1);
        else
        end
    end
end

% plot results
figure;
subplot(3,1,1); plot(t,f, '-r'); xlabel('t');
ylabel('f(t)'); grid on;

subplot(3,1,2); plot(t,g, '-r');
xlabel('t'); ylabel('g(t)'); grid on;

axis=(0:length(Y)-1)*(t(2)-t(1));
subplot(3,1,3); plot(axis,Y,'-r');
ylabel('Y(t)'); grid on;
title('Convolution of Two Signals without conv function');
```
![](Prob1b.jpg)

##### (c)

```matlab
close all
clearvars

A = 1;
a = 1;
t = -a*2:0.01:a*2;

f = A*(a>abs(t)); 

subplot(311); plot(t,f,'-r');hold on;
title('f(t)'); grid on; hold off;

g = A*(a>abs(t)); 

subplot(312); plot(t,f,'-r');hold on;
title('g(t)'); grid on; hold off;

% Convolution

y = conv(f,g,'full');
axis=(0:length(y)-1)*(t(2)-t(1));

subplot(313); plot(axis,y,'-r');hold on;
title('Convolution of f(t) and g(t)'); grid on; hold off;
```
![](Prob1c.jpg)

### Problem 2
---
##### (a)
![](Prob2a.jpg)

##### (b)
![](Prob2b.jpg)

##### (c)
![](Prob2c.jpg)


### Problem 3
---
##### (a)
The relationship means that frequencies at multiples of the sampling rate ( ω = 2πn/T) look like they are constant.

##### (b)
The relationship means that if we sample too slowly, the shifted spectrums overlap. High frequency components are “folded” back into the spectrum. If the sampling frequency is an integer multiple of Cn, then the sampling result would remain the same.

##### (c)
The first one it the Fourier transform of an impulse train, the second one is the Fourier transform of a discrete sequence.

### Problem 4
---
##### (a)

```matlab
clear; clc ; close all; 

a1 = 2;
b1 = 2;
c1 = 2;
f11 = 3;
f21 = 6;

a2 = 0.3;
b2 = 10;
c2 = 3;
f12 = 5;
f22 = 8;

ncycle = 5;
fs = 50;
t = 0:1/fs:ncycle;

z1 = exp(-a1*abs(t)).*(b1*cos(2*pi*f11*t)+c1*cos(2*pi*f21*t));

z2 = exp(-a2*abs(t)).*(b2*cos(2*pi*f12*t)+c2*cos(2*pi*f22*t));

plot(t,z1,'ob',t,z1,':b'); hold on;
plot(t,z2,'or', t, z2, ':r'); hold off;
grid on; xlim([0 1.5]);
ylabel('Amplitude'); 
xlabel('Time (sec)'); 
legend('z1','z1','z2','z2');
title('Discrete Signals z1 and z2');
```
![](Prob4a.jpg)

##### (b)

```matlab
fz1 = fft(z1);
fz2 = fft(z2);

n = length(fz1);

P1 = abs(fz1/n);
p1 = P1(1:n/2+1);
p1(2:end-1) = 2*p1(2:end-1);

P2 = abs(fz2/n);
p2 = P2(1:n/2+1);
p2(2:end-1) = 2*p2(2:end-1);

f = fs*(0:(n/2))/n;


plot(f,p1,':b'); hold on;
plot(f,p2,':r'); hold off;
grid on;
xlabel('Frequency (in hertz)');
legend('z1','z2');
title('FFT of z1 and z2 in Frequency Domain');
```
![](Prob4b.jpg)

##### (c)
The frequency curve for z2 is thinner comparing to that for z1. In the time domain graph plotted in (a), z2 has a higher amplitude. Considering the two sets of coefficients, z2 has a relatively small exponential part but higher frequencies and amplitudes for the cosine part, which makes it narrow in the frequency domain.


### Problem 5
---
##### (a)
```matlab
clear; clc; close all; 

a1 = 3;
a2 = 10;
a3 = 5;

ncycle = 3;
fs = 500;
t = 0:1/fs:ncycle;

y1 = a1*sin(2*pi*(25)*t)+a2*sin(2*pi*(75)*t)+a3*sin(2*pi*(125)*t);

plot(t,y1,'ob',t,y1,':b'); 
grid on; xlim([0 0.1]);
ylabel('Amplitude'); 
xlabel('Time (sec)'); 
title('Discrete Signal y1 (fs=500Hz)');
```
![](Prob5a.jpg)

##### (b)
```matlab
fy1 = fft(y1);

n = length(fy1);

P1 = abs(fy1/n);
p1 = P1(1:n/2+1);
p1(2:end-1) = 2*p1(2:end-1);

f = fs*(0:(n/2))/n;

plot(f,p1,':b');
grid on;
xlabel('Frequency (in hertz)');
title('FFT of y1 in Frequency Domain');
```
![](Prob5b.jpg)

##### (c)
```matlab
clear; clc;

a1 = 3;
a2 = 10;
a3 = 5;

ncycle = 3;
fs = 100;
t = 0:1/fs:ncycle;

y1 = a1*sin(2*pi*(25)*t)+a2*sin(2*pi*(75)*t)+a3*sin(2*pi*(125)*t);

plot(t,y1,'ob',t,y1,':b'); 
grid on; xlim([0 0.1]);
ylabel('Amplitude'); 
xlabel('Time (sec)'); 
title('Discrete Signal y1 (fs=100Hz)');
```
![](Prob5c.jpg)

##### (d)
```matlab
fy1 = fft(y1);

n = length(fy1);

P1 = abs(fy1/n);
p1 = P1(1:n/2+1);
p1(2:end-1) = 2*p1(2:end-1);

f = fs*(0:(n/2))/n;

plot(f,p1,':b');
grid on;
xlabel('Frequency (in hertz)');
title('FFT of y1 in Frequency Domain');
```
![](Prob5d.jpg)

##### (e)
![](Prob5e.jpg)
The frequencies contained in the original signal cannot be extracted since the graph only has one peak. The original equation has three components with different frequencies. The nyquist frequency is 100/2 = 50 Hz and is smaller than 75 and 125.In this case, the frequencies cannot be extracted.

##### (f)
![](Prob5f.jpg)
The frequencies cannot be extracted from the graph. The nyquist frequency is 105/2 = 52.5 Hz and is smaller than 75 and 125. In this case, the 75 Hz and 125 Hz parts cannot be observed on the graph. The peaks at 20 Hz and 30 Hz are the noises generated by the 25 Hz peak as 105 is not integer multiple of 25.

##### (g)
![](Prob5g.jpg)
All three frequencies can be extracted from the graph. The three peaks appear in the graph are at 25 Hz, 75 Hz and 125 Hz, which match the frequencies of the original function. This is because the sampling frequency is 251 Hz and the Nyquist frequency is 125.5 Hz and is greater than all three frequencies in the original signal.

### Problem 6

##### (a)
```matlab
clear; clc; close all;

load('vib_data1.mat');
plot(time,zvib,':r'); grid on;
xlabel('Time');
ylabel('Acceleration Signal');

fy1 = fft(zvib);

n = length(fy1);

P1 = abs(fy1/n);
p1 = P1(1:n/2+1);
p1(2:end-1) = 2*p1(2:end-1);

f = 1000*(0:(n/2))/n;

plot(f,p1,':b');
grid on;
xlabel('Frequency (in hertz)');
title('FFT of Acceleration Signal in Frequency Domain');
```
![](Prob6a1.jpg)
![](Prob6a2.jpg)

The frequency of the wave is 200.

##### (b)
```matlab
clear; clc;

load('vib_data2.mat');
plot(time,zvib,':b'); grid on;
xlabel('Time');
ylabel('Acceleration Signal');

fy1 = fft(zvib);

n = length(fy1);

P1 = abs(fy1/n);
p1 = P1(1:n/2+1);
p1(2:end-1) = 2*p1(2:end-1);

f = 1000*(0:(n/2))/n;

plot(f,p1,':b');
grid on;
xlabel('Frequency (in hertz)');
title('FFT of Acceleration Signal in Frequency Domain');
```
![](Prob6b1.jpg)
![](Prob6b2.jpg)

The frequency of the wave is 150.
