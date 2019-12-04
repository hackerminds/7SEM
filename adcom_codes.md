## VECTOR ERRORS (FIX)
```
%Add these 3 line in all codes
clc
clear all
close all
```
## MANCHESTER LINE CODE(NEW)
```matlab
h = [1 0 0 1 1 0 1 0 1 0];

h(h<=0) = -1; % change all 0's to -1

l=1;
a=0;
b=0.5;
t=0:0.01:length(h);
for j=1:length(t)
    if t(j) >=a && t(j) <=b
        y(j) = h(l);
    elseif t(j)>=b && t(j)<=l
        y(j) = -1*h(l) %invert output after t crosses 0.5
    else
        y(j) = y(j-1); % remove spikes assign a previous value
        l = l+1;
        a = a+1;
        b = b+1;
    end
end
plot(t,y);
title('Manchester line code');
axis([0 length(h) -2 2]);
```

## HALF SINE (NEW)
```matlab
f = 2;
fs = f*20;
t = 0:1/fs:1;
y = sin(2*pi*f*t);
y(y<0) = 0;
plot(t,y)
```

## RAISED COSINE
```matlab
fs = 200;
fd = 5;
y = rcosine(fd,fs);
figure(1)
plot(y)
```
## PCM
```Matlab
 f = 2;
 fs = f*20;
 t = 0:1/fs:1;
 a = 2;
 x = a*sin(2*pi*f*t);
 x1 = x+a;
 quantized = round(x1);
 encoded = de2bi(quantized,'left-msb');
 decoded = bi2de(encoded,'left-msb');
 reconstructed = decoded - a;
 plot(t,x,'r-',t,reconstructed,'k+-');
 xlabel('time');
 ylabel('amplitude');
 legend('original signal','reconstructed signal');
```

## QPSK
```matlab
BER = runQPSKSystemUnderTest(commqpsktxrx_init, true, false);
disp('Error rate')
disp(BER(1))
disp('Number of detected errors');
disp(BER(2))
disp('Total number of compared samples')
disp(BER(3))
```
## EYE DIAGRAM
```matlab
fs = 20;
fd = 1;
pd = 200;
m = 5;
x = randi([0 m-1],pd,1); % new matlab %help("randi")
% x = randint(pd,1,m);  %old matlab
delay = 3;
r = 0.01;
rcv = rcosflt(x,fd,fs,'fir/normal',r,delay);
n = fs/fd;
eyediagram(rcv,n)
```
## DPSK
```matlab
M = 4; 
x = randi([0 M-1],500,1); % Random data
y = dpskmod(x,M,pi/8); 
plot(y) 
```
## POLAR NRZ
```matlab
%h = [1 0 0 1 1 0 1 0 1 0];
h = input('Enter the input: '); %Enter the input inside square bracket eg. [1 0 1 0 0 1]

h(h<=0) = -1; % change all 0's to -1

l=1;
t=0:0.01:length(h);
for j=1:length(t)
    if t(j) < l
        y(j) = h(l);
    else
        y(j) = h(l);
        l = l + 1;
    end
end

plot(t, y)
title('Line code POLAR NRZ');
axis([0 length(h) -2 2]);
```


## POLAR RZ LINE CODING
```matlab
%h = [1 0 0 1 1 0 1 0 1 0];
h = input('Enter the input: '); %Enter the input inside square bracket eg. [1 0 1 0 0 1]

h(h<=0) = -1; % change all 0's to -1

l=1;
a=0;
b=0.5;
t=0:0.01:length(h);
for j=1:length(t)
    if t(j) >=a && t(j) <=b
        y(j) = h(l);
    elseif t(j)>b && t(j)<=l
        y(j) = 0;
    else
        l = l+1;
        a = a+1;
        b = b+1;
    end
end

plot(t,y);
title('Line code POLAR RZ');
axis([0 length(h) -2 2]);
```



