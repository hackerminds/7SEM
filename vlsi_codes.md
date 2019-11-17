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


