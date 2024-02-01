```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : Portfoile API
Doc         : paging
```


# paging

Nu skal vi arbejde med lidt mere kompliceret data.

Åbn postman og kig på resultatet af `Get Images` - `http://localhost:3000/api/images`.

Her er et udsnit af resultatet.

```json
[
    {
        "metadata": [
            {
                "total": 81,
                "page": 1,
                "itemsPrPage": 10
            }
        ],
        "data": [
            
            // --- //

        ]
    }
]
```
Som vi kan se er der et `metadata` object. Dette objekt fortølle os at der er: 
1. `81` billeder ialt. 
2. At vi er på side `1`.
3. At hver side indeholde `10` image objekter.

Så alt i alt er der 81 billeder, men der kunne være 1000 og i denne backend er det valgt, at man får maks 10 resultater for hvert kald. Nu er det op til os at lave funktionaliteten til at håndterer dette.

Men lad os starte med at kigge på endnu et endpoint `Get Images By Page` - `http://localhost:3000/api/images?page=2`.

Nu kan vi se på `metadata` at vi er på side 2 og kigger vi i `data` array´et er objekterne nye.

### Antal sider

Nu skal vi regne ud hvor mange sider vi har ialt.
```
"metadata": [
    {
        "total": 81,
        "page": 1,
        "itemsPrPage": 10
    }
]

( total / itemsPrPage ) = ( 81/10 ) = 8.1 
```
Det betyder at vi har 9 sider i alt når vi runder op til nærmeste hele tal. Det betyder også i dette tilfælde at der kun er ét resultat på side 9. Prøv at hente data´en *(stadig bare i postman)*  - `http://localhost:3000/api/images?page=9`.

I javascript benytter vi `Math` biblioteket til at runde tal op og ned.

```Javascript
const totalPages        = Math.ceil(8.1)    //  = 9     <-- Runder op (ceiling/loft)
const almostTotalPages  = Math.floor(8.1)   //  = 8     <-- Runder ned (floor/gulv)
```
Prøv dem af i "inpsectoren/consollen" `Math.floor(8.1)` eller `Math.ceil(8.1)`


