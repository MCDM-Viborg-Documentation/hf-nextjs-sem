# SEM Opgave

```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : Start med serverside data 
                      
```
### Indledning.

Nu ikke så meget tekst - mere bas.

Vi fortsætter hvor vi slap i forrige opgave.

### Forudsætning.

1. Læs ovenstående indledning.
2. De forrige opgaver i indexet.

### :dart: 1. Flow, Routes, Params og Links.

Nu hvor vi har komponenter der kan vise.

1. Galleri (*umbra*).
2. Author (*Lena Riis*)
2. Portfolie for én Author (*Lena Riis og hendes billeder*)

Så har vi det der skal til for at lave et mindre Galleri af Portfolier.

Vi skal lave følgende flow.

![alt text](../../assets/flow_gallery.png)

:bulb: *Se godt på billedet ovenover*.

Hvis vi kigger på vores rute fra forsiden til en portfolie som den er skrevet i diagrammet ser den således ud:

`/galleries/umbra/lena-riis/` altså `http://localhost:3000/galleries/umbra/lena-riis/`

Men som der stpr ved de to sidste rute så er de dynamiske?.

ruten kan hedde noget forskllig alt efter hvilket `gallery` (*umbra eller obscura*) og alt efter hvilken `author` (**lena-riis eller bjarne-reuter*).

Så vores dynamisk rute kan oversættes til:

`http://localhost:3000/galleries/ [GALLERY] / [AUTHOR] /`

På den måde skal vi kune lave en side til at håndtere *hvilket* `[GALLERY]` og *hvilken* `[AUTHOR]` vi ønsker at vise.

I next er det præcis det man gør. Man oprette via mapper (*eller filer, men én ting af gangen*) sin dynamiske ruter.

![alt text](../../assets/dynamic_folder_structure.png)

Kig godt på mappe strukturen den *reflektere* vores url oven over.

```
├── ...
├── galleries               # Mappe
│   ├── [gallery]           # Mappe hvor `gallery` bliver placholder for det der måtte komme.
│   |       ├── [author]    # Mappe hvor `author` bliver placholder for det der måtte komme.
├── ...
```

Hver mappe har i dette tilfælde så også en `page.js`og `page.module`, se billedet. 

Fuldstændig som vi har lavet de andre ruter, bortset fra at vi bruger `[]` og dermed *definere* en *dynamisk* rute.

1. Brug følgende `page.js` og `page.module.css` og opret alle sider og ruter (mapper).
2. Erstat samtidigt overskriften på hver side. (*Galleries, Portfolier, Portfolio*) Se fuld stuktur nedenfor.

`page.js`
```javascript
import Link from 'next/link'
import styles from './page.module.css'

export default async function Page() {
  
  return (
    
    <main className={styles.page}>
      <h1>Galleries</h1>
    </main>

  )
}
```

`page.css`
```css
.page {

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100%;

}
```

Fuld fil og mappe struktur i galleries mappen:
```
├── ...
├── galleries               
│   ├── [gallery]           
│   |       ├── [author]    
│   |           ├── page.js             # Overskrift : Portfolio
│   |           ├── page.module.css   
│   ├── page.js                         # Overskrift : Portfolio´s
│   ├── page.module.css             
├── page.js                             # Overskrift : Portfolie Gallerier
├── page.module.css
├── ...
```

3. Indsæt nu følgende link under `<h1></h1>` overskriften på følgende sider.

    1. `galleries/page.js` : `<Link href="/galleries/umbra" alt="umbra">UMBRA</Link>`          
    2. `galleries/[gallery]/page.js` : `<Link href="/galleries/umbra/lena-riis" alt="Til Lena Riis portfolio">Lena Riis</Link>`         
    3. `galleries/[author]/page.js` : `<Link href="/galleries" alt="Lena Riis - Portfolio">Tilbage til gallerierne</Link>`

:goal_net: Nu har vi et flow med dynamiske ruter, du kan prøve at sætte et link ind til "bjarne-reuter". Vores links er `hardcoded`men vi har skabt flowet og er klar til at tage imod de værdier der befinder sig i de nye "placeholder/slug", `[gallery]` og `[author]`.


### :dart: Lad os trække værdier vi skal bruge før vi sætter komponenterne ind.

Det giver os også en mulighed for at *illustrerer* flowet for num skal vi kigge på `params`.

`dynamic-routes`
:link: https://nextjs.org/docs/app/building-your-application/routing/dynamic-routes

:coffee: *så tag smid lige dit blik på ovenstående link*

*fra nexjs dokumentationen*
```javascript
export default function Page({ params }) {
  return <div>My Post: {params.slug}</div>
}
```

Det de *prøver* at sige er at `slug` er det som vi har skrevet som "placeholder" for vores dynamiske rute.

Altså enten `[gallery]` eller `[author]`. 

Eller endnu mere præsist.

`[gallery]` trækkes ud som dynamisk parameter.
```javascript
export default function Page({ params }) {
  return <div>Gallery Placeholder/slug: {params.gallery}</div>
}
```
`[author]` trækkes ud som dynamisk parameter.
```javascript
export default function Page({ params }) {
  return <div>Author Placeholder/slug: {params.author}</div>
}
```

1. indsæt følgende `<h2></h2>` elementer under `<h1></h1>` elementerne på de følgende sider.     
    2. `galleries/[gallery]/page.js` : `<h2>Gallery: {params.gallery}</h2>`         
    3. `galleries/[author]/page.js` : `<h2>Author: {params.author}</h2>`

Husk også på *begge* sider at indsætte `{params}`som `parameter`.

:bulb: *indsæt params som page parameter på sider med dynamiske ruter*    
`export default async function Page({ params })` <- *indsæt params så vi kan modtage, det der står i url´en*.

:goal_net: Når du navigere kan du se at vores `[gallery]` og `[author]` dynamiske ruter bliver udskrevet.

Lige nu kan du skrive hvad som helst i urlen fordi vi ikke, henter noget data.

Kopiere og afprøv denne url:    
```
http://localhost:3000/galleries/umbra/se-vi-lave-en-dynamisk-rute-og-udskrive-den-med-author-placeholder`
```

:bulb: Sådan! - Det virker ikke som meget, men det er rent fatisk *utroligt* brugbart og stærkt. :muscle:

1. Du kommer til at lave mange ruter. 
2. Du kommer til at arbejde med ruter som din tankegang.

*Hvorfor?*

* Fordi du med en simple rute kan vise 1000vis af "produkter".
* Fordi du **ikke skal** *hardcoded* de samme 1000vis af produkt sider.
* Fordi du i næste opgave vil se hvor hurtigt vi nu kan få samlet vores komponenter. Med alt det vi har lært indtil nu. 

Så mangler der bare en designer :)

:bulb: Vi hopper videre og ignorerer, at du i sidste opgave har brugt tid på at lave et toggle komponent, man bliver ***tit*** overset som udvikler - hvis i vil ***ses***, så bliv *projekleder eller... rektor* :fire::eyes: .

*Se index for næste skridt*.