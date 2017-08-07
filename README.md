# tutorial-functional-programming
Este repositorio contiene el material explicado en el video tutorial de Functional Programming en mi Canal de YouTube https://www.youtube.com/StevenPerezAlfaro


# Functional Programming
Es un Paradigma de programación, una forma de pensar sobre como construir aplicaciones.


## Características

### Prevenir Side Effects
#### Side Effects:
- Sobre-escribir el valor de un parámetro.
- Utilizar una variable global dentro de la función directamente.
- Utilizar objetos que conllevan a procesos no referentes a la función y que utiliza recursos adicionales (consola, HTTP, LocalStorage, document).
- Llamar una función que produce Side Effects.

```javascript
let total = 0;
const numero_1 = 5;
let numero_2 = 5;

function procesar(num1, num2) {
	num1 = 10; // e_ Sobre-escribir el valor de un parámetro
	total = num1 + num2; // e_ Utilizar una variable global
	console.log('-'); // e_ Utilizar la consola involucra otros procesos no referentes a la función
	// c_ Otros: HTTP, LocalStorage, document
	return duplicar(total); // e_ Llamar una función que produce Side Effects
}

function duplicar(valor) {
	valor = valor * 2; // e_ Sobre-escribe el valor del parámetro
	return valor;
}

const resultado = procesar(numero_1, numero_2); // Esperado 20 !== Resultado 30
console.log('resultado', resultado);
console.log('numero_1', numero_1);
```

### Pure functions
Reciben los mismos inputs y devuelven siempre el valor esperado, *SIN producir Side Effects.*
```javascript
const numero_1 = 5;
const numero_2 = 5;

function proceso(num1, num2) {
	return (num1 + num2) * 2;
}
const resultado = proceso(numero_1, numero_2); // Esperado 20 === Resultado 20
console.log(resultado);
```

### Evitar estados compartidos
Ejemplo donde necesitamos crear las funciones obtenerImpuesto y aumentoSalario de un colaborador.

```javascript
const persona = {
	nombre: 'John',
	salario: 100,
};

console.log('persona', persona);

function obtenerImpuesto(salario, porcentaje) {
	return salario * (porcentaje / 100);
}

function aumentoSalario(salario, porcentaje) {
	return salario * (porcentaje / 100);
}

const impuesto = obtenerImpuesto(persona.salario, 10);
const aumento = aumentoSalario(persona.salario, 50);

console.log('impuesto', impuesto);
console.log('aumento', aumento);
console.log('persona', persona);
```
### FP es Declarativo - No Imperativo

#### Declarativo: Es abstracto, no tiene un flujo definido y se compone de múltiples piezas re-utilizables.
```javascript
const cuadradoMap = numeros => numeros.map(n => n * 2);
const resultado = cuadradoMap([2, 3, 4]);
console.log('cuadradoMap', resultado); // [4, 6, 8]
```

#### Imperativo: Se muestra el paso a paso por medio de líneas de código.
```javascript
const cuadradoMap2 = numeros => {
	const cuadrado = [];
	for (let i = 0; i < numeros.length; i++) {
		cuadrado.push(numeros[i] * 2);
	}
	return cuadrado;
};

const resultado2 = cuadradoMap2([2, 3, 4]);
console.log('cuadradoMap2', resultado2); // [4, 6, 8]
```

### Composición
f(g(x)) = Las funciones se resuelven de adentro hacia afuera, de derecha a izquierda.

```javascript
const sumar = (x, sum) => x + sum;
const restar = (x, res) => x - res;
const multiplicar = (x, mul) => x * mul;

const num = 10;
const resultado = multiplicar(restar(sumar(num, 10), 5), 2);

console.log('resultado', resultado); // 30
console.log('num', num); // 10
```

### High Order Functions
Función q toma una ó mas funciones como argumentos y retorna una función como su resultado.
```javascript
// Composition + High Order Functions

// Jugando con Pipes
const pipe = (...funs) => init => funs.reduce((acc, fun) => fun(acc), init); // c_ HOF

const resultado2 = pipe(
	x => sumar(x, 10),
	x => restar(x, 5),
	x => multiplicar(x, 2)
)(num); // num = 10

console.log('resultado2', resultado2); // 30
console.log('num', num); // 10
```


## Como resultado obtenemos soluciones:

- Consisas.
- Predecibles.
- Faciles de testear.

<br/>
<br/>
Fuente sobre conceptos:
Eric Elliott
https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0
