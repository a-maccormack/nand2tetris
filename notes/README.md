# Unit 1:
## 1.1 Boolean Logic:

### Basic boolean operations
The 3 most basic boolean operations are AND, OR, and NOT. Their outputs can be represented by the following truth table:
<table>
<tr><td>
  
|x|y|AND|
|-|-|---|
|0|0| 0 |
|0|1| 0 |
|1|0| 0 |
|1|1| 1 |
  
</td><td>
  
|x|y|OR|
|-|-|--|
|0|0|0 |
|0|1|1 |
|1|0|1 |
|1|1|1 |
  
</td><td>
  
|x|NOT|
|-|---|
|0| 1 |
|1| 0 |
  
</td></tr> 
</table>

### We can combine operations as such
These are called Boolean Expressions
```
NOT(0 OR (1 AND 1)) = 0
```

### We can use general forms using indeterminates
These are called Boolean Functions

```
f(x,y,z) = (x AND y) OR (NOT(x) AND z)
```
and we can evaluate them as such:

|x|y|z|f|
|-|-|-|-|
|0|0|0|0|
|0|0|1|1|
|0|1|0|0|
|0|1|1|1|
|1|0|0|0|
|1|0|1|0|
|1|1|0|1|
|1|1|1|1|

### Boolean Identities
#### Commutative Laws:
```
(x AND y) = (y AND x)
(x OR y) = (y OR x)
```

#### Associative Laws:
```
(x AND (y AND z)) = ((x AND y) AND z)
(x OR (y OR z)) = ((X OR Y) OR z)
```

#### Distributive Laws:
```
(x AND (y or z)) = (x AND y) OR (x AND z)
(x OR (y AND z)) = (x OR y) AND (x OR z)
```

#### De Morgan Law:
```
NOT(x OR y) = NOT(x) AND NOT(y)
```

#### Idempotence Law:
```
NOT(x) AND NOT(x) = NOT(x)
```

## 1.2 Boolean Functions:
Given a truth table below, construct a function...

|x|y|z|f|
|-|-|-|-|
|0|0|0|1|
|0|0|1|0|
|0|1|0|1|
|0|1|1|0|
|1|0|0|1|
|1|0|1|0|
|1|1|0|0|
|1|1|1|0|

### Finding applicable function for row 1:
```
(NOT(x) AND NOT(y) AND NOT(z)) = 1 
```
This function gets a value of 1 on the first row, but 0 for all other table rows. Because of this, we must move to the the next table row that expects a 1. In our case, it's located on row #3.

### Finding applicable function for row 3:
```
(NOT(x) AND y AND NOT(z)) = 1
```
Again, this function gets a value of 1 only in this row, and a 0 everywhere else. We must move to the next table row that expects a 1. In this case, row #5

### Finding applicable function for row 5:
```
(x AND NOT(y) AND NOT(z) = 1
```
Again, this function gets a value of 1 only in this row, and a 0 everywhere else. Now that we have found equations that suit all the expected 1 values. We can "or" all equations toghether and then simplify.

```
Equation 1 (row 1): (NOT(x) AND NOT(y) AND NOT(z))
Equation 2 (row 3): (NOT(x) AND y AND NOT(z))
Equation 3 (row 5): (x AND NOT(y) AND NOT(z))

#Equation1 OR Equation2 OR Equation3:
(NOT(x) AND NOT(y) AND NOT(z)) OR (NOT(x) AND y AND NOT(z)) OR (x AND NOT(y) AND NOT(z))

#We could then simplify this using Boolean Laws from Unit 1.1
...
```

### Theorem:
Any Boolean function can be represented using an expression containing AND, OR, and NOT operators.

#### OR is not really needed:
```
#Proof:
(x OR y) = NOT(NOT(x) AND NOT(y))
```

### The NAND opperator does suffice to compute everything:
#### What is NAND?
<table>
<tr>NAND can be represented by the following truth table:</tr>
<tr><td>
  
|x|y|NAND|
|-|-|----|
|0|0|1   |
|0|1|1   |
|1|0|1   |
|1|1|0   |

</td><td>
  
    (x NAND y) = NOT(x AND y)
  
</td></tr>
</table>

#### Proof of earlier claim:
We already prooved that OR is not needed, so all that there's missing to prove are thr NOT and AND Boolean operators:
1) NOT:
```
NOT(x) = (x NAND x)
```
2) AND:
```
(x AND y) = NOT(x NAND y)
```
## 1.3 Logic Gates
### Gate Logic
* A technique for implementing boolean functions using logic gates
* Logic Gates:
  * Elementary (NAND,AND, OR, NOT, ...) 
  * Composite (MUX, ADDER) 

### Elementary Logic gates:
#### NAND:
```python
if (a == 1 and b == 1):
  return 0
else:
  return 1
```

#### AND:
```python
if (a == 1 and b == 1):
  return 1
else: 
  return 0
```

#### OR:
```python
if (a == 1 or b == 1):
  return 1
else:
  return 0
```

#### NOT:
```python
if (in == 0):
  return 1
else:
  return 0
```

### Composite Gates:
Combining elementary gates to form "mixed" gates

### Circuit implementations:
Logical gates can be implemented in circuits, electrically. 

## 1.4 Hardware Description Language (HDL)
### Design: from requirements to interface:
Given specific requirements, we can start building or delivering a gate with a specific functionality on an HDL script with the following syntax:

```vhdl
CHIP Xor {
  IN a, b;
  OUT out;
  
  PARTS:
  //Implementation missing
}
```
#### Electrical Diagram:
![Screenshot from 2022-02-27 19-01-40](https://user-images.githubusercontent.com/78695941/155901773-dcec78f1-55f3-4e1b-8e3b-a1302511c4ae.png)

* The dashed line serves as the boundary of the chip diagram. 
  * What remains outside the boundary is the high level view
  * What remains inside the boundary is  lower level view

##### A few things to notice:
* The "a" and "b" signals are being distributed across 2 distinct gates [NOT, AND]
* Dispatching of signal is done simultaneously

Knowing this, we can now continue filling out our HDL program:

**HDL is no more than a textual description of the diagram above**
```vhdl
CHIP Xor {
  IN a, b;
  OUT out;
  
  PARTS:
    Not (in=a, out=nota);
    Not (in=b, out=notb);
    And (a=a, b=notb, out=aAndNotb);
    And (a=nota, b=b, out=notaAndb);
    Or  (a=aAndNotb, b=notaAndb, out=out);
}
```

### General HDL comments:
1. Diagram should be described from left to right.
2. HDL is a functional / declarative language. It is a static description that is not run. Usually goes into an interpreter and nothing more.
3. It is important to remember the parameters for already defined gates:
```
Not(in, out);
And(a, b, out);
Or(a, b, out);
```

## 1.5 Hardware Simulation
### Overview:
HDL code gets opened by hardware simulator. We can then test our chip in order to see everything is working correctly. 
We can also write tests for our chips using `testscript`.

### Simulator: 
1. Static version of HDL code shown on bottom left. 
2. Input pins allow us to manipulate the input pins
3. Calculator button allows us to evaluate our circuit using the input pin values that we have defined. 

### Test Scripts
1. Files have a .tst extension and look like this:
```
load Xor.hdl;
output-file Xor.out,
output-list a b out;

set a 0, set b 0, eval, output;
set a 0, set b 1, eval, output;
set a 1, set b 0, eval, output;
set a 1, set b 1, eval, output;
```
2. Scripts and chips must be loaded manually
3. Compare files can be generated in order to test expected outputs

### Carrying out Hardware Construction Projects
* People at play:
  * System architects &rarr;  Has user level specifications. Decides which chips are needed.
  * Developer &rarr; Given architect specifications, developers build the chips using HDL or something of the sorts.

## 1.6 Multi-bit Buses
When designing hardware we must manipulate arrays of bits. It is convenient to think of such bits as a single entity (BUS). HDL provides the following convenient notation to handle these buses:

### Using Buses
Chip that adds two 16 bit numbers:
```vhdl
/*
 * Adds two 16-bit values.
 */
  
CHIP Add16 {
  IN a[16], b[16];
  OUT out[16];
    
  PARTS:
    ...
}
```

Chip that adds 3 16 bit numbers:
```vhdl
/*
 * Adds three 16-bit values.
 */
  
  CHIP Add16 {
    IN first[16], second[16], third[16];
    OUT out[16];
    
    PARTS:
      
      Add16(a=first, b=second, out=temp);
      Add16(a=temp, b=third, out=out);
}
```

#### Breaking buses into sub-buses:
```vhdl
  IN lsb[8], msb[8], ...
  
  Add(a[0..7]=lsb, a[8..15]=msb, b=..., out=...);
  Add(..., out[0..3]=t1, out[4..15]=t2);
```

## 1.7 Project 1 Overview
### Statement:
Given Nand, build the following gates:

|Elementary Logic Gates|16-Bit Variants|Multi-way Variants|
|----------------------|---------------|------------------|
| `Not`                | `Not16`       | `Or8Way`         |
| `And`                | `And16`       | `Mux4Way16`      |
| `Or`                 | `Or16`        | `Mux8Way16`      |
| `Xor`                | `Mux16`       | `DMux4Way`       |
| `Mux`                |               | `DMux8Way`       |
| `Dmux`               |               |                  |


All of these 15 gates comprise all of the elementary logic gates that we need to build a computer. 

### Multiplexor [Mux]

![Screenshot from 2022-03-01 22-48-43](https://user-images.githubusercontent.com/78695941/156279188-7ecd618c-390a-45c2-85b2-decadba6cc30.png)

#### Behaviour:
```python
if sel == 0:
  return a
elif sel == 1:
  return b
```
#### Where is it used:
1. Digital design
2. Comunication Networks

#### Using mux logic to build a programable gate:

```
#We could build an AndMuxOr gate:

if sel == 0:
  out = (a And b)
elif sel ==1:
  out = (a Or b)
```

#### AndMuxOr HDL

```
CHIP AndMuxOr {
  IN a, b, sel;
  OUT out;
  
  PARTS:
  And(a=a, b=b, out=andOut);
  Or(a=a, b=b, out=orOut);
  Mux(a=andOut, b=orOut, sel=sel, out=out);
}
```

### Demultiplexor [DMux]

![Screenshot from 2022-03-01 23-01-44](https://user-images.githubusercontent.com/78695941/156280436-de15055a-ba82-486a-8af2-73e984f8c98b.png)

#### Behaviour
```python
if sel == 0:
  a,b = in,0
elif sel == 1:
  a,b = 0, in
```
Receives single input, and depending on selection bit, it routes input through a or b. The channel that is not chosen, returns 0.

#### Multiplexing / Demultiplexing in communication networks:

![Screenshot from 2022-03-01 23-08-10](https://user-images.githubusercontent.com/78695941/156281062-1cf811f8-6ba1-43e5-8b8e-19aebdfeb824.png)

### And16

![Screenshot from 2022-03-01 23-09-48](https://user-images.githubusercontent.com/78695941/156281246-7b896add-9f6d-4517-a135-f14d98a87b95.png)

#### Behaviour
```python
a = 1010101101011100
b = 0010110100101010

out = 0010100100001000
```
And(a[0], b[0]), And(a[1], b[1]), And(a[2], b[2]) ...
out = out[0] out[1] out[2]....

Calculation is not secuential but parallel


### 16 bit, 4-way multiplexor [Mux4Way16]

![Screenshot from 2022-03-01 23-16-18](https://user-images.githubusercontent.com/78695941/156281855-bb32288f-5af2-4ef8-bc32-9c157383be44.png)

#### Simplified truth table:

|sel[1]|sel[0]|out|
|------|------|---|
|0     |0     |a  |
|0     |1     |b  |
|1     |0     |c  |
|1     |1     |d  |






