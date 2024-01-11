
### `<DevAuthorHero author={}></DevAuthorHero>`

Tager imod `author={}` og udskriver navn og galleri.

#### :dart: Opret følgende 2 filer.

1. **File & Folder**    
:pencil: `devAuthorHero.js` :file_folder: `@components/dev/devAuthorHero/devAuthorHero.js`
```javascript
import DevDebugJson from '../../devDebugJson/devDebugJson';
import styles from './devAuthorHero.module.css';
const DevAuthorHero = ({author}) => {
    return (
        <>
            <div className={styles.hero}>
                <div className={styles.content}>
                    <div className={styles.profile}><div>{author.author.split('')[0]}</div></div>
                    <div className={styles.text}>
                        <h2>{author.author}</h2>
                        <p>
                            {author.gallery}
                        </p>
                    </div>
                </div>
                
            </div>
            <DevDebugJson content={author}></DevDebugJson>
        </>
    )
};
export default DevAuthorHero
```

2. **File & Folder**   
:pencil: `devAuthorHero.module.css` :file_folder: `@components/dev/devAuthorHero/devAuthorHero.module.css`

```css
.hero {
    background-color: green;
    width: 100%;
    height: 100%;
    aspect-ratio: 1/1;
    border : #fff solid 6px;
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
    text-align: center;
}

.profile {
    position: relative;
}

.text {
    text-align: center;
    width: 100%;
}
.text h2{
    margin : 10px;
    font-size: calc(32px + 16 * ((100vw - 568px) / (768 - 568)));
 }
 
.text p{
    font-size: calc(22px + 16 * ((100vw - 568px) / (768 - 568)));
    color : #333;
 }

.profile {
    width : 50%;
    margin : auto;
}

.profile div {
    
    color : green;
    font-weight: 700;
    background-color: aliceblue;
    aspect-ratio: 1/1;
    width: 100%;
    border-radius: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: calc(52px + 16 * ((100vw - 568px) / (768 - 568)));
    
}

.content {
    width: 100%;
    text-align: center;
}
```