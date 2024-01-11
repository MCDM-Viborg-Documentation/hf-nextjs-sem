
### `<DevGalleryImage image={}></DevGalleryImage>`

Tager imod `image={}` og udskriver billede med mere..

#### :dart: Opret følgende 2 filer.

1. **File & Folder**    
:pencil: `devGalleryImage.js` :file_folder: `@components/dev/devGalleryImage/devGalleryImage.js`
```javascript
import Image from 'next/image';
import DevDebugJson from '../../devDebugJson/devDebugJson';
import styles from './devGalleryImage.module.css';
const DevGalleryImage = ({image}) => {
    return (
        <>
            <img src={image.path} alt={`Portfolio billede taget af ${image.author} udstillet i falleriet ${image.gallery}`} className={styles.image} />
            
            <DevDebugJson content={image}></DevDebugJson>
        </>
    )
};
export default DevGalleryImage

```

2. **File & Folder**   
:pencil: `devGalleryImage.module.css` :file_folder: `@components/dev/devGalleryImage/devGalleryImage.module.css`

```css
.image {
    object-fit: contain;
    width: 100%;
    height: 100%;
    border : 10px #fff solid;
}
```