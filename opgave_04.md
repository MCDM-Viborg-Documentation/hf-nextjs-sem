# MediaCollege Denmark

# Forudsætning.

At alt er læst og *forstået* i den forrige opgave.

Det er vigtigt at alle opgaver :dart: og spørgsmå :question: er løst.

Husk også at læs igennem de links der er vedhænngt.

## :dart: 1. Opgave Styling og dynamik.

Lad os arbejde en lille smule med vores ikoner.

Eller det vil lidt om styling og det er vigtigt at vi følger dette da vi skal bruge den i næste opgave også.

Nogenlunde således skal vores Icons se ud.      
 

```javascript
import { 
    Fa500Px, 
    FaAccessibleIcon,  
    FaBlackTie,
    FaBomb,
    FaBroom,
    FaCog,
    FaCoffee,
    FaGithub,
    FaJsSquare,
    FaBeer
} from "react-icons/fa";
import styles from "./devicons.module.css"

const DevIcons = () => {

    return <div className={styles.icons}>

        <Fa500Px />
        <FaAccessibleIcon />
        <FaBlackTie />
        <FaBomb />
        <FaBroom />
        <FaCog />
        <FaCoffee />
        <FaGithub  />
        <FaJsSquare  />
        <FaBeer  />

    </div>

};

export default DevIcons;
```

Som i kan se har jeg tilføjet `className={styles.icons}` til vores primære `div` element.

Hvis du ikke allerede har oprettet en `devicons.module.css` til dit komponent så gør det nu. Og indsæt føgende.

```css
.icons {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;
    margin : 100px auto;
}
```

Så har vi en fin samling af vores ikoner.

Alle ikoner er i virkeligheden `svg` og hvis vi kigger i `sourcecode` vores html i `inspectoren`så kan vi se at der er `svg elementer`.

Så vi kunne ændre størrelsen på alle ikoner ved at indsætte.

```css

.icons svg {
    width : 50px;
    height : 50px;
};

```

Og vi vil også kunne style direkte på elementet.

```javascript
 // ---
 <FaBroom style={{width:'100px', height:'100px'}} />
 // ---
```

Sæt `inline style` på et af elementerne.

Begge metoder har sin funktionalitet. Direkte `inline styling` er brugbart i tilfælde hvor vi vil ændre noget dynamisk som ikke kan defineres eller vil være alt for omfattende at tilføje som klasser i css.

Det anbefales at bruge klasser, men som i vil se omlidt, så udnytter vi `inline-styling` til dynamisk funktionalitet.

Lad os starte med at gøre vores `inline-style` til en `variable`.

```javascript
let style = {width:'150px', height:'150px'}
```

Indsæt variablen øverst i komponentet.

```javascript 
const DevIcons = () => {

    let style = {width:'150px', height:'150px'}
```

og benytte variable på vores element med `inline style`

```javascript
<FaBroom style={style} />
```

Læg mærke til vores ene ikon stadig er større end de andre.

Nu kunne vi lave en variable `size`, Som i kan se skal vores ikoner have samme højde og bredde for at fungere optimalt. Og vi skal sætte begge værdier.

Men hvis vi opretter `let size = 150` så kan vi bruge `size` og kun ændre den ét sted.

I denne opgave skal vi lave en mulighed for at se ikoner i listen i forskellige størrelser. Altså : Lille, Mellem, Stor. Men måske også justérbar størrelse.

Og vi vil gerne gøre det muligt for vores bruger at vælge via af UI´et. (*knapper*).

## Client Komponent og useState

Så vi starter med at gøre vores komponent til et `client komponent`.

Indsæt øverst i komponent filen `'use client'`.

Dernæst opretter vi `size` men som et react hook `useState`.

Så ovenover vores style variabel indsætter vi:

```JavaScript
// ---
const [size, setSize] = useState(150);

let style = { width: `${size}px`, height:`${size}px` }
// ---
```
*(*husk at importere en reference til useState*)

Læg mærke til at vi også benytte `size` `state` (variablen) i vores style.

Nu er det `useState(150)` der sætter størrelsen. Prøv at ændre den til 300. 

## En knap.

Vi har brug for knapper og vi har brug for at et sted i koponentet til knapperne.

Vi starter helt lav praktisk ved at lave en container div med en span-knap i.

```html
<div className={styles.actionBar}>
    <span className={styles.btn}>KNAP</span>
</div>
```

Vi vil gerne have vores knapper/action panel under vores ikoner så vi udvider komponetet med en ny omkringliggende forældre `<div></div>`.

Vores `return template` ender med at se således ud.

```javascript
return (
        <div className={styles.container}>
            <div className={styles.icons}>

                <Fa500Px />
                <FaAccessibleIcon />
                <FaBlackTie />
                <FaBomb />
                <FaBroom style={style} />
                <FaCog />
                <FaCoffee />
                <FaGithub  />
                <FaJsSquare  />
                <FaBeer />

            </div>
            <div className={styles.actionBar}>
                <span className={styles.btn}>KNAP</span>
            </div>
        </div>
```

Og til module.css er tilføjet.

```css
.container {

    text-align: center;

}

.actionBar {

    display: flex;
    align-items: center;
    justify-content: center;
    margin : 20px auto;
    
}

.actionBar .btn{

    padding : 20px;
    color : var(--main-color);
    border-radius: 10px;
    background-color: var(--box-color);
    cursor: pointer;
}
```

Så skulle vi have en knap centreret i bunden af vores ikoner.

Vi skal også arbejde med dette i opgave 5 og inden vi afslutter denne opgave, så laver vi et `click event`. Meningen er at vi skal forstørre og formindske vores ikon. Vi venter med alle ikoner.

## onClick event.

På vores knap tilføjer vi nu et klik event `onClick`.

```<span className={styles.btn} onClick={() => setSize(20)}>KNAP</span>```

## Afslutning.

:dart: Inden du hopper til opgave 3. 

Så lav lige 3 knapper der sætter Alle ikoer til at være enten LILLE, STOR og MELLEM.

Du bestemmer i denne omgang hvad de størrelser er. Leg lidt med det.

I næste opgave laver vi lidt mere og så skal du gøre action panelet til et selvstændigt komponent.

`<DevIconsActionPanel></DevIconsActionPanel>`

Men der er i næste opgave.


### Næste skridt.

Opgave 05



