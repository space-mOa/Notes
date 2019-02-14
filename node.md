# node .js 🦇

- oproti javascriptu, kde jsou všechny objekty, funkce, proměnné dány do -> **window objektu**
```javascript
var zprava = 'Ahoj'
// Vypise: Ahoj 
console.log(window.zprava)
// Vypise: Ahoj
window.console.log(window.zprava)
```
- node má **global**
  * node používá V8 runtime pro javascript, který je zabalený v aplikaci, jenž je napsaná v C++
  * oproti javascriptu v prohlížeči nelze udělat 

```javascript
var zprava = 'Ahoj'
// Vypise: Ahoj
global.console.log(zprava)
// Vypise: undefiend
// proměnné nejsou pod global
console.log(global.zprava)
```
- funkce, proměnné a objekty, které definuju **!!!** nejsou ve window jako u javascriptu v prohlížeči 
- node používá moduly
  * modul = soubor 
  * prázdný modul je jen objekt ve formátu JSON
- funkce a proměnné jsou, co vytvořím v modulu/souboru jsou dostupné jen v tomto modulu a ne v jiném
- node nespouští kód v souborech jako takových, ale **!!!** zabalí je do funkce **module wraper function**

```javascript
(function (exports, require, module, __filename, __dirname) {
	let url = 'url'
})
```

## Moduly

- pro exportování modulů -> mého/cizího
```javascript
module.exports.log = log
module.exports.endPoint = url
```
- pro importování modulů
  * require funkce je jen v node 
  * lepší používat ```const``` pro moduly -> nechceme změnit obsah objektu v loggeru

```javascript
const logger = require('./sub_folder/logger')
console.log(logger.log('zprava')
```

## Primitivní data typy

``` null``` - reprezentuje úmyslně chybějící hodnotu

``` undefined``` - reprezentuje chybějící hodnotu, ale má jiné použití 

``` object``` - kolekce dat,
  * javascript má několik objektů už v sobě např. **Math**

```javascript
// Deklarace objektu
let spaceship = {};
```	
- pomocí ``` .``` **dot operátoru** získám hodnotu z objektu ```spaceship.homeplanet```
- pomocí **bracket notation** získám hodnotu z objektu 

```javascript
let spaceship = {
  'Fuel Type': 'Turbo Fuel',
  'Active Duty': true,
  homePlanet: 'Earth',
  numCrew: 5
};
// Vrátí: undefined
spaceship['homeplanet']
// Vrátí: Trubo Fuel
spaceship['Fuel Type']
```

- objekty jsou vkládány jako reference **pass by reference** -> pc interpretuje paramter ve funkci jako ukazatel do paměti, kde je uložen objekt
- data jsou organizována do **key** a **value** párů

![objekt](https://s3.amazonaws.com/codecademy-content/courses/learn-javascript-objects/objectliteraldiagram.svg)
- objekt je mutable
- můžu přidávat další pole po deklaraci

```javascript
const spaceship = {type: 'shuttle'};
spaceship = {type: 'alien'}; // TypeError: Assignment to constant variable.
spaceship.type = 'alien'; // Změní type hodnotu
spaceship.speed = 'Mach 5'; // Vytvoří nový klíč 'speed' s hodnotou 'Mach 5'
```
- vymazání hodnoty pomocí: ```delete``` např: ```delete spaceship['Secret Mission'];```

```javascript
// Nested/více ůrovňové objekty
const spaceship = {
     telescope: {
        yearBuilt: 2018,
        model: '91031-XLT',
        focalLength: 2032 
     },
    crew: {
        captain: { 
            name: 'Sandra', 
            degree: 'Computer Engineering', 
            encourageTeam() { console.log('We got this!') } 
         }
    },
    engine: {
        model: 'Nimbus2000'
     },
     nanoelectronics: {
         computer: {
            terabytes: 100,
            monitors: 'HD'
         },
        'back-up': {
           battery: 'Lithium',
           terabytes: 50
         }
    }
```

- Loopování přes object

```javascript
let spaceship = {
    crew: {
    captain: { 
        name: 'Lily', 
        degree: 'Computer Engineering', 
        cheerTeam() { console.log('You got this!') } 
        },
    'chief officer': { 
        name: 'Dan', 
        degree: 'Aerospace Engineering', 
        agree() { console.log('I agree, captain!') } 
        },
    medic: { 
        name: 'Clementine', 
        degree: 'Physics', 
        announce() { console.log(`Jets on!`) } },
    translator: {
        name: 'Shauna', 
        degree: 'Conservation Science', 
        powerFuel() { console.log('The tank is full!') } 
        }
    }
}; 
// for...in
for (let crewMember in spaceship.crew) {
  console.log(`${crewMember}: ${spaceship.crew[crewMember].name}`)
};
```

- Pokud chci použít pří deklaraci medoty v objektu, některé definované ```key``` a 
```value``` páry musím použít ```this```

```javascript
const robot = {
  model: '1E78V2',
  energyLevel: 100,
  provideInfo() { 
    return `I am ${this.model} and my current energy level is ${this.energyLevel}.`
  }
};
console.log(robot.provideInfo());
```

- V případě **arrow funkce** **!!!** nesmím použít vůbec v těle funkce ```this``` 
```javascript
const goat = {
  dietType: 'herbivore',
  makeSound(){
    console.log('baaa');
  },
  diet: () => {
    console.log(this.dietType)
  }
};

goat.diet(); // Vytiskne undefined
```
- Pokud chci, aby se nějaká hodnota neměnila v objektu použiju ```_``` před jménem **!!!** je to jen konvence

```javascript
const bankAccount = {
  _amount: 1000
}
```

- Getters a Setters: metody pro bezpežné vkládání nebo získávání hodnot do objektů
- Gettery a Settery nemohou používat stejné jméno jako vlastnosti objektu
- Pro Gettter použiju ```get```

```javascript 
const person = {
  _firstName: 'John',
  _lastName: 'Doe',
  get fullName() {
    if (this._firstName && this._lastName){
      return `${this._firstName} ${this._lastName}`;
    } else {
      return 'Missing a first name or a last name.';
    }
  }
}

// To call the getter method: 
person.fullName; // 'John Doe'
```

- Setter nastavují hodnotu, již existujícím vlastnostem
  * Můžu např. zkontrolovat hodnotu, která má změnit hodnotu vlastnosti

```javascript
const person = {
  _age: 37,
  set age(newAge){
    if (typeof newAge === 'number'){
      this._age = newAge;
    } else {
      console.log('You must assign a number to age');
    }
  }
};

person.age = 40;
console.log(person._age); // Logs: 40
person.age = '40'; // Logs: You must assign a number to age
```

- **Factory funkce:** pokud potřebuju vytvořit několik ```object```/objektů

```javascript
const monsterFactory = (name, age, energySource, catchPhrase) => {
  return { 
    name: name,
    age: age, 
    energySource: energySource,
    scare() {
      console.log(catchPhrase);
    } 
  }
};
const ghost = monsterFactory('Ghouly', 251, 'ectoplasm', 'BOO!');
ghost.scare(); // 'BOO!'

// Lze využít destructirualizace pro kratší zápis
const monsterFactory = (name, age) => {
  return { 
    name,
    age,
	beep() {
      console.log('Beep Boop');
    }
  }
};
```

``` Symbol``` - jedinečný identifikátor

``` String``` - řetězec znaků např. a, b, @
pokud chci vytisknout ```'``` -> použiju ```\'``` např: ```console.log('It\'s winter! Everything is covered in snow.')```

**Některé metody:**
```javascript 
console.log('Hello'.length) 		     // Vytiskne: 5
console.log('Hello'.toUpperCase())   // Vytiskne: HELLO
console.log('Hello'.startsWith('H')) // Vytiskne: true
console.log('   Hello   '.trim()) 	 // Vytiskne: 'Hello'
```

**Využití String literálů:**
- umožňuje vložit/interpolate proměnné do ```String``` pomocí *template literals*
- template literal je zabalen pomocí ``` `` ``` a proměnná je vložena do ```${}```

```javascript
const myPet = 'kapustnak'
console.log(`I own a pet ${myPet}.`); // Vytiskne: I own a pet kapustnak.
```

další: ```Number, Boolean```

**Pro zjištění jaký datový typ je proměnná:** ```console.log(typeof(variable))```

**Spojení/concatenation Stringů:** 
- Můžu spojovat ```Stringy``` pomocí operátoru ```+```

```javascript
console.log('wo' + 'ah'); // Vytiskne: 'woah'
```
- Pokud se pokusím spojit String a Number -> vznikne String

## Array
- položku mohu dostat: ```['A', 'B', 'C'][0] // Dostanu A```

## Operátor

*operator* - character/znak, který vykonná úlohu v kódu
+, -, *, /, %: modulo = zbytek, .: **dot operátor**

porovnávací: <, >, <=, >=, a ===: **identify operátor**
logické: &&, ||

## Kód

komentáře: ```/* */```, ```//```

## Způsoby deklarování proměnné

Pokud deklaruju proměnnou pomocí ```let``` a ```var``` s nepřiřazenou hodnotou např. ``` let variable;``` bude hodnota nastavena jako ```undefined```

```let``` - proměnné může být přiřazena jiná hodnota

```const``` - konstanta, která může mutovat, ale nemůže být přiřazena nová či jiná hodnota 

```undefined``` - když, deklaruju proměnnou bez hodnoty

- Lze přiřadit funkci do proměnné -> proměnná drží **reference** k funkci

**short-circuit evaluation:** ```let defaultName = username || 'Stranger';```, protože je nejprve zkontrolován username tak -> se vybere username pokud není **Falsy** přiřadí se hodnota z variable username **!!!** pokud ne přiřadí se do defaultName 'Stranger'

- Destructuring: stejně jako factory function nám pomáhají vytvářet 
 * proměnná je zabalena do ```{ }```
 * Můžeme používat takto i objekty celé
```javascript
const vampire = {
  name: 'Dracula',
  residence: 'Transylvania',
  preferences: {
    day: 'stay inside',
    night: 'satisfy appetite'
  }
};
// První způsob
// Vytiskne: Transylvania
const residence = vampire.residence
console.log(residence)
// Pomocí destructuring
// Vytiskne: Transylvania
const { residence } = vampire
console.log(residence)
// Celý objekt
const { upir } = vampire
// Vytvoření nového objektu pomoci Object 
const novyUpir = Object.keys(upir)

```
## Funkce

![funkce](https://s3.amazonaws.com/codecademy-content/courses/learn-javascript-functions/Diagram/declaration.svg)

![identifier](https://s3.amazonaws.com/codecademy-content/courses/learn-javascript-functions/Diagram/name.svg)

![parametry](https://s3.amazonaws.com/codecademy-content/courses/learn-javascript-functions/Diagram/function+parameters.svg)

![identifier a argumenty](https://s3.amazonaws.com/codecademy-content/courses/learn-javascript-functions/Diagram/by_variable.svg)

![return](https://s3.amazonaws.com/codecademy-content/courses/learn-javascript-functions/Diagram/function+return.svg)

anonymní funkce: 

![anonymní funkce](https://s3.amazonaws.com/codecademy-content/courses/learn-javascript-functions/Diagram/expression.svg)

arrow funkce: 

![arrow funkce](https://s3.amazonaws.com/codecademy-content/courses/learn-javascript-functions/Diagram/parameters.svg)
- funkce jsou *First class OBJECTS*
- jsou brány jako datový typ
- je to object
- má **vlastnosti** a **metody**
- **anonymní funkce:** nemůžou být zavolány, před deklarací narozdíl od fuknci definovaných pomocí ```function``` (zavolání před deklarací se nazývá **hoisting**)
- **callback funkce:** takové funkce, které jsou dány jako parametry do další funkce a jsou vyhodnoceny během vyhodnocování **higher-order** funkce
	* pokud dáváme funkci jako parametr, tak jí nevoláme, ale dáváme do parametru funkci jako takovou
	* do parametru ji dáváme bez ```()``` -> jinak by se vyhodnotila
	* anonymní funkce mohou být parametry další funkce
```javascript
const timeFuncRuntime = funcParametr => {
	let t1 = Date.now()
	funcParametr()
	let t2 = Date.now()
	return t2 - t1;
}
const addOneToOne = () = 1 + 1
timeFuncRuntime(addOneToOne);
// Anonymní funkce jako parametr
timeFuncRuntime(() => {
		for	(let i = 10; i > 0; i--){
			conosle.log(;)
		}
	});


// Další příklad:
const checkThatTwoPlusTwoEqualsFourAMillionTimes = () => {
  for(let i = 1; i <= 1000000; i++) {
    if ( (2 + 2) != 4) {
      console.log('Something has gone very wrong :( ');
    }
  }
};

const addTwo = num => num + 2;

const timeFuncRuntime = funcParameter => {
  let t1 = Date.now();
  funcParameter();
  let t2 = Date.now();
  return t2 - t1;
};

const time2p2 = timeFuncRuntime(checkThatTwoPlusTwoEqualsFourAMillionTimes);

const checkConsistentOutput = (func, val) => {
    let firstTry = func(val);
    let secondTry = func(val);
    if (firstTry === secondTry) {
        return firstTry
    } else {
        return 'This function returned inconsistent results'
    }
};

checkConsistentOutput(addTwo, 10);
```

- arrow funkce, použíavjí syntaxi **fat arrow** ```() =>``` 
	- pokud arrow funkce nebere žádny parametr musí být dány ```()```
	- pokud je arrow funkce na jednom řádku nepotřebuju ```return```
```javascript 
const rectangleArea = (width, height) => {
	let area = width * height;
	return area
}

// Vrátí vypočítanou hodnotu num 
const squareNum = num => num * num;
// Další příklad
const plantNeedsWater = day => day === 'Wednesday' ? true : false;

```

**Default parametry:**
```javascript 

function greeting(name = 'stranger') {
	console.log(`Hello, ${name}`)
}
greeting('Nick') // Vytiskne: Hello, Nick
greeting() 		 // Vytiskne: Hello, stranger
```

**Příklad jak přiřadit jméno funkci:**
```javascript
const checkThatTwoPlusTwoEqualsFourAMillionTimes = () => {
  for(let i = 1; i <= 1000000; i++) {
    if ( (2 + 2) != 4) {
      console.log('Something has gone very wrong :( ');
    }
  }
};

const is2p2 = checkThatTwoPlusTwoEqualsFourAMillionTimes;
is2p2();
console.log(is2p2.name);
```


## Větvení, rozhodování

if: pokud je ```true``` provede se
```javascript
// Vytiskne: ahoj
if (true) {
	console.log("ahoj")
}

// Vytiskne: ahoj
let bool = true
if (bool) {
	console.log("ahoj")
}

```
Truthy a Falsy: např. pokud mám proměnnou, ve které je ```String``` tak se větev if provede, ikdyž není typ ```Boolean```
Falsy hodnotu mají: **prázdné Stringy** ```''``` nebo ```""```, ```0```, ```null```, ```undefined```, ```NaN```: Not a Number/ není číslo
```javascript
// Vytiskne: I exist!
let myVariable = 'I exist!'
if (myVariable) {
	console.log(myVariable)
} else {
	console.log('The variable does not exist!')
}
```
**termary operator:** zjednodušuje zapisování ```if..else``` statemantů 
- podmínka je dána před ```?```
- expression jsou násladovány za ```?``` a ```:```
- pokud je podmínka ```true``` první expression/výraz se vyhodnotí/zvolí
- pokud je podmínka ```false``` druhá expression/výraz se vyhodnotí/zvolí
```javascript
// Vytiskne: You will not need a key to open the door.
let isLocked = false;
isLocked ? console.log('You will need a key to open the door.') : console.log('You will not need a key to open the door.');

// Vytiskne: I love that!
let favoritePhrase = 'Love That!';
favoritePhrase === 'Love That!' ? console.log('I love that!')  : console.log("I don't love that!");
```

Switch

```javascript
// Vypíše Jiná barva
let color = "blue"
switch (color) {
	case "white":
		console.log('white')
		break
	default:
		console.log('Jiná barva')
		break
}
```

## Metody 

Deklarace metody na objektu
```javascript
// První způsob deklarace
const alienShip = {
  invade: function () { 
    console.log('Hello! We have come to dominate your planet. Instead of Earth, it shall be called New Xaculon.')
  }
};
// Druhý způsob deklarace
const alienShip = {
  invade () { 
    console.log('Hello! We have come to dominate your planet. Instead of Earth, it shall be called New Xaculon.')
  }
};
```

## Iterátory
Provádí se na Array/poli: 
- ```.forEach()```
- ```.map()```
	- vratí **nový** array 
- ```filter()```
	- vrátí **nový** array
	- callback funkce -> musí vracet ```true``` nebo ```false```
	- elementy, díky kterému se vyhodnotí callback funkce jako ```true``` -> se přidají do nového Arreye/pole
```javascript
// Vypíše: [ 200, 3.14, 7, 13 ]
const randomNumbers = [375, 200, 3.14, 7, 13, 852];
const smallNumbers = randomNumbers.filter(number => number < 250)
console.log(smallNumbers)
```
- ```.findIndex()``` 
	- najde najde lokaci elementu v Arreyi/poli
	- vrátí array s indexi, prvků -> které byly vyhodnoceny pomocí podminky
```javascript
// startsWiths vrátí: 3
const animals = ['hippo', 'tiger', 'lion', 'seal', 'cheetah', 'monkey', 'salamander', 'elephant'];
const startsWithS = animals.findIndex(animal => {
  return animal[0] === 's' ? true : false;
});
```
- ```.reduce()```
	- vrátí jednu hodnotu **!!!** ne Arrey/pole 
```javascript
// Vytiskne: 17
// accumulator je první hodnota v Arreyi/poli a currentValue je druhá hodnota v Arreyi/poli
const numbers = [1, 2, 4, 10];
const summedNums = numbers.reduce((accumulator, currentValue) => {
  return accumulator + currentValue
})
console.log(summedNums)

// Vrátí: 
/* 
The value of accumulator:  10
The value of currentValue:  1
The value of accumulator:  11
The value of currentValue:  3
The value of accumulator:  14
The value of currentValue:  5
The value of accumulator:  19
The value of currentValue:  7
26
*/
const newNumbers = [1, 3, 5, 7];
const newSum = newNumbers.reduce((accumulator, currentValue) => {
  console.log('The value of accumulator: ', accumulator);
  console.log('The value of currentValue: ', currentValue);
  return accumulator + currentValue;
}, 10);
console.log(newSum);
```

## Class/Třídy 
- Jsou to **Templates/vzory** pro objekty
- Pro definovíné jak vytvořit novou instanci třídy používáme constructory
```javascript
class Dog {
  constructor(name) {
    this._name = name;
    this._behavior = 0;
  }

  get name() {
    return this._name;
  }
  get behavior() {
    return this._behavior;
  }   

  incrementBehavior() {
    this._behavior ++;
  }
}
```
- nová instance třídy ``` const halley = new Dog('Halley')```
 * ```new``` zavolá constructor třídy např. Dog 
- narozdíl od objektu nejsou metody oddělené ```,``` a ```_``` indikuje, že by vlastnost neměla být přímo dostupná

### Inheritance/Dědičnost
- ```extend``` -> zpřístupňuje metody, které jsou ve vyšší třídě např: Animal
- ```super``` -> zavolá **constructor** vyšší třídy např: Animal
 * předá argument z Classy/Třídy do Higher Class/Vyšší třídy např. Cat do Animal -> do **constructoru** Higher Class/Vyšší Třídy např. Cat do Animal
 * vždy volám ```super``` před ```this```
```javascript
class Cat extends Animal {
  constructor(name, usesLitter) {
    super(name);
    this._usesLitter = usesLitter;
  }
}
```
- ```static``` -> umožňuje určit metody které se nebudou dědit do Child Classy/ Nižších tříd
 * pro zavolaní ```static``` metody musím použít jejich původní třídu, nelze zavolat na instanci
```javascript
class Animal {
  constructor(name) {
    this._name = name;
    this._behavior = 0;
  }

  static generateName() {
    const names = ['Angel', 'Spike', 'Buffy', 'Willow', 'Tara'];
    const randomNumber = Math.floor(Math.random()*5);
    return names[randomNumber];
  }
}
```


## Moduly v javascriptu
- umožňují nám dostat přístup k např: objektům, funkcí, proměnných z jiných souborů
```javascript
const Airplane = {};
Airplane.myAirplane = "StarJet";

module.exports = Airplane;
```
- pomocí ```require()``` získám přístup k např: objektům, funkcím, proměnných z jiných souborů 
```javascript
const Menu = require('./menu.js');

function placeOrder() {
  console.log('My order is: ' + Menu.specialty);
}

placeOrder();
```
## Podpora verzí javascriptu v prohlížečích
[!verze](https://caniuse.com/)



[js concepts ](https://github.com/leonardomso/33-js-concepts)

## Handbook
[handbook javascriptu](https://jshandbook.com/)