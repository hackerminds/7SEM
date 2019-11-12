
## RAISED COSINE
```matlab
fs=200;
fd=5;
y=rcosine(fd,fs);
figure(1)
plot(y)
```
## QPSK
```matlab
BER = runQPSKSystemUnderTest(commqpsktxrx_init, true, printReceivedData);

fprintf('Error rate = %f.\n',BER(1));
fprintf('Number of detected errors = %d.\n',BER(2));
fprintf('Total number of compared samples = %d.\n',BER(3));
```
## EYE DIAGRAM
```matlab
clc
clear all;
close all;
fs=20;
fd=1;
pd=500;
m = 50;
x=randint(pd,1,m);
a=length(x);
delay=3;
r=0.01;
rcv=rcosflt(x,fd,fs,'fir/normal',r,delay);
n=fs/fd;
eyediagram(rcv,n)
```



## DPSK
```matlab
M = 4; % Use DQPSK in this example, so M is 4.
x = randi([0 M-1],500,1); % Random data
y = dpskmod(x,M,pi/8); % Modulate using a nonzero initial phase.
plot(y) % Plot all points, using lines to connect them.
```
## POLAR RZ LINE CODING
```matlab
h = [1 0 0 1 1 0 1 0 1 0];

for i=1:length(h)
    if h(i) == 1
        n(i) = 1;
    else
        n(i) = -1;
    end
end

l=1;
a=0;
b=0.5;
t=0:0.01:length(h);
for j=1:length(t)
    if t(j)>b && t(j)<=l
        y(j) = 0;
    else
        l = l + 1;
        a = a+1;
        b=b+1;
    end
end

plot(t, y)
title('Line code POLAR RZ');
axis([0 length(h) -2 2]);
```
## POLAR NRZ
```matlab
h = [1 0 0 1 1 0 1 0 1 0];

for i=1:length(h)
    if h(i) == 0
        n(i) = -1;
    end
end

l=1;
t=0:0.01:length(h);
for j=1:length(t)
    if t(j) <= l
        y(j) = n(l);
    else
        y(j) = n(l);
        l = l + 1;
    end
end

plot(t, y)
title('Line code POLAR NRZ');
axis([0 length(h) -2 2]);
```


