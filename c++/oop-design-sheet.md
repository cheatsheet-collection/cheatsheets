# OOP Design Cheat SHeet
Ingo Andelhofs   
1ste bachelor informatica

## OOP ontwerp (GRASP)
### Information hiding
- De complexiteit van een klasse afzonderen van de gebruiker.
- De gebruiker moet een(zelfde) interface kunnen gebruiken afgezonderd van de implementatie.
- Je laat dus enkel de nodige functionaliteit van de klasse aan de gebruiker beschikbaar.

Voorbeeld:
```cpp
// String: 
// Je kan als gebruiker van string niet aan m_data, m_length aangezien dit interne details zijn en je hier geen kennis over nodig hebt. 
// Hierdoor kan je je bezig houden met hebt gebruiken van de klassen en niet het implementeren zelf.
private:
    int m_data;
    int m_length;
```


### Cohesion
Wat?
- Hoe sterk hangt de functionaliteit van een klasse samen?
- Doet de klasse slechts één (samenhangend) ding?
- Houdt deze zich ook bezig met taken die niet thuishoren in deze klasse?
- Zijn er uiteenlopende verantwoordelijkheden?
- Heeft de klasse een onduidelijke focus van wat de klasse doet?

Nadelen (Low Cohesion)?
- De klasse is moeilijk te begrijpen.
- Je kan de klasse niet hergebruiken.
- De klasse blijft groeien en veranderen.

```cpp
// High cohesion (GOOD):
class Game {
    public:
        void start();
        void update();
        void stop();
};

// Low Cohesion (BAD):
class Game {
    public:
        void new();
        void addPlayer();
        void doMove();
        void printMenu();
        void readUserInpiut();
        ...
};
```

### Coupling
Wat?
- Hoe sterk is de klasse verbonden met andere klassen. 
- Bevat de klasse veel informatie over andere klassen.
- Hoeveel weet deze klasse over andere klassen.
- Is de klasse afhankelijk van een andere klasse.

Nadelen (High Coupling)?
- 

```cpp

```




### Creator



## UML
### Arrows