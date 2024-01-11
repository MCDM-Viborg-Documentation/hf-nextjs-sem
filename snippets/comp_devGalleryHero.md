
### `<DevGalleryHero gallery={}></DevGalleryHero>`

Tager imod `gallery={}` og udskriver navn og år.

#### :dart: Opret følgende 2 filer.

1. **File & Folder**    
:pencil: `devGalleryHero.js` :file_folder: `@components/dev/devGalleryHero/devGalleryHero.js`
```javascript
import styles from './devGalleryHero.module.css';
const DevGalleryHero = ({gallery}) => {
    return (
        <div className={styles.hero}>
            <div className={styles.content}>
                <h1>{gallery.name}</h1>
                <p>{gallery.year}</p>
            </div>
        </div>
    )
};
export default DevGalleryHero
```

2. **File & Folder**   
:pencil: `devGalleryHero.module.css` :file_folder: `@components/dev/devGalleryHero/devGalleryHero.module.css`

```css
.hero {
    background-color: red;
    width: 100%;
    height: 100%;
    aspect-ratio: 1/1;
    border-radius: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding : 20px;
}

.content h1{
    padding : 10px;
    font-size: calc(52px + 16 * ((100vw - 168px) / (768 - 568)));
}
```