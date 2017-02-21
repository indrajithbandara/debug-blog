---
layout: post
title:  "MongoDB!"
date:   2016-10-13 15:32:03 -0300
categories: start blog
---
## MongoDB

## Aula 1

###### NOSQL
Nos bancos relacionais o que importa são as respostas que voce tem, sabemos os dados que vao entrando, normalizando, separando todas
informacoes para nao ter duplicidade nas tabelas, só existe uma forma de modelar o relacional, normalizando, agora se vc for NoSQL
as perguntas que importam, o que o sistema quer no inicio dele

###### Terminologia
SQL RDBMS         MongoDB
DATABASE          DATABASE
TABLE             COLLECTION
ROWS              DOCUMENT JSON
QUERY             QUERY
INDEX             INDEX
PARTITION         SHARD

###### Vantagens
Normalmente as empresas utilizam os bancos NoSQL quando possuem um banco de dados em franco crescimento e precisam escalar horizontalmente com performance.

###### Tipos
Nesse universo de Banco de Dados NoSQL temos alguns grupos grandes com diversos bancos de dados e para as mais diversas finalidades, então vamos conhecer um pouco sobre eles para entender um pouco onde iremos nos enfiar. :p
Chave/Valor;
Documento;
Grafo;
Coluna.

##### Para iniciarmos o MongoDb precisamos rodar o seu serviço, executando o comando:
mongod

##### Caso seja sua primeira vez com o MongoDb e ter dado erro e você localizar isso na mensagem de erro:
data/db

##### Significa que sua pasta data/db não está criada, para criar em sistema unix e da as permissões necessárias use:
sudo mkdir /data
sudo mkdir /data/db
sudo chmod 777 -Rf /data'

###### Para conectarmos no servidor do MongoDb usaremos seu cliente, o:
mongo

###### Antes instale o Mongo Hacker para colocrir o console
https://github.com/TylerBrock/mongo-hacker

###### Para exportarmos os dados de uma coleção no MongoDb usaremos o comando: 
mongoexport

###### Chamamos o mongo export com  nome da database, nome da coleção a ser exportada, e  nome do arquivo Jason que vc quer salvar.
$ mongoxport --db nome_da_database --collection nome_da_colecao --out minha_colecao.json

##### mongoimport é mesma coisa, porem dessa vez temos o --drop que apaga sua colecao se ela existir e joga os dados em cima da colecao vazia,  e file eh o aquivo que tem os dados desse json
$ mongoimport --db database --collection collection --drop --file data.json

#### Exercicios 1
https://bitbucket.org/rxon7/be-mean-exercicios/commits/3d31141bcaa9d344a23f020c3c4fa9d935daa150

## ================================================= Aula 2

#### Utilizando databases
use nome_database

### Caso queria escolher uma database na hora de levantar o mongod basta executar
mongo nome_database

##### Então agora é sua hora de mudar seu banco de dados, vamos todos usar a mesma base:
use achievements

##### Perceba que logo abaixo você receberá uma mensagem assim:
switched to db achievements

###### Isso significa que agora nossa variável `db` está aprontando para nosso database, para você verificar basta digitar `db` e apertar o ENTER:Isso
$ db
achievements

###### Rodando um show dbs agora sõ vamos consegui vê o local.
show dbs
local  0.078GB

###### Isso acontece porque o MongoDb só irá criar sua database quando você tiver inserido algo nela, para inserirmos algo faremos da seguinte maneira:
db.teste.insert({nome: "Renan", idade: 30})
s})

###### Agora dando um show dbs vamos ve nossa datcoleçãoabase lá pq foi inserido um JSON nela.
$ show dbs
-be-mean          
→ 0.203GB
    
#### show collections  é o responsável por listar as coleções da sua database especificada com use.
show collections
invt           →  0.000MB /  0.008MB
pokemons       →  0.106MB /  0.246MB

###### Caso deseje criar uma coleção vazia você deverá usar o comando: 
db.createCollection()
https://docs.mongodb.org/v3.0/reference/method/db.createCollection/#db.createCollection

## db.insert() Create

##### Como vamos fazer um CRUD primeiro vamo fazer um Create, primeiro mudamos e criamos nossa nova database
use 

###### Agora vamos adcione mais 3 games.
var registerGames = [{name: "I Am Alive", pwd:  70, plataform: "PS4", velocista: 8, comments: "Dificuldade nao tão dificil", online: "Nao", origem: "Indefinido", guia: "Sim", platina: "Nao" }]

###### Analisando a variavel eh sempro bom antes de inserir
$ registerGames
[
  {
    "name": "I Am Alive",
    "pwd": 70,
    "plataform": "PS4",
    "velocista": 8,
    "comments": "Dificuldade nao tão dificil",
    "online": "Nao",
    "origem": "Indefinido",
    "guia": "Sim",
    "platina": "Nao"
  }
]
##### Agora basta inserir todos eles
db.pc.insert(registerGames)
Inserted 1 record(s) in 290ms

##### Depois de inserido todos os games basta listá-los:
 db.pc.find()
{
  "_id": ObjectId("58a36d56a871e2de734c4fb3"),
  "name": "I Am Alive",
  "guia": "Sim",
  "platina": "Nao"
}
Fetched 1 record(s) in 1ms

##### save() 
Insere e Salva

###### Vamos criar uma variavel achieves que chama Grow Home
var registerGames = [{name: "Grow Home", pwd:  61, plataform: "PS4", velocista: 5, comments: "Jogo muito bom", online: "Nao", origem: "Plus", guia: "Nao", platina: "Sim" }]

###### Verificamos a nossa variavel
$ registerGames
[
  {
    "name": "Grow Home",
    "pwd": 61,
    "platina": "Sim"
  }
]

##### Agora que já temos a variavel archieves basta salvar
db.pc.save(registerGames)
Inserted 1 record(s) in 0ms

##### Verificando nossas coleções
$ db.pc.find()
{
  "_id": ObjectId("58a36d56a871e2de734c4fb3"),
  "name": "I Am Alive",
  "pwd": 70,
  "platina": "Nao"
}
{
  "_id": ObjectId("58a37822a871e2de734c4fb5"),
  "name": "Grow Home",
  "pwd": 61,
  "platina": "Sim"
}
Fetched 2 record(s) in 1ms

### Buscando e Adcionando

##### Vamos criar uma query de busca, vamos modificar o Darksiders com um save, primeiramente criamos uma query:
$ var query = {name: 'Darksiders'}
$ var p = db.achievements.find(query)
> p
{
  "_id": ObjectId("58920e71dd33ba0377f1eeea"),
  "name": "Darksiders",
  "platina": "Nao"
}  

##### Se tentar-mos acessa-lo novamente ele nao existe mais pq vem em forma de cursor (para usar cursor busque documentacao)
$ p.name
> 
##### Então precisamos utilizar o findOne pois ele retorna um objeto comum, com a mesma query agora usando o findOne
var p = db.achievements.findOne(query)

#### Agora podemos digitar a variavel p e fazer a busca quantas vezes quisermos
$ p
{
  "_id": ObjectId("58920e71dd33ba0377f1eeea"),
  "name": "Darksiders",
  "platina": "Nao"
}

##### Se usarmos o p.name agora funcioana normal
$ p.name
Darksiders

## Modificando

##### Vamos mudar platina de nao para sim
$ p.platina = "Sim"
Sim

#### Podemos ve que modificou localmente
$ p
{
  "_id": ObjectId("58920e71dd33ba0377f1eeea"),
  "name": "Darksiders",
  "platina": "Sim"
}

###### Agora vAmos salvar no banco, porém temos dois passos, mas com save ele só faz tudo de uma vez
$ db.achievements.save(p)
Updated 1 existing record(s) in 202ms

##### Agora podemos vê que ele alterou de verdade
$ db.achievements.find()
{
  "name": "Darksiders",
  "platina": "Sim"
}

## Cursor (desnecessario agora)

##### Primeiramente fazemos um find(), lembrando que o find() retorna o cursor e o findOne o objeto direto, depois vamos fazer um while nesse cursor
var cur = db.pokemons.find();

#### Fazemos um while onde se cursor tiver uma proxima posição(hasNext) ele vai imprimir { print(tojson) } e ai vamos pegar o nosso cursor com (cur.next) que é a funcao que pega o valor da proxima posicao, se ele tiver has next vc pode pegar o valor com  next
hile( cur.hasNext() ) { print(tojson(cur.next()))};
{
  "_id": ObjectId("58920e71dd33ba0377f1eeea"),
  "name": "Darksiders",
  "platina": "Sim"
}

#### Exercicios 2
https://bitbucket.org/rxon7/be-mean-exercicios/commits/7e022e06c25d1976d30ade6d06bd0ee4cacd3f9f

#### Aula 3 ============================ 

## Fizemos o C do Crud agora é o R do retrive, 
find() Retrieve

##### já mostramos o find e vamos mostrar o findOne também
findOne() Retrieve

###### _id UUID
Quando adcionamos qualquer atributo em nosso documento ele cria o _id UUID, e um indicador universal.

###### O _id trabalha separando quatro tipos de dados:
4-bytes: valor que representa os segundos desde a época Unix;
3-bytes: identificador de máquina;
2-bytes: ID do processo;
3-bytes: contador, começando com um valor aleatório.

##### Sintaxe, o find aceita dois parametros, pensando em forma relacional o primeira parametro eh o where e o segundo os campos (seria select)
db.colecao.find ({clausulas}, {campos})

#### Criamos a query numa variavel
var query = {name: 'I Am Alive'}

#### E depois passamos o find nela
db.achievements.find(query)
{
  "_id": ObjectId("58922855dd33ba0377f1eeec"),
  "name": "I Am Alive",
  "platina": "Nao"
}

##### Fields (campos)
Fildes é o nosso segundo parametro, se o nosso JSON de `query` é o WHERE do relacional, logo o JSON `fields` será o nosso SELECT onde o mesmo irá selecionar quais campos desejados na busca da query.
Para isso especificamos os campos desejados com 1 que significa TRUE ou os campos indesejados com 0 que significa FALSE.

###### Para facilitar vamos criar um json para nossa query da seguinte forma
var query = {name: 'I Am Alive'}

###### Nosso objeto de fields eh esse aqui, com name 1 e description 1
var fields = {name: 1, description: 1}

##### São esses dois objetos acima que precisamos para conslconcluir a busca com find
b.achievements.find(query, fields)
{
  "_id": ObjectId("58922855dd33ba0377f1eeec"),
  "name": "I Am Alive"
}

##### Para negar o o _ID, é só digitar _id: 0
var fields = {name: 1, description: 1, _id:0 }

##### Execultamos novamente veja que só veio o nome e o description
db.achievements.find(query, fields)
{
  "name": "I Am Alive"
}
## Operadores Aritméticos

###### Menor que
< é $lt
less than

###### Menor ou igual
<= é $lte
less than or equal

###### Maior que
> é $gt
greater than

###### Maior ou igual
>= é $gte
greater than or equal

##### Depois de especificamos qual campo vamos fazer a busca temos que passar o objeto para identificar qual operacao que vamos fazer nesse campo
var query = {pwd: {$lt: 42}}

##### Podemos vê que a busca está bem mais clara para um programador do que o SQL
$ query {"pwd": {"$lt": 42}}

##### Agora passamfazemos a nossa busca.
db.pokemons.find(query)
{
  "_id": ObjectId("5893710df5e61894d5b75ecc"),
  "name": "Prince of Persia: The Two Thrones",
  "pwd": 25,
}

## Operadores Lógicos

##### O primeiro é o nosso or(ou), se tiver duas ou mais primicias, se uma delas for verdadeira, retorna verdadeiro 
$or (OU)

###### Veja a nossa sintaxe, precisamos de duas premmissias para testar o operador logico, e esses objetos json é aceito pelo nosso 'or'  
var query = {$or: [{name: 'RenanMon'}, { height: 1.69 }]}

Retorna objetos caso a cláusula OU for verdadeira.

##### Vamos ve o que temos nessa query
db.pokemons.find(query)
{
  "_id": ObjectId("587e50a95a64ab4282a4698d"),
  "name": "RenanMon",
  "height": 0.4
}

Ou seja, se pelo menos 1 premissa for verdadeira ele irá retornar o objeto que contém essa premissa.

#####  $nor Not OU

#####  É a negação do OR, ou seja, retorna TODOS os objetos que não possuem as premissas buscadas. 
var query = {$nor: [{name: 'RenanMon'}, { height: 1.69 }]}

#####  Ele tras todos menos o que veio no OR (no caso o RenanMon)
$ db.pokemons.find(query)
{ "_id": ObjectId("587e70385a64ab4282a4698e"),
     "height": 0.4}
{  "_id": ObjectId("587e70965a64ab4282a4698f"), 
  "height": 0.6}

###  $and E

##### Retorna objetos caso a cláusula E for verdadeira.
var query = {$and: [{name: 'RenanMon'}, { height: 0.4 }]}

#####  Vamos fazer o noss find, ele vai retornar pq as duas premissas sao verdadeiras
db.pokemons.find(query)
{  "_id": ObjectId("587e50a95a64ab4282a4698d"),
"name": "RenanMon",,}

#####  Operadores “Existênciais”
$exists

Como o mondo DB é steamaless vc nao tem uma estrutura pré definida da sua coleção
um operador desse tipo nos facilita muito a nossa busca para serto tipos de objeto que
nois necesitamos, muito usado para buscar tags em blogs, veremos exemplos mais para frente

##### Exercicio
https://bitbucket.org/rxon7/mongodb-excercises/commits/31d25fc09c00aaebdac5c70786dc29a71e4351b9

#####  ============================ Aula 4
update() Update

##### Para alteramos um documento no MongoDb possuímos duas formas:
- save
- update.

##### Recordando que para utilizar o save eu preciso antes buscar o documento necessário antes de poder modificá-lo, com o update isso não será necessário.

##### A função update recebe 3 parâmetros:
- query
- modificação
- options

##### No caso não eh obrigado passar o options, essa eh a sintaxe:
db.colecao.update(query, mod, options);

##### Vamos inicar uma biblioteca nova e adcionar um game
var registerGames = [ 
...       {name: "Life Is Strange", pwd: 30 , plataform: "Pc", velocista: 7, comments: "jogo facil", online: "Nao", origiem: "Demo", guia: "Sim", platina: "Nao" } 
... ]

##### Salvar no banco de dados diretamente
$ db.pc.save(registerGames)
Inserted 1 record(s) in 0ms

##### Dando o find só para dá aquela constada basica que inseriu
$ db.pc.find()
{"_id": ObjectId("58a36d56a871e2de734c4fb3"),

"name": "I Am Alive",}
{"_id": ObjectId("58a37822a871e2de734c4fb5"),
"name": "Grow Home",}

##### Criando a query de busca, o /i eh para ficar case sensitive
var query = {name: /Life Is Strange/i}

##### Fazendo a busca para garantir o ID
db.pc.find(query)
{  "_id": ObjectId("58a5e0abc9e7034c53ff5fa2"),
"name": "Prison architect",}

##### Depois de inserido vamos tentar fazer o nosso primeiro update, para isso iremos criar uma query para buscar nosso Pokemon e posteriormente, modificá-lo:
var query = {"_id": ObjectId("58a5e0abc9e7034c53ff5fa2")}

##### Vamos criar a query  nosso objeto de modificação
var mod = {name: "Prison architect", pwd: 30 , plataform: "Pc", velocista: 8, comments: "Da para agilizar comprando prisoes", online: "Nao", origiem: "Comprado", guia: "Nao", platina: "Nao" }

##### Agora vamos fazer o update na nossa coleção
db.pc.update(query, mod)

#### $set

##### O operador $set modifica um valor ou cria ele caso ele não exista, sintaxe:
{ $set : { campo : valor } }

##### Exemplo
db.colecao.update( { name: 'Pikachu'}, { $set: { attack: 120 }

##### Então vamos reaproveitar nossa query que já possui nosso _id e adicionar o nosso objeto de alteração
var mod = {$set: {comments: "add jogar online" }}

##### Vamos passar o nosso update para a nossa query
$ db.play.update(query, mod)

##### Pronto o nosso objeto já esta devidamente alterado.
db.play.find()
{"_id": ObjectId("58a5e0abc9e7034c53ff5fa2"),
"comments": "add jogar online",}

#### $unset

##### Primeiro criamos a nossa variavel passando o unset com true (1) no campo que for deletar
$ var mod = {$unset: {comments: 1}}

##### Depois basta passamos o update na query
$ db.play.update(query, mod)
Updated 1 existing record(s) in 56ms

##### Damos o find e confirmamos que o campo comments foi deletado.
db.play.find(query)
{"_id": ObjectId("58a5e0abc9e7034c53ff5fa2"),
"guia": "Sim",}

#### $inc

#####  O operador $inc incrementa um valor no campo com a quantidade desejada. Caso o campo não exista, ele irá criar o campo e setar o valor. Para decrementar, basta passar um valor negativo, sintase:
{ $inc : { campo : VALOR} }

##### Sintaxe
var mod = {$inc: { campo: Valor }}

##### Vamos supor que aumentou o pwd do jogo entao incrementamos com 1 para ele ir para 31 (para decrementar eh o 2) 
$ var mod = {$inc: { pwd: 1 }}

##### Passamos o update (bem facil)
$ db.play.update(query, mod)
Updated 1 existing record(s) in 34ms

##### Vamos conferir e podemos vê que ele era 30 e agora eh 31
$ db.play.find()
{
  "_id": ObjectId("58a5e0abc9e7034c53ff5fa2"),
  "name": "Need for speed",
  "pwd": 31,
}
Fetched 1 record(s) in 1ms

#### Operadores de Array

##### $push

O operador $push adiciona um valor ao campo, caso o campo seja um *Array* existente. Caso não exista irá criar o campo novo, do tipo *Array* com o valor passado no $push.
Caso o campo exista e não for um *Array*, irá retornar um erro.

##### Sintaxe
{ $push : { campo : valor } }

##### Então vamos adicionar  um array de jogadores, passamos o campo coop e o valor que eh rxon7
$ var mod = {$push: {coop: 'rxon7'}}

##### Vamos rodar o update com essa query
$ db.pokemons.update(query, mod)

##### Vamos conferir e podemos vê que ele criou o array coop tudo automatico com o $push.
$ db.play.find()
{
  "_id": ObjectId("58a5e0abc9e7034c53ff5fa2"), 
  "coop": [
    "rxon7"
  ], 
  "name": "Need for speed", 
}

##### $pushAll

##### O operador $pushAll adiciona cada valor do [Array_de_valores], caso o campo seja um *Array* existente. Caso não exista irá criar o campo novo, do tipo *Array* com o valor passado no $pushAll. Caso o campo exista e não for um *Array*, irá retornar um erro, Sintaxe:
{ $pullAll : { campo : [Array_de_valores] } }

##### Adcionando novos jogadores para o campo coops
$ var jogadores = ['netosurf', 'Prof_Sidney', 'Prof_Sidney', 'JamesCapitall' ]

##### Vamos fazer o nosso modificador do $pushall, passando para  os jogadores  para o array coop
var mod = {$pushAll: {coop: jogadores}}

##### Passamos o nosso updade
$ db.play.update(query, mod)
Updated 1 existing record(s) in 1ms

##### E vamos conferir os nobos jogadores para o cooper
db.play.find()
{
  "_id": ObjectId("58a5e0abc9e7034c53ff5fa2"),
  "comments": "add jogar online",
  "coop": [
    "rxon7",
    "netosurf",
    "Prof_Sidney",
    "Prof_Sidney",
    "JamesCapitall"
  ],
  "name": "Need for speed",
 }

### $pull
O operador $pull retira o valor do campo, caso o campo seja um *Array* existente. Caso não exista ele não fará nada. Caso o campo exista e não for um *Array*, irá retornar um erro, sintaxe:
{ $pull : { campo : valor } }

##### Vamos retirar o rxon7 do array coop
$ var mod = {$pull: {coop: 'rxon7'}}

##### Passamos o update e ele encontrou e modificou
$ db.play.update (query, mod) 
Updated 1 existing record(s) in 2073ms

##### Agora fazemos um find e está eliminado o rxon7 do coop
$ db.play.find(query)
{
  "_id": ObjectId("58a5e0abc9e7034c53ff5fa2"),
  "comments": "add jogar online",
  "coop": [
    "netosurf",
    "Prof_Sidney",
    "Prof_Sidney",
    "JamesCapitall"
  ],
  "name": "Need for speed",
}

### $pullAll

#####O operador $pullAll retira cada valor do [Array_de_valores], caso o campo seja um *Array* existente. Caso não exista ele não fará nada. Caso o campo exista e não for um *Array*, irá retornar um erro, sintaxe:
{ $pullAll : { campo : [Array_de_valores] } }

##### Nosso objeto de modificação utilizando o $pullAll
var mod = {$pullAll: {coop: jogadores}}

##### Fazemos o update
db.play.update(query, mod)
Updated 1 existing record(s) in 1ms

##### Verificamos que retirou os dois jogadores do cooop
db.play.find(query)
{
  "_id": ObjectId("58a5e0abc9e7034c53ff5fa2"),
  "comments": "add jogar online",
  "coop": [
    "netosurf"
  ],
  "guia": "Sim",
  "name": "Need for speed",
  
 ##### options    
 
##### Objeto options servirá para configurarmos alguns valores diferentes do padrão para o update, sintaxe
{
  upsert: boolean, (padrão eh falso)
  multi: boolean, (padrão eh falso)
  writeConcern: document (A procupacao da escrita)  
}

##### upsert
O parâmetro upsert serve para caso o documento não seja encontrado pela query ele insira o objeto que está sendo passado como modificação. Ele por padrão é FALSE.

##### Imagine que precisamos ativar, para ler suas informações, os games na nossa tabela, pegaremos o Payday 2 

##### Pegamos nossa query do payday 2 que vamos add
var query = {name: /Payday 2/i}

##### Nosso operdor de modificação com set, o active true eh para se ele achar o payday vai criar o campinho novo
var mod = {$set: {active: true}}

##### Upsert true eh para caso ele nao ache ele vai criar esse objeto
var options = {upsert: true}

##### Passsamos a query, o modificador, e por ultimo o option
db.pc.update(query, mod, options)

##### Fazendo a pesquisa ele esta lah
{
  "_id": ObjectId("58a84d3ed0867a0215645c35"),
  "active": true,
  "name": /Payday 2/i
}
#### Então perceba que se o Pokemon existir ele só fará a alteração, agora vamos ver com um Pokemon que não exista na pokeagenda.
$ var query = {name: "Payday 2", pwd: 89 , plataform: "PC", velocista: 5, comments: "Sofrido", online: "Sim", origiem: "Comprado", guia: "Sim", platina: "Nao" }
$ var mod = {$set: {active: true}}
$ var options = {upsert: true}
$ db.pokemons.update(query, mod, options)

#### Nosso ojeto jah inserido.
$ db.pc.find() 
{
  "_id": ObjectId("58a84e15d0867a0215645c36"),  
  "name": "Payday 2",
  "active": true,
}

#### $setOnInsert
Com esse operador você pode definir valores que serão adicionados apenas se ocorrer um upsert, ou seja, se o objeto for inserido pois não foi achado pela query.
Vamos pegar um cenário onde buscaremos um game em nossa planilha, porém o mesmo não se encontra nos registros, então inserimos ele com valores padrões.

#### Vamos criar uma query que nao existe
var query = {name: /Street Fighter x Tekken/i}

#### Vamos setar actvite true(vai que ele exista), caso ele nao exista ele vai inserir o dados
var mod = {
  $set: {active: true},
  $setOnInsert: {
name: "Street Fighter x Tekken", 
pwd: 40, 
plataform: Vita, 
velocista: 45,
velocista: 45,
 
description: "Sem maiores informações"}
}

#### 
var options = {upsert: true}

#### 
db.pc.update(query, mod, options)



db.pokemons.find(query)
{
  "_id": ObjectId("564a89f33888e5da82899ccb"),
  "active": true,
  "name": "NaoExisteMon",
  "attack": null,
  "defense": null,
  "height": null,
  "description": "Sem maiores informações"
}

### multi








