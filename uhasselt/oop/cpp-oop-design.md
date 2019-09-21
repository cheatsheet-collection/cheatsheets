# OOP Design Cheat Sheet
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
        void newGame();
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
- RULE: Don't talk to strangers.

Nadelen (High Coupling)?
- De klasse is te afhankelijk van andere klassen.
- Als je een klasse aanpast kan dit een andere klasse beïnvloeden.
- Niet altijd mogelijk om Low Coupeling toe te passen.
- Je kan vak aan teveel gegevens van andere klassen. Dit kan de state van een klasse (nadelig) beïnvloeden. 
- Samenhangende functies worden apart uitgevoerd.

Levels (High -> Low)?
- X is afgeleid van Y.
- X bevat een pointer naar Y.
- X roept een functie in Y aan.
- X method verwijst naar Y. (param, var, return)

```cpp
class Piece {
    public:
        void moved();
};

// Low Coupling (GOOD)
// De pion wordt verplaatst en en in die functie wordt de state van die pion op moved gezet.
board->movePiece(from, to);         // In Game
piece->moved();                     // In Game->Board->movePiece

// High Coupling (BAD)
// De pion wordt verplaatst. Apart wordt de state op moved gezet. 
// Hier moet Game dus met 2 dingen rekening houden. Terwijl board dit ook kan.
getBoard()->movePiece();            // In Game
getBoard()->getPiece()->moved();    // In Game
```

### Information Expert
Wat?
- Geef de verantwoordelijkheid aan de klasse die de nodige informatie al bevat.

```cpp
// BAD
Game::Print() {
    // print( m_board->piece(x, y) )
    // print( p->color )
}

// GOOD
Game::Print() {
    // m_board->print()
}
Board::Print() {
    // m_piece->print()
}
Piece::Print() {
    // ...
}
```

### Creator
Wat?
- Wie is verantwoordelijk voor het aanmaken en verwijderen van klasse A?

Wanneer mag A een B aanmaken/deleten.
- A bevat B.
- A houdt de state van B bij.
- A maakt sterk gebruik van B.
- A data bevat die nodig is om B aan te maken.

```cpp
class Bike {
    private:
        Wheel m_wheel1;
        Wheel m_wheel2;
        Frame m_frame;
};

// BAD
int main() {
    Wheel* wheel1{ new Wheel{wheelSize} };
    Wheel* wheel2{ new Wheel{wheelSize} };
    Frame* bikeFrame{  new Frame{frameSize} };

    Bike myBike{ new Bike{wheel1, wheel2, bikeFrame} };
}

// GOOD
int main() {
    // Hier worden de wielen en het frame aangemaakt door het Bike object zelf waardoor je deze niet moet meegeven aan bike.
    Bike myBike{ new Bike{wheelSize, frameSize} };
}
```


## UML (Unified Modelling Language)
- Attributen toevoegen
- Beperkingen toevoegen
- Relaties toevoegen
- Klassen samenvoegen / splitsen / ...
- Graphische weergave
- Inzicht krijgen in bestaande code / nieuw ontwerp

### Public, Private en Protected
```cpp
// Code
class MyClass {
    public:
        void setValue(int newVal);
    private:
        int m_value;
    protected:
        int getValue() const;
}

// UML
----------------------------------
| (C) MyClass                    |
----------------------------------
| -m_value : int                 |
----------------------------------
| +setValue(newVal : int) : void |
| #getValue() : int {readonly}   |
----------------------------------
```

### Associaties (lijn)
Een gewone lijn tussen klasse A en klasse B wilt zeggen dat A bij B hoort. 
Je kan ook in B een reference naar een klasse A toevoegen.  
Multipliciteiten:
- `1`: exact 1
- `4`: exact 4
- `0..1`: 0 of 1
- `1..4`: 1 tot 4
- `0..* of *`: 0 of meer
- `4..*`: 4 of meer

### Aggregatie (lege diamant)
Er wordt verwezen naar iets (geen eigenaar). Bij aggregatie kan het object A bestaan zonder B te bevatten. 

### Compositie (volle diamant)
Bevat iets (wel eigenaar). Hier moet het object A het object B bevatten om te kunnen bestaan. Er is een 'A heef een B / A bevat een B' relatie.

### Enums en static members (cirkel met + in )
Het symbool aan de kant van de klasse. Niet de enum `<<enumeration>>`.

### Inheritance (lege driehoek)
Het symbool aan de kant van de Base class. Dus van subclass naar baseclass. Er is een 'A is een B' relatie.