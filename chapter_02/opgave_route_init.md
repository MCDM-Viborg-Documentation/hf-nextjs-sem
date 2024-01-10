# Forudsætning.

At alt er læst og *forstået* i de forrige opgaver.

* Alle intielle opgaver
    * 0-7
    * Aflevering via git.
* Layout Init opgaven

Det er vigtigt at alle opgaver :dart: og spørgsmå :question: er "løst".

Husk også at læs igennem de links der er vedhængt.

## :dart: 1. Opgave Route.

Vi springer lige ud i det og tager første skridt til hvordan vi benytter 'routing'

Routing, altså det at navigere sig rundt på sitet. Fra `http://localhost:3000/assignments/icons` til `http://localhost:3000/assignments/` og tilbage igen. Det er routing i en programerings forstand.

Når vi gør det ændre url´en sig og måske er der endda parametre sendt med som query.

Feks. `http://localhost:3000/assignments?name=Anders&age22`

`path` : `/assignments`        
`search/query` : `?name=Anders&age22`

Prøv at kalde urlen og åbn `inspectoren` i browseren.

Skriv følgende i consollen:

```javascript
document.location
```

Se hvad der bliver udskrevet. Der kan vi se vores at dat´en er tilstede for url´en.

Så routing er en vigtig del af en applikation og vi kan brugen den til at `redirecte`, låse for adgang. Vi kan se hvilken side der er aktiv, vi kan læse værdier til at udfylde forme osv.

Og heldigvis er alt det bygge for os i et framework. Men vi skal selvfølgelig gøre brug af funktionaliteten.

Og i denne intielle opgave om routing tager vi bare fat i hvordan vi i vores DevAssignMent Navigation kan give et menupunkt en aktiv klasse - hvis den matcher den rute vi er på.

:link: `Linking and navigation`    
https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating

## Client Side Hook.

Men der findes en hook som vi kan bruge.

:link: `usePathname`    
https://nextjs.org/docs/app/api-reference/functions/use-pathname

Og `hools`kan vi godt lidt for dem kan vi bruge til at trække forskellige ting ud af, alt efter hvilken `hook`vi benytter. Husk `useState`, `useRef`, `useEffect` alle er hooks. Og du genkender dem ved at de benytter `use` foran. Og det er et krav når man lave hooks.

Vi har ingen grund til at lave vores egen vi benytter dem der allerede er lavet til formålet, når det er muligt.

Åbn `devAssignmentsNavBtn.js` filen og benyt `usePathName`.

```javascript
'use client'

// ---
import { usePathname } from 'next/navigation';
// ---

const DevAssignmentsNavBtn = ({link, title}) => { 

    const pathname = usePathname()

    return (
        <div className={styles.navBtn}>
            <Link href={`${link}`}><FaJsSquare / > {pathname}</Link>
        </div>
    );

};
// ---
```

:bulb: Bemærk : vi udskifter *for testen skyld* vores link titel med `pathname` fra vores `usePathname()` hook funktion `{pathname}`.

:bulb: Bemærk : Bemærk også at vores hook er `clientside` så vi skal have `'use client'` i toppen af vores komponent.

Nu kan man se hvilken aktiv path vi er på. Det kan vi bruge til at sammenligne med knapps link og dermed tilføje en klasse hvis den er aktiv.  

Lad os være smarte og definere det som en variable.

```javascript
const DevAssignmentsNavBtn = ({link, title}) => { 
    const pathname = usePathname()
    const active = pathname === link ? styles.active : ''
    return (
        <div className={`${styles.navBtn} ${active}`}>
            <Link href={`${link}`}><FaJsSquare / > {title}</Link>
        </div>
    );

};
```

:link: Vi benytte en `Conditional (ternary) operator`   
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator

Den benytter vi her til at afgøre om `active` indeholder `styles.active` eller `''` (ingenting)
`const active = pathname === link ? styles.active : ''`

Vi kunne også benytte en `if/else` sætning, men når vi `toggler` så skriver vi mindst mulig kode.

`const VARIABLE = (udtryk) ? (udtryk er sandt) : (udtryk er falsk)`.

Så hvis `pathname` er `assigments/icons` og knappens `link` værdi er `assigments/icons` så sætter vi en flot grøn `styles.active` klasse.

Altså:  
`const active = "assigments/icons" === "assigments/icons" ? (SÆT STYLE ACTIVE) : (GØR INGENTING)`. 

Bliver til:     
`const active = pathname === link ? styles.active : ''`

Således kan vi nu benytte denne måde til at undersøge om vi er på den rigtige path.


### Næste skridt.

:bulb: Man kan diskutere hvorvidt selve navigations komponentet skulle styre ansvaret, men her er det oplagt at vi gør det så simpelt som muligt og holder vores `<DevAssignmentsNavigation />` `serverside` altså **ikke** benytter `use client` i den.

Vi vender tilbage ti l `routing` men vi lader det ligge fornu - vi har hvad vi skal bruge for at gøre vores UI responsiv i forhold til vores URL/ROUTE.

Se index for næste opgave.