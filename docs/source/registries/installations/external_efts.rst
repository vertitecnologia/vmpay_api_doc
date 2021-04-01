############################
Transações cashless externas
############################

Criar
=====

Cria uma transação cashless externa.

::

  POST /api/v1/machines/[machine_id]/installations/[installation_id]/external_efts

Parâmetros de URL:
------------------

===============  ================  ===========
parâmetro        descrição         obrigatório
===============  ================  ===========
machine_id       id da máquina     sim
installation_id  id da instalação  sim
===============  ================  ===========

Request::

  {
    "items": [
      {
        "physical_locator": "10",
        "value": 5.00,
        "quantity": 1
      },
      {
        "physical_locator": "11",
        "value": 4.50,
        "quantity": 2
      }
    ],
    "payment": {
      "success": true,
      "request_number": "123456789",
      "eft_provider_id": 123,
      "eft_authorizer_id": 123,
      "eft_card_brand_id": 123,
      "eft_card_type_id": 123,
      "masked_card_number": "123456******6789",
      "cpf": "12345678901",
      "cancel_code": "A01",
      "cancel_reason": "Motivo da falha"
    }
  }

Campos
------

* *items*: os itens da transação.

  * *physical_locator*: o número do item no planograma. É o identificador **físico** do item.

  * *value*: o valor **total** do item.

  * *quantity*: a quantidade vendida. Se não for informada, considera-se 1.

* *payment*: os dados de pagamento.

  * *success*: se a transação foi bem-sucedida ou não.

  * *request_number*: o número da requisição.

  * *eft_provider_id*: o id do Provedor TEF. Se não informado, será considerado como indefinido.

  * *eft_authorizer_id*: o id do Adquirente TEF. Se não informado, será considerado como indefinido.

  * *eft_card_brand_id*: o id da Bandeira de Cartão. Se não informado, será considerado como indefinido.

  * *eft_card_type_id*: o id do Tipo de Cartão. Se não informado, será considerado como indefinido.

  * *masked_card_number*: O número mascarado do cartão.

  * *cpf*: o CPF do comprador. Não é obrigatório.

  * *cancel_code*: o código do erro. Somente é considerado se *success* for *false*; caso contrário, é desconsiderado.

  * *cancel_reason*: a descrição do erro. Somente é considerada se *success* for *false*; caso contrário, é desconsiderada.

Retorno
-------

======  ==================
status  descrição
======  ==================
201     Criado com sucesso
======  ==================

Erros
-----

==========  ====================================  ====================================================
status      descrição                             response body
==========  ====================================  ====================================================
400         parâmetros faltando                   { "status": "400", "error": "Bad Request" }
404         máquina/instalação não encontrada     { "status": "404", "error": "Not Found" }
422         erro ao criar                         ver exemplo abaixo
==========  ====================================  ====================================================

422 - erro ao criar

::

  {
    "error": "Esta instalação não aceita transações cashless externas"
  }
