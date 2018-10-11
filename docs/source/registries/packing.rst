########
Packings
########

Listar
======

::

    GET /api/v1/packings

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
      "id":2,
      "created_at":"2018-08-08T14:22:34.000Z",
      "updated_at":"2018-08-08T14:22:34.000Z",
      "name":"Caixa de Latas",
      "unit":"default",
      "quantity":12,
      "good_ids":[2,10352,17480,6423,11,6424,17481,17483,17479]
    },
    {
      "id":22,
      "created_at":"2018-08-07T13:22:34.000Z",
      "updated_at":"2018-08-07T13:42:34.000Z",
      "name":"Pacote 1kg",
      "unit":"gram",
      "quantity":1000,
      "good_ids":[3,102,482,484,485,747]
    }
  ]

Ver
===

::

    GET /api/v1/packings/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id do packing    sim
=========  ===============  ===========

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
    "id":2,
    "created_at":"2018-08-08T14:22:34.000Z",
    "updated_at":"2018-08-08T14:22:34.000Z",
    "name":"Caixa de Latas",
    "unit":"default",
    "quantity":12,
    "good_ids":[2,10352,17480,6423,11,6424,17481,17483,17479]
  }

Erros
-----

==========  ========================  =========================================
status      descrição                 response body
==========  ========================  =========================================
404         registro não encontrado    {"error":"Registro não encontrado"}
==========  ========================  =========================================

Criar
=====

::

    POST /api/v1/packings

Request::

  {
    "packing": {
      "name":"Pacote 2kg",
      "unit":"gram",
      "quantity":2000
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *packing*

  * *name*: nome do packing.
  * *unit*: A unidade de medida do packing.

    * Valores permitidos: *default* (Unidade), milliliter (Mililitro) e *gram* (Grama).

  * *quantity*: A quantidade em medidas de *unit* presente no packing.


Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criado com sucesso
======  ==================

Exemplo:

::

  {
    "id":23,
    "created_at":"2018-08-15T12:22:34.000Z",
    "updated_at":"2018-08-15T12:22:34.000Z",
    "name":"Pacote 2kg",
    "unit":"gram",
    "quantity":2000,
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
422         erro ao criar                         ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao criar

::

  {
    "unit": [
      "não pode ficar em branco"
    ]
  }

Atualizar
=========

::

    PATCH /api/v1/packings/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id do packing    sim
=========  ===============  ===========

Request::

  {
    "packing": {
      "name": "Novo nome"
    }
  }

Campos
------

Ao menos um campo interno a *packing* deve ser passado.

Retorno
-------

======  ======================
status  descrição
======  ======================
200     Atualizado com sucesso
======  ======================

Exemplo:

::

  {
    "id":23,
    "created_at":"2018-08-15T12:22:34.000Z",
    "updated_at":"2018-08-15T12:22:34.000Z",
    "name":"Novo nome",
    "unit":"gram",
    "quantity":2000,
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
404         registro não encontrado                { "status": "404", "error": "Not Found" }
422         erro ao atualizar                     ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao atualizar

::

  {
    "name": [
      "é muito longo (máximo: 255 caracteres)"
    ]
  }

Excluir
=======

::

    DELETE /api/v1/packings/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id do packing    sim
=========  ===============  ===========

Retorno
-------

======  ====================  =============
status  descrição             response body
======  ====================  =============
204     Excluído com sucesso  (vazio)
======  ====================  =============

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
404         registro não encontrado                { "status": "404", "error": "Not Found" }
==========  ====================================  ====================================================
