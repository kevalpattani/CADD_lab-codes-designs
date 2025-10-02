### Full adder
```
`timescale 1ns / 1ps

module Fulladder(
input wire a,
input wire b,
input wire c,
output reg sum,
output reg carry
    );
    
    assign {carry, sum} = a + b + c;
    
endmodule

```

---
### Gates 
```
`timescale 1ns / 1ps

module gates (
    input  logic a, b,      
    output logic y_and,     
    output logic y_or,      
    output logic y_xor,     
    output logic y_nor,     
    output logic y_xnor,    
    output logic y_not      
);

    assign y_and = a & b;
    assign y_or = a | b;
    assign y_xor = a ^ b;
    assign y_nor = ~(a | b);
    assign y_xnor = ~(a ^ b);
    assign y_not = ~a;
    
endmodule
```

---
### MUX 8:1
```
`timescale 1ns / 1ps

module mux8_1(a,b,c,d,e,f,g,h,s0,s1,s2,y);
input logic a,b,c,d,e,f,g,h,s0,s1,s2;
output logic y;
logic o1,o2;

mux4_1 first(a,b,c,d,s0,s1,o1);
mux4_1 second(e,f,g,h,s0,s1,o2);
mux2_1 third(o1,o2,s2,y);

endmodule

```

---
### MUX 4:1
```
`timescale 1ns / 1ps

module mux4_1(a,b,c,d,s0,s1,y);
input logic a,b,c,d,s0,s1;
output logic y;
logic w1,w2;

mux2_1 low1(.a(a),.b(b),.s(s0),.y(w1));
mux2_1 low2(.a(c),.b(d),.s(s0),.y(w2));
mux2_1 high(.a(w1),.b(w2),.s(s1),.y(y));

endmodule

```

---
### MUX 2:1
```
`timescale 1ns / 1ps

module mux2_1(a,b,s,y);

input logic a,b,s;
output logic y;

logic sbar,p,q; 

not I1(sbar,s);
and I2(p,sbar,a);
and I3(q,s,b);
or I4(y,p,q);

endmodule

```

---
### Half-adder struct style 
```
`timescale 1ns / 1ps

module mux2_1(a,b,s,y);

input logic a,b,s;
output logic y;

logic sbar,p,q; 

not I1(sbar,s);
and I2(p,sbar,a);
and I3(q,s,b);
or I4(y,p,q);

endmodule

```

---
### Full_adder_using_half_adder
```
`timescale 1ns / 1ps

module FA_u_HF(a,b,c,sum,carry);

input logic a,b,c;
output logic sum,carry;
logic s1,c1,c2;

HF_struc first(a,b,s1,c1);
HF_struc second(s1,c,sum,c2);
or (carry,c2,c1);


endmodule

```

---
### MUX 4:1 DATA
```
`timescale 1ns / 1ps

module mux4_1_data(a,b,c,d,s0,s1,y);
input logic a,b,c,d,s0,s1;
output logic y;

assign y = s1 ? (s0 ? d : c) : (s1 ? b : a);

endmodule

```

---
### Two to One TRI-state Buffer
```
`timescale 1ns / 1ps

module Two_to_one_tri(a,b,s,y);
input logic a,b;
input logic s;
output logic y;

buffer U1 (.a(a),.en(s),.y(y));
Tristate_buffer U0 (.a(b),.en(s),.y(y));

endmodule

```

---
### TRISTATE INVERTER
```
`timescale 1ns / 1ps

module Tristate_Inverter(a,en,y);
input logic a,en;
output logic y;

assign y = en ? ~a : 1'bz;

endmodule

```

---
### 8:1 MUX
```
`timescale 1ns / 1ps

module eight_1_mux_condi(a,b,c,d,e,f,g,h,s,y);
input logic [3:0]a,b,c,d,e,f,g,h;
input logic [2:0]s;
output logic [3:0]y;

assign y = s[2] ? (s[1]?(s[0]?h:g):(s[0]?f:e)):(s[1]?(s[0]?d:c):(s[0]?b:a));

endmodule
```

---
### Binary To Gray
```
`timescale 1ns / 1ps

module bnrc_to_gc(input logic [3:0] b,
                  output logic [3:0] g
                  );

assign g[0] = b[0] ^ b[1];
assign g[1] = b[1] ^ b[2];
assign g[2] = b[2] ^ b[3];
assign g[3] = b[3];

endmodule
```

---
### Gray To Binary
```
`timescale 1ns / 1ps

module gc_to_bnrc(input logic [3:0] g,
                  output logic [3:0] b);
                  
assign b[3] = g[3];
assign b[2] = g[2] ^ g[3];
assign b[1] = g[2] ^ g[1] ^ g[3];
assign b[0] = g[2] ^ g[1] ^ g[0] ^ g[3]; 

endmodule

```

---
### Async 
```
`timescale 1ns / 1ps

module async_4 (input logic clk, 
                input logic reset, 
                input logic [3:0] d,
                output logic [3:0] q
                );

always @(posedge clk or posedge reset) begin
    if (reset)
        q <= 4'b0000; 
    else
        q <= d;    
end
endmodule
```

---
### Sync
```
`timescale 1ns / 1ps

module sync_4 (input logic clk,
               input logic reset,
               input logic [3:0] d,
               output logic [3:0] q
               );

always @(posedge clk) begin
    if (reset)
        q <= 4'b0000; 
    else
        q <= d;
end
endmodule
```

---
### BCD to Excess 3
```
`timescale 1ns / 1ps

module bcd_to_excess3(input logic [3:0] bcd,
                      output logic [3:0] excess3);
                      
assign excess3 = bcd + 4'b0011;

endmodule

```
