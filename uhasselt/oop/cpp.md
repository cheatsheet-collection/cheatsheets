# C++ Cheat Sheet
Ingo Andelhofs   
1ste bachelor informatica


## Introductie
C++ is een object-georiënteerde taal ontworpen door de Noor Bjarne Stroustrup. C++ groeide uit de taal C waardoor het geen echte/pure (oo) taal is. C++ is een taal voor performantie, efficiëntie en flexibiliteit. De taal is nog steeds actief met C++20 in de maak. 

### Imperatief vs Object Georiënteerd
> software structuur bepaald door functies  
> vs  
> software strutuur bepaald door objecten

## Object Georiënteerd ontwikkelen
### Hello World
Een simpel hello world voorbeeld wat zeer hard overeen komt met C.
```cpp
#include <iostream>

int main() {
    std::cout << "Hello World" << std::endl;
}
```

### ADT (Abstract DataType)
- De complexiteit van de implementatie wordt afgeschermt wat we `information hiding` noemen. 
- Toegang tot het ADT moet via `operaties` gebeuren.

## Invoer en uitvoer (+ files)
In c++ wordt er voor in- en uitvoer gebruik gemaakt van streams. Voor output kennen we `cerr` en `cout`. Voor invoer kennen we dan `cin`. Om data in te lezen of uit te schrijven gebruiken we de `<<` en `>>` waar deze de richting van de stream weergeven.  

```cpp
// Invoer:
// Lees 1 woord in
std::string str{};
std::cin >> str;

// Lees in tot een newline
std::getline(std::cin, str);

// Lees een int, char, ... in
int i{};
char c{};
std::cin >> i;
std::cin >> c;
```

```cpp
// Uitvoer:
// Lees 1 woord in
std::string str{"uitvoer ..."};
std::cout << str << std::endl;
```

### Range Bases for-loop
```cpp
std::vector<int> numbers{1, 2, 3};

for (auto number : numbers) {
    std::cout << number;
}
```


## Klassen en Members
### Een simpel klasse template
```cpp
class ClassName {
    public:
        // Constructor
        // Destructor

        // Getters
        // Setters
        // Utils

    private:
        // private member variables
        // private member functions (helpers)

    protected:
        // Only accessible by the derived class 
        // protected member variables
        // protected member functions (helpers)
};
```

### Een klasse aanmaken
```cpp
// On the stack
ClassName newSClass{param1, param2};

// On the heap
ClassName* newHClass{ new ClassName{param1, param2} };
```

### Members in klassen
```cpp
// MyClass.h
class MyClass {
    public:
        void aMethode();
    private:
        int m_aMemberVariable;
};

// MyClass.cpp
#include "MyClass.h"
void MyClass::aMethode() {
    // Code hier ...
}
```

### Const in klassen
Je kan achter je klasse method `const` toevoegen waardoor je in deze method geen aanpassingen kan doen aan member variabelen of functies kan oproepen die niet const zijn. Wil je dat sommige member variabelen wel kunnen worden aangepast moet je voor het type `mutable` zetten.

### Constructors
De constructor wordt aangeroepen bij het aanmaken van een klasse. Als je zelf geen constructor aanmaakt wordt deze door de compiler voorzien. Je kan toch een default laten genereren door `MyClass() = default;` toe te voegen. Ook kan je constructors hergebruiken in andere constructors of default parameters meegeven. 

```cpp
// MyClass.h
class MyClass {
    public:
        MyClass(params...);
};

// MyClass.cpp
MyClass::MyClass(params...) : m_param1{p1}, m_param2{p2} {
    // Verdere initializatie...
}
```

### Destructors
De destructor wordt opgeroepen bij het verwijderen van een klasse. Dit gebeurt als de scope afloopt. Als je in de constructor membervariabelen alloceert op de heap met `new` moet je in de destructor deze ook terug verwijderen met `delete` om memory leaks te vermijden.

```cpp
// MyClass.h
class MyClass {
    public:
        ~MyClass();
};

// MyClass.cpp
MyClass::~MyClass() {
    // Ruim eventuele gealloceerde data op...
}
```

### Converting constructors
Eerst een type converten en dan bewerken is niet altijd efficiënter maar dit kan wel handig vanpas komen. Als je dus een constructor voorziet voor bv. `const char*` naar een `MyString` kan je dus ook ipv een `s1.concat(MyString)` een `s1.concat(const char*)` zonder problemen uitvoeren.


### Copy Constructor
Een copy constructor is een constructor die een kopie maakt van een bestaand object en zo dus een nieuw object aanmaakt. Default is dit een shallow copy en willen we dus onze eigen copy constructor maken die een deep copy maakt. Een voorbeeld van een copy is als je een getal vermenigvuldigt met een coördinaat klasse.
```cpp
MyClass(const MyClass& mc) {
    // Copying here....
}
```

### Move Constructor
Een move constructor is een constructor die de inhoud van een klasse verplaast naar een nieuw object en dus alle members overzet. Het is belangrijk dat er een mogelijkheid is om te move'n. Dit kan namelijk veel efficiënter zijn dan slechts het object te kopiëren (geen allocatie, geen kopie). Je kan ook een move forceren via `std::move`. Een voorbeeld waar move wordt gebruikt is bij het teruggeven van een temp value van een functie.
```cpp
MyClass(MyClass&& mc) {
    // Moving here....
}
```

### Copy/Move algemeen.
Vaak voorzie je ook een copy/move assignment operator. Als je een copy/destructor/assignment toevoegt wotdt er default geen move meer aangemaakt.  
Je voorziet een copy/move voor:
- Initialisatie.
- Return By Value.
- Pass By Value.

### Rvalues en Lvalues
Een `lvalue` is een expressie waarvan je het adress kan opvragen. Een `rvalue` is een expressie die geen `lvalue` is. Een `lvalue` reference wordt weergegeven met `&`. Terwijl een `rvalue` reference wordt weergegeven met `&&`. 


## C++ features part 1
### New, Delete and Nullptr
In C++ kan je ook types op de heap alloceren zoals in c. Hiervoor gebruik je echter `new type` om een nieuwe allocatie te doen voor type. Deze verwijder je dan weer door `delete` aan te roepen. Je kan met `new` ook meerdimentionale array's aanmaken zoals `new int[2][2]`. Deze kan je dan met `delete[]` weer verwijderen.

### STL
C++ voorziet een heel deel containers en algoritme in de STL (STandard Library). Waaronder `vector`, `array`, `list`, `set`, `map`, `stack` en `queue`. Ook wordt er een basic `string` voorzien. Enkele functies hiervan bespreken we later.

### References
Naast pointers heb je in C++ ook references. Dit is echter een alias voor het originele element. Als je aan een functie/method een reference parameter mee geeft dan wordt er geen kopie gemaakt maar een alias meeegegeven naar dat element. Je kan wel geen alleenstaande (constante) elementen meegeven aan deze functie/method aangezien hier geen reference van gemaakt kan worden. Je kan parameters voor de rest meegeven als gewone parameters. In C++ verkies je vaak Const references.
```cpp
// Een swap voorbeeld
void swapRef(int &r1, int &r2) {
    int temp{r1};
    r1 = r2;
    r2 = temp;
}

// Een int ref
int x{5};
int &y{x}; // y is een reference naar x
```

### Templates
Je kan in C++ ook templates voor functies/methods/classes voorzien. 
```cpp
// Functies/Methods
template <typename T>
T max(T a, T b) {
    return a > b ? a : b;
}

// Classes
template <typename T>
class MyClass {
    public: 
        MyClass(T data) : m_data{data} {}
    private:
        T m_data;
};

// Aanroepen
max<int>(4, 3);
MyClass<char> mc{'c'};
```

### Niet besproken features
- auto -> &, const, decltype(), ...
- inline
- default arguments
- std::pair, std::max
- static (in klasse)
- enum class `enum class Color{ Red, Blue, Green };`
- #pragma once (compilers)
- forward declaration


## Inheritance
### Introductie
Als je een subklasse maakt waar een 'is een' relatie geldt. Bijvoorbeeld een student is een persoon. Dan kan je hier inheritance gebruiken. De `Student` klasse kan nu aan alle `public` en `protected` members van `Person`. De private members van `Person` kan je niet accessen. De `Student` class erft zeg maar over van `Person`.
```cpp
class Person {
    // ...
};

class Student : public Person {
    // Een Student is nu ook een Person
    // Alles van person + ...
};
```

### Constructors en destructors
Bij het aanmaken van een `Student` klasse wordt eerst de constructor van `Person` aan geroepen en dan pas die van `Student`. Algemeen wordt dus eerst de baseclass constructor aangeroepen en dan de subclass constructor. Als we het over destructors hebben wordt in het voorbeeld eerst die van `Student` aangeroepen die vervolgens de destructor van `Person` aanroept. In de initializer list van `Student` kan je nu ook een `Person` constructor aanroepen.   
Als we het hebben over een Vector van `Person*` en we hebben de destructor van `Person` niet virtual gemaakt zal enkel de `Person` destructor worden aangeroepen. Zie virtual destructors.

### Copy en Move
Als je afgeleide/subklasse een move/copy constructor heeft wordt default de 'default constructor' van de base/superklasse aangeroepen. Als je toch wilt dat de copy/move wordt aangeroepen van je base class ipv de default constructor moet je de copy/move via de initializatie lijst van de subclass meegeven.

```cpp
class Base {};

class Sub : public Base {
    public:
        Sub::Sub(const Sub& s) : Base{s};
        Sub::Sub(Sub&& s) : Base{std::move(s)};
};
```

### Toegankelijkheid
Wanneer je afleid van een Base class.  
- **public:** public->public, protected->protected
- **protected:** public->protected, protected->protected
- **private (default):** public->private, protected->private


### Multiple inheritance
In C++ kan je van meerdere klassen inheriten. Dit kan echter soms wel voor probelemen zorgen wanneer functienamen dezelfde naam hebben. Dit kan je oplossen door specifiek te vermelden van welke klasse je dit wilt aan roepen door gebruik van `MyClass::method()`. Ook kan je het diamant probleem tegen komen wat hieronder wordt aangetoont. We gebruiken hier `virtual public` om aan te tonen dat we slechts van 1 `Person` moeten inheriten en niet twee keer van `Person` wat voor problemen kan zorgen.

```cpp
class Person {...};
class Student : virtual public Person {...};
class Employee : virtual public Person {...};
class PHDStudent : public Student, public Employee {...};
```

## Polymorpism
### Introductie
In C++ en andere OOP talen heb je de mogelijkheid om een overriden method met eenzelfde signature op te roepen vanaf de Base- of Subclass. Dit is mogelijk door polymorphisme. Als je bijvoorbeeld een Person pointer of een reference hebt naar een Student/Employee. En je roept een method aan die zowel door Student als Employee wordt ondersteunt kan je afhankelijk van wat er in de Person pointer/reference zit andere functionaliteit uitvoeren. Je moet er wel voor zorgen dat deze worden overschreven met `virtual` en eventueel `override`. Wil je toch een method van bv. Person aanroepen in kan die via Person::method(). Je kan het gebruik van `virtual` ook laten stoppen door gebruikt te maken van het keyword `final`. Dit geeft aan dat dit de laatste versie is van een method waardoor je in een afgeleide klasse niet meer kan overriden.

```cpp
class Person {
    public:
        virtual void print() const override;
};
class Student : public Person {
    public:
        void print() const override;
};

// Beide klassen bevatten een functie print met zelfde signature. 
// Deze wordt in student overschreven met virtual en override.
// Als we nu een Person pointer aanmaken met een student in kunnen we via print de functie van Student aanspreken.

Person* aPerson{ new Student{} };
aPerson->print(); // De print functie van Student wordt hier aangeroepen
```

### Object slicing
Als je niet met pointers of references werkt kan er object slicing optreden. Dit wil zeggen dat je bijvoorbeeld een `Student` aan een `Person` toekent waardoor alle `Student` data verloren gaat en er enkel nog `Person` data overblijft.

```cpp
Student stud{};
Person pers{stud}; // slicing

aFunction(stud); // slicing if signature -> aFunction(Person p) {...}
```

### Early/Late binding
**Early binding:** Als een method van een Subclass en Baseclass dezelfde signature hebben en deze wordt in de Baseclass niet als `virtual` gemarkeert dan zal er altijd early binding optreden. Dit wilt zeggen dat als je een `Baseclass*` aanmaakt en er een `Subclass*` in steekt dat als je dan deze method aanroept die niet `virtual` is je toch de method van de Baseclass gaat aanroepen ookal wil je dit vaak niet. Om dit op te lossen kan je `virtual` toevoegen. Ook kan je deze Person pointer casten naar een Student pointer via `dynamic_cast<Student*>()`.

**Late binding:** Als een method van een Subclass en Baseclass dezelfde signature hebben en deze wordt in de Baseclass wel als `virtual` gemarkeert dan zal er altijd late binding optreden. Dit wilt zeggen dat als je een `Baseclass*` aanmaakt en er een `Subclass*` in steekt dat als je dan deze method aanroept die `virtual` is je ook de method van Subclass zal aanroepen ookal zit deze in een `Baseclass*`. Bij late binding wordt pas tijdens het runnen beslist welke functie er wordt opgeroepen. Dit gebeurt aan de hant van een Vtable of Virtual Table. 

### Virtual destructor
**Algemene regel:** Ofwel maak je de constructor public en virtual, ofwel maak je deze protected en niet-virtual.

### Abstracte klassen
Als je wilt dat een klasse enkel kan gebruikt worden om van te inheriten kan je een klasse of haar methodes pure virtual maken. Hierdoor moeten alle afgeleide klassen deze method implementeren. Bijvoorbeeld een Abstracte klasse Shape. Die kan gebruikt worden voor een Rect, Circle, ... aan te maken.

```cpp
class Shape {
    public:
        virtual void draw() const = 0; // Pure virtual
};
```

## Operator overloading
In C++ heb je de mogelijkheid om bepaalde operator over te schrijven met zelfgekozen functionaliteit. Het is echter niet de bedoeling dat je onbegrijpbare operatoren gaat inbouwen die geen duidelijke betekenis hebben. 

**In een klasse:** Je schrijft je overloaded operator binnen de klasse als een deel van de method deel is van de klasse. Zo heb je bijvoorbeeld twee operator+() met 1 extra parameter en de klasse zelf. Waarbij de klasse + param wordt uitgevoerd.  
**Buiten een klasse:** Je schrijft overloaded operator buiten de klasse als je de volgorde van 'klasse + param' bv wilt omwisselen. Of gewoon de klasse zelf niet wordt gebruikt. Zoals bij ostream. Je gebruikt hier bv al geïmplementeerde operators als +=, ...   
**Buiten een klasse (als friend):** Als je toch nog member variabelen moet kunnen bewerken buiten de klasse gebruik je het keyword friend om hier toegang tot te krijgen of zorg je voor de nodige getters.    

```cpp
// We nemen als voorbeeld een Point klasse die de meeste operators overload

class Point {
    private:
        int m_first;
        int m_second;
    
    public:
        // Constructors
        Point(int f = 0, int s = 0) : m_first{f}, m_second{s} {}
        Point(const Point& p) : m_first{p.m_first}, m_second{p.m_second} {}
        Point(Point&& p) : m_first{p.m_first}, m_second{p.m_second} {}

        // Destructors
        ~Point() = default;

        // Assignment operatoren
        Point& operator=(const Point& p) {
            m_first = m_first;
            m_second = p.m_second;
            return *this;
        }
        Point& operator=(Point&& p) {
            m_first = m_first;
            m_second = p.m_second;
            return *this;
        }

        // Copy swap assignment (move + copy)
        swap(Point& p) {
            std::swap(m_first, p.m_first);
            std::swap(m_second, p.m_second);
        }

        Point& operator=(Point p) {
            swap(p);
            return *this;
        }

        // Operator overloading
        Point operator-() {
            return Point{-m_first, -m_second};
        }

        Point& operator++() {
            ++m_first;
            ++m_second;
            return *this;
        } 

        Point operator++(int) {
            Point temp{*this};
            ++(*this);
            return temp;
        }

        Point& operator+=(const Point& p) {
            m_first += p.m_first;
            m_second += p.m_second;
            return *this;
        }

        Point& operator*=(const int i) {
            m_first *= i;
            m_second *= i;
            return *this;
        }

        int operator[](const int index) {
            return (index == 0) ? m_first : m_second;
        }

        // Friend operator overloading
        friend bool operator==(const Point& p1, const Point& p2) {
            return (p1.m_first = p2.m_first && p1.m_second == p2.m_second);
        }

        friend std::ostream& operator<<(std::ostream& stream, const Point& p) {
            stream << '(' << p.m_first << ',' << p.m_second << ')';
            return stream;
        }

        // Cast operator
        operator std::pair<int, int>() {
            return std::pair{m_first, m_second};
        }
}

// Non-friend operators
Point operator+(const Point& p1, const Point& p2) {
    return Point{p1} += p2;
}

Point operator*(const Point& p, const int i) {
    // Dit geldt enkel voor Point + int niet voor int + Point
    return Point{p} *= i;
}
```

## Smart pointers
In C++ is er een nieuwe manier om pointers op te slaan waardoor je geen rekening meer moet houden met het verwijderen van je pointer. Dit kan met behulp van de smart pointer klassen van C++. 

### Unique pointers
Een unique pointer kan maar één keer bestaan en niet gekopiëert worden maar wel verplaatst met bv std::move(). Ook als je een unique pointer aanmaakt in een klasse als member variabele worden automatisch de copy/copy-assignment operatoren verwijderd. Je moet hier dus shared pointers gebruiken of zelf de copy functionaliteit voorzien.

```cpp
// Een pointer naar een int aanmaken
std::unique_ptr<int> int1{ new int{10} };

// Alternatief met std::make_unique
std::unique_ptr<int> int2{ std::make_unique<int>{10} };

// Int arrays of 5 ints
std::unique_ptr<int []> ints{ std::make_unique<int []>{5} };

// Get raw pointer (returns pointer)
int1.get();

// Move the pointer
auto int3{ std::move(int2) };

// De pointer terug geven aan de developer (returns pointer)
int1.release();

// De pointer opruimen
int1.reset();
```

### Shared pointers
Als je toch wilt kopiëren moet je gebruik maken van de std::shared_ptr en std::make_shared klassen. Er wordt via `reference counting` bijgehouden hoeveel pointers er nog zijn en deze worden opgeruimt als er dus 0 instaties over zijn. De werking is hetzelfde als de unique_ptr met als extra functie dat je `p.use_count()` kunt aanroepen voor de reference count. 

## Streams en File IO
Includes: &lt;iostream&gt;, &lt;ios&gt;, &lt;streambuf&gt;, ... 

### Manipulators (ios)
Je kan eender welke van onderstaande functionaliteit toevoegen aan de stream via <<. Hierna wordt hun functionaliteit op achterliggende types toegepast.
- std::setprecision(int): Voeg cijfers na de komma toe.
- std::setfill(char): Vul string op met 'char' totdat std::setw(). 
- std::setw(int): Geeft het totaal aantal chars weer.
- std::hex, std::oct, std::dec: Zet om naar hex, oct, dec.

### Files
Files worden geopend door de constructor of `.open()`. Je kan de file sluiten met `.close()` of dit gebeurt zelf. Vervolgens kan je via `<<` en `>>` schrijven en lezen naar een file of je kan dit via `getline()` doen. Vaak word er als vlogt een if rond gezet `if (std::ofstream out{"file.txt"}) {...`. Via `read()` en `write()` kan je ook naar .dat files schrijven hiervoor moet je wel `std::ios::binary` gebruiken als tweede parameter.

- std::ofstream (schrijven naar een file)
- std::ifstream (lezen van een file)

### String streams
- std::istringstream sstream{aString};

Vervolgens kan je >> gebruiken om data naar een type uit te schrijven.

## Exception handling
### Een simpel voorbeeld
```cpp
try {
    // Code here
    if (indexOutOfRange) {
        throw std::out_of_range{"Index out of range"};
    }
}
catch(const std::out_of_range &e) {
    std::cerr << e.what();
}
catch(...) {
    std::cerr << "Another error occured...";
}
```


<!-- 

## C++ Standard Template Library (STL)
### std::string
### std::vector
### std::array
### std::stack
### std::map
### std::tuple
### std::pair 

-->