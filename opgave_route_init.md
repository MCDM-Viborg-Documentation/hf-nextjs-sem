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

`Linking and navigation` : https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating

