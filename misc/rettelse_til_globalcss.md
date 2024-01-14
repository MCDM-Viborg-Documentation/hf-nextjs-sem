# Rettelse til jeres /app/globals.css

:bulb:  Efter første gennemgang af løsninger er der en rettelse til selve projektet.

Erstat **ALT** indhold i filen med dette:

*Skulle i selv have oprettet classer skal i selvfølgelig gemme den dem. ALT andet skal udskiftes.*


```css
:root {

  /* Global Variables */
  --main-color: lightblue;

  /* Component Specific Variables */
  --box-color: #fff;

  /* Navigation */
  --navigation-background-color: rgb(0, 0, 0);
  --navigation-logo-background-color: rgb(255, 255, 255);
  --navigation-color: rgb(255, 255, 255);
}


@media (prefers-color-scheme: dark) {

  :root {
    
    /* Global Variables */
    --main-color: #333;


    /* Component Specific Variables */
    --box-color: rgb(235, 235, 160);

    /* Navigation */
    --navigation-background-color: rgb(235, 235, 160);
    --navigation-logo-background-color: rgb(255, 255, 255);
    --navigation-color: rgb(0, 0, 0);
  }

}

* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

html,
body {
  background-color: var(--main-color);
  height: 100%;
}

body {
  background-color: var(--main-color);
}

a {
  color: inherit;
  text-decoration: underline;
}



@media (prefers-color-scheme: dark) {
  html {
    color-scheme: dark;
  }
}
```