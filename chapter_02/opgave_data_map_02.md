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

### :dart: 1. Assets, `<Image> vs <img>`.

Vi starte med at oprette endnu en under-under side til data.



### :dart: Opret en ny under-under side.

Vi skal lave en underside til `/assignments/data/images` så:

1. Opret en `page.js`/`page.module.css` under `/assignments/data/images`.
2. Opret et menupunkt i assignments menu´en.

Indsæt følgende i `page.js`:

```JavaScript
import { fetchImagesForGallery } from '@/lib/data.service';
import styles from './page.module.css'
import DevDebugJson from '@/components/dev/devDebugJson/devDebugJson';

const Page = async () => {

    let gallery = 'umbra';
    const images = await fetchImagesForGallery(gallery);

    return (
        <main className={styles.page}>
            <h1>Alle Billeder Fra {gallery} Data</h1>
            <DevDebugJson content={images}></DevDebugJson>

            <h1>Hvert Enkelt Billede</h1>
            {images.map((image, index) => {
                return <DevDebugJson key={index} content={image}></DevDebugJson>
            })}
        </main>
    );

}

export default Page
```
Igen ser vi json-debug-elmentet men nu for **alle** billder i ét galleri.

Først hele objektet derefter hver enkelt.

:bulb: Bemærk at vi her "hardcoder" galleri navnet `let gallery = 'umbra'` og derefter kalder vi `fetchImagesForGallery(gallery)` altså => `fetchImagesForGallery('umbra')`.

Det kan fordi vi ved vi har to gallerier `umbra`og `obscura`.

Igen gør vi det samme som sidst og indsætter et komponent.

### :dart: Hente Assets til public folder.

:bulb: 1. Først skal du som en *beklagelig rettelse*, tilføje 3 linier til `.gitignore` filen.

```
# Gallery Assets.
/public/obscura
/public/umbra
```
:link: 2. Så skal du downloade zip filen fra dette link    
https://github.com/MCDM-Viborg-Documentation/hf-nextjs-sem/blob/main/assets/galleries.zip       
:bulb: *Du skal trykke "download raw file" knappen* :arrow_down:

Begge gallerier skal ligge i `public` mappen.

```
├── ...
├── public
│   ├── umbra              
│   ├── obscura              
│   └── square_logo.png
├── ...
```

:goal_net: Hvis følgende url viser et billede så er alt godt.   
`http://localhost:3000/umbra/lena_jespersen/A01.jpg`

3. Opret nu følgende snippet.     
**Snippet**     
:pencil: `snippets/comp_devGalleryImage.md`.

4. Så udskifter vi igen vores json-debugger i loop´et til det nye `<DevGalleryImage image={}>` komponent.

:goal_net: Så kom der billeder.

Men kig nu godt efter i consollen under `network`tabben og se hvor dan alle billeder er loadet. Også alle dem vi end ikke har set endnu. Det kan jo være fint, så er de klar når vi scroller.

Men det vil være langt bedre hvis de preloader lige *inden* de skal ses. Det vil også være godt at de er optimeret og cachet.

Alt det og meget mere tager Next/Image sig af.

### :dart: Åbn `devGalleryImage.js`.

Udskift.

```html
<img src={image.path} alt={`Portfolio billede taget af ${image.author} udstillet i falleriet ${image.gallery}`} className={styles.image} />
```

med
```html
<Image src={image.path} alt={`Portfolio billede taget af ${image.author} udstillet i halleriet ${image.gallery}`} className={styles.image} width={image.width} height={image.height} />
```

og importere komponentet `import Image from 'next/image';` fra NextJS.

Nu kan du både se og høre forskel :)

:bulb: Kig også på json data´en for et billede der er meget meta med.

## :dart: Opret et Meta Komponent

Komponentet skal placeres inde i image komponentet. Læs vejledning, du er på egen hånd.

1. Opret et `<DevImageMeta meta={meta}></DevImageMeta>`.
2. Indsæt det i `<DevGalleryImage />` komponetet, erstat den med `<DevDebugJson>` komponetet.
3. `<DevImageMeta meta={meta}></DevImageMeta>` skal *præsentere* mindst 10 meta informationer i en liste men ikke det hele. Brug evt `deconstruction` :eyes:

:link: Destructuring assignment     
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment
```
const x = [1, 2, 3, 4, 5];
const [y, z] = x;
console.log(y); // 1
console.log(z); // 2
```

Det skal ikke ligne guld som alt det andet.

God Arbejdslyst og push din løsning.

### Næste skridt.

Kig i index.


