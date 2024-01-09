# Forudsætning.

At alt er læst og *forstået* i den forrige opgave.

Det er vigtigt at alle opgaver :dart: og spørgsmå :question: er løst.

Husk også at læs igennem de links der er vedhænngt.

## :dart: 1. Opgave Action Bar.

Nu er vi snart færdig med vores action bar.

Vi har dog lige 2 ting tilbage.

Det første er at vi indstille vores actionbar til de værdier vi ønsker som en configuration.

Kig på det object.
```javascript
let config = {
    small : 50,
    medium : 100,
    max : 150
};
```

Hvis vi indsætte dette configurations object i `devicons.js` og tildeler det som property til `DevActionBar` så kan vi bruger værdier til at sætte vores udgangspunkt.

```javascript
<DevActionBar setSizeFunction={setSize} size={size} config={config}></DevActionBar>
```

Nu kan vi tage imod vores config i `devActionBar.js`.

```javascript
const DevActionBar = ({setSizeFunction, size, config}) => {
// ---
```

og bruger værdierne hvor det giver mening `{config.small}, {config.medium}, {config.large}`

```html
<span className={styles.btn} onClick={() => setSizeFunction(config.small)}>{config.small}</span>
```

Nu kan vi med cofig opsætte forskellige settings.

Nu er vi ved afslutningen af dette komponent. Men der er ret meget her som kan bruges generelt.

Og vi kommer til at lave mange komponenter hvor dette er den oplagte "struktur".

Så kig det godt igennem. :eyes:

Men der var lige en sidste ting.

:dart: Opgave : En farverig opgave.

Indsæt denne knap i `<DevActionBar></DevActionBar>`

```html
<span className={styles.btn} >
    <input type="color" className={styles.color} onChange={(e) => console.log(e.target.value)}></input>
</span>
```

Tryk på knappen og kig i `consollen`.

Din opgave er at gøre det muligt at ændre farven på ikonerne med farve vælgeren.

:muscle: God Arbejdslyst.

### Næste skridt.

Kontakt anders@mediacollege.dk når du er nået hertil.

Du må meget gerne tilføje dit projekt til github - hvis du holder det private så inviter "McAndersC" som "collaborator".  



