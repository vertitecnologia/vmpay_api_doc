########
Estoques
########

Listar
======

::

    GET /api/v1/storables

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo:

::

  [
    {
       "id": 1,
       "created_at": "2014-08-07T12:26:16.000Z",
       "updated_at": "2020-01-17T17:56:58.000Z",
       "type": "Product",
       "manufacturer_id": 2,
       "category_id": 1,
       "name": "Coca-Cola Zero",
       "upc_code": "1",
       "barcode": null,
       "external_id": null,
       "url": "http://127.0.0.1:3001/api/v1/storables/1",
       "inventories": [
         {
           "distribution_center_id": 1,
           "total_quantity": 576.0,
           "committed_quantity": 0.0
         }
       ]
     },
     {
       "id": 2,
       "created_at": "2014-08-07T12:26:31.000Z",
       "updated_at": "2020-01-17T21:56:42.000Z",
       "type": "Product",
       "manufacturer_id": 2,
       "category_id": 1,
       "name": "Coca-Cola",
       "upc_code": "2",
       "barcode": null,
       "external_id": null,
       "url": "http://127.0.0.1:3001/api/v1/storables/2",
       "inventories": [
         {
           "distribution_center_id": 1,
           "total_quantity": 236.0,
           "committed_quantity": 0.0
         }
       ]
     }
  ]

Ver
===

::

    GET /api/v1/storables/[id]

Parâmetros de URL:
------------------

=========  ==============  ===========
parâmetro  descrição       obrigatório
=========  ==============  ===========
id         id do estoque   sim
=========  ==============  ===========

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo:

::

  {
    "id": 2,
    "created_at": "2014-08-07T12:26:31.000Z",
    "updated_at": "2020-01-17T21:56:42.000Z",
    "type": "Product",
    "manufacturer_id": 2,
    "category_id": 1,
    "name": "Coca-Cola",
    "upc_code": "2",
    "barcode": null,
    "external_id": null,
    "url": "http://127.0.0.1:3001/api/v1/storables/2",
    "inventories": [
      {
        "distribution_center_id": 1,
        "total_quantity": 236.0,
        "committed_quantity": 0.0
      }
    ]
  }

Campos
------

* *type*: tipo do estoque
* *manufacturer_id*: id do fabricante
* *category_id*: id da categoria
* *name*: nome do produto
* *upc_code*: código UPC do produto
* *barcode*: código de barras do produto
* *external_id*: id externo
* *inventories*: lista de inventários relacionados ao estoque

  * *distribution_center_id*: id do centro de distribuição
  * *total_quantity*: saldo do produto
  * *committed_quantity*: quantidade reservada

    * Para o cálculo do saldo disponível, deve-se considerar
      (total_quantity - committed_quantity)


Erros
-----

==========  ========================  =========================================
status      descrição                 response body
==========  ========================  =========================================
404         registro não encontrado    {"error":"Registro não encontrado"}
==========  ========================  =========================================

Atualizar
=========

::

    PATCH /api/v1/storables/[id]

Parâmetros de URL:
------------------

=========  ==============  ===========
parâmetro  descrição       obrigatório
=========  ==============  ===========
id         id do estoque   sim
=========  ==============  ===========

Request::

  {
    "storable": {
      "inventories": [{
        "distribution_center_id": 1,
        "quantity_delta": 2
      }]
    }
  }

Campos
------

* *storable*

  * *inventories*: lista dos inventários relacionados ao estoque

    * *distribution_center_id*: id do centro de distribuição.
    * *quantity_delta*: diferença desejada para alteração do saldo, positiva
      ou negativa.

Retorno
-------

======  ======================
status  descrição
======  ======================
200     Atualizado com sucesso
======  ======================

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
404         registro não encontrado               { "status": "404", "error": "Not Found" }
==========  ====================================  ====================================================

