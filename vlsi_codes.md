### Inverter
```verilog
module inverter(a,y);
input a;
output y;
assign y = ~a;
endmodule

//Test bench:
module test_inv;
reg a;
wire y;
inverter U1 (a,y);
initial
begin
a = 1'b1;
#40 a = 1'b0;
#40 a = 1'b1;
end
endmodule
```

### A Buffer
```verilog
module buffer (a, en, y);
input a, en;
output y;
reg y;
always @ (a,en)
begin
if(en==1'b1)
y=1'bz;
else
y=a;
end
endmodule

//Test bench:
module test_buffer;
reg a,en;
wire y;
buffer U1 (a, en, y);
initial
begin
a = 1'b1; en=1'b1;
#20 a = 1'b0; en=1'b1;
#20 a = 1'b0; en=1'b0;
#20 a = 1'b1; en=1'b0;
end
endmodule
```
### transmission gate
```verilog
module tg(a,c, y);
input a,c;
output y;
wire cb;
supply1 vdd;
supply0 gnd;
pmos p1 (cb, vdd, c )
nmos n1 (cb, gnd, c)
pmos p2 (y, a, cb)
nmos n2 (y, a, c )
end
endmodule

Test bench:
module test_tg;
reg a,c;
wire y;
tg tg1 (a,c,y);
initial
begin
a = 1'b1; c = 1'b0;
#20 a = 1'b1; c = 1'b1;
#20 a = 1'b0; c = 1'b1;
end
endmodule
```

### 4. Basic / Universal Gates
### 4a. Basic Gates
```verilog
module b_gates (not1, or2, and2, a, b);
input a, b;
output not1, or2, and2;
assign not1 = ~a;
assign or2 = a | b ;
assign and2 = a & b;
endmodule

Test bench:
module test_basic_gates;
reg a, b;
wire not1, or2, and2;
b_gates U1 (not1, or2, and2, a, b);
initial
begin
a = 1'b0; b = 1'b0;
#20 a = 1'b0; b = 1'b1;
#20 a = 1'b1; b = 1'b0;
#20 a = 1'b1; b = 1'b1;
end
endmodule

Truth Table:
Input Output
A B Not1 And2 Or2
0 0   1   0   0
0 1   1   0   1
1 0   0   0   1
1 1   0   1   1

### 4b. Universal Gates
```verilog
module ugates (nor2, nand2, a, b);
input a, b;
output nor2, nand2;
assign nand2 = ~(a & b);
assign nor2 = ~(a | b);
endmodule
Test bench:
module test_ugates;
reg a, b;
wire nor2, nand2;
ugates U1 (nor2, nand2, a, b);
initial
begin
a = 1'b0; b = 1'b0;
#20 a = 1'b0; b = 1'b1;
#20 a = 1'b1; b = 1'b0;
#20 a = 1'b1; b = 1'b1;
end
endmodule
Truth Table:
Input Output
A B Nand2 Nor2
VLSI Lab Manual VII sem, ECE 15ECL77
Canara Engineering College Dept of ECE
0 0 1 1
0 1 1 0
1 0 1 0
1 1 0 0
5. Flip Flop – RS, D, JK, MS, T
5a. RS Flip Flop
module srff(sr,rst,clk, q, qb);
input [1:0]sr;
input clk,rst;
output q, qb;
reg q,qb,ff;
always @ (posedge clk )
begin
if(rst==1'b1)
ff=1'b0;
case({sr})
2'b01:ff=1'b0;
2'b10:ff=1'b1;
2'b11:ff=1'bZ;
default:ff=ff;
endcase
q=ff;
qb=~ff;
end
endmodule
Test bench:
module test_rs_ff;
reg [1:0]sr;
reg clk,rst;
wire q, qb;
srff srff_0 (sr,rst,clk,q, qb);
initial
begin
clk = 1'b0;
forever #10 clk = ~clk;
end
initial
begin
sr = 2'b01; rst = 1'b1;
#20 sr = 2'b01; rst = 1'b0;
VLSI Lab Manual VII sem, ECE 15ECL77
Canara Engineering College Dept of ECE
#20 sr = 2'b10;
#20 sr = 2'b11;
#20 sr = 2'b00;
end
endmodule
Truth Table:
Input Output
clk rst sr[1] sr[0] q qb
↑ 1 X X 0 1
↑ 0 0 0 q qb
↑ 0 0 1 0 1
↑ 0 1 0 1 0
↑ 0 1 1 Z Z
5b. D Flip Flop
module dff1(d,clk,rst, q,qb);
input d,clk,rst;
output q,qb;
reg q,qb;
always@(posedge clk)
begin
if(rst==1'b1)
q=1'b0;
else
q=d;
qb=~q;
end
endmodule
Test bench:
module test_d_ff;
reg clk,d,rst;
wire q, qb;
dff1 srff_0 (d,clk,rst,q, qb);
initial
begin
clk = 1'b0;
forever #10 clk = ~clk;
end
VLSI Lab Manual VII sem, ECE 15ECL77
Canara Engineering College Dept of ECE
initial
begin
#20 d = 1'b1; rst = 1'b1;
#20 d = 1'b1; rst = 1'b0;
#20 d = 1'b0;
end
endmodule
Truth Table:
Input Output
clk rst d q qb
↑ 1 X 0 1
↑ 0 0 0 1
↑ 0 1 1 0
5c. JK Flip Flop
module jkff1(jk, clk,q,qb);
input [1:0] jk;
input clk;
output q,qb;
reg q,qb,temp;
always@(posedge clk)
begin
case(jk)
2'b01:temp= 1'b0;
2'b10:temp= 1'b1;
2'b11:temp= ~(temp);
default:temp= temp;
endcase
q = temp;
qb = ~temp;
end
endmodule
Test bench:
module test_jk_ff;
reg [1:0]jk;
reg clk;
wire q,qb;
jkff1 jkff_0 (jk, clk, q, qb);
initial
begin
VLSI Lab Manual VII sem, ECE 15ECL77
Canara Engineering College Dept of ECE
clk = 1'b0;
forever #5 clk = ~clk;
end
initial
begin
jk = 2'b01;
#20 jk = 2'b10;
#20 jk = 2'b11;
#20 jk = 2'b00;
end
endmodule
Truth Table:
Input Output
clk jk[1] jk[0] q qb
↑ 0 0 q qb
↑ 0 1 0 1
↑ 1 0 1 0
↑ 1 1 qb q
5c. T Flip Flop
module tff2(t, rst, clk, q,qb);
input t,clk,rst;
output q,qb;
reg q,qb,temp;
always@(posedge clk)
begin
if (rst==1'b1)
temp =1'b0;
else
if(t==1'b1)
temp =~temp;
q = temp;
qb =~temp;
end
endmodule
Test bench:
module tff;
reg clk,rst,t;
wire q,qb;
tff2 tff2 (t, rst, clk, q, qb);
initial
begin
clk = 1'b0;
forever #10 clk = ~clk;
end
initial
begin
t = 1'b0;rst = 1'b1;
#20t = 1'b0; rst = 1'b0;
#20 t = 1'b1;
end
endmodule

Truth Table:
Input Output
clk rst t q qb
↑   1   X 0 1
↑   0   0 q qb
↑   0   1 qb q
```
