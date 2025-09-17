# EXPERIMENT 3: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module flipflop_four(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @(posedge clk)
begin
if(rst==1)
q=0;
else if(s==0 && r==0)
q=q;
else if(s==0 && r==1)
q=0;
else if(s==1 && r==0)
q=1;
else
q=1'bx;
end
endmodule
```
### SR Flip-Flop Test bench 
```verilog
module flipflop_four_tb;
reg s,r,clk,rst;
wire q;
flipflop_four uut(s,r,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
s=0;
r=0;
rst=1;
#10 rst=0;
#10 s=1;r=0;
#10 s=0;r=0;
#10 s=0;r=1;
#10 s=1;r=1;
#10 s=0;r=0;
#20 $finish;
end
endmodule


```
#### SIMULATION OUTPUT

## SR Flip-Flop Output

![WhatsApp Image 2025-09-17 at 09 09 53_4b187eb8](https://github.com/user-attachments/assets/37055da4-05ab-4992-8f80-312bbf7b3388)


 
### JK Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module jk_flip_flop(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @(posedge clk)
begin
if(rst==1)
q=0;
else if(j==0 && k==0)
q=q;
else if(j==0 && k==1)
q=0;
else if(j==1 && k==0)
q=1;
else
q=~q;
end
endmodule
 
```
### JK Flip-Flop Test bench 
```verilog
module  jk_flip_flop_tb;
reg j,k,clk,rst;
wire q;
jk_flip_flop uut(j,k,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
j=0;
k=0;
rst=1;
#10 rst=0;
#10 j=1;k=0;
#10 j=0;k=0;
#10 j=0;k=1;
#10 j=1;k=1;
#10 j=0;k=0;
#20 $finish;
end
endmodule
```
#### SIMULATION OUTPUT

## JK Flip-Flop Output

![WhatsApp Image 2025-09-17 at 09 22 57_ff933573](https://github.com/user-attachments/assets/9dd18e28-dbd5-4c5f-b351-dfd928e0afc4)

---
### D Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module dfflop(clk,rst,d,q);
input clk,rst,d;
output reg q;
always @(posedge clk)
begin
if(rst)
q<=0;
else
q<=d;
end
endmodule

```
### D Flip-Flop Test bench 
```verilog
module dfflop_tb;
reg clk,rst,d;
wire q;
dfflop uut(clk,rst,d,q);
always #5 clk=~clk;
initial begin
clk=0;
rst=1;
d=0;
#10 rst=0;
#10 d=1;
#10 d=0;
#10 d=1;
#10 rst=1;
#10 rst=0;
#10 d=0;
#20 $finish;
end
endmodule
```

#### SIMULATION OUTPUT

## D Flip-Flop Output
 
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/de44c7e9-e23c-4290-8ad9-4eff358063d8" />

---
### T Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps
module toggleff(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if(rst==1)
q=0;
else if(t==0)
q=q;
else
q=~q;
end
endmodule
```
### T Flip-Flop Test bench 
```verilog
module toggleff_tb;
reg clk,rst,t;
wire q;
toggleff uut(clk,rst,t,q);
always #5 clk=~clk;
initial
begin
clk=0;
t=0;
rst=1;
#10 rst=0;t=0;
#10 t=1;
end
endmodule
```

#### SIMULATION OUTPUT

##  T Flip-Flop Output

![WhatsApp Image 2025-09-17 at 09 53 34_08ac99e7](https://github.com/user-attachments/assets/83645157-7283-4cc9-8ef4-55a6d1db2f16)


---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
