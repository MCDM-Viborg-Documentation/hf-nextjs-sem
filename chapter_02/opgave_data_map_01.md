# Media College

```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : NextJS Opgave
Doc         : opgave_data_map_01
```
### Indledning.

Nu ikke så meget tekst - mere bas.

Vi fortsætter hvor vi slap i forrige opgave.

### Forudsætning.

1. Læs ovenstående indledning.
2. De forrige opgaver i indexet.

### :dart: 1. Data loop og en lille smule om modeller.

Vi fik oprettet vores nye komponent og vi kan se vores galleries data blive udskrevet.
Vi kan også se at der i det data er 2 objekter. Svarende til 2 gallerier.

```json
[
  {
    "_id": "659d10f5d8344e1429921fb0",
    "name": "obscura",
    "year": 2023,
    "created": "2024-01-09T09:25:09.837Z",
    "__v": 0
  },
  {
    "_id": "659d10f6d8344e1429921fc3",
    "name": "umbra",
    "year": 2023,
    "created": "2024-01-09T09:25:09.837Z",
    "__v": 0
  }
]
```
Lad os prøve at `loop´e` over dette `array` og udskrive dem én ad gangen.

Prøv at erstatte return funktion med dette:

```javascript
return (
<main className={styles.page}>

    <h1>Alt Galleri Data</h1>
    <DevDebugJson content={galleries} />
    
    <h1>Hvert Enkelt Galleri</h1>
    {galleries.map((gallery, index) => {
        return <DevDebugJson key={index} content={gallery} />
    })}

</main>
);
```

Her udskriver vi først alt galleri data. Derefter loop´er vi over hele `galleries` array´et.

I react vil vi *næste* altid benytte array `.map` funktionen når vi loop´over `arrays` og udskriver komponenter. Vi husker når vi `mapper` og udskriver komponenter så skal de have en 
unik `key={}`value.

:link: `array.map()`     
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map

:bulb: Læs side linket herunder. Det handler om at rendere lister - hvilket i virkeligheden er det vi gør **konstant**. Så arrangere vi listerne, med css, js, til at se ud som vi gerne vil have: *vandret*, *lodret*, *cards*, *graphs*, *ikoner*, *tabeller* *etc*.

:link: `react - rendering lists`      
https://react.dev/learn/rendering-lists

Opret følgende snippet.     
**Snippet**     
:pencil: `snippets/comp_devGalleryHero.md`.

Erstat
```javascript
{galleries.map((gallery, index) => {
    return <DevDebugJson key={index} content={gallery} />
})}
```
Med vores Hero Komponent.
```javascript
{galleries.map((gallery, index) => {
    return <DevGalleryHero key={index} gallery={gallery} />
})}
```
Så præsentere vi hvert galleri i et hero komponent. En rød cirkel med hvid tekst.

### Modeller.

Vores galleri data består af tre MongoDB collections. Galleries, Authors og Images.

Hver Author tilhøre ét galleri og hver author har en række billeder som udgør en portfolio.

:bulb: *I virkeligheden kunne vi hente alt data med det samme og bruge den derfra - men vi tager højde for at dette kan indholde mange gallerier og dermed portfolier.*.

Lige nu er der ikke en metode til at hente alle `authors`. Og hvis vi husker tilbage på CRUD og MongoDB så har vi faktisk en idé om hvad vi skal gøre.

Åbn `data.service.js` filen. 

Når man kigger på `fetchGalleries` funktionen så er detkun `galleryModel.find({})` der afgør hvad der bliver retuneret.

Havde vi skrevet en `query` såsom `galleryModel.find({'name' : 'obscura'})` så havde vi kun fået det ene galleri.

```javascript
// ---
export const fetchGalleries = async () => {
    
    console.log('fetchGalleries')

    try {

        await dbConnect();

        let result = await galleryModel.find({});

        return JSON.parse(JSON.stringify(result))

    } catch (error) {

        console.log(error)

    }
};
// ---
```

Og husk det er vores `mongoose` modeller der gør det så let for os.

Kig i mappen `lib/db/models/` der ligger tre modeller.

Med alt det i tankerne så lad os lave en metode til at hente alle authors.

```javascript
/*

    Get Authors

*/
export const fetchAuthors = async () => {

    console.log('fetchAuthors')
    try {

        await dbConnect();
        let result = await authorModel.find({});
    
        return JSON.parse(JSON.stringify(result))

    } catch (error) {

        console.log(error)

    }

};
```

Vi skifter stort set bare navn og model ud.

Sæt metoden ind i `data.service.js` filen.

Nu kan vi som `await fetchGalleries()` lave `await fetchAuthors()`.

### :dart: Opret en ny under-under side.

*Ja du læste rigtig, ikke endnu en slå/stave/sjuske fejl fra dokument-artisten.*

Vi skal lave en underside til `/assignments/data/` så:

1. Opret en `page.js` under `/assignments/data/authors`

Mappe stukturen ser herefter således ud:

```
├── ...
├── assignments
│   ├── data        
│   |   ├── authors             
│   |   |    └── page.js        
│   |   |    └── page.module.css        
│   |   └── page.js        
│   |   └── page.module.css        
│   ├── icons
│   |   └── page.js        
│   |   └── page.module.css
│   └── page.js        
│   └── page.module.css
├── ...
```

2. Opret nu et link i assignments menuen. Husk vi går en rute dybere nu.   
Data - Authors `/assignments/data/authors`.

Indsæt: på din ny page følgende: 
```javascript
import { fetchAuthors } from '@/lib/data.service';
import styles from './page.module.css'
import DevDebugJson from '@/components/dev/devDebugJson/devDebugJson';

const Page = async () => {

    const authors = await fetchAuthors();

    return (

        <main className={styles.page}>
            
            <h1>Alt Author Data</h1>
            <DevDebugJson content={authors}></DevDebugJson>

            <h2>Hvert Enkelt Author</h2>
            {authors.map((author, index) => {
                return <DevDebugJson key={index} content={author}></DevDebugJson>
            })}
        </main>

    );

}

export default Page
```

:goal_net: Se hvordan det hele er en kopi fra før. Vi har bare udskiftet `fetchGalleries` med `fetchAuthors` og kan nu konstatere at der er 6 authors ialt.

Vi kan også kigge på deres objekter.

Lad os som under galleries udskifte DebugJson med en `<DevAuthorHero author={}/>` komponent.

### :dart: Opret følgende snippet.     
**Snippet**     
:pencil: `snippets/comp_devAuthorHero.md`.


:bulb: Bemærk hvordan vi har indsat en Debug i Komponentet. Den kan du fjerne igen - men igen kan man se hvor let det er at genbruge komponenter der "bestemmer selv".

:coffee: Næste skridt er billederne.


### Næste skridt.

Kig i index.


