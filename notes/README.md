# Notes:
## Unit 1:
### 1.1 Boolean Logic:

#### Basic boolean operations
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

#### We can combine operations as such
These are called Boolean Expressions
```
NOT(0 OR (1 AND 1)) = 0
```

#### We can use general forms using indeterminates
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

#### Boolean Identities
##### Commutative Laws:
```
(x AND y) = (y AND x)
(x OR y) = (y OR x)
```

##### Associative Laws:
```
(x AND (y AND z)) = ((x AND y) AND z)
(x OR (y OR z)) = ((X OR Y) OR z)
```

##### Distributive Laws:
```
(x AND (y or z)) = (x AND y) OR (x AND z)
(x OR (y AND z)) = (x OR y) AND (x OR z)
```

##### De Morgan Law:
```
NOT(x OR y) = NOT(x) AND NOT(y)
```

##### Idempotence Law:
```
NOT(x) AND NOT(x) = NOT(x)
```
