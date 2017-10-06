---
layout: post
title:  "Flask - Construir uma Api Rest Full"
date:   2017-09-05 16:54 -0300
categories: blog
---

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

Por exemplo,
http: // localhost: 5000 / api / messsages / 6 identifica a mensagem cujo id é igual a
6.



