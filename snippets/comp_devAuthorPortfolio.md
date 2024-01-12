
### `<DevAuthorPortfolio author={}></DevAuthorPortfolio>`

Tager imod `author={}` og udskriver og henter selv sine billeder.

:bulb: Bemærk hvordan komponent selv kalder `fetchImagesForAuthor(author.author)`. Det er altid svært at afgøre hvor, hvrdan og hvornpr man skal hente sin data. Det handler meget om * formålet*.

Vi sikre at vi kun henter de billeder der er nødvendige for at vise én portfolio. Hvis vores brugerer kun besøger én portflio, så har vi ikke hentet for meget og brugt unødig trafik. (*data-trafik = penge / dollars / pesetos, monéter* :eyes:).

#### :dart: Opret følgende 2 filer.

1. **File & Folder**    
:pencil: `devAuthorPortfolio.js` :file_folder: `@components/dev/devAuthorPortfolio/devAuthorPortfolio.js`
```javascript
import { fetchImagesForAuthor } from '@/lib/data.service';
import styles from './devAuthorPortfolio.module.css';
import DevGalleryImage from '../devGalleryImage/devGalleryImage';

const DevAuthorPortfolio = async ({author}) => {

    const images = await fetchImagesForAuthor(author.author);
    
    return (
        <div className={styles.container}>
            <h1>{author.author}</h1>
            <div className={styles.portfolios}>
                {images.map((image, index) => {
                    return <div className={styles.portfolio} key={index}>
                        <DevGalleryImage image={image} showMeta={false}></DevGalleryImage>
                    </div>
                })}
            </div>
        </div>
    )
};
export default DevAuthorPortfolio
```

2. **File & Folder**   
:pencil: `devGalleryImage.module.css` :file_folder: `@components/dev/devAuthorPortfolio/devAuthorPortfolio.module.css`

```css
.container {
    border : 2px white solid;
    padding : 20px;
    width: 100%;
}

.portfolios {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    width: 100%;

}

.portfolio {
    width : 25%;
}
```