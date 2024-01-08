# MediaCollege Denmark

# Forudsætning.

At alt er læst og *forstået* i den forrige opgave.

Det er vigtigt at alle opgaver :dart: og spørgsmå :question: er løst.

Husk også at læs igennem de links der er vedhænngt.

## :dart: 1. Opgave Action Bar

Fik vi leget med knapperne.

Jeg ender med at have tre knapper der ser sådan her ud i action baren.

```html
<div className={styles.actionBar}>
    <span className={styles.btn} onClick={() => setSize(50)}>LILLE</span>
    <span className={styles.btn} onClick={() => setSize(100)}>MELLEM</span>
    <span className={styles.btn} onClick={() => setSize(150)}>STOR</span>
</div>
```

og jeg har sat `style` på alle ikoner.

```html
<div className={styles.icons}>

    <Fa500Px style={style}/>
    <FaAccessibleIcon style={style}/>
    <FaBlackTie style={style}/>
    <FaBomb style={style}/>
    <FaBroom style={style} />
    <FaCog style={style} />
    <FaCoffee style={style} />
    <FaGithub style={style} />
    <FaJsSquare style={style}/>
    <FaBeer style={style}/>

</div>
```

Nu kan jeg skifte størrelse på alle ikoner i sættet med knapperne.

## ActionBar som komponent

Vi vil gerne gøre ActionBar til et komponent som kan aflevere en størrelse f.eks 150, som vi gør nu med vores knapper. Så kan man bruge det Action Panel andre steder hvor man har behov for at ændre størrelse på "noget".

## :dart: 1. Opret Action Panelet som komponent.

Tag Action Baren og opret et nyt komponent `<devActionBar></devActionBar>`.

```html
<div className={styles.actionBar}>
                
    <span className={styles.btn} onClick={() => setSize(50)}>LILLE</span>
    <span className={styles.btn} onClick={() => setSize(100)}>MELLEM</span>
    <span className={styles.btn} onClick={() => setSize(150)}>STOR</span>
                
</div>
```

Opret komponentet i/som `compoents/dev/devActionBar/devActionbar.js`
Husk at oprette `devActionbar.module.css` og flyt klasserne fra `devIcons.module.css`.

Når du har oprettet komponentet skal du indsætte det i `devIcons.js` igen.

Nu kan du se at hvis du trykker på knapperne så får du en fejl.

```html
Unhandled Runtime Error
ReferenceError: setSize is not defined
```

Vi prøver at kalde setSize funktionen i action komponentet men setSize funktionen er i icons komponentet så det er to forskellige steder. 

Men heldigvis kan vi sende setSize funktionen med ind til komponentet.

Så lad os tilføje `setSize` funktionen som en `property` på vores action bar komponent i `devIcons.js` filen.

```html
<DevActionBar setSizeFunction={setSize}></DevActionBar>
```

Læg mærke til at jeg har givet property navnet: `setSizeFunction` og sat den lig med `setSize`.

Hvis vi så åbner `devActionBar.js` så tager vi imod property funktionen ved at benytte det navn `setSizeFunction` som parameter i vores komponent.

Indsæt `{setSizeFunction}` som parameter i DevActionBar komponentet.
```javascript
const DevActionBar = ({setSizeFunction}) => {
```

Det sidste der mangler, er at vi i actionbar komponentet udskifter `setSize` med `setSizeFunction`.

Nu skulle vi kunne ændre størrelse på vores ikoner nøjagtig lige som før.

:coffee: Flyt nu din `<DevActionBar></DevActionBar>` op over ikonerne så den ligger i toppen.

# Input Range.

Nu skal vi lave en ny knap til vores action bar.

Kig *godt* på disse linier.

```html
<span className={styles.btn}>
    <input type="range" min="50" max="150" onChange={(e) => setSizeFunction(e.target.value)}></input>
</span>    
```

Vi har vores knap `<span className={styles.btn}></span`.

I den indsætter vi et `input` men typen `range` - vi benytte eventen `onChange` og kalder vores funktion `setSizeFunction` med værdien fra vores `target` => `e.target.value`. 

`e.target.value` er en værdi imellem `min` og `max` properties på `input` range feltet. 

Indsæt knappen i action panelet og prøv at slide frem og tilbage.

Så har vi en ikone oversigt hvor vi kan sætte størrelser.

## Afslutning.

Inden vi går til næste opgave.

Vores "slider"/range input indstiller sig ikke på størrelsen hvis vi trykker på knapperne.

Og hvordan kan vi i actionbaren skrive den værdi vores action bar er sat til?

Vi løser det i næste opgave men forsøg lige at give det et skud.

### Næste skridt.

Opgave 06







