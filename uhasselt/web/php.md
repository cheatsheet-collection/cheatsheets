# PHP summary 2018-2019 Uhasselt
Created by Ingo Andelhofs  
Student at Uhasselt

## Introduction
Php is een Server Side taal die gebruikt kan worden voor database acces, form validation, mailing, content creation, photogalleries, ... Php moet op een server gerunt worden en kan niet via de browser worden geinterpreteerd.

## HTTP
- Request/reply system.
- Browser stuurt een GET request en krijgt data terug (vaak html).
- Websites die meerdere files/images nodig hebben vergen dus ook meerdere GET requests.

## PHP
De server zet de php om in html via echo etc. en stuurt een complete webpagina naar de gerbuiker. PHP WORDT DUS NOOIT NAAR DE GBERUIKER GESTUURD. PHP kan dus gebruikt worden om html te genereren.  

## Syntax
Alle php code die we schrijven moet tussen &lt;?php en ?> geschreven worden. De file extensie moet ook .php zijn.

### Variables
Variabelen moeten beginnen met een $.
```php
$var = 1;
$var = 'hello';
```

### Arrays
```php
$array = [1, 2, 3];
$assoc_array = [
    "een" => 1,
    "drie" => 3
];

$assoc_array['twee'] = 2;

foreach($assoc_array as $key => $val) {
    echo "$key => $val";
}
```

### $_POST en $_GET
Als je iets via een form submit kan je dat in php opvangen met `$_POST` of `$_GET` afhankelijk van je request. Je kan hiermee data in de database vergelijken etc. het nadeel is wel dat je voor elk request een page reload nodig hebt.

### PDO
```php
try {
    $connection = new PDO("pgsql: host=location; dbname=test; port=5432;", "uname", "pwd");
}
catch(PDOException $e) {
    print "Error: {$e->getMessage()}";
}

$query = $connection->prepare("SELECT * FROM tablename WHERE col = :col;");
$query->bindParam(':col', $col, PDO::PARAM_STR, 255);

if ($query->excecute()) {
    $data = $query->fetchAll();
    foreach($data as $row) {
        // Code here...
    }
}
else {
    die "Database fail... {$connection->errorInfo()}";
}
```