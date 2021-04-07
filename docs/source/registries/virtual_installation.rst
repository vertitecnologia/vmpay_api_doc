####################
Instalações Virtuais
####################

Instalações Virtuais são as que não possuem uma vending machine e, por
consequência, uma VMbox. Tais instalações são utilizadas em micro markets.

Com exceção da criação e da atualização, pode-se utilizar também os serviços em
`Instalações <./installation.html>`__ para operar sobre estas instalações.

Listar
======

Lista as instalações virtuais de determinada máquina.

::

  GET /api/v1/machines/[machine_id]/virtual_installations

Parâmetros de URL:
------------------

==========  ===============  ===========
parâmetro   descrição        obrigatório
==========  ===============  ===========
machine_id  id da máquina    sim
==========  ===============  ===========

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
        "id": 1234,
        "created_at": "2020-10-19T12:34:56.000-03:00",
        "updated_at": "2020-10-19T12:56:34.000-03:00",
        "location_id": 56,
        "machine_id": 678,
        "equipment_id": 4321,
        "place": "Micro market",
        "notifications_enabled": true,
        "virtual_equipment": true,
        "issues_invoice": true,
        "enable_market_app": true,
        "enable_restricted_door_control": true,
        "enable_external_eft": true
      },
      {
        "id": 1236,
        "created_at": "2020-10-20T12:34:56.000-03:00",
        "updated_at": "2020-10-20T12:56:34.000-03:00",
        "location_id": 2345,
        "machine_id": 8654,
        "equipment_id": 4389,
        "place": "Sala do mercado",
        "notifications_enabled": true,
        "virtual_equipment": true,
        "issues_invoice": false,
        "enable_market_app": true,
        "enable_restricted_door_control": false,
        "enable_external_eft": false
      }
    ]

Ver
===

Mostra determinada instalação de uma máquina.

::

  GET /api/v1/machines/[machine_id]/virtual_installations/[id]

Parâmetros de URL:
------------------

==========  ================  ===========
parâmetro   descrição         obrigatório
==========  ================  ===========
machine_id  id da máquina     sim
id          id da instalação  sim
==========  ================  ===========

Retorno
-------

======  =========
status  descrição
======  =========
200     OK
======  =========

* O campo *issues_invoice* indica se são emitidas NFCe depois da compra. Este campo só é retornado se o operator suportar a emissão.
* O campo *enable_market_app* indica se esta instalação irá aparecer no app VMmarket. Este campo só é retornado se o operator estiver configurado.
* O campo *enable_restricted_door_control* indica se esta instalação possui uma porta de controle de acesso a produtos restritos a maiores de idade e se o app VMmarket irá controlar a sua destrava. Este campo só é retornado se o operator estiver configurado.
* O campo *enable_external_eft* indica se a API de Transações cashless externas está habilitada para esta instalação.

::

    {
      "id": 1234,
      "created_at": "2020-10-19T12:34:56.000-03:00",
      "updated_at": "2020-10-19T12:56:34.000-03:00",
      "location_id": 56,
      "machine_id": 678,
      "equipment_id": 4321,
      "place": "Micro market",
      "notifications_enabled": true,
      "virtual_equipment": true,
      "issues_invoice": true,
      "enable_market_app": true,
      "enable_restricted_door_control": true,
      "enable_external_eft": true,
      "pending_planogram": null,
      "current_planogram": {
        "id": 1235678,
        "created_at": "2020-10-19T12:34:56.000-03:00",
        "updated_at": "2020-10-19T12:34:56.000-03:00",
        "due": "now",
        "started_at": "2020-10-19T12:34:56.000-03:00",
        "items": [
          {
            "id": 346354,
            "type": "Coil",
            "name": "1",
            "good_id": 1234,
            "capacity": 20,
            "par_level": 20,
            "alert_level": 4,
            "desired_price": 5.0,
            "logical_locator": 1,
            "physical_locators":[
              "1"
            ],
            "current_balance": 15.0
          },
          {
            "id": 346355,
            "type": "Coil",
            "name": "2",
            "good_id": 1237,
            "capacity": 10,
            "par_level": 10,
            "alert_level": 2,
            "desired_price": 7.8,
            "logical_locator": 2,
            "physical_locators":[
              "2"
            ],
            "current_balance": 9.0
          }
        ]
      }
    }

Erros
-----

==========  ====================================  ================
status      descrição                             response body
==========  ====================================  ================
404         máquina ou instalação não encontrada  (vazio)
==========  ====================================  ================

Criar
=====

Cria uma nova instalação virtual em determinada máquina.

Se a máquina já possuir uma instalação ativa (virtual ou não), a mesma é baixada automaticamente na data e hora atuais. A instalação criada torna-se a ativa.

::

  POST /api/v1/machines/[machine_id]/virtual_installations

Parâmetros de URL:
------------------

==========  ===============  ===========
parâmetro   descrição        obrigatório
==========  ===============  ===========
machine_id  id da máquina    sim
==========  ===============  ===========

Request::

    {
      "installation": {
        "location_id": 56,
        "place": "Micro market",
        "notifications_enabled": true,
        "issues_invoice": true,
        "enable_market_app": true,
        "enable_restricted_door_control": true,
        "enable_external_eft": true,
        "planograms_attributes": [
          {
            "items_attributes": [
              {
                "type": "Coil",
                "name": "1",
                "good_id": 1234,
                "capacity": 20,
                "par_level": 20,
                "alert_level": 4,
                "desired_price": 5.0,
                "logical_locator": 1
              },
              {
                "type": "Coil",
                "name": "2",
                "good_id": 1237,
                "capacity": 10,
                "par_level": 10,
                "alert_level": 2,
                "desired_price": 7.8,
                "logical_locator": 2
              }
            ]
          }
        ]
      }
    }

Campos
------

Obrigatórios
^^^^^^^^^^^^

* *installation*

  * *location_id*: id do local.
  * *equipment_id*: id do equipamento.
  * *notifications_enabled*: enviar notificações?
  * *planograms_attributes*: os planogramas da instalação. Nesse caso, somente um planograma é preenchido: o inicial. Para detalhes, ver `Instalações <./installation.html#criar>`__.

Opcionais
^^^^^^^^^

* *installation*

  * *place*: local interno.
  * *issues_invoice*: emitir NFCe?

    * Valor será ignorado a menos que o operador tenha suporte à emissão de NFCe.
  * *enable_market_app*: Habilitar app market?

    * Valor será ignorado a menos que o operador tenha suporte ao app market.
  * *enable_restricted_door_control*: Habilitar controle de porta 18+?

    * Valor será ignorado a menos que o operador tenha suporte ao app market.
  * *enable_external_eft*: Habilitar TEF externo?

    * Valor será ignorado a menos que o operador tenha suporte a esta funcionalidade.

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
      "id": 1234,
      "created_at": "2020-10-19T12:34:56.000-03:00",
      "updated_at": "2020-10-19T12:56:34.000-03:00",
      "location_id": 56,
      "machine_id": 678,
      "equipment_id": 4321,
      "place": "Micro market",
      "notifications_enabled": true,
      "virtual_equipment": true,
      "issues_invoice": true,
      "enable_market_app": true,
      "enable_restricted_door_control": true,
      "enable_external_eft": true,
      "pending_planogram": null,
      "current_planogram": {
        "id": 1235678,
        "created_at": "2020-10-19T12:34:56.000-03:00",
        "updated_at": "2020-10-19T12:34:56.000-03:00",
        "due": "now",
        "started_at": "2020-10-19T12:34:56.000-03:00",
        "items": [
          {
            "id": 346354,
            "type": "Coil",
            "name": "1",
            "good_id": 1234,
            "capacity": 20,
            "par_level": 20,
            "alert_level": 4,
            "desired_price": 5.0,
            "logical_locator": 1,
            "physical_locators":[
              "1"
            ],
            "current_balance": 15.0
          },
          {
            "id": 346355,
            "type": "Coil",
            "name": "2",
            "good_id": 1237,
            "capacity": 10,
            "par_level": 10,
            "alert_level": 2,
            "desired_price": 7.8,
            "logical_locator": 2,
            "physical_locators":[
              "2"
            ],
            "current_balance": 9.0
          }
        ]
      }
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
    "location_id": [
      "não pode ficar em branco"
    ]
  }

Atualizar
=========

Atualiza uma instalação virtual de determinada máquina.

::

  PATCH /api/v1/machines/[machine_id]/virtual_installations/[id]

Parâmetros de URL:
------------------

==========  ================  ===========
parâmetro   descrição         obrigatório
==========  ================  ===========
machine_id  id da máquina     sim
id          id da instalação  sim
==========  ================  ===========

Request::

  {
    "installation": {
      "location_id": 56,
      "place": "Micro market",
      "notifications_enabled": true,
      "issues_invoice": true,
      "enable_market_app": true,
      "enable_restricted_door_control": true,
      "enable_external_eft": true
    }
  }

Campos
------

Ao menos um campo interno a *installation* deve ser passado.

Não é permitido atualizar um planograma ativo, somente cadastrar um outro planograma pendente. Para tanto, ver Planogramas.

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
      "id": 1234,
      "created_at": "2020-10-19T12:34:56.000-03:00",
      "updated_at": "2020-10-19T12:56:34.000-03:00",
      "location_id": 56,
      "machine_id": 678,
      "equipment_id": 4321,
      "place": "Micro market",
      "notifications_enabled": true,
      "virtual_equipment": true,
      "issues_invoice": true,
      "enable_market_app": true,
      "enable_restricted_door_control": true,
      "enable_external_eft": true,
      "pending_planogram": null,
      "current_planogram": {
        "id": 1235678,
        "created_at": "2020-10-19T12:34:56.000-03:00",
        "updated_at": "2020-10-19T12:34:56.000-03:00",
        "due": "now",
        "started_at": "2020-10-19T12:34:56.000-03:00",
        "items": [
          {
            "id": 346354,
            "type": "Coil",
            "name": "1",
            "good_id": 1234,
            "capacity": 20,
            "par_level": 20,
            "alert_level": 4,
            "desired_price": 5.0,
            "logical_locator": 1,
            "physical_locators":[
              "1"
            ],
            "current_balance": 15.0
          },
          {
            "id": 346355,
            "type": "Coil",
            "name": "2",
            "good_id": 1237,
            "capacity": 10,
            "par_level": 10,
            "alert_level": 2,
            "desired_price": 7.8,
            "logical_locator": 2,
            "physical_locators":[
              "2"
            ],
            "current_balance": 9.0
          }
        ]
      }
    }

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
401         não autorizado                        (vazio)
404         máquina ou instalação não encontrada  (vazio)
422         erro ao atualizar                     ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao atualizar:

::

  {
    "location_id": [
      "não é válido"
    ]
  }

Baixar
======

Baixa uma instalação virtual de determinada máquina.

::

  DELETE /api/v1/machines/[machine_id]/virtual_installations/[id]

Parâmetros de URL:
------------------

==========  ================  ===========
parâmetro   descrição         obrigatório
==========  ================  ===========
machine_id  id da máquina     sim
id          id da instalação  sim
==========  ================  ===========

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
401         não autorizado                        (vazio)
404         máquina ou instalação não encontrada  (vazio)
==========  ====================================  ====================================================

Reabastecer manualmente
=======================

Efetua o reabastecimento da pick list atualmente pendente, caso exista e a
operação seja permitida.

::

  POST /api/v1/machines/[machine_id]/virtual_installations/[id]/restock

Parâmetros de URL
-----------------

==========  ================  ===========
parâmetro   descrição         obrigatório
==========  ================  ===========
machine_id  id da máquina     sim
id          id da instalação  sim
==========  ================  ===========

Retorno
-------

======  ======================================
status  descrição
======  ======================================
200     Reabastecimento criado com sucesso
422     Não foi possível criar reabastecimento
======  ======================================
