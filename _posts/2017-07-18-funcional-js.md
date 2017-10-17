---
layout: post
title:  "Javascript - Capitulo 1, Passando pelo funcional"
date:   2017-07-18 12::3 -0300
categories: blog
---

## Principios básicos de Javascript

#### Como na matematica uma funcao é denotada quando está entre parentese
f(x) = y  // uma funcao pode ter um, dois ou nnenhum parametros 

#### Na matematica usamos a uncao acimo como essa abaixo
x + y //

#### E para criar uma funcao para adicionar qualquer numero que entrar fazemos assim
y = x + 2

#### Para criar essa mesma funcao no javascript fazemos da seguinte maneira 
const f = x + y  //Onde (f) é o nome que damos a funcao, esta correto mas falta o parentese para valor de X entrar

#### Para criar uma funcao no JS, damos o nome F", e passamos o parametro que vamos definir ( x ) e atribundo o "igual" =>
const f = ( x ) => x + 2 // E aqui falamos que o resultado dessa funcao eh X + 2

### Definimos uma constante, o "F" é uma variavel que nao pode ser mudadai, se quiser mudar use o "Let"
$ const f = ( x ) => x + 2 

#### Passndo os valores correspondentes
$ f(2) 
4

#### Criamos a nossa constante  add, e etribuimos à funcao de( x, y ) que soma x + y
const add = ( x, y ) => x + y

#### Testando a funcao no terminal do node.js
$ add (3, 5)
8

## Agora vamos fazer qualquer operação matemática usando apenas adição e subtração

#### Primeiro criamos uma funcao que retorna o x - y
$ const subtract  = ( x, y ) => x - y

#### Testando a nova funcao no terminal do node.JS
$ subtract ( 5, 3 ) 
2

#### E tabem podemos fazer com + -y que retorna a negação dos sinais.
$ const _subtract  = ( x, y ) => x + ( -y )

#### Testando podemos vê que é o mesmo resultado
$ subtract ( 5, 3 )
2

#### Para invertaer qualquer valor é só criar uma função com ( * -1) no final
const inverse = ( x ) => x * -1

#### TEstamos recebemos o valor investido do valor
inverse (2)
-2

#### Uma funcao que retorna outra (no caso o resultado) de outra funcao
$ const __subtract = ( x, y ) => add( x, inverse( y ) ) 
_subtract ( 5, 3 ) //E que retorna o (x) inverso de (y);
2

#### Agora vamos somar o valor de PA, usando nossas funcoes ja criadas
```
const f = ( x, y ) => x
const inverse = ( x, y ) => x * -1

const add = ( x, y ) => x + y
const subtract = ( x, y ) => add(x, inverse( y )  )

const PA = ( x ) => ( y ) => x + y // Uma funcao q recebe o valor de x, e chama a outra funcao para somar x + y

const PA_razao2 = PA( 2 ) // ( y ) => x + 2 (pq criamos um encapsulamento, e a funcao filha (y) acima tem acesso a funcao pai "x") 
const PA_razao5 = PA( 5 ) //  ( y ) => x + 5 (Aqui estamos reutiizando novamente uma parte do nosso codigo, poderia ser  PG = ( x ) => ( y ) => x * y
 
console.log ( PA_razao2( 5 )  )
console.log ( PA_razao5( 5 )  )

``
#### Podemos observar que ele retornou os valores esperados
$ node add.subtract.js
7
10

#### Aqui nois criamos a funcao com as
```
const f = ( x ) => x
const inverse = ( x ) => x * -1

const add = ( y ) => ( x ) => x + y
const subtract = ( y ) => ( x ) => add( inverse ( y ) )( x )

console.log( add( 4 ) ( 6 ) )
console.log( subtract( 4 ) ( 6 ) )
```
####
$ node add.subtract.js
10
-2

#### Aqui temos um ana funcao que multiplicao "x" e o "y" usando subtracao e soma
```
"use strict"
const inverse = ( x ) => ( y ) => x *-1

const add = ( y ) => ( x ) => y + x
const subtract = ( y ) => ( x ) => add( inverse( y ) ) ( x )

const multiply = ( x, y ) => {  // nossa funcao pega o valor de x e y

  let result = 0;

  while ( y > 0 ) {  // enquanto y ( 4 ) for menor que zero
    result = result + x  // o valor de x vai sendo alterado (let)
    y = y - 1
  }

  return result
}

console.log( multiply( 3, 5 ) )
``
#### Testando podemos ve que esta tudos nos conformes...
$ node multiply.js
15

#### Aqui estamos fazendo a mesma soma acima porém usando as funcoes já criadas

```
"use strict";

const inverse = ( x, y ) => x *-1

const add = ( y ) => ( x ) => y + x
const subtract = ( y ) => ( x ) => add( inverse( y ) )( x )

const multiply = ( x ) => ( y ) => {
//const multiply = ( x, y ) => {

  let result = 0

  const addX = add ( x )  // tamos adiconando o valor de "x" durante o loop
  const decrement1 = subtract ( 1 )  // tamos decrementando e com valor "1" pq inverse dah numeros negativos

  while ( y > 0 ) {
    result = addX ( result )  // tamos adionando sempre o valor de "x' a result
    y = decrement1 ( y )
  }

  return result
}

console.log('3 x 5 =', multiply( 4 ) ( 3 ) )

```
#### Para fazer a divisão é só deixar o negativo de inverse sem o ( 1 )
```
"use strict";

const inverse = ( x, y ) => x *-1

const add = ( y ) => ( x ) => y + x
const subtract = ( y ) => ( x ) => add( inverse( y ) )( x )

const multiply = ( x ) => ( y ) => {

  let result = 0

  const addX = add ( x )
  const decrement1 = subtract // Aqui é retirado o valor quei tira a negativa

  while ( y > 0 ) {
    result = addX ( result )
    y = decrement1 ( y )
  }

  return result
}

console.log('9 / 3 =', multiply( 2 )( 100 ) )
```
#### Para a exponenciação (raiz quadrada), usaremos a seguinte forma
```
const pow = ( y ) => ( x ) => {
  "use strict";

  let result = 1

  while ( y > 0 ) {
    result *= x  // O x vai  receber 3x(result = 1), e depois result vai ser 3x3 = 9
    y -= 1       // o y vai fazer o loop 2 vezes depois  3 e  4...
  }

  return result
}

console.log (' 3^2 =', pow( 2 ) ( 3 ) )
console.log (' 3^3 =', pow( 3 ) ( 3 ) )
console.log (' 3^4 =', pow( 4 ) ( 3 ) )
console.log (' 3^5 =', pow( 5 ) ( 3 ) )

```
#### Podemos testar nosso codigo e ve que esta tudo nos funcioando perfeitamente.

$ node pow.almost.there.js

3^2 = 9
3^3 = 27
3^4 = 81
3^5 = 243

## Valores boleanos

#### Usaremos os dois valores da algebra
0 = falso
1 = verdadeiro

#### Para negar usamos o operador "!" de negacao
! = not (inverter o valor)

#### Simbolos logicos
&& = and
|| = or

#### Quando o valor testado for igual o resultado é sempre o mesmo valor para ambos operadores
> (0 && 0)
0
> (0 || 0)
0
> ( 1 && 1)
1
> ( 1 || 1)
1

#### o operador "Ou" sempre que utilizado com uma premissa verdadeira (1) ele sera verdadeiro
( 1 || 0 )
1
( 1 || 1 )
1

#### Já o "E" ou "AND" quando utilizado com uma premissa falsa (0)ele sempre será falso
( 0 && 1 )
0
( 0 && 1 ) 
1

#### Uma dica muito facil é usar multiplicacao para "E" e soma para "OU"

## Aula 3

#### O numero eh par se ele for divisivel por 2, usamos a funcao "%" para testar
$ const ehPar = ( x ) => x % 2 === 0
$ ehPar(4)
true

#### Para saber se eh impar eh soh usar logicamente a negacao acima.
$ const ehImpar = ( x ) => x % 2 !== 0
ehImpar(7)
true

#### Vejamos valores que o JS entende como falso, caso nao seja nao entra no "IF"
$  if( !"" ) console.log('falso')
falso
$ if( !0 ) console.log('falso')
falso
$ if( !NaN ) console.log('falso')
falso
$ if( !null ) console.log('falso')
falso
$ if( !undefined ) console.log('falso')
falso
$ if( !false ) console.log('falso')
falso

### Só há um pequeno problema, como vemos abaixo mesmo negando o resto do valor ele retorna "True"
$const ehPar2 = ( x ) => !x % 2
$ ehPar2(8)
0
$ ehPar2(5)
0

### Pois como na matematica precisamos usar o "()" para encapsular a funcao
$ const ehPar3 = ( x ) => !(x % 2)
$ ehPar3(8)
true

### Aqui criamos uma clasure, ou seja, uma funcao chamando a outra

const NOT = ( x ) => !x
const isDivisibleBy = ( y ) => ( x ) => NOT( x % y )

const isEven = isDivisibleBy( 2 ) // Aqui estamos executando e ele vai retornar:( x ) => NOT( x % y ) 
que no caso é ( x % 2)

console.log( 'isEven 4: ', isEven( 4 ) )

#### Agora só testar e ve se o resultado é par ou impar do valor passado
$ node aula3.js
isEven 4:  true

#### 

















