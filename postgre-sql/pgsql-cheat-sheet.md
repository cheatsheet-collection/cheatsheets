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


## Database Modifications
1. `INSERT` tuples
2. `DELETE` tuples
3. `UPDATE` tuples

### Insertion
Hierbij wordt er een nieuwe rij toegevoegd aan de relatie `t`. Als er bepaalde attributen niet worden meegegeven worden hiervoor de `DEFAULT` values voor gebruikt. Als je gewoon alle waarde wilt invullen hoef je `(c1, c2, ..., cn)` zelfs niet mee te geven en kan je direct `VALUES` aanvullen. Je kan ook meerdere tuples inserten door een meerdere `(v1, v2, ..., vn)` tuples met een komma achteraan toe te voegen.
```SQL
INSERT INTO t(c1, c2, ..., cn) VALUES (v1, v2, ..., vn);
```

### Deletion
Als je alle tuples wilt verwijderen uit tabel `t` waar een specifieke conditie geldt kan je volgende code uitvoeren.
```SQL
DELETE FROM t WHERE <condition>;
```

### Updates
Als je een bepaalde tuple van tabel `t` wil updaten kan je dit als volgt doen. Je kan dus een attribut hernoemen door `attr='value'` in te vullen waarbij `attr` de naam is van het attribut en `value` de nieuwe waarde is voor dit attribut. 
```SQL
UPDATE t SET <reassignments> WHERE <condition>;
```

## Foreign-Key Constraints
1. Waarnaar gerefereerd wordt moet een `PRIMARY KEY` of `UNIQUE` zijn. Anders zouden we naar meerdere items tegelijk kunnen wijzen wat dus niet mogelijk is.
2. Het attribut (vaak een id) waarnaar gerefereerd moet altijd bestaan in de gerefereerde tabel.


De makkelijkste manier om een foreign key te definiëren is in de tabel zelf bij het attribut dat je al foreign key wilt maken.
```SQL
-- PRIMARY KEY TO REFERENCE
CREATE TABLE t (
    id SERIAL PRIMARY KEY NOT NULL 
);

-- FOREIGN KEY (method a)
CREATE TABLE u (
    t_id INTEGER REFERENCES t(id)
);
-- FOREIGN KEY (method b)
CREATE TABLE u (
    t_id INTEGER,
    FOREIGN KEY (t_id) REFERENCES t(id)
);
```

Er zijn wel enkele problemen. Als je in tabel `t` een tuple zou willen updaten of deleten en er is een reference naar dit tuple in tabel `u` zal er een error optreden omdat postgresql niet weet wat er moet gebeuren. Je moet dus zelf keizen wat er moet gebreuren als je een tuple `UPDATE` of `DELETE`.

1. De `DEFAULT` of `REJECT` policy zorgt ervoor dat eender welke modificatie niet wordt toegelaten. 
2. De `CASCADE` policy zorgt ervoor dat dezelfde actie wordt uitgevoerd op de tuple met een reference. Als je deze dus `DELETE` in `t` zal dit ook gelden in `u`. Hetzelfde geld voor update.
3. De `SET NULL` policy zet de reference op `NULL` bij een modificatie van `t`.

```SQL
CREATE TABLE u (
    t_id INTEGER REFERENCES t(id)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);
```

MINDER BELANGRIJK: Als we twee tuples tegelijk in de database willen steken wordt tijdelijk constraint checking uitgeschakeld en pas later gekeken of de tuples wel voldoen aan de constraint. Hiervoor wordt intern `DEFERRABLE` en `NOT DEFERRABLE` gebruikt. ALs je `DEFERRABLE` moet dit gevolgd worden door ` INITIALLY DEFERRED` of `INITIALLY IMMEDIATE`. In het eerste geval wordt de constraint gechecked na elke transactie en in het tweede geval na elk statement.

Je kan constraints updaten met `SET CONSTRAINT`. Hieronder nemen we een constraint met naam `c`. Waarbij `constraint` eenderwelk bovenstaand constraint kan zijn.
```SQL
SET CONSTRAINT c <constraint>;
```

## Constraints
1. Op een enkel attribut
2. Op meerdere attributten

### NOT-NULL Constraint
Je kan een `NOT NULL` constraint opleggen door dit achter het attribut te schrijven. Dit zorgt ervoor dat geen enkele waarde een `NULL` value mag hebben en er dus altijd een reference moet zijn.
```SQL
CREATE TABLE u (
    t_id INTEGER REFERENCES t(id) NOT NULL
);
```

### CHECK Constraint
Je kan een `CHECK` constraint zien als een `WHERE` conditie voor een attribut die altijd moet gelden. Eerst geven we enkele voorbeelden van attribut-based constraints en daarna tuple-based constraints.
```SQL
-- syntax
CREATE TABLE t (
    c1 INTEGER CHECK <condition>
);
```

```SQL
-- example (attribute-based)
CREATE TABLE users (
    amount INTEGER CHECK (amount > 0),
    genders CHAR(1) CHECK (genders IN ('f', 'm'))
);
```

```SQL
-- example (tuple-based)
CREATE TABLE users (
    ...,
    CHECK (genders = 'f' OR name NOT LIKE 'Ms.%')
);
```

### Modification of constraints
Je kan een constraint een naam geven waardoor je het constraint later beter kan bewerken. Een primary key constraint zou er dan zo uit kunnen zien. Je kan hier ook een `CHECK` constraint benoemen. 
```SQL
CREATE TABLE t (
    id SERIAL CONSTRAINT IdIsKey PRIMARY KEY
);
```

### Altering constraints
Je kan een constraint verwijderen met het `DROP` keyword of een constraint pas later toevoegen via het `ADD` keyword in combinatie met `ALTER TABLE`.
```SQL
ALTER TABLE t DROP CONSTRAINT IdIsKey;
```
```SQL
ALTER TABLE t ADD CONSTRAINT IdIsKey PRIMARY KEY(id);
```

## Assertions (NIET VOOR PGSQL)
Assertions kunnen een algemeen constraint leggen op eenderwelke conditie. Je kan een assertion aanmaken alsvolgt.
```SQL
CREATE ASSERTION <aname> CHECK <condition>;
```

Je kan een assertion dan ook terug verwijderen met het `DROP` keyword.
```SQL
DROP ASSERTION <aname>;
```

## LES 5 VIEWS en TRIGGERS ...

## LES 8 Relational databases
anomalies: problemen veroorzaakt door slechte database schema's.
functional dependencies (FD): de veralgemening voor wat een key/ sleutel is voor de relatie.
normalization: het omzetten van relaties in meerdere kleinere relaties door anomalies te verwijderen.
multivalued dependencies: zorgen er voor herhaaling te elimineren.

### Functional Dependencies
decomposition: een relatie met meerdere attributen vervangen door meerdere relaties met 1 attribuut (beide hebben samen dezelfde algemene attributen)

A1, A2, ..., An --> B1, B2, ..., Bm
Is een functionele dependency als alle A's overeenkomen moeten ook alle B's overeen komen. Je kan dit dus zien als een functie die alle A's als input neemt en vervolgens alle B's teruggeeft. We kunnen dit enkel een functionele dependency noemen als dit voor alle gevallen van de relatie geldt en niet slechts enkele gevallen.

### Keys of Relations
{A1, A2, ..., An} is een key als: 
- Dit wil zeggen dat alle overige attributen functioneel worden bepaald. Het is dus onmogelijk om twee verschillende uitkomsten te hebben voor de rechterkant.
- Er is geen goede subset van {A1, A2, ..., An} die alle andere attributen bepaald. (de sleutel is minimaal)

### Superkeys
Een set van attributen dat een alle attributen van een key bevat is een super key. Elke (minimal)key is dus een superkey maar niet omgekeerd. 

### Transitive rule
A -> B, B -> C dan A -> C

### Splitting/Combining rule
A1, A2, ..., An --> B1, B2, ..., Bm 
<=> 
A1, A2, ..., An --> B1 
A1, A2, ..., An --> B2 
... 
A1, A2, ..., An --> Bm 

### Trivial FD's 
Een FD is trival als de rechterkant een subset is van de linkerkant. Elke triviale FD geldt dan ook aangezien een subset overal geldt als de set overal geldt.

### Closure
De closure van {A1, A2, ..., An} is gelijk aan {A1, A2, ..., An}+.

1. Gebruik de splitting rule en pas deze toe op alle FD's
2. Maak een nieuwe set X die uiteindelijk de closure is.
3. Zoek herhaald naar de FD's
4. Waarbij de linkerkant al in de set zet en de rechterkant niet. Hierdoor kan je de rechterkant nu ook toevoegen.
5. Herhaal tot er geen attributen meer kunnen toegevoegd worden.

Als {A1, A2, ..., An}+ de closure is dan is {A1, A2, ..., An} een super key. 

### Minimal Basis
- Een verzameling van alle gelijkaardige FD's van een relatie.
- Alle FD's hebben een enkel attribuut aan de rechterkant (single-ton).
- Als een FD van de basis verwijderd wordt is het niet langer een basis.
- Als een attribut van een linkerkant van een FD verwijderd wordt is het resultaat geen basis meer.
- Er kunnen geen triviale FD's in de basis bestaan.


