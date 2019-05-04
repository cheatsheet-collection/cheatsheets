# PostgreSQL CheatSheet
Ingo Andelhofs  
1ste bachelor informatica  

Rechte haken `[]` worden gebruikt voor opties voor een bepaalde query weer te geven zoals bijvoorbeeld `[TYPE]` waar je eender welke datatype kan invullen


## SQL basics
### Datatypes
- **Strings** (single quotes only): &nbsp;&nbsp; **`CHAR(N)`, `VARCHAR(N)`**
- **Bitstrings** (`B'01'` voor binair of `X'0F'` voor hexadecimaal): &nbsp;&nbsp; **`BIT(N)`, `VARYING BIT(N)`**
- **Booleans** (`TRUE`, `FALSE` or `UNKOWN`): &nbsp;&nbsp; **`BOOLEAN`**
- **Date** (format `yyyy-mm-dd`) padded with 0's: &nbsp;&nbsp; **`DATE`**
- **Time** (format `hh:mm:ss.f`) f is the fraction: &nbsp;&nbsp; **`TIME`**
- **Time stamp** (format `yyyy-mm-dd hh:mm:ss.f`): &nbsp;&nbsp; **`TIMESTAMP`**
- **Floating point numbers** (format `-x.yEz`): &nbsp;&nbsp; **`FLOAT`, `REAL`, `DOUBLE PRECISION`**
- **Decimal numbers** (format 'totaal aantal digits', 'aantal fracties'): &nbsp;&nbsp; **`DECIMAL(t, f)`**, **`NUMERIC(t, f)`**

### Modifying a table
Create a table with name `t` and columns/attributes `c1`, `c2`.
```SQL
CREATE TABLE t (
    c1 [TYPE],
    c2 [TYPE]
);
```

Remove a table called `t`.
```SQL
DROP TABLE t;
```

Add a column/attribute `c3` to table `t`. All columns `c3` will be initialized to `NULL`.
```SQL
ALTER TABLE t ADD c3 [TYPE];
```

Remove a column/attribute `c3` from table `t`.
```SQL
ALTER TABLE t DROP c3;
```


### Default values
Add default values `c1` when creating a new table `t`.
```SQL
CREATE TABLE t (
    c1 [TYPE] DEFAULT [VALUE]
);
```

Add default values to an existing table `t`.
```SQL
ALTER TABLE t ADD c2 [TYPE] DEFAULT [VALUE];
```

### Keys
Mogelijke keys in pgSQL zijn `PRIMARY KEY`, `UNIQUE` en `FOREIGN KEY`.  

Geef één enkele kolom/attribuut `c1` in tabel `t` een key `PRIMARY KEY` of `UNIQUE`.
```SQL
CREATE TABLE t (
    c1 [TYPE] [KEY]
);
```

Geef meerdere kolommen/attributen `c1`, `c2` in tabel `t` een key `PRIMARY KEY` of `UNIQUE`. 
```SQL
CREATE TABLE t (
    c1 [TYPE],
    c2 [TYPE],
    c3 [TYPE],
    [KEY] (c1, c2)
);
```

### Simple queries
Selecteer alle kolommen/attributen van tabel `t`.
```SQL
SELECT * FROM t;
```

Selecteer kolommen `c1`, `c2` van tabel `t`.
```SQL
SELECT c1, c2 FROM t;
```

Selecteer alle kolommen van een tabel `t` waar een bepaalde conditie geldt.
```SQL
SELECT * FROM t WHERE [condition];
```

De basis structuur van een SQL query bestaat dus uit:
- L: Een lijst van expressies
- R: Een relatie of tabel
- C: een conditie
```SQL
SELECT L FROM R WHERE C;
```

Mogelijke operatoren zijn: 
- `=`, `<`, `<=`, `>`, `>=`, `<>`, `!=`
- `AND`, `OR`, `NOT`
- `+`, `-`, `*`, `/`
- `||` (voor strings te concateneren)

### Aliases
```SQL
-- alias using the AS keyword
SELECT column1 AS c1, column2 AS c2 FROM t;

-- alias without using the AS keyword
SELECT column1 c1, column2 c2 FROM t;

-- calculations on columns as alias
SELECT inch*0.393700787 AS cm FROM t;

-- constant column as alias
SELECT 'cm' AS inCentimeters FROM t;
```

### Pattern matching
```SQL
-- algemene vorm waar [s] een string is en [p] een patroon is
-- e is een escape char voor als je % of _ wilt escapen
s [NOT] LIKE p ESCAPE [e]

-- bevat een substring
%  -- sequentie van chars
_  -- één enkele char
'' -- een single quote
```

### NULL values
```SQL

-- value unkown: wanneer je bepaalde attributen niet weet
UNKOWN

-- value inapplicable: wanneer er geen waarde voor een bepaald attribuut is 
NULL

-- value withheld: wanneer een attribuut wordt leeggelaten/ we geen recht hebben
NULL

-- inserted nulls: wanneer we te inserten data leeglaten en er geen DEFAULT is
NULL

-- !all! arithmetic with null
NULL

-- comparing nulls
UNKOWN

-- check if a value is NULL
SELECT * FROM t WHERE c1 IS [NOT] NULL;


-- Logical operations with TRUE (1), FALSE (0), UNKOWN (½)
-- Tuples met FALSE/UNKNOWN worden niet meegerekend
AND -- minimum(OPERATORS)
OR  -- maximum(OPERATORS)
NOT -- 1 - [OPERATOR]  
```

### Ordering selections
```SQL
-- Sorteer op attributen [c1], [c2] met ASC als default optie
SELECT * FROM t WHERE condition [GROUP BY | HAVING] [condition]
ORDER BY c1, c2 [ASC | DESC];

-- sorting using an expression
SELECT * FROM t
ORDER BY c1 + c2;
```

### Queries on multiple relations
```SQL
-- simple joins on attribute [id] with tables [t1] and [t2]
SELECT *
FROM t1, t2
WHERE t1.id = t2.id;

-- dot notation with tables [t1] and [t2] with both an attribute called [c1]
SELECT * FROM t1.c1, t2.c1;

-- dot notation on the same query
SELECT * FROM t1.c AS c1, t1.c AS c2;
```

### Unions, Intersections and Difference of queries
```SQL
-- Unie: Wat in de ene of de andere table zit
(SELECT * FROM t1)
UNION
(SELECT * FROM t2);

-- Doorsnede: Wat twee tabellen gemeenschappelijk hebben
(SELECT * FROM t1)
INTERSECT
(SELECT * FROM t2);

-- Verschil: Wat in de eerste tabel zit en niet in de tweede
(SELECT * FROM t1)
EXCEPT
(SELECT * FROM t2);
```

## SQL subqueries
### Basic subqueries
```SQL
-- returning a single constant
-- relations that can be used in the where clause
SELECT c1 FROM t1
WHERE c1 = (SELECT c2 from t2);

-- in the from clause followed by ist alias
SELECT t.c1 FROM (SELECT * FROM table) AS t;  
```

### Subquery conditions
```SQL
-- Controleer of de table [t] niet leeg is
[NOT] EXISTS t;

-- Controleer of een tuple [s] in table [t] zit
s [NOT] IN t;

-- Controleer of voor alle tuples [s] een bepaalde conditie geldt
s [operator] ALL t;

-- Controleer of er een tuple [s] bestaat waarvoor een bepaalde conditie geldt
s [operator] ANY t;
```

## SQL Joins
```SQL
-- Cross Join (Cartesian Product)
SELECT * 
FROM t1 
CROSS JOIN t2;

-- Theta Join (all possible combinations on a condition)
SELECT *
FROM t1
JOIN t2 ON condition;

-- 
```

Natural joins. Join two relations/tables on a certain column(s)/attribute(s) name. And the name is equated. 
```SQL
SELECT * 
FROM t1
NATURAL JOIN t2;  
```


Outerjoins. Join tables padded with `NULL` values.

```SQL
SELECT * 
FROM t1
NATURAL [FULL] OUTER JOIN t2 ;  
-- or
[FULL] OUTER JOIN t2 ON condition;
```

Left/right outer joins. (Left contains only the left `NULL` values. Rightcontains only the right `NULL` values.) 
```SQL
SELECT *
FROM t1
[LEFT] [RIGHT] JOIN t2 ON condition;
```

## Full-relation operations
> GROUP-BY, HAVING

### Eliminating duplicates
Follow the `SELECT` keyword with `DISTINCT` if you want to eliminate duplicates. 
```SQL
SELECT DISTINCT *
FROM t;
``` 

`UNION`, `INTERSECT` and `EXCEPT` eliminiate duplicates by default. You can add the keyword `ALL` after the `UNION`, `INTERSECT` and `EXCEPT` if you want to keep all duplicate tuples. 


Bij `UNION ALL` krijg je de som van het aantal dubbels terug.  
Bij `INTERSECT ALL` krijg je het minimum van het aantal dubbels terug.  
Bij `EXCEPT ALL` krijg je het verschil van het aantal dubbels terug (A - B). Als dit minder is dan 0 wordt deze niet meegrekend natuurlijk.  

The keyword `GROUP BY` also removes dublicates automatically. De groepen worden gerograniseerd en gegroepeerd. 
> SUM, AVG, MIN, MAX, COUNT, ...  
> COUNT(DISTINCT c1)
```SQL
SELECT AGGREGATE_FUNCTION(*)
FROM t
GROUP BY c1;
```

`NULL` values worden genegeerd door aggregate functies.
Groups itself can be `NULL` values.  
Als er enkel `NULL` values zijn is al de rest ook `NULL` met `COUNT` als uitzondering.


## LES 3