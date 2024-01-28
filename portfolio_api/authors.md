# Media College

```
Author      : Media College
Department  : WEB 
Year        : 2024 
Description : Portfoile API
Doc         : authors
```

# Indledning.

Så er det opgave tid.


## Opgave
Nu skal du oprette en underside og et par komponenter.

### 1. AuthorsCollection Component.

1. Opret en underside :file_folder: `authors`.
2. Opret et **AuthorsCollection** Client Komponent.
2. Hent og udskriv alle Authors  ved hjælp af `<DebugJson data={}>` komponentet (*som i client component*).      
Endpoint:`Get Authors` *(se postman)*

### 2. AuthorImages Component.

1. Opret et **AuthorImages** Client Komponent.
2. Komponentet skal hente alle billeder for en author, via navnet.
3. Det skal være muligt at sætte `<AuthorImages name={'Lena Riss'}></AuthorImages>` attribut.
Endpoint:`Get Images By Author` *(se postman)*

### 3. Indsæt

1. Indsæt én author på forsiden, du vælger selv hviklen.
2. Indsæt din AuthorImages komponent i AuthorsCollection komponentet. 