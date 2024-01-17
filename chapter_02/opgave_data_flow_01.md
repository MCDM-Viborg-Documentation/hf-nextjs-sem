# Media College NextJS Opgave
```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : Start med serverside data 
Doc         : opgave_data_flow_01                     
```
### Indledning.

Nu ikke så meget tekst - mere bas.

Vi fortsætter hvor vi slap i forrige opgave.

### Forudsætning.

1. Læs ovenstående indledning.
2. De forrige opgaver i indexet.

# :dart: VIGTIG!

Vi starter denne opgave med lidt generelle rettelse, igen med baggrund i jeres afleveringer.!

1. Erstat `/lib/data.service.js` med indholdet fra denne md.   	    
:link:  [`misc/rettelse_til_dataservice.md (i dette repositorie)`](../misc/rettelse_til_dataservice.md)

1. Erstat `/app/global.css` med indholdet fra denne md.   	    
:link:  [`misc/rettelse_til_globalcss.md (i dette repositorie)`](../misc/rettelse_til_globalcss.md)

### :dart: Knap så VIGTIG!

Mindre (*ikke nødvendige men kosmetiske rettelser*)

1. Navigation Øverst.  
`navigation.module.css` 

*Erstat*
```css
{
    .container {
        position: fixed;
        width: 100%;
        z-index: 100; /* <- Vi løfter navigation op over alle andre elementer hvor z-index er mindre end 100. */
    }
}
```

# :dart: SÅ! - Komponenter, Links og flow.

Lad os kommer igang med at bliver færdig i denne omgang!.


### Galleries Siden (oversigt over alle gallerier.)
Lad os starte med `/galleries/page.js` og fjerne vores link.

Nu skal vi, som vi gjorde i `assignments` hente gallerierne og indsætte vores komponent.

`/galleries/page.js`
```Javascript
// imports

export default async function Page() {

  // Henter gallerier fra vores serverside data.
  const galleries = await fetchGalleries();

  return (
    
    <main className={styles.page}>
        <h1>Portfolie Gallerier</h1>
        {/* Loop´er over vores galleri data. */}
        {galleries.map((gallery, index) => {
            {/* Indsætter vores Hero komponent og sender "gallery" objectet med */}
            return <DevGalleryHero key={index} gallery={gallery}></DevGalleryHero>
        })}
    </main>

  )
}
```

Nu mangler vi at oprette link i vores hero komponent.

Så åbn `@components/dev/devGallery/devGalleryHero/devGalleryHero.js` og ændre:

 `<h1>{gallery.name}</h1>` til 
`<h1><Link href={url}>{gallery.name}</Link></h1>`

Som du kan se ændre vi til et Link (*husk import*) men vi sætter også `href={url}` og `{url}` er en variable som vi skal oprette. Vi kunne vælge at gøre det direkte i `href={ [scripte et eller andet] }` men det er "pænere" at vi gør det lige efter vi har modtaget vores data.

Så lad os definere `let url = '/galleries/' + gallery.name;` lige over vores `return ()`.

Så vores fulde komponet ser således ud.

```Javascript
import Link from 'next/link';
import styles from './devGalleryHero.module.css';
const DevGalleryHero = ({gallery}) => {

    // Opretter en URL til vores galleri.
    let url = '/galleries/' + gallery.name;

    return (
        <div className={styles.hero}>
            <div className={styles.content}>
                {/* Linker til vores galleri side. Med url´en. */}
                <h1><Link href={url}>{gallery.name}</Link></h1>
                <p>{gallery.year}</p>
            </div>
        </div>
    )
};

export default DevGalleryHero
```

Nu kan vi klikke overskriften på vores gallri element og vi linker lige nu til enten 

`http://localhost:3000/galleries/obscura` eller `http://localhost:3000/galleries/umbra`.



### Galleri Siden [gallery] (Authors) (oversigt over alle authors i ét galleri.)
Så går vi til galleri siden.

Åbn `galleries/[gallery]/page.js`.

Lad os bare udskifte filen med det samme.

```javascript
import styles from './page.module.css'
import { fetchAuthorsByGalleryName } from '@/lib/data.service';
import DevAuthorHero from '@/components/dev/devGallery/devAuthorHero/devAuthorHero';

export default async function Page({ params }) {
  
  const authors = await fetchAuthorsByGalleryName(params.gallery);

  return (
    <main className={styles.page}>
      {authors.map((author, index) => {
          return <DevAuthorHero key={index} author={author}></DevAuthorHero>
      })}
    </main>
  )
}
```

:bulb: Hvad sker der nu? Hvad gær vi med `{params}`. Husk vores `params.gallery` indholder nu enten `obscura` eller `umbra`.

1. Vi henter Authors og vi tager `params.gallery` og bruger som `parameter` til vores `fetchAuthorsByGalleryName` funtion i `data.service.js`.

2. Forskellen fra vores `assignment/data/authors/page.js` side og denne er `endpointet` her henter vi et specifikt galleri udfra det galleri navn vi ønsker at hente. f.eks. `fetchAuthorsByGalleryName('umbra')` 

Nu skal vi tilføje et link til vore hero komponent.

Åbn `@components/dev/devGallery/devAuthorHero/devAuthorHero.js`.

Udskift `<h2></h2>`med denne `<Link href={url}>{author.author}</Link>`. Og som i forrige komponet, definere vi url´en: 

```javascript
let url = `/galleries/${author.gallery}/${author.niceUrl}`;
```

Nu benytter vi 2 parameter til url´en. Vi ved vores Author kun tilhøre ét galleri og vi har faktisk navnet på det galleri i selve vores auhtor data.

Eksempel: 
```json
{
  "_id": "659d10f5d8344e1429921fb3",
  "author": "Lena Riis",
  "gallery": "obscura",
  "folder": "lena_riis",
  "niceUrl": "lena-riis",
  "created": "2024-01-09T09:25:09.844Z"
}
```

Der er også en nice-url som sør at ikke skal omskrive en url der fungere i browseren.

Så ``/galleries/${author.gallery}/${author.niceUrl}`` bliver til eksempelvis ``/galleries/umbra/lene-riis``.


### Portfolio Siden [author] (Author) (Viser én author eg. portfolio.)

Nu ender vi på `/galleries/obscura/lena-riis` og skal vise vores portfolier. 

Åbn `galleries/[gallery]/[author]/page.js`. Og udskift med dette indhold.

```javascript 
import { fetchAuthorByNicUrl } from '@/lib/data.service';
import styles from './page.module.css'
import DevAuthorPortfolio from '@/components/dev/devGallery/devAuthorPortfolio/devAuthorPortfolio';

export default async function Page({params}) {
  
  let author = await fetchAuthorByNicUrl(params.author)

  return (
    <main className={styles.page} >
      <DevAuthorPortfolio author={author} />
    </main>
  )
}
```

Simpelt! 

Vi trækker `{paams.author}` kunne være `lena-riis` vi benytter `endpointet` -> `fetchAuthorByNicUrl({params.author}).

Så vores `let author` indeholder vores `author` object.

Så indsætter vi `<DevAuthorPortfolio author={author} />` og vores portfolio `renderes`. 

Og så har vi lavet et "fuldt" flow og benyttet vores elementer.

## Afslutning

Der er mange ting vi kan gøre i dette projekt. Men inden vi gør noget som helst så **"push"** et commit **"Afsluttet 2-9".**.

:bulb: Gør din underviser opmærksom på at du er færdig og afvent herefter respons.

:bulb: Husk du kan *enten* tage en kopi af projektet eller oprette et "branch" og arbejde mere frit i det. Men hod projektet i sin originale form indtil videre. (*farver er op til dig, men det skal være læsbart*)

:muscle: Godt Arbejde!.




