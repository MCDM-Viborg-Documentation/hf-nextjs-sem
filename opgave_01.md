# MediaCollege Denmark

# Forudsætning.

At alt er læst og *forstået* i den indlende opgave.

Det er vigtigt at alle opgaver :dart: og spørgsmå :question: er løst.

Husk også at læs igennem de links der er vedhængt.

I de kommende opgaver bygger vi vidre på samme projekt.

## :dart: Opgave

Nu skal vi til at arbejde med vores applikation og i starten skal du bare følge anvisningerne i dette dokument.

### Opret Navigations Komponent

I `components` mappen opretter vi en `navigation`mappe.

Og i den nye `navigation`mappe opretter vi to filer:

`navigation.js` og `navigation.module.css`

I `navigation.js` indsættes følgende:

```javascript
import Link from 'next/link';
import styles from './navigation.module.css'
import Image from 'next/image';

const Navigation = () => {

    return (
        <div className={styles.container}>
            <div className={styles.navBar}>
                <div className={styles.logo}>
                    <Link href="/"><Image src={'/square_logo.png'} width={40} height={40} alt={'logo'}></Image></Link>
                </div>
                <div>
                    NAVIGATION
                </div>
                <div>
                    {/* BURGER ICON */}
                </div>
            </div>
        </div>
    )

}

export default Navigation;
```

I `navigation.module.css` indsættes. 

```css
.container {
  position: fixed;
  width: 100%;
  height: 100%;
}

.navBar {
  padding : 0 20px;
  width: 100%;
  height : 60px;
  display: flex;
  background-color: var(--navigation-background-color);
  color: var(--navigation-color);
  justify-content: space-between;
  align-items: center;
}

.navBar img {
  padding: 5px;
  left: 2px;
  top: 1px;
  position: relative; 
}

.navBar .logo {
  background-color: var(--navigation-logo-background-color);
  border-radius: 20px;
  height: 40px;
  width: 40px;
  cursor: pointer;
  object-fit: contain;
}
```

Nu har vi oprettet vores main navigation og mangler bare at indsætte den i applikationen.

Åbn `layout.js` filen og indsæt `<Navigation></Navigation>` komponentet lige efter `<body>` tagget.

Hvis alt er gået godt skulle du gerne se en menu-bar på siden med et logo i venstre hjørne.

### Indbyggede komponenter

Åbn `navigation.js`.

Vi benytter to indbyggede Next Komponenter i navigationen

```javascript
import Link from 'next/link';
import Image from 'next/image';
```

:link: `<link>`
Vi benytter Link for at optimere vores links struktur i applikationen.      
https://nextjs.org/docs/app/api-reference/components/link

:link: `<Image>`
Vi benytter Image for at optimere vores billeder applikationen. 
https://nextjs.org/docs/app/api-reference/components/image

Brug lidt tid på at læse om begge komponenter.

### Layout.js

Vi arbejder også med `layout.js` og i dette tilfæde viroes root.layout. Vi vil senere lavet endnu en layout fil.    

:link: `layout.js`    
https://nextjs.org/docs/app/api-reference/file-conventions/layout

### module.css og variabler dark/light.
I `navigation.module.css` filen skal i ligge mærke til brugen af variabler. Disse variabler er oprettet i `global.css`.

Prøv at ændre "dark" og "light" mode på dit styressystem og benyt lidt tid på a se hvordan stylesheetet er opsat.


### Afslutning af denne opgave.

Nu har vi indsat et globalt navigation vi vender tilbage til den senere.

### Næste skridt.

Opgave 02
