# Entity-Relationship-diagrammen
1. Entity Sets
2. Attributes
3. Relationships

## Entity Sets (rechthoek)
Een collectie van entiteiten. Je kan een entity set zien als een collectie van data waarbij de naam van de entity set beschrijft welke data er wordt bijgehouden.

## Attributes (ovaal)
Vergelijkbaar met de attributen/kolommen van een tabel. Ze geven aan wat er wordt bijgehouden in een entity set. 

## Relationships (diamant)
Relaties geven weer wat het verband is tussen verschillende entity sets. Vaak is dit tussen slechts 2 entiteiten en noemen we dit binaire relaties.




## ER to Relational Designs
### Entiteiten
- Turn each entity set into a relation with the same set of attributes.

### Relaties
- Replace a relationship by a relation whose attributes are the keys for the connected entity sets.
- For each entity set involved in relationship R, we take its key attribute or attributes as part of the schema of the relation for R.
- If the relationship has attributes, then these are also attributes of relation R.
- Als dezelfde entiteit meerdere keren voorkomt komen ook zijn keys meerdere keren voor (met een andere naam om dublicatie te vermijden)

- Relaties combineren: Als we veel many-one relaties hebben kan je ook alle attributten van relatie E nemen en de keys van F waarbij E aan de one kant ligt.

### Entities
- The relation for the weak entity set W itself must include not only the attributes of W but also the key attributes of the supporting entity sets. The supporting entity sets are easily recognized because they are reached by supporting (double-diamond) relationships from W. 

- The relation for any relationship in which the weak entity set W appears must use as a key for W all of its key attributes, including those of other
entity sets that contribute to W ’s key.

- However, a supporting relationship R, from the weak entity set W to a supporting entity set, need not be converted to a relation at all. The justification is that, as discussed in Section 4.5.3, the attributes of manyone relationship R's relation will either be attributes of the relation for W , or (in the case of attributes on R) can be added to the schema for W 's relation.
