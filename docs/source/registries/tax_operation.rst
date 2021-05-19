#################
Operações Fiscais
#################

Listar
======

::

  GET /api/v1/tax_operations

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
      "id": 78,
      "created_at": "2020-09-23T16:17:17.000Z",
      "updated_at": "2020-09-23T16:17:17.000Z",
      "name": "CFOP: 5102; CSOSN: 102",
      "cfop": "5102",
      "pis_cst": "01",
      "pis_aliquot": 0.65,
      "cofins_cst": "01",
      "cofins_aliquot": 3.00,
      "icms_cst": "00",
      "icms_aliquot": 18.00,
      "icms_reduction": 0.00,
      "benefit": null
    }
  ]

Ver
===

::

  GET /api/v1/tax_operations/[id]

Parâmetros de URL:
------------------

=========  =====================  ===========
parâmetro  descrição              obrigatório
=========  =====================  ===========
id         id da operação fiscal  sim
=========  =====================  ===========

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
    "id": 78,
    "created_at": "2020-09-23T16:17:17.000Z",
    "updated_at": "2020-09-23T16:17:17.000Z",
    "name": "CFOP: 5102; CSOSN: 102",
    "cfop": "5102",
    "pis_cst": "01",
    "pis_aliquot": 0.65,
    "cofins_cst": "01",
    "cofins_aliquot": 3.00,
    "icms_cst": "00",
    "icms_aliquot": 18.00,
    "icms_reduction": 0.00,
    "benefit": null
  }

Erros
-----

==========  ========================  =========================================
status      descrição                 response body
==========  ========================  =========================================
404         máquina não encontrada    { "status": "404", "error": "Not Found" }
==========  ========================  =========================================

Criar (caso esteja usando Simples Nacional)
===========================================

::

  POST /api/v1/tax_operations

Request::


  {
    "tax_operation": {
      "name": "CFOP: 5102; CSOSN: 102",
      "cfop": "5102",
      "csosn": "102",
      "pis_cst": "01",
      "cofins_cst": "01"
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *tax_operation*

  * *name*: Nome da operação fiscal.
  * *cfop*: Código Fiscal da Operação, CFOP da operação válido para NFe.
  * *csosn*: Código de Situação da Operação do Simples Nacional.

Opcionais
^^^^^^^^^

* *tax_operation*

  * *pis_cst*: Código da situação tributário do PIS.
  * *cofins_cst*: Código da situação tributário do COFINS.

Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criado com sucesso
======  ==================

Exemplo::

  {
    "id": 82,
    "created_at": "2021-03-16T12:32:34.083Z",
    "updated_at": "2021-03-16T12:32:34.083Z",
    "name": "Operação Fiscal 1",
    "cfop": "5102",
    "csosn": "102"
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
401         não autorizado                        (vazio)
422         erro ao criar                         ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao criar

::

  {
    "name": [
      "já está em uso"
    ],
    "cfop": [
      "não pode ficar em branco"
    ],
    "csosn": [
      "não pode ficar em branco"
    ]
  }

Criar (caso NÃO esteja usando Simples Nacional)
===============================================

::

  POST /api/v1/tax_operations

Request::

  {
    "tax_operation": {
      "name": "teste 3",
      "cfop": "5102",
      "pis_cst": "01",
      "pis_aliquot": 0.65,
      "cofins_cst": "01",
      "cofins_aliquot": 3.0,
      "icms_cst": "00",
      "icms_aliquot": 18.0,
      "icms_reduction": 0.0,
      "benefit": null
    }
  }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *tax_operation*

  * *name*: Nome da operação fiscal.
  * *cfop*: Código Fiscal da Operação, CFOP da operação válido para NFe.
  * *pis_cst*: Código da situação tributário do PIS.
  * *pis_aliquot*: Aliquota do PIS.
  * *cofins_cst*: Código da situação tributário do COFINS.
  * *cofins_aliquot*: Alíquota do COFINS.
  * *icms_cst*: Código da situação tributário do ICMS.
  * *icms_aliquot*: Alíquota do ICMS.
  * *icms_reduction*: Alíquota redução da base de cálculo do ICMS.
  * *benefit*: Código de Benefício Fiscal.

Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criado com sucesso
======  ==================

Exemplo::

  {
    "id": 82,
    "created_at": "2021-03-16T12:32:34.083Z",
    "updated_at": "2021-03-16T12:32:34.083Z",
    "name": "Operação Fiscal 1",
    "cfop": "5102",
    "pis_cst": "01",
    "pis_aliquot": 0.65,
    "cofins_cst": "01",
    "cofins_aliquot": 3.0,
    "icms_cst": "00",
    "icms_aliquot": 18.0,
    "icms_reduction": 0.0,
    "benefit": null
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
401         não autorizado                        (vazio)
422         erro ao criar                         ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao criar

::

  {
    "name": [
      "já está em uso"
    ],
    "icms_cst": [
      "não pode ficar em branco"
    ],
    "pis_cst": [
      "não pode ficar em branco"
    ],
    "cofins_cst": [
      "não pode ficar em branco"
    ],
    "pis_aliquot": [
      "não é válido",
      "não é um número"
    ],
    "cofins_aliquot": [
      "não é válido",
      "não é um número"
    ],
    "icms_aliquot": [
      "não é válido",
      "não é um número"
    ],
    "icms_reduction": [
      "não é válido",
      "não é um número"
    ]
  }

Atualizar
=========

::

  PATCH /api/v1/tax_operations/[id]

Parâmetros de URL:
------------------

=========  =====================  ===========
parâmetro  descrição              obrigatório
=========  =====================  ===========
id         id da operação fiscal  sim
=========  =====================  ===========

Request::

  {
    "tax_operation": {
      "name": "Operação Fiscal 1 - Alterado"
    }
  }

Campos
------

Ao menos um campo interno a *tax_operation* deve ser passado.

Retorno
-------

======  ======================
status  descrição
======  ======================
200     Atualizado com sucesso
======  ======================

Exemplo::

  {
    "id": 82,
    "created_at": "2021-03-16T12:32:34.083Z",
    "updated_at": "2021-03-16T12:32:34.083Z",
    "name": "Operação Fiscal 1",
    "cfop": "5102",
    "pis_cst": "01",
    "pis_aliquot": 0.65,
    "cofins_cst": "01",
    "cofins_aliquot": 3.0,
    "icms_cst": "00",
    "icms_aliquot": 18.0,
    "icms_reduction": 0.0,
    "benefit": null
  }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
401         não autorizado                        (vazio)
404         operação fiscal não encontrada        { "status": "404", "error": "Not Found" }
422         erro ao atualizar                     ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao atualizar

::

  {
    "name": [
      "não pode ficar em branco"
    ]
  }

Excluir
=======

::

  DELETE /api/v1/tax_operations/[id]

Parâmetros de URL:
------------------

=========  =====================  ===========
parâmetro  descrição              obrigatório
=========  =====================  ===========
id         id da operação fiscal  sim
=========  =====================  ===========

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
404         operação fiscal não encontrada        { "status": "404", "error": "Not Found" }
==========  ====================================  ====================================================
