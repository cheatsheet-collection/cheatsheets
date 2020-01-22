# CSS3 summary 2018-2019 Uhasselt
Created by Ingo Andelhofs  
Student at Uhasselt

## Intoduction
- CSS dient om je html structuur op te maken door er styling aan te geven.
- Een aparte file met alle styling `.css`. 
- Niet alle browsers support'n alle css.
- Check support at [CanIUse](http://caniuse.com/)

```css
/* Basis structuur van een css selectie. */
selector {
    property: value;
}

/* Type selector */
type { ... }

/* Class selector */
.class-name { ... }

/* Id selector */
#id-name { ... }

/* Combinations of selectors */
type.class-name > #id-name { ... }

/* Universal selctor */
* { ... }
```

## Best practices
- De beste manier om je css aan html te linken is via een extern .css bestand. Als je gebruik maakt van inline/document-level styling meng je de structuur van html met de styling van css wat niet de bedoeling is.
- Probeer ook altijd css regels met dezelfde selectors samen te houden. 
- De laatste css regel of die met de hoogste prioriteit wordt behouden als je overschrijft.
- Je kan andere stylesheets schrijven voor verschillende media tags (print, screen, width, mobile, ...).

## Fonts
```css
selector {
    font-family: 'option1', 'option2', sans-serif; 
    /* Andere fallbacks: serif, monospace. */
    /* Ook kan je web-safe fonts zoals 'Verdana', 'Georigia', ... gebruiken. */
    /* Simpele fonts hebben vaak minder render tijd. */
    /* Ook kan je web-embedded fonts gebruiken die dan via Google fonts/Eigen server kunnen worden gedownload. */

    font-size: 16px; 
    /* Alternatieve eenheden: ems, rems. */
    /* In CSS3 verkeizen we rems. */
    /* Voordelen: De tekst wordt afhankelijk van het device bepaald. */
    /* Em gaat relatief van zijn parent resizen. Hoe meer parents, hoe kleiner/groter de scaling. */
    /* Rem daarentegen is relatief ten opzichte van de root. */

    line-height: 16px;      
    /* Lijn hoogte */
    
    font-style: underline;  
    /* italic, underline, ... */
    
    font-weight: 400;       
    /* light, bold, dark */
}
```

## Colors
```css
selector {
    /* naam:    blue, red, ... */
    /* rgb:     rgb() */
    /* rgba:    rgba() */
    /* hsl:     hsl() */
    /* hex:     #fff */

    color: red;
    background-color: rgba(0, 0, 0, 0.5);
}
```

## CSS Box Model
- Content > padding > border > margin;
- Color, background, ... is zichtbaar tot de border
- Margin is altijd transparant.
- vertical margin collapse (als je twee elementen boven elkaar hebt wordt de grootste margin behouden).
- Je kan center alignen met `margin: auto;`.

```css
selector {
    /* Format: top, right, bottom, left; */
    /* Format: top-bottom, right-left; */
    /* Format: top-right-bottom-left */

    padding: 10px;
    border: 1px solid green;
    margin: 20px 10px;
}
```

## Floats (OUTDATED)
- Relative to parent.
- Syntax: `float: right;`.
- Na een float moet je ook een clear doen zodat onderliggende onderdelen nog steeds de juiste layput hebben.
- Een column based design kan je maken door meerdere `float-left;`s te gebruiken. En een width in %.

## Tables
```css
table {
    border: 1px solid #000;
    text-align: right;
    ...
}
```

## Responsive design (PARTLY OUTDATED)
- Maak gebruik van media-queries.

## Veel gebruikte layouts
- Containers / wrappers (deze hebben een vaste breedte van bijvoorbeeld 80% en worden overal consitent toegepast).
- Menu's zijn lijsten van links.


## Pseudo selectors & attribute selectors
```css
a:link {...}
a:focus {...}
a:hover {...}
a:visited {...}
a:active {...}

input[type='submit'] {...}
```