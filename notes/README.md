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
1) NOT(x) = (x NAND x)
2) (x AND y) = NOT(x NAND y)
