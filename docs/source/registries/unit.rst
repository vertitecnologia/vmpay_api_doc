##################
Unidades de medida
##################

Listar
======

::

  GET /api/v1/units

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo::

  [
    {
      "id": 2,
      "name": "gram",
      "fractionable": true,
      "conversion_factor": 1000
    },
    {
      "id": 3,
      "name": "milliliter",
      "fractionable": true,
      "conversion_factor": 1000
    },
    {
      "id": 1,
      "name": "unit",
      "fractionable": false,
      "conversion_factor": 1
    }
  ]

Ver
===

::

  GET /api/v1/units/[id]

Parâmetros de URL:
------------------

=========  ===============  ===========
parâmetro  descrição        obrigatório
=========  ===============  ===========
id         id do produto    sim
=========  ===============  ===========

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

Exemplo::

  {
    "id": 1,
    "name": "unit",
    "fractionable": false,
    "conversion_factor": 1
  }

Erros
-----

==========  ========================  =========================================
status      descrição                 response body
==========  ========================  =========================================
404         produto não encontrado    { "status": "404", "error": "Not Found" }
==========  ========================  =========================================
