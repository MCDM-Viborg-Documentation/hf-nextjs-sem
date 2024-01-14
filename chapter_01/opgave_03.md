# Media College

```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : NextJS Opgave
Doc         : opgave_03
```

# Forudsætning.

At alt er læst og *forstået* i den forrige opgave.

Det er vigtigt at alle opgaver :dart: og spørgsmå :question: er løst.

Husk også at læs igennem de links der er vedhænngt.

## :dart: 1. Opgave

Fordi dette er et "skole projekt" opretter vi nu en rute til opgave løsninger og eksperimenter.

1. Opret en `assignments` mappe i `app` mappen.
2. Opret `page.js` og `page.module.css` i `assigments` mappen.

I `page.js` indsættes følgende:

```javascript
import styles from './page.module.css'

export default async function Page() {

  return (
    <main className={styles.page} >
        Assignents
    </main>
  )
}
```

I `page.module.css` indsættes. 

```css
.page {

  padding-top : 60px;
  
}
```

Nu har vi oprette det minmum der skal til for en lave en underside.

### Læg mærke til..

At vores `page.module.css` har padding-top på 60 pixels. Der er fordi vores menu lige nu er fixed og dermed ligger ovenpå og fylder 60 oixels i højden.

Gå nu til siden `http://localhost:3000/assignments` og du skulle skulle se der står `Assignments` øverst til venstre.

## :dart: 2. Opgave

Opret en ny rute/underside (route) i `assigments` mappen.

Den skal hedde `icons`.

Når du er færdig skal man kunne gå til siden `http://localhost:3000/assignments/icons` og se der står `Icons` øverst til venstre som på assignments siden.

### Afslutning af denne opgave.

Vi har oprettet et sted til opgaver løsninger og diverse.

Man kommer til at oprette utrolig mange `page.js` filer og mapper - Det gælder om at holde tunge lige i munden.

:link: `page.js`      
https://nextjs.org/docs/app/api-reference/file-conventions/page

Se linkey og bemærk de to parametre et `page`komponent "bære" med sig, `params` og `searchParams`

```
export default function Page({ params, searchParams }) {
  return <h1>My Page</h1>
}
```

Dem vender vi tilbage til, men det er værd at huske at de to parametre altid er til stede på et `page` komponent.

### Næste skridt.

Opgave 03