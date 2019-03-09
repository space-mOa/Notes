# icons 


# CSS a SASS

```css
@import url("");
```

## SASS
je preprocessor -> umožňuje generovat CSS, na základě preprocessorově vlastní styntaxe
přidává např. proměnné, nestování, dědičnost atd.
[SASS_tutorial](https://gist.github.com/blackfalcon/5480118)

## Class, ID

id - pro to co se objevuje pouze jednou
```css

#id {

}
```

proto ce se objevuje více, např. několik divu ve stejné třídě/class
```css
.class {

}
```

## CSS grid
```css
display: grid;	
```

## CSS propety

### Pozicování elementů

osy: x, y, z-index -> "hloubka, 3d, vrstvy"
z-index -> ovlivňuje rendrování elementů -> protože elementy mají nastavené properties/vlastnosti, které následně vyvolají vytvoření: _stacking context_ 

__position:__

nastaví pozici elementů např. div

postion: static | relative | absolute | sticky;

```css
position: static;	/* element je pozicován normálně, jak by byl, vlastnosti jako: right, bottom, left a z-index nemají efekt */
position: relative;	/* relativní vůči elementu ve kterém je */
position: absolute;	/* pozice je dána bez ohledu, kde se nachází, např. není ovlivněn rodičovským divem, It means that the position of an element with that property will not affect the position of other 
elements, and will not be affected by their position either. Assigning the position: absolute property to all elements by default will ensure they will all be independent from each other  */
position: sticky; 	/* element zůstane na pozici svojí, ikdyž budeme scrollovat*/
```

__top, left__

nastaví pozici elementu vůči jeho rodiči

```css
top: 10px;
left: 50%;
```

### Obsah elementů

__owerflow:__

Co se má stát s obsahem jestli, přesáhne velikost

owerflow: visible | hidden | scroll | auto;
```css
overflow: visible; /* content is not clipped */ 
overflow: hidden; /* no scrollbars are provided */ 
overflow: scroll; /* always show scrollbars */
overflow: auto; /* append scrollbars if necessary */ 
```

### Transformace elementů
__translate:__

Umožňuje zešikmit, roztáhnout nebo zmenšit, přetočit, či nastavit pozici elementu
[mozilla](https://developer.mozilla.org/en-US/docs/Web/CSS/transform) 

__border-radius:__
zakulatí rohy
```css
border-radius: 50%; /* udělá kolečko */
```


Pro restartování animací !!!
https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetWidth
https://css-tricks.com/restart-css-animation/
