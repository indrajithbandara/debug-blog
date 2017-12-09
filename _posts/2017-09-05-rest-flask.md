---
layout: post
title:  "Flask - Construir uma Api Rest Full"
date:   2017-09-05 16:54 -0300
categories: blog
---








------
A tabela a seguir mostra os verbos HTTP, o escopo e a semântica para os métodos que nossa primeira versão da API deve suportar.
Cada método é composto por um verbo HTTP e um escopo e todos os métodos têm um significado bem definido para todas as mensagens e coleções.
Em nossa API, cada mensagem tem seu próprio URL exclusivo.

HTTP        verb Scope                 semantics
GET         Collection of messages     Retrieve all the stored messages in the collection, sorted by their name in ascending order
GET         Message                    Retrieve a single message
POST        Collection of messages     Create a new message in the collection
PATCH       Message                    Update a field for an existing message
DELETE      Message                    Delete an existing message

Compreendendo as tarefas realizadas por cada Método HTTP
Consideremos que http: // localhost: 5000 / api / messages / é o URL para a coleção de mensagens.ii

Se nós adicionarmos um número ao URL anterior, nós identificamos uma mensagem específica cujo id é igual ao valor numérico especificado.

Por exemplo, http: // localhost: 5000 / api / messsages / 6 identifica a mensagem cujo id é igual a 6.

Queremos que nossa API seja capaz de diferenciar coleções de um único recurso da coleção nos URLs.

```
Quando referimos uma coleção, usaremos uma barra (/) como o último caractere para o URL, como em http://localhost:5000/api/messages/ .

Quando nos referimos a um único recurso da coleção, nós não vai usar   uma barra (/) como o último caractere para o URL, como em
http: // localhost: 5000 / api / messages / 6.
```
Temos que compor e enviar uma solicitação HTTP com o verbo POST HTTP e o http: // localhost: 5000 / api / messages / request URL
para criar uma nova mensagem. Além disso, temos que fornecer os pares de valores-chave JSON com os nomes dos campos e os valores
para criar a nova mensagem. Como resultado da solicitação, o servidor irá validar os valores fornecidos para os campos, certifique-se 
de que seja uma mensagem válida e persisti-lo no dicionário de mensagens.

IO servidor retornará um código de status criado 201 e um corpo JSON com o recente mensagem adicionada serializada para JSON, 
incluindo o id atribuído que foi automaticamente gerado pelo servidor para o objeto de mensagem:

POST http: // localhost: 5000 / api / messages /


IIIIII
Temos que compor e enviar uma solicitação HTTP com o verbo GET HTTP e
URL http: // localhost: 5000 / api / messages / {id} para recuperar a mensagem
cujo id corresponde ao valor numérico especificado no local onde {id} está escrito.


IIIIIII


Por exemplo, se usarmos o URL da solicitação http: // localhost: 5000 / api / messages / 82, o
o servidor recuperará o jogo cujo id corresponda 82. Como resultado da solicitação, o servidor recuperará uma mensagem com o id especificado no dicionário.


Se uma mensagem for encontrada, o servidor serializará o objeto de mensagem em JSON e retornará um código de status de 200 OK e um corpo JSON com o objeto de mensagem serializado.

Se nenhuma mensagem corresponder à ID ou à chave primária especificada, o servidor retornará um status 404 Not Found: GET http: // localhost: 5000 / api / messages / {id}






























