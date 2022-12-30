# Σημειώσεις στην CSS
## Περιεχόμενα
1. [CSS Selectors](#css-selectors)
2. [CSS Grid](#css-grid)
## CSS Selectors
--------------------------------
[MDN Reference for CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
### 1. Basic selectors
#### - Universal Selector
Συμβολίζετε ώς `*` και επιλέγει *όλα* τα στοιχεία:
```css
/* Selects all elements */
* {
  color: green;
}
```
[MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Universal_selectors)
####  - Type Selector
```css
header {
    color: red;
}
```
[MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Type_selectors)

####  - Class Selector
Επιλέγει τα στοιχεία μιας κλάσσης
```css
.my-class-name {
    color: red;
}
```
[MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors)

#### - ID Selector
Επιλέγει ένα στοιχείο με βάση το id του:
```css
#my-id {
    color: red;
}
```
[MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/ID_selectors)

#### - Attribute Selector
Επιλέγει τα στοιχεία που έχουν αυτό το attribute:
```css
[attribute] {
    color: red;
}
```
[MDN Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)

## CSS Grid
[MDN Reference for CSS GRID](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Grids)
```css
/* Small Screen */
body {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-areas:
        "head"
        "main"
        "news"
        "info"
        "foot";
}
/* Medium screens */
@media all and (min-width: 600px) {
    body {
        grid-template-columns: 1fr 2fr;
        grid-template-areas:
            "head head"
            "aside main"
            "foot foot";
    }

/* Large screens */
@media all and (min-width: 800px) {
    body {
        grid-template-columns: 1fr 4fr 1fr;
        grid-template-areas:
            "head head head"
            "aside main main"
            "aside main main"
            "foot foot foot";
    }

    /* Styling */
    header {
        height: 10vh;
    }
    aside {
        height: 80vh;
    }
    main {
        height: 80vh;
    }
    footer {
        height: 20vh;
    }
}
```