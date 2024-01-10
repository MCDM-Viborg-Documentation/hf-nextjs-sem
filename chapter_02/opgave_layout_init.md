# Forudsætning.

At alt er læst og *forstået* i den forrige opgave.

Det er vigtigt at alle opgaver :dart: og spørgsmå :question: er løst.

Husk også at læs igennem de links der er vedhænngt.

## :dart: 1. Opgave Layout.

:link: `layout.js`            
https://nextjs.org/docs/app/api-reference/file-conventions/layout

`layout.js` er en "indbygget" file type lige som `page.js` - selve navnet tjerne et formål og kan *ikke* omdøbes.

Layout er en god måde at opdele dele af dokumentet i forskellige layouts som de underliggende sider vil arve.

Man **skal** have minimum én layout fil i sit projekt.

Den kalder vi `root layout`. Den ligger i `app/layout`. Det var her vi lagde vores Navigation. Det er også her vi har `<html></html>` og `<body></body>` tags.

```javascript
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body className={oswaldFont.className}>
        <Navigation></Navigation>
        {children}
      </body>
    </html>
  )
}
```

Men man kan herefter have en eller flere `layout.js` filer hvis man har behov for at dele indhold og grafik på tværs af en sektion.

Lad os gøre `assigments` til et område med navigation til venstre og indhold til højre.

Start med at oprette to filer i `assignments` mappen.

`layout.js` og `layout.module.css`.

I `layout.module.css` indsætter vi:

```css
.navBtn {
    user-select: none;
    background-color: cadetblue;
    padding : 0 10px;
}

.navBtn:hover {
    background-color: #333;
    color: #fff;
}

.navBtn.active {
    background-color: green;
}

.navBtn svg {
    width : 25px;
    height : 25px;
}

.navBtn a {
    display: flex;
    align-items: center;
    gap: 10px;
    width: 100%;
    height: 100%;
    text-decoration: none;
    line-height: 60px;
}

```

og i `layout.js` indsætter vi:

```javascript
import styles from "./layout.module.css"

export default function AssignmentsLayout({ children }) {
    return <section className={styles.layout}>
        <div className={styles.navigation}>
            <div className={styles.navContainer}>
                navigation - links
            </div>
        </div>
        <div className={styles.content}>
            {children}
        </div>
    </section>
}
```

Kig godt på `AssignmentsLayout` den tager imod `{children}` det vil sige de sider de er under layout filen.

Den udskriver `{children}` i content div
```html
<div className={styles.content}>
    {children}
</div>
```

Og ovenover har vi et navigations element:

```html
<div className={styles.navigation}>
    <div className={styles.navContainer}>
        navigation - links
    </div>
</div>
```

N vil du kunne gå på `http://localhost:3000/assignments/` siden og du vil se at vores `page.js` nu optræder i venstre side loaded in som `{children}`.

For god ordens skyld behøver vi ikke længere `padding-top:60px` i vores page filer under assigment. Vi har tilføjet den padding til layout.module.css. Så fjern dem fra de to `page.module.css` filer under `assigments`.

Kig nu godt på `css` og selve `layout`filen. Det hele er sat op så navigationen er sticky (*bliver stående selvom du scroller*) og fordi vi har brug for den fulde højde uanset indhold så skal vi gå ind i vores `app/global.css` og tilføje `height: 100%;` til vores `html,body` tag.

```css
html,
body {
  background-color: var(--main-color);
  height: 100%;
}
```

Gå nu ind på `http://localhost:3000/assignments/icons` siden. I koden laver du 3 kopier af `<DevIcons />`.

```html
<main className={styles.page}>
    <DevIcons></DevIcons>
    <DevIcons></DevIcons>
    <DevIcons></DevIcons>
</main>
```

Nu skulle der gerne komme en scrollbar.

Men ud over det! - Læg mærke til hvordan hver enkelt `<DevIcons />` er individuelle. Du kan sætte størrelse og farver individuelt - de holder selv på deres indhold. De har selv ansvaret!. 

:dart: Delopgave     
(*kan løses senere - men løsningen er ligetil, hvis man har fanget fidusen! det skal nok komme*)

Man får helt lyst til at man kan "config´urere" hver `<DevIcons />` til at have forskellige indstillinger/config fra start.

Det vil være rart hvis de start med hver deres farve og forskllige størrelses valg.

Det er nu op til dig at få det til at virke.

:coffee: En lille tår kop kaffe!

## :dart: Assignments Navigation

I `assignments/layout.js` har vi vores navigations container.

```html
<div className={styles.navigation}>
    <div className={styles.navContainer}>
        navigation - links
    </div>
</div>
```

Her skal vi **ikke** skrive vores links. Vi *kunne* godt. Men det er langt bedre at vi opretter et komponent til dette formål.

Så opret `<DevAssigmentsNavigation />` komponententet.

`@/components/dev/devAssigmentsNavigation/devAssignmentsNavigation.js`
`@/components/dev/devAssigmentsNavigation/devAssignmentsNavigation.module.css`

`devAssignmentsNavigation.module.css`:
```css
.navigation {
    color : #fff;
}

.navigation .header {
    background-color: red;
    padding : 10px;
}

.navigation .links {
    background-color: green;
}
```

`devAssignmentsNavigation.js`
```javascript
import styles from './devAssignmentsNavigation.module.css';

const DevAssignmentsNavigation = () => {

  return (
    <div className={styles.navigation}>
      <div className={styles.header}>
         <h3>Assigments</h3>
      </div>
      <div className={styles.links}>
        <div>LINK BTN</div>
      </div>
    </div>
  );
}

export default DevAssignmentsNavigation;
```

Indsæt nu komponentet i `layout.js`.

```html
//---
<div className={styles.navigation}>
    <div className={styles.navContainer}>
        <DevAssignmentsNavigation />
    </div>
</div>
//---
```
Nu har vi et komponent hvor vi kan styre navigationen af assigments undersiderne.

## Vi mangler bare at lave links/knapper.

Så opret `<DevAssigmentsNavBtn />` komponentet.         
(*note: bemærk at komponentet oprettes som en undermappe til devAssigmentsNavigation mappen*)

`@/components/dev/devAssigmentsNavigation/devAssignmentsNavBtn/devAssignmentsNavBtn.js`
`@/components/dev/devAssigmentsNavigation/devAssignmentsNavBtn/devAssignmentsNavBtn.module.css`

`devAssignmentsNavBtn.module.css`
```css
.navBtn {
    user-select: none;
    background-color: cadetblue;
    padding : 0 10px;
}

.navBtn:hover {
    background-color: #333;
    color: #fff;
}

.navBtn.active {
    background-color: green;
}

.navBtn svg {
    width : 30px;
    height : 30px;
}

.navBtn a {
    display: flex;
    align-items: center;
    gap: 10px;
    width: 100%;
    height: 100%;
    text-decoration: none;
    line-height: 60px;
}
```
`devAssignmentsNavBtn.module.js`
```javascript
import styles from './devAssignmentsNavBtn.module.css';
import { 
    FaJsSquare,
} from "react-icons/fa";

const DevAssignmentsNavBtn = ({link, title}) => { 

    return (
        <div className={styles.navBtn}>
            <a href={`/assignments/icons`}><FaJsSquare / > icons</a>
        </div>
    );

};

export default DevAssignmentsNavBtn;
```

Indsæt nu knappe i navigationen og lav evetuelt flere kopier til at atarte med.

Lige u beholder vi det samme ikon i knapperne til alle links. Vi vil senere arbejde med hvordan ikonerne kan benyttes dynamisk. Det er både en lidt kringlet erfære men der er også nogle hensyn man skal tage i forhold til hvad man arbejder med.

Så til de her knapper mangler vi bare at tilføje properties.

```javascript 
const DevAssignmentsNavBtn = ({link, title})
```

Så vi kan indsætte knapper efterhånden som vi laver flere og flere opgaver/assignments.

```html
<DevAssignmentsNavBtn link={'/assignments'} title={'Assignments'} />
<DevAssignmentsNavBtn link={'/assignments/icons'} title={'Icons'} />
```

Men læg mærke til hvordan det *blinker og bamler* når vi navigere med vores knapper. 

Det er fordi vi benytter helt admindelige `<a href=""></a>` links/knapper i vores knap.

NextJs har lavet et link komponent der sørger for at "cache" den rute den føre til. Det gør at når vi benytte det komponent i stedet - så får en langt mere optimeret udgave.

Så lad os straks ændre det og se den store forskel.

Vi ændre 
```html
<a href={`${link}`}><FaJsSquare / > {title}</a>
```
til `Link`
```html
<Link href={`${link}`}><FaJsSquare / > {title}</Link>
```

og importere komponentet.
```javascript
import Link from 'next/link';
```

Se nu hvor "snappy" :8ball: det hele er  - side skiftene er instant og alt efter hvordan vi arrangere vores indhold kan vi lave virkelig hurtigt responderede applikationer. - Nu er det data´en vi venter på!.

Nu kunne man få lyst til at ændre på scrll i forhold til at det kunne ligge internet i komponent icons f.eks. Men det lader vi lige ligge for nu - det handler mere om styling.

Men der er ingen tvivl om at det hele er en kombination. Og måden layout css´en er lavet er ikke tilfældigt. Man skal benytte lidt triks og have en god sans for hvordan man "arrangere" sine elementer og komponenter.

Men til gengæld så bliver det også en "dans med klodser" som du forbinder, hvor det giver mening.

Og det tager tid at lære det hele. 

I balancerer lige nu med:

`css`, `js`, `nextJS` og `react` :eyes: 

Alle områder der er i rivende udvikling, så træk vejret, det tager tid og "5-øren" falder på de mærkeligste tidspunkter for hver især. Det er helt naturligt - nogen gange er de de mindste ting der pludselig giver et øjebliks "åbenbaring" - bare nyd den process - og giv jer tid til at acceptere den - bliv stædig! :muscle: 

### Næste skridt.

Læs dokumentationen om `layout.js` og læs også om `Link`

:link: `layout.js`      
https://nextjs.org/docs/app/api-reference/file-conventions/layout       
:link: `Link`     
https://nextjs.org/docs/app/api-reference/components/link

Der er især god viden at hente omkring `Link` - se f.eks hvad attributten 'scroll' er for én.


Senere gør vi menu-punkterne dynamisk - hvis du ikke kan vente :) så er du velkommen til at gøre det. Men vi vender tilbage til det senere. Lav det eventuelt som et *alternativt* komponent. 

Se index for næste opgave.