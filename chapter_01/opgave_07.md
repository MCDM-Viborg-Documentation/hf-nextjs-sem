# Media College

```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : NextJS Opgave
Doc         : opgave_07
```
# Forudsætning.

At alt er læst og *forstået* i den forrige opgave.

Det er vigtigt at alle opgaver :dart: og spørgsmå :question: er løst.

Husk også at læs igennem de links der er vedhænngt.

## :dart: 1. Opgave Action Bar.

Svaret på forrige opgaver er **size** vi skal selvfølgelig bruge vores size værdi.

I `devicons.js` sætter vi size værdien `const [size, setSize] = useState(150);` og vi gør det hver gang vi kalder `setSize` funktionen.

Vi sender `size` med som property til vores `<DevActionBar>` komponent 

```html
<DevActionBar setSizeFunction={setSize} size={size}></DevActionBar>
```

Så åbner vi komponentet `devActionBar.js` og tage imod vores ny `parameter`.

```javascript
const DevActionBar = ({setSizeFunction, size}) => {
// ---
```

For at få plads til at udskrive vores size skal vi ændre lidt på vores `DevActionBar` komponent layout og opsætning. 

Det sker ofte under udvikling at man har behove for at omstrukturere/refakturere sin kode og tilpasse den nye omstændigheder.

Det gælder især når man starter med at udvikle fordi man ikke altid har taget højde for alle de elementer man har behov for. 

Ofte bliver man også klogere undervejs og ser nye muligheder.

Komponenter kan altid "lige" få en container mere :)

Vi har behov for en "header" til vores komponent. Så vi kan udskrive vores størrelse.

```html
    <div className={styles.container}>
        <div className={styles.status}><h1>{size}</h1></div>
        <div className={styles.actionBar}>

            // --- lad indholdet blive.

        </div>
    </div>
```

Tilføj følgende style til `devActionBar.module.css`

```
.status{

    margin-top: 20px;
}
```

Nu skulle vi gerne se `size` ændre sig når vi trykker på knapperne. 

På vores `input` har vi en mulighed for sætte en `defaultValue` lad os sætte den til size.

`defaultValue={size}`

Når du refresher browseren skulle slideren stå på den værdi vores `useState(150)` er sat til som udgangspunkt.

# useEffect og useRef hooks.

Men! - Når vi trykker på knapperne så ændre vores slider sig ikke det giver nogle uheldige "glitches" når man tager fat i slider bagefter. I har nok selv set det allerede!.

Når et `state` ændre sig som vedhjælp af `useState` og man skal reagere på den state forandring. 

Så benytter man hook´en `useEffect`.

Indsæt følgende `useEffet` i `DevActionBar`

```javascript
const DevActionBar = ({setSizeFunction, size}) => {

    const activeSlideRef = useRef(null);

    useEffect(() => {

        let slider = activeSlideRef.current;
        slider.value = size;

    }, [size])

    return (
        <div className={styles.container}>
    // --
```

og `import` begge hook´s.

```javascript
import { useEffect, useRef } from "react";
```

Kig godt på useEffect :eyes:

```javascript
useEffect(() => {

    let slider = activeSlideRef.current; // i virkeligheden svare det til -> document.querySelector("input[type=range]");
    slider.value = size;

}, [size])
```

I denne `useEffect` hook. Der sætter vi en reference til en slider variabel.

```javascript
let slider = activeSlideRef.current;
```

Vores "reference" ser mærkelig ud `activeSlideRef.current`. 
Og hvis vi kigger i toppen af vores `DevActionBar` funktion så ser vi

```javascript
const activeSlideRef = useRef(null);
```

Men det betyder at vi vil lave en reference (useRef, en slags querySelector) og lige nu er den null, altså ingen ting.

Men nu skal vi på vores `input` element fortælle at dette er reference elementet.

Så indsæt referencen på input elementet.

```javascript
ref={activeSlideRef}
```

```html
<input type="range" ref={activeSlideRef} className={styles.range} min="50" max="300" defaultValue={size} onChange={(e) => setSizeFunction(e.target.value)}></input>
```

Nu kan vi benytte `activeSlideRef.current` som en reference til vores element i `useEffect` hook´en.

Hvis slideren tilpasser sig knappernes værdi - så er alt godt :muscle:

# Afslutning

Her er react dokumentationen for react hooks     
:link: `hooks` generelt     
https://react.dev/reference/react/hooks

Start med:      
:link: `useState`       
https://react.dev/reference/react/useState    
:link: `useEffect`   
https://react.dev/reference/react/useEffect    
:link: `useRef`   
https://react.dev/reference/react/useRef        


:link: Man kan lave sine egne og der er også nogen der laver en masse til forskellig brug.  
https://usehooks.com/


### Næste skridt.

Opgave 07
