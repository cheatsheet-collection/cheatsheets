# AJAX summary 2018-2019 Uhasselt
Created by Ingo Andelhofs  
Student at Uhasselt

## Introduction
Ajax is een manier om async een request te doen naar bv een .php file.
```js
let xhr = new XMLHttpRequest();

xhr.onreadystatechange = () => {
    if ((xhr) && (xhr.readyState == 4) && (xhr.status == 200)) {
        let result = xhr.responseText;
        // Code here...
    }
};

xhr.open("POST", "request.php", true);
xhr.send("firstname=John&lastname=Doe");
```

In php:
```php
echo json_encode($data);
```

In Ajax:
```js
let data = JSON.parse(xhr.responseText);
```
