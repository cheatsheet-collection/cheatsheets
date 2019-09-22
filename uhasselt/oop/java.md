# Java Cheat Sheet
Ingo Andelhofs  
2de bachelor informatica

## Introductie
Een simpel `Hello world` voorbeeld.
```java 
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello Java!");
    }
};
```

## About Java
- JVM (Java Virtual Machine)
- JRE (Java Runtime Envirement)
- JDK (Java Development Kit)

- Garabage Collection
- Lazy Evaluation

## Operators
### Arithmetic
Add: `+`, sub: `-`, mult: `*`, div: `/`, mod: `%`  
Incr: `++i` & `i++`, decr: `--i` & `i--`

### Relational
Lt: `<`, gt: `>`, lte: `<=`, gte: `>=`, eq: `==`, neq: `!=`

### Logical
And: `&&`, or: `||`, not: `!`

### Bitwise
And: `&`, or: `|`, xor: `^`, not: `~`

### Shift
Ls: `<<`, rs: `>>`, signed-rs: `>>>`

### Ternary
If-else: `?:`

### Assignment
`+=`, `-=`, `*=`, `/=`, `%=`  
`&=`, `^=`, `|=`  
`<<=`, `>>=`, `>>>=`


## Types
### Primitive types
Deze types zijn al op voorhand door Java gedefinieerd.
```java
// Integer types
byte b = (byte)127;
short s = (short)32767;
int i = 2147483647;
long l = 9223372036854775807l;

// Floating point types
float f = 1.0f;
double d = 12e4d; // e -> power of 10

// Boolean types
boolean t = true; // or false

// Character types
char c = 'a'; // c = 97
```

### Reference types
Deze types kunnen door de programmeur aangemaakt worden en refereren naar een Object.
```java
// Number types
Byte b = new Byte();
Short s = new Short();
Integer i = new Integer();
Long l = new Long());

// Floating point types
FLoat f = new FLoat();
Double d = new Double();

// Boolean types
Boolean t = new Boolean();

// Character types
Character c = new Character();
```

```java
// String types
String s0 = "A string.";
String s1 = new String("A string.");

// 1D array types
String[] strings = {"String1", "String2"};
int[] ints = {1, 2, 3};
int[] ints = new int[10]; // 10 elements

// 2D array types
int[][] ints2 = {{1, 2}, {3, 4}};
int[][] ints2 = new int[3][3]; // 3 rows, 3 cols
```


## Control structures
### General structure
```java
// Single line
keyword (condition)
    ...;

// Multiline
keyword (condition) {
    ...
}
```

### `If ... else if ... else` statements
```java
if (condition0)         
    ...;
else if (condition1)    
    ...;
else                    
    ...;
```

### `Switch ... case` statements
```java
switch (value) {
    case 0:
        ...
        break;

    case 1: 
    case 2:
        ...
        break;

    default:
        ...
        break;
}
```

### `For` loops
Een `normal` type for lus.
```java
for(init; condition; increment)
    ...;
```

Een `foreach` type for lus.
```java
for(Type element : iterable)
    ...;
```

### `Do ... while` loops
```java
do
    ...;
while(condition);
```

### `While` loops
```java
while(condition) 
    ...;
```

### `Break` and `continue`
Een simpele break
```java
while(condition) {
    break;
    ...
}
// <--
```

Een simpele continue
```java
// <--
while(condition) {
    continue;
    ...
}
```

Een gelabelde continue
```java
start: // <--
while(condition0) {
    ...
    while(condition1) {
        ...
        continue start;
    }
}
```


## Classes

