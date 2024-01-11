
### `<DevDebugJson content={}></DevDebugJson>`

Tager imod `content={}` iform af et `javascipt object` og udskriver det i en `Accordion` element.

#### :dart: Opret følgende 2 filer.

1. **File & Folder**    
:pencil: `devDebugJson.js` :file_folder: `@components/dev/devDebugJson/devDebugJson.js`
```javascript
'use client';
import { useState } from "react";
import styles from "./devDebugJson.module.css"
import { 
    FaChevronUp,
    FaChevronDown 
} from "react-icons/fa";

// Client Component.
const DevDebugJson = ({ content }) => {

    // State.
    const [active, setActive] = useState(false);

    // Benytter en ternary operator for at sætte Icon efter active true/false.
    let icon = active ? <FaChevronUp  /> :  <FaChevronDown />;
    
    // Benytter en ternary operator for at sætte Style efter active true/false.
    let style = active ? styles.active : '';

    // Template (benytter style, icon og content variablerne).
    return <div className={`${styles.container} ${style}`}>
        <div className={styles.handle} onClick={() => setActive(!active)}>
            {icon} Print Json
        </div>
        <pre className={styles.content}>
            {JSON.stringify(content, null, 2)}
        </pre>
    </div>

};

// Default Export.
export default DevDebugJson;
```

2. **File & Folder**   
:pencil: `devDebugJson.module.css` :file_folder: `@components/dev/devDebugJson/devDebugJson.module.css`

```css
/* 
    Hvis container har active klasse "display´er"/viser vi content.
    display: block;
*/
.container.active .content {
    display: block;
}

.handle {
    display: flex;
    justify-content: left;
    align-items: center;
    background-color: #111;
    padding: 10px;
    user-select: none;
    cursor: pointer;
}

.handle:hover {
    color: #fff;
    background-color: #222;
}

.handle svg{ 
    width : 20px;
    height : 20px;
    margin-right: 10px;
}

/* 
    Hvis container ikke har active stadie viser vi ikke content.
    display: none; 
*/
.content {
    display: none;
    padding: 10px;
    background-color: #fff;
    color: #000;
    font-size: 11px;
    overflow-x: auto;
}
```