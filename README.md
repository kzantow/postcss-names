# postcss-names

This package generates a file containing JavaScript-compatible identifiers based on the selector names of your CSS at the top-level and certain combinatorial levels.

For example, if you have the following CSS:
```
.Table {
    background: red;
}
.Button {
    border: 1px solid #ddd;
}
.Button-active { /* like Oxygen */
    border: 1px solid #ddd;
}
.Button.active {
    color: yellow;
}
.SomethingElse .SomeChildren {
    color: olive;
}
```

... you will get an additional file generated (`styles.js` by default) with:

```
exports.styles = {
    Table: "Table",
    Button: {
        active: "Button.active",
        toString() { return "Button" }
    }
    ButtonActive: "Button-active",
}
```

... the whole point is you can reference these styles and get code completion, for example in React, like this:

```
import { css, styles } from 'your-css-project';
...
export default (<div className={css(styles.Table, isActive && styles.ButtonActive)}> ... </div>);
```
... and as an added bonus, it generates `<filename>.d.ts` (e.g. `styles.d.ts`) for your pleasure, so you know if something changes and you're doing the wrong thing because your downstream project won't compile.