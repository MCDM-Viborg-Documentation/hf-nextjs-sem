# Media College

```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : NextJS Opgave
Doc         : opgave_data_init 
```

### Indledning.

Nu ikke så meget tekst - mere bas.

Vi fortsætter hvor vi slap i forrige opgave.

### Forudsætning.

1. Læs ovenstående indledning.
2. De forrige opgaver i indexet.

### Indledning.

Vi arbejder med serverdata, for at vende os til at benytte det i projekter fremad. Dette er også, så vi kan begynde at loop´e over data og lave komponeter tilsvarende.

Vi tildeler vores komponenter data/json fra `serverside` så kan komponentet, om nødvendigt, blive `client side` vedhjælp af `'use client'`.

Det er den optimale måde at arbejde med NextJS/React. 

Vi har allerede i undervisningen arbejde med at hente data via `useEffect`.

Det vender vi tilbage til i et senere kapitel.

#### :bulb: Vigtig information.

Opgaverne i disse kapitler er til for at vi lære at benytte NextJS og React.

Fremad vil der ikke være så meget om hvordan vi laver styles eller opretter et komponent.

Styling vil vi lære i forbindelse med andre opgaver end opgaverne i disse kapitler.  
*Med mindre andet bliver oplyst i selve opgaven.!*

:dart: En side quest er dog at i gerne må ændre farver og variabler til dark/light theme. Men det skal være læsbart. Jeg vil gerne se forslag. (*men kun for sjov*!)

#### :bulb: Stadig Vigtig information.
Fra nu af ved vi godt hvordan vi opretter komponenter.

Så i dette repositorie er der en `snippets` mappe.

I den mappe vil i finde de `snippets` der skal bruges til komponenter, når det oplyses i en opgave.

Der vil dog også komme opgaver hvor i selv skal oprette sider, komponenter uden snippets. Og andre hvor det vil være beskrevet i dokumentet - en ***"kom-bi"***

Snippets er til for at arbejde effektivt - samtidigt kan i lære lidt om ombygning af komponenter ved at kigge godt på de komponenter vi benytter. De vil som oftes være med kommentarer der forklare hvad der nogenlunde sker :)

### Forudsætning.

1. Læs ovenstående indledning.
2. De forrige opgaver i indexet.


### :dart: 1. Data Init.

Denne opgave skal vi starte med at benytte `serverside` data.

Men det handler mest om at udskrive og loop´e over den data vi henter.

1. Start med at lave en ny rute `data` under assignments.

`/assigments/data/page.js`      
`/assigments/data/page.module.css`

2. Indsæt følgende i `page.js`

```javascript
import { fetchGalleries } from '@/lib/data.service';
import styles from './page.module.css'

const Page = async () => {

    const galleries = await fetchGalleries();

    return (

        <main className={styles.page}>
            <h1>Data</h1>
            <pre>{galleries.toString()}</pre>
        </main>

    );

}

export default Page
```

Det "nye" for os her er:

1. Page er `async` - det er vigtigt for at vi længere nede kan hente `serverside` data `fetchGalleries()` som et `promise` = `await fetchGalleries()`.
2. Vi afventer serverdata´en `await fetchGalleries()` før vi går videre i koden.
3. Derfor er `galleries` data´en også bare tilgænglig "uden problemer" når vi udskriver den længere nede. `{galleries.toString()}`


4. Opret nu et ny link i navigationen `devAssignmentsNavigation.js` og gå til `/assignments/data` siden i browseren.

:goal_net: Nu skulle du gerne se en "Data" overskrift og en tekst hvor der står `[object Object],[object Object]`. 

Det vi forsøger er at udskrive den data vi har hentet i et `<pre></pre>` element som er velegnet til at udskrive kode i.

Men man kan **ikke** toString() et javascript object man er nødt til at konvertere det til en `JSON` streng, ligesom hvis man skal sende det til et endpoint.

1. Ændre `{galleries.toString()}` til `{JSON.stringify(galleries)}`.

Så kan i se at data bliver skrevet ud - men i én lang køre.

2. Ændre igen `{JSON.stringify(galleries)}` til `{JSON.stringify(galleries, null, 2)}`

Det giver en "flot" formateret udgave af det JSON data vi lige har hentet og kaldes i de fede kredse `prettyfi`. :eyes:

Det svare jo i virkeligheden til at skrive `console.log(galleries)` og istedet kigge i consollen - men vi gør det for at synliggøre json-data i html.

Som udvikler kan det være smart, at have et par hjælpe/teste komponenter man kan indsætte når man er lidt i tvivl eller bare som "placeholder" når man arbejder med siden.

Så lad os teste den første snippet af fra snippets mappen i dette repositorie og oprette et komponent der kan bruges til at udskrive json dataen hvis vi tildeler den et javascript objekt som property.

:dart: Opret komponet fra snippet. 

**Snippet**     
:pencil: `snippets/comp_devDebugJson.md`.

I `snippets` mappen ligger der en md-fil: `comp_devDebugJson.md` den indeholder 
`js`og `css` koden til et `<DevDebugJson content={}>` komponent `comp_`.

I dokumentet er det beskrevet hvad **fil-navn**, **type**, **folder** og **indhold** skal være, brug **ikke** .md filnavnet, comp_xxx. Oplysningerne står i selve filen. 

Så :pencil: ikonet henviser til en snippet-fil i snippets mappen. 

Erstat nu `{JSON.stringify(galleries, null, 2)}` med `<DevDebugJson content={galleries} />`

:goal_net: Nu skulle du have en "Accordion" der ved klik toggler alt galleri dataen udskrevet som streng.

:bulb: Du kan *for sjov* sætte `<DevDebugJson content={ { hello : "world" } } />` ind på siden og se helloworld data´en.

Bare en nem måde, at udskrive sin data på, inden man opretter et komponent til rent faktisk at præsentere denne data.

Og det skal vi arbejde med i næste opgave.

### Næste skridt.

Kig i index.


