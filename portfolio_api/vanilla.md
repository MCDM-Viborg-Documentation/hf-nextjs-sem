```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : Portfoile API
Doc         : vanilla
```

# Api & Vanilla Javascript.

Nu skal vi lige træde et skridt tilbage og kigge lidt på Vanilla Javascript og API.

Men inden vi kommer dertil så skal vi lige oprette en ny fil vi kalder `corsOptions.js` og placerer i `src/lib` mappen.

Opret `src/lib/corsOptions.js` og indsæt følgende.

```javascript
export const corsOptions = (methods) => {
     // 'GET, POST, PUT, DELETE, OPTIONS'
     return {
        status: 200,
        headers: {
        'Access-Control-Allow-Origin': '*',
        'Access-Control-Allow-Methods': methods,
        'Access-Control-Allow-Headers': 'Content-Type, Authorization',
        }
    }
}
```

Indtil nu har vi kunne tilgå vores api ved at kalde de enkelte endpoints. F.eks.
`http://localhost:3000/api/authors` og hvis vi indtaster urlen i vores browser ser vi JSON resultatet.

Vi ser resultatet uden problemer fordi vi kalder fra samme `domæne` i vores tilfælde `http://localhost:3000`.

Nu skal vi prøvet at kalde vores api fra en andet domæne og derfor skal vi angive hvilke endpoints man må tilgå fra et andet domæne og hvilke metoder. 
```
origin = '*' <-- Alle domæner må tilgå dette.
Access-Control-Allow-Methods : 'GET, POST, PUT, DELETE, OPTIONS' <-- Hvilke metoder skal være tilgængelige 
``` 

`corsOptions` metoden vi lige har oprettet giver os mulighed for at åbne for enpoints og tildele de metoder vi ønsker skal være mulige. F.eks `corsOptions('GET')` vil åbne for at man kan tilgå via GET metoden.

Åbn filen `src/app/(api)/api/authors/route.js` og udskift begge `NextResponse.json(result)` med `NextResponse.json(result, corsOptions('GET'))` og importér corsOptions filen `import { corsOptions } from "@/lib/corsOptions";`.

Nu kan vi kalde vores Authors endpoint fra en andet domæne.

## Opgave

Lad dette projekt køre. Men nu skal vi have oprettet endnu et projekt og åbne denne i visualcode.
Projektet skal være et vanilla html/javascript projekt som vi åbner med liveserveren.

Så opret en mappe (gerne ved siden af dette projekt) og kald den `portfolio_api_vanilla` i mappen opretter du:

:file_folder: portfolio_api_vanilla    
```
├── scripts
│   ├── index.js              
├── styles
│   ├── index.css        
├── index.html
```

index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vanilla API</title>
    <link rel="stylesheet" href="./styles/index.css">
    <script src="./scripts/index.js" type="module"></script>
</head>
<body>
    

    <div id="authors"></div>


</body>
</html>
```

index.css
```css
body {
    background-color: #444;
    color: #fff;
    width : 100%;  
}
```

index.js
```
fetch('http://localhost:3000/api/authors')
.then(response => response.json())
.then(result => {

    let authorsElem = document.querySelector('#authors');

    result.map(author => {

        authorsElem.insertAdjacentHTML('beforeend', `<div>${author.author}</div>`)

    });

})
```

Når du har oprettet prokeltet start den med "liveserver" og du skulle gerne se alle author navne blive skrevet ud.

Prøv at fetch´e `http://localhost:3000/api/galleries`. 

Husk, hvad er det vi skal åbne i nextjs/api´et, for at vi kan få adgang til galleries endpointet fra liverserver domænet `http://127.0.0.1:5500/`?.

## Opgave.

Prøv at hente alle billeder fra én specifik author og udskriv dem hvad skal vi tilføje for at få fat i billederne?

*:bulb: Du bestmmer selv hvordan!, du må gerne lave nye filer og slette det nuværende.*

Men det handler bare om at få billederne vist.

## Afsutning.

Denne lille side-quest til vanilla er til for at vise at vi kan "udstille" et API, som vi kan tilgå fra andre servere/domæner og dermed benytte nextjs som en backend til andre projekter. Vi kunne levere data til en info skærm, vi kunne aflevere data til en mobil applikation osv.

Det kunne være en fordel, at lave en lille vanilla apllikation til f.eks Raspberry Pie. Denne applikation trækker/fetcher data fra vores Next/React applikation i skyen. F.eks dette galleri - så sbehøver vi ikke have alt data på Raspberry Pie, men kan nøjes med en Client Applikation. 

Og husk, det behøver ikke være med MongoDB osv - det kan også bare være flade filer og et "push" til serveren - der er selvfølgelig et sikkerheds moment, men så længe det handler om at hente data, så skal vi ikke tænke så meget på det.

Nu kan du lukke live serveren og vanilla projektet. Vi skal tilbage til det oprindelige projekt.



