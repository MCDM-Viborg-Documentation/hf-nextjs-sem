# Media College
```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : Start med serverside data 
Doc         : opgave_data_portfolio
```
### Indledning.

Nu ikke så meget tekst - mere bas.

Vi fortsætter hvor vi slap i forrige opgave.

### Forudsætning.

1. Læs ovenstående indledning.
2. De forrige opgaver i indexet.

### :dart: 1. Portfolie Komponent.

Vi arbejde på at lave en galleri af portfolier.

Portfolie er i denne sammenhæng en fotograf=`author from author collection` tilknyttet en række billeder=`author images from images collection`.

Så i vores `data.service.js` er der en mulighed for at kalde `fetchImagesForAuthor('Lena Riis')`, altså med et navn, og dermed få alle billede tilknytte denne. 

Det kan vi bruge til at hente lave en *Portfolio/galleri* af billeder for én *Author*.

Men inden vi gør det skal vi lige lave et par ænndringer til vores `<DevGalleryImage />` komponent.

"Vi" har lavet et nyt `<DevImageMeta meta={meta}></DevImageMeta>` som viser meta data´en for billedet.

Vi har udskiftet den med `<DevDebugJson />` komponentet. Men nu ønsker jeg 2 ændringer.

1. Istedet for at komponentet har et tomt `<>` omkransende *element (altså ingen)* så skal vi nu lave den til en `<div>`.
Nu er det ikke længere "bare" et debug-element - nu er det en samlet del af et komponent. Det gør at vi har styr på indholdet hvis vi ønsker at ændre størrelse, udefra (*forældre elementer*).

2. Dernæst vil skal vi gøre det mulig at vise eller ikke vise selve  `<DevImageMeta meta={meta}></DevImageMeta>` komponentet.
Så har vi en mulighed for at bruge billedet i flere sammenhænge, med og uden meta.

```JavaScript
const DevGalleryImage = ({image, showMeta}) => {

    let displayDetails = showMeta ? <DevImageMeta meta={image.meta}></DevImageMeta> : null;

    return (
        <div>
            <Image src={image.path} alt={`Portfolio billede taget af ${image.author} udstillet i halleriet ${image.gallery}`} className={styles.image} width={image.width} height={image.height} />
            {displayDetails}
        </div>
    )
};
export default DevGalleryImage
```

:bulb: Kig godt på ovestående, kan du se hvad der foregår?

1. Vi har tildelt `DevGalleryImage` en extra parameter `showMeta`. `showMeta` kan være `true` eller `false`.
2. Vi opretter en vaiable.

```JavaScript
let displayDetails = showMeta ? <DevImageMeta meta={image.meta}></DevImageMeta> : null;
```

Vi benytter en ternary-operator for at sætte `<DevImageMeta />` komponentet efter showMeta = `true` eller `false`.

3. Vi indsætter `displayDetails` variable i vores template.

```html
<div>
    <Image src={image.path} alt={`Portfolio billede taget af ${image.author} udstillet i halleriet ${image.gallery}`} className={styles.image} width={image.width} height={image.height} />
    {displayDetails}
</div>
```

Og på den måde kan vi vise eller ikke vise meta. Det eneste vi mangler at gøre er:

1. Tildele en default værdi til vores parameter. `const DevGalleryImage = ({image, showMeta=false}) => {`
    bemærk `showMeta=false` vi fortælle komponetet/functionen at hvis der ikke er sat et `showMeta` property så er `showMeta` = `false` som `default`.

Nu vil det allerede kunne testes de steder vi viser billeder. Lige nu har vi slået met fra `showMeta` : `false`.

Hvis vi sætter en property på selve komponentet `<DevImageMeta image={image} showMeta={true}/>` så vil den blive vist. Vi kan også vælge at lave vores default parameter om til `true` og så vil det være udgangpunktet at meta blier vist.

### :dart: Med billede på plads.

Nu er vi klar til at lave det sidste element inden vi skifter spor for en stund. Vi skal lave et `<DevAuthorPortfolio></DevAuthorPortfolio>` komponent.

Vi laver et komponent der viser billeder for én **Author**.

#### 1. Men først portfolios undersiden (*en kopi af authors til at starte med, men en anden rute.*)

    1. Vi starter med at oprette en side/rute under `assignments/data/` kaldet `portfolios`
    2. Vi gør som vi har gjort det de sidste par gange. Opretter `page.js` og `page.module.js`
    3. Kopier indholdet fra `authors/page.js` ind i vores nye fil. (Vi skal bruge det samme i denne fil `loop` over alle `Authors`)
    4. Lav en `Data - Portfolios` knap i navigationen.

:goal_net: Nu har du en side som ligner `assignments/data/authors` siden på en prik. En ren kopi men med ny *rute/route* `/assignments/data/portfolios`.

#### 2. Opret `<DevAuthorPortfolio></DevAuthorPortfolio>` komponent. 

**Snippet**     
:pencil: `snippets/comp_devAuthorPortfolio.md`.

:bulb: *Læs komponent beskrivelse i snippet filen.*

Som beskrevet så henter vores Portfolio kmponent selv sin data og fordi vi stadig er `serverside`, gør vi det på nøjagtig samme måde som vores `page.js` filer.

Vi mangler bare at erstatte `<DevAuthorHero>` på vores nye side med `<DevAuthorPortfolio />` og så har vi en samling af alle **Authors** billeder i èt komponent/portfolio for sig.

### Nu har vi lavet de komponeter der skal til for at vi kan bygge et "flow".

Vi har lavet alle komponenter og i næste opgave samler vi det hele til en "applikation" med et flow.

:dart: M;en inden da er der lige en lille udfordring.

1. Opret et komponet med et forstørrelsesglas ikon. 
2. Det skal være diskret.
3. Det skal indsættes i `<DevGalleryImage />`komponentet,
4. Man skal kunne toggle meta data af og på ved kilk på forstørrelsesglasset.

:muscle: God arbejdslyst, næste skridt kig i indexet.