###################
Ativos
###################

Listar
======

::

    GET /api/v1/device_configs

Filtros
-------

Os parâmetros abaixo podem ser passados como uma
`query string <https://en.wikipedia.org/wiki/Query_string>`_. Mais de um filtro
pode ser passado na mesma consulta.

Este serviço suporta `paginação <../overview.html#paginacao>`_.

* **location_id**: o id do local dos ativos.

  * Se passado, a consulta retorna somente ativos deste local.

* **machine_id**: o id da máquina dos ativos.

  * Se passado, a consulta retorna somente ativos desta máquina.

* **equipment_id**: o id do equipamento dos ativos.

  * Se passado, a consulta retorna somente ativos relacionados a esse equipamento.

* **kind**: o tipo do ativo.

  * Se passado, a consulta retorna somente ativos deste tipo.
  * Os valores aceitos são "coin", "bill", "pinpad", "wifi" e "modem", que correspondem a Moedeiro, Noteiro, Pinpad, Wi-Fi e Modem, respectivamente. Qualquer outro valor não surtirá efeito para filtragem.

* **serial_number**: o número serial do ativo.

  * Se passado, a consulta retorna somente ativos com número serial semelhante a este.

* **model_number**: o número do modelo do ativo.

  * Se passado, a consulta retorna somente ativos com número de modelo semelhante a este.

* **manufacturer**: o fabricante do ativo.

  * Se passado, a consulta retorna somente ativos cujo fabricante é semelhante a este.

* **active_installations_only**: pode ser *true* ou *false*. Se for *true*, apenas os ativos de instalações ativas serão listadas; se for *false*, qualquer instalação é listada.

  * Caso não seja passado, é considerado *true*.

Retorno
-------

É retornado um `JSON <https://en.wikipedia.org/wiki/JSON>`_ contendo um array com objetos que correspondem aos ativos. O array é ordenado por nome do local em que se encontra a instalação cujo ativo está relacionado. O campos de cada ativo são os seguintes:

* **id**: o id do ativo.
* **installation_id**: o id da instalação do ativo.
* **location_id**: o id do local do ativo.
* **machine_id**: o id da máquina do ativo.
* **vmbox**: o número de etiqueta e o número de série do equipamento.
* **kind**: o tipo do ativo.
* **serial_number**: o número serial do ativo.
* **model_number**: o número do modelo do ativo.
* **manufacturer**: o fabricante do ativo.
* **location**: detalhes do local do ativo.
* **machine**: detalhes da máquina do ativo.

Segue um exemplo de retorno de consulta:

::

    [
      {
        "id":123489,
        "installation_id":4,
        "location_id":2,
        "machine_id":3,
        "vmbox":"0422 (70B3D5CB8047)",
        "kind":"pinpad",
        "serial_number":"7121641505007192",
        "model_number":"PPC920;10MB;UC",
        "manufacturer":null,
        "location": {
          "client_id":1,
          "name":"Location X"
        },
        "machine": {
          "machine_model_id":9,
          "asset_number":"123"
        }
      },
      {
        "id":123456,
        "installation_id":5,
        "location_id":3,
        "machine_id":4,
        "vmbox":"2001/01463 (70B3D5CB8285)",
        "kind":"bill",
        "serial_number":"",
        "model_number":"",
        "manufacturer":"GERTEC"
        "location": {
          "client_id":2703,
          "name":"Espaço de convivência"
        },
        "machine": {
          "machine_model_id":80,
          "asset_number":"0010"
        }
      }
    ]
