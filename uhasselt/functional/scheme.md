# Scheme Cheat Sheet
Ingo Andelhofs  
2de bachelor informatica

## Introductie
Een simpel `Hello world` voorbeeld.
```scheme
#lang scheme
"Hello Scheme"
```

## About Scheme
- Alles is een lijst in Scheme.
- Het is een functionele programmeertaal.
- Scheme maakt veel gebruik van recursieve oproepen.

## Basis types
### Atoms
Een atom is een string van (speciale) karakters en/of cijfers die geen `(` of `)` bevat.

### Lists
Een lijst is een collectie van s-expressies omsloten door `(` en `)`. Deze s-expressies zijn nieuwe lijsten of atomen. We spreken over een lege lijst als deze `()`, `empty` of `null list` is.

## Basis functies
### Car
De `car` van een (niet-lege) lijst is de eerste s-expressie van die lijst. Voorbeeld:
```scheme
(car (a b c)) 
; retuns: a
```

### Cdr
De `cdr` van een (niet-lege) lijst is de lijst met s-expressies op de eerste s-expressie na. Voorbeeld:
```scheme
(cdr (a b c)) 
; retuns: (b c)
```

### Cons
De `cons` van een s-expressie en een lijst is een nieuwe lijst waaraan de s-expressie vanvoor is toegevoegd. Voorbeeld:
```scheme
(cons a (b c)) 
; retuns: (a b c)
```

### Quote
De `quote` van een s-expressie geeft exact die s-expressie terug zonder deze als een functie uit te voeren. Voorbeeld:
```scheme
(quote (car (a b c)))
; returns: (car (a b c))
```
```scheme
'(car (a b c))
; returns: (car (a b c))
```

### Null?
De `null?` (van een lijst) geeft waar terug als deze lijst leeg is. Voorbeeld:
```scheme
(null? '())
; returns: #t or true
```

### Atom?
De `atom?` functie geeft waar terug als de s-expressie een atoom is. Voorbeeld:
```scheme
(atom? hello)
; returns: #t or true
```

### Number?
De `number?` functie geeft waar terug als de s-expressie een getal is. Voorbeeld:
```scheme
(number? hello)
; returns: #f or false
```

### Eq?
De `eq?` functie geeft waar terug als de twee s-expressies gelijk zijn. Voorbeeld:
```scheme
(eq? hello hello)
; returns: #t or true
```

### Define
```scheme
; variable
(define variableName value)

; function
(define functionName 
    (lambda (arg1, arg2, ...)
        ...
    )
)
```

### Cond
```scheme
(cond
    (condition returnValue0)
    (else returnValue1)
)
```

### And, Or, Not
```scheme
(and s-expr0 s-expr1)
(or s-expr0 s-expr1)
(not s-expr0)
```

### Member
```scheme
(member a (a b c))
; returns: #t or true
```