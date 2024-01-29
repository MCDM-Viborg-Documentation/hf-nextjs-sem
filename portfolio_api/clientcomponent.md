# Media College

```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : Portfoile API
Doc         : clientcomponent
```

# Indledning.

Når man skal hente data er der flere måder vi kan gøre det på. Men vi deler det som regle op i *serverside* og *clientside*.

Serverside er "statisk data" - det kan i princippet komme fra en fil eller en database eller være hardcoded og på den måde være skabt på "server siden".

*client-side* er derimod data vi henter fra client siden (*browseren i vores tilfæde som bruger*) og derefter benytte til et formål.

I React henter kan vi hente data *clientside* i vores `use client` komponenter.

Vi benytter en hook `useEffect` til at fortage vores `fetch` efter at komponentet er sat ind på siden, i `html dom`´en.

Man kan gøre det på flere måde men jeg anbefaler at ved "simple" opgaver at vi benytter nogenlunde samme fremgang, det er *best practise* og det er også en forholdsvis "let" måde at håndtere et kald til et api for derefter at tildele komponenter data´en. Husk det er ikke forkert at have flere `useEffect` og `useState` til at håndtere forskellige data endpoints.

### Client Component.

Her er koden fra `Client Component`. Du finder komponentet i `components/dev` mappen. Indsæt komponentet på forsiden.

Læs nu igennem **ALLE** kommentarer i dette script.
```javascript
'use client';
import { useEffect, useState } from 'react';
import styles from './clientComponent.module.css';
import DebugJson from '../debugJson/debugJson';

const ClientComponent = () => {

    const [data, setData] = useState([]); // Vi sætter "data" til at være et tomt array som udgangspunkt.

    // useEffect er en Hook/funktion der kaldes når "html"´en er klar.
    useEffect(() => {

        // Vi opretter en "async" funktion og udnytter dermed "await/promise" til vores fetch.
        const fetchData = async () => {

            // Vi fetcher fra vores endpoint.
            const response = await fetch(`http://localhost:3000/api/authors`);

            // Vi omdanner vores response fra tekst til json.
            const result = await response.json();

            // Vi opdatere "data" state, ved hjælp af setData(), useState hook´en.
            setData(result);

        }

        // Vi kalder fetch data funktionen.
        fetchData();

    }, []);

    // Vores Template
    return (
        
        <div className={styles.container}>

            <div className={styles.header}>
                <h1>Client Component</h1>
                <p>Fetching Data</p>
            </div>

            {/* Vi udskriver indholdet af data ved hjælp af map */}
            {data.map((item, index) => (
                <DebugJson key={index} content={item.author} /> // Bemærk at vi skriver item.author, vi kunne vælge at skrive hele objektet ud med item (prøv det!)
            ))}

        </div>
    )
};
export default ClientComponent
```

Som du kan se er vores komponent et "selvstændigt" komponent der henter sin "egen" dat og udskriver den. Nu vil vi kunne sætte dette komponent ind på hvilken som helst side og vi vil få listen af authors.

Prøv nu at udskiftet endpointet til `http://localhost:3000/api/author?gallery=obscura`

Nu får vi alle `authors`for obscura.

Opret nu en `useState` hook så vi kan udskifte `obscura` med noget andet.

```javascript
const [galleryName, setGalleryName] = useState('obscura');
```

Nu skal vi ændre endpointet til at benytte vores variabel.

```javascript
`http://localhost:3000/api/authors?gallery=${galleryName}`
```

Læg mærke til at vores `useEffect` hook nu fortæller at vi mangler noget i vores "afhænigheds-array".

```javascript
useEffect(() => { 

    // --- //

}, []); <-- Dette er vores "afhængigheds-array".
```
Hvis vi benytter variabler inde i vores "useEffekt" som kommer "udefra" som f.eks vores `galleryName` så skal den tilføjes som en afhængighed. Dermed kan React kalde useEffekten igen, hvis `galleryName` variablen ændre sig.

Så indsæt `galleryName`som afhængighed.
```javascript
useEffect(() => { 

    // --- //

}, [galleryName]);
```

Nu kan vi ændre `useState('obscura');` til `useState('umbra');` og se et andet resultat.

Vi kan nu gøre det mulig at man via et `parameter` kan sætte hvilket galleri vi skal starte med.

Så lad os oprette et paratmeter vi kalder "gallery".

```javascript
ClientComponent = ({gallery = 'obscura'})
```

Læg mærke til at vi sætter det `= 'obscura'` dermed sikre vi at `{gallery}` parameteret har en default værdi.

Sæt nu `useState` til at benytte `{gallery}` som default "galleryName" værdi.

```javascript
const [galleryName, setGalleryName] = useState(gallery);
```

Nu skulle alt være ved det gamle, vi kan se resultatet af "obscura" authors.

På forsiden kan vi nu vælge at tilføje `<ClientComponent gallery={'umbra'}></ClientComponent>` og så vil det være umbra som vil være vores default author liste. Nu kan vi placere komponentet på forskellige sider og samtidigt give den forskellige udgangspunkter.

Som det sidste skal du indsætte følgende i Client Component lige efter `<p>Fetching Data</p>`.


```html
<div>
    <h2>Gallery {galleryName}</h2>
    <button onClick={() => setGalleryName('umbra')}>UMBRA</button>
    <button onClick={() => setGalleryName('obscura')}>OBSCURA</button>
</div>
```

Nu kan vi skifte imellem de to gallerier. Vi har dog "hardcoded" navnene.

