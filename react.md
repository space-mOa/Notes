# React 🥑

- javascript framework
- může být jen pro části stránky nebo celou aplikaci
- Component-based: skoro úplně všechno je v reactu component
	- např: 
		máme webovou stránku a obsahuje: search component, directory component, singup component
- většína html je napsaná v js (in component files)-> a v JSX 
	- JSX: XML + js (dovoluje použít HTML v js)
	- pro JSX se pokaždé zavolá -> React.createElement() -> proto potřebuju naimportovat React knihovnu ```import React from 'react';```
	- JSX: např. ```const myArticle = <article></article>```nebo ```<a href = "https://www.google.com"><h1>google</h1></a>```
	- v JSX je nutné v tzv. self-closing tagů dát ```/``` např. ```<br />``` nebo ```<img />``` v HTML toto není poviné
	- všechno uvnitř JSX bude interpretován jako JSX a ne jako javascript
	- pro použití javascriptu v JSX musím kód vložit do ```{}``` 
```
ReactDOM.render(<h1>2+3</h1>, document.getElementById('app')) // Vytiskne 2 + 3
ReactDOM.render(<h1>{2+3}</h1>, document.getElementById('app')) // Vytiskne 5
```
- pokud JSX zabírá víc jak jeden řádek, musím JSX zabalit do ```()``` např.
```javascript
(
  <a href="https://www.example.com">
    <h1>
      Click me!
    </h1>
  </a>
)
```
- JSX může mít jen **jeden** nejvíce kořenový element
	* např. tento kód by nefungoval
```javascript
const paragraphs = (
  <p>I am a paragraph.</p> 
  <p>I, too, am a paragraph.</p>
);
```
- rendrovat JSX znamená, objevit se na obrazovce
- když component je required -> react je vezme a vloží je do DOMu (Document object model)

```javascript
<div id="root"></div>
	<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
	<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>	
	<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
	<script type="text/babel">
		const rootElement = document.getElementById("root")
		// Jak to udělat BEZ Reactu

		// const element = document.createElement("div")
		// element.textContent = "Ahoj"
		// element.className = "container"
		// rootElement.appendChild(element)
		
		// Jak to udělat pouze S Reactem
		// const element = React.createElement(
		// 	"div", 
		//	{className: "container"},
		// 	"Ahoj"
		// )
		// ReactDOM.render(element, rootElement)

		// Jak to udělat S Reactem a JSX
		
		// Tento řádek není syntaxe js, ale JSX 
		// Pokud se to pokusím zobrazit hodí to syntax error
		// Potřebuju to přepsat, přeložit, do podoby jako v příkladu: pouze s Reactem bez JSX
		// K tomu to přepsání, přeložení potřebuju BABEL
		// naimportuju babel
		// Přepíšu <script type="text/javascript"> na <script type="text/babel">
		const element = <div className="container">Ahoj</div>
	

		ReactDOM.render(element, rootElement)
		
	</script>
```
- JSX je bráno jako *expression*/výraz -> můžu je uložit do objektu, pole, porměnné atd.
- v HTML používáme CLASS, ale v JSX používáme className

```javascript
	// Pokud chci použít v JSX proměnné
	cosnt content = "Ahoj"
	// Pak do JSX vpíšu, použiju interpolation
	// Když použiju {} dostávám se z JSX do JS "světa" jazyku
	// Můžu tam napsat cokoliv, pokud to je expression - výraz
	const element = <div className="container">{content}</div>



	// Další příklady
	const content = ":) ahoj!"
	// 1.
	const element = <div className="container">{(() => content())}</div>

	// 2.
	const myClassName = "container"
	const element = <div className={myClassName}>{(() => content())}</div>

	// 3.
	const props = {
		className: "container",
		childern: "Ahoj",
	}
	const element = <div {...props} />

	// 4,
	const props = {
		className: "container",
		childern: "Ahoj",
	}
	// Pokud nám např. neposkytnou class name můžu definovat vlastní
	// v tomto případě mám className v props, ALE kdyby nebylo nastavíse na "moje_class"
	const element = <div className="moje_class" {...props} />
	
	// 5.
	// Pokud chci přenastavit jméno
	const props = {
		className: "container",
		childern: "Ahoj",
	}
	// Jenom dám definici className za props
	const element = <div {...props} className="moje_class"/>
		// stejně tak u children  
		const element = <div {...props} children="ahoj :)">
		// nebo 
		const element = <div {...props}>ahoj :)</div>
	// Tímhle to rendruju
	ReactDOM.render(element, rootElement)
```
- v JSX nemůžu použít ```if``` statement/podmínku
	- jeden způsob je vytvořit podmínku mimo JSX např.
	```javascript
	import React from 'react';
	import ReactDOM from 'react-dom';

	let message;

	if (user.age >= drinkingAge) {
		message = (
			<h1>
				Hey, check out this alcoholic beverage!
			</h1>
		);
	} else {
		message = (
			<h1>
				Hey, check out these earrings I got at Claire's!
			</h1>
		);
	}
	ReactDOM.render(
		message, 
		document.getElementById('app')
	);
	```
	- nebo použít termary operátor v JSX ```? :```
	```javascript
	const img = <img src={pics[coinToss() === 'heads' ? 'kitty' : 'doggy']} />;
	```
	- nebo použití ```&&``` -> kdy se buď zobrazí něco nebo vůbec nic
	```javascript
	const judgmental = Math.random() < 0.5;
  {!judgmental && <li>Nacho Cheez Straight Out The Jar</li>}
	```
### Event listeners
- stejně jako v HTML jsou v JSX event listenery 
- v HTML jsou malými písmeny např. ```onclick``` v JSX se používá camelCase ```onClick```
- vythořím ho pomocí speciálního atributu ```<img onClick = {myFunc} />```
- zpravidla slovo ```on``` + typ eventu, který poslouchám např. ```onClick``` nebo ```onMouseOver```
- event Listener by měl být funkce
## Components/komponenty
- Componenty začínají velkými písmeny
- Componenty s malými písmeny např. ```<div />```interpretuje react jako DOM tagy
- všechny Componenty musí být pure funkce nemění argumenty
- nejjednodušší způsob, jak vytvořít je js funkce
- druhý způsob je použít ```Class``` React.Component
- oba dva pohledy jsou ekvivalentní/stejné pro react
```javascript
// První způsob
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

// Druhý způsob
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

- Elementy mohou být custom vytvořené nejen HTML tagy např. ```const element = <Welcome name="Sara" />;```
- **!!!** Když react narazí na *custom-defined* element -> předá JSX atributy do tohoto Componentu - tento ```object``` se jmenuje *props*
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
- nejprve zavoláme ```ReactDOM.render()```
- react zavolá *Welcome* Componenet s *props* Sara
- zavolá se funkce *Welcome* která vrátí JSX
- ReactDOM updatuje DOM jako: ```<h1>Hello, Sara</h1>```
- Componenty mohou mít v sobě obsažené další Componenty, klidně i ty samé
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```
- *state* je něco jako *props*
	* ale je private a plně kontrolován Componentem samotným
	* pro *state* potřebuju Class z reactu, která má některé vlastnosti jako *Local state*
```javascript
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
- rendrovací metody se zavolá pokaždé, když se provede nějaký update
- přídádní stavu do Componentu
```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
```

- ```ReactDOM.render()``` -> javascriptová knihovna
	* obsahuje několik method, které pracují s DOM
	* vezme JSX expression/výraz -> vytvoří odpovídající node tree/strom -> a vloží tree/strom do DOMu -> objeví se na obrazovce
	* první argument by měl být vyhodnocen jako JSX expression/výraz
		- první argument se také objeví na obrazovce
	* druhý argument specifikuje, co kam se má JSX přidat
		- první argument -> je přídán do jakéhokoliv elementu, jenž je dán druhým argumentem
	* updatuje element, jen pokud se **změní**D

### Virtual DOM
- v reactu je pro každý DOM objekt -> virtuální DOM objekt
- je to representace DOM objektu
- je to jeho lightweight/málo náročná verze
- manipulace DOMu je pomalé, manipulace virtuálního DOMu je rychlé
- virtual DOM má vlastnosti originálního DOMu, ale **!!!** nemá možnosti změnit originální DOM (ten co vidíme na obrazovce)
- ReactDOM porovná aktuální stav virtuálního DOMu s originální a v případě odlišností aktualizuje originální, ale **!!!** pouze ty co se změnili
## Install

- nodejs + npm

## Resources: 

### web, text

[list of valid names for Event listiners](https://reactjs.org/docs/events.html#supported-events)

[github: create react app](https://github.com/facebook/create-react-app)

[react.expresss](http://www.react.express/)

[reactflux](https://www.reactiflux.com/)

[guide: front-end](https://github.com/grab/front-end-guide)

[react-redux](https://github.com/markerikson/react-redux-links)

[virtual-DOM](https://www.codecademy.com/articles/react-virtual-dom)

### youtube + videa

[YT](https://www.youtube.com/watch?v=yZ0f1Apb5CU&list=PL4cUxeGkcC9i0_2FF-WhtRIfIJ1lXlTZR&index=2&t=0s)

[REACT](https://egghead.io/lessons/react-replace-react-createelement-function-call-with-jsx)
