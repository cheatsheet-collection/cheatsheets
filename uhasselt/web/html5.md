# HTML5 summary 2018-2019 Uhasselt
Created by Ingo Andelhofs  
Student at Uhasselt

## Introduction WWW
Enkele bekende namen:
- HTTP of HyperText Transfer Protocol - 1991 door Tim Berners-Lee
- Eerste webbrowser, WWW project - Robert Cailliau

De eerste webbrowsers:
- Uitwisseling van tekstuele informatie
- Commando's moesten manueel worden uitgevoerd

Het WWW:
- WWW != het internet
- WWW is een service die runt op het internet
- HTML of HyperText Markup Language


## Voorgangers van HTML
### SGML
Het concept van tags:
- begin tag &lt;tagname&gt;
- eind tag &lt;/tagname&gt;

Attributes/properties en attribute values:
- &lt;tagname attribute="value"&gt;

Comments:
- &lt;!-- comment -->
- Je kan geen -- gebruiken in je comment.
- Je kan ook geen &lt; of &gt; gebruiken.

Document Type Definition:
- Voor het maken van complexere structuren.

### XML
- Maakt gebruik van tags (begin en eind)
- Case gevoelige namen.
- Tags zijn niet voor-gedefinieert zoals HTML.

### HTML
- HTML is based on SGML.
- Geen eind tag verplicht.
- Niet case gevoelig.
- Browsers zijn minder gevoelig voor fouten.

### XHTML
- HTML die aan de XML standaard voldoet.
- Lower case letters.
- Eind tags verplicht.
- Inline elementen moeten in een block geschreven worden.

## HTML5
Focus op: 
- Indeling inhoud en presentatie.
- Media elementen.
- Betere semantiek.
- Betere foutafhandeling.

Verplichtingen:
- Gebruik lowercase tags.
- Gebruik altijd eind tags.
- Als je een attribut value aangeeft, doe dit met quotes.
- Elke document start met &lt;!DOCTYPE html&gt;

Basis skeleton:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Document title</title>
  </head>

  <body> 
    <!-- Comment -->
    <p>Sample text here...</p>
  </body>
</html>
```

DOM of Document Object Model:
- Is een boom voorstelling van je webpagina.

Content vs Visuals:
- Probeer zo weinig mogelijk styling tags te gebruiken als `b`, `i`, `br`, `hr`, ...
- HTML zorgt voor de structuur.
- CSS zorgt voor de styling van de HTML structuur.

Head tag:
- Meta data verzamelen.
- Veelgebruikte tags `meta`, `title`, `style`, `link`, `script`, ...

Body tag:
- Het visuele wat we zien als we de webpagina bekijken.
- Alles wat gerendered moet worden.

Headings:
```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
<h4>Heading 4</h4>
<h5>Heading 5</h5>
<h6>Heading 6</h6>

<p>Paragraph</p>
<pre>Preformatted Paragraph</pre>
```

Lists:
```html
<!-- Ordered List -->
<ol>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ol>

<!-- Unordered List -->
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

Images:
```html
<img src='path/image.png' alt='An image of a ...'>
<figcaption>Caption here</figcaption>
```

Tables:
```html
<!-- Gebruik tables enkel als een tabel. Niet voor layout. -->
<table>
  <caption>A caption for your table.</caption>

  <thead>
    <tr>
      <th>Col1</th>
      <th>Col2</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>Item 11</td>
      <td>Item 21</td>
    </tr>
    <tr>
      <td>Item 12</td>
      <td>Item 22</td>
    </tr>
  </tbody>
</table>
```

Article:
```html
<!-- Visueel zie je geen verschil. Wordt gebruikt door search engines, styling, ... -->
<!-- Gebruikt voor eender welk soort item. -->
<article>
  <!-- Content here... -->
</article>
```

Section:
```html
<!-- Zoals article is dit puur een structurele indeling voor een sectie. -->
<section>
  <!-- Content here... -->
</section>
```

Figures:
```html
<!-- Representeerd een deel content met een evenuele cpation. -->
<figure>
  <p>A paragraph</p> <!-- or <img src='...' alt='...'> -->
  <figcaption>A caption</figcaption>
</figure>
```

Nav en header/footer:
```html
<header>
  <!-- Header content -->
  <nav><!-- Navigation content --></nav>
</header>

<footer>
  <!-- Footer content -->
  <nav><!-- Navigation content --></nav>
</footer>
```

Divs:
```html
<!-- Dit is slechts een container voor content. Vaak in combinatie met een class attribute. -->
<!-- Vaak gebruikt als er geen standaard html element bestaat. -->
<div class='class-value'>
  <!-- Content here... -->
</div>
```

Links:
```html
<a href='http://www.example.com'>Alias voor de link.</a>

<element id='example-anchor'></element>
<a href='#example-anchor'>Anchor alias tekst.</a>
```

Text styling:
```html
<em>Italic text.</em>
<strong>Bold text.</strong>

<code></code>
<var></var>
<small></small>
<abbr></abbr>
<time></time>
...
```

Spans:
```html
<!-- Vergelijkbaar met div maar voor inline-text -->
<p>
  <span id='id-value'>Special inline style...</span>
</p>
```