#######
Visitas
#######

Listar
======

::

    GET /api/v1/visits

Filtros
-------

Os parâmetros abaixo podem ser passados como uma
`query string <https://en.wikipedia.org/wiki/Query_string>`_. Mais de um filtro
pode ser passado na mesma consulta.

Este serviço suporta `paginação <../overview.html#paginacao>`_.

* **start_date**: a data de início das visitas.

  * A consulta retorna somente visitas ocorridas a partir desta data e hora, inclusive.
  * Este filtro é **obrigatório**. Se não for passado, será retornado erro com o código HTTP 400 (*bad request*).
  * Se o formato da data for inválido, será retornado erro com o código HTTP 400 (*bad request*).
  * Se a data for maior que a do filtro *end_date*, será retornado erro com o código HTTP 400 (*bad request*).
  * Se a data for menor que 30 dias antes da data do filtro *end_date*, será retornado erro com o código HTTP 400 (*bad request*).
  * Deve-se passar a data e também a **hora**; se não for passada, será considerado **00:00:00** `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Os segundos passados na hora são desconsiderados. O sistema considera sempre **00**.
  * Um formato possível é *dd/mm/yyyy hh:mi*. Nesse caso a data e hora devem estar em `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Este filtro também suporta o formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.

* **end_date**: a data final das visitas.

  * A consulta retorna somente visitas ocorridas até esta data e hora, inclusive.
  * Este filtro é **obrigatório**. Se não for passado, será retornado erro com o código HTTP 400 (*bad request*).
  * Se o formato da data for inválido, será retornado erro com o código HTTP 400 (*bad request*).
  * Se a data for menor que a do filtro *start_date*, será retornado erro com o código HTTP 400 (*bad request*).
  * Se a data for maior que 30 dias depois da data do filtro *start_date*, será retornado erro com o código HTTP 400 (*bad request*).
  * Deve-se passar a data e também a **hora**; se não for passada, será considerado **23:59:59** `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Os segundos passados na hora são desconsiderados. O sistema considera sempre **59**.
  * Um formato possível é *dd/mm/yyyy hh:mi*. Nesse caso a data e hora devem estar em `UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`_.
  * Este filtro também suporta o formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.

* **restock**: pode ser *true* ou *false*. Se for *true*, apenas as visitas que foram reabastecimentos serão listadas; se for *false*, apenas as visitas que não foram reabastecimentos; se não for passado, retorna tanto um, quanto o outro. Pode ser usado juntamente com o filtro *cash_collect*.

* **cash_collect**: pode ser *true* ou *false*. Se for *true*, apenas as visitas que foram coletas serão listadas; se for *false*, apenas as visitas que não foram coletas; se não for passado, retorna tanto um, quanto o outro. Pode ser usado juntamente com o filtro *restock*.

* **location_id**: o id do local das visitas. Se passado, a consulta retorna somente visitas ocorridas neste local.

* **event_id**: o id do evento. Se passado, a consulta retorna somente a visita deste evento.

* **machine_id**: o id da máquina das visitas. Se passado, a consulta retorna somente visitas ocorridas nesta máquina.

* **machine_type_id**: o id do tipo de máquina das visitas. Se passado, a consulta retorna somente visitas ocorridas em máquinas deste tipo.

* **route_id**: o id da rota das visitas. Se passado, a consulta retorna somente visitas ocorridas em instalações pertencentes a esta rota.

Retorno
-------

É retornado um `JSON <https://en.wikipedia.org/wiki/JSON>`_ contendo um array com objetos que correspondem às visitas. O array é ordenado por data e hora de visita, da mais recente para a mais antiga. O campos de cada visita são os seguintes:

* **id**: o id da visita.
* **previous_session_id**: o id do caixa anterior à visita, se esta foi uma coleta. É o caixa que foi fechado pela coleta. Este campo será *null* caso a visita não tenha sido uma coleta.
* **occurred_at**: a data e hora da visita, no formato `ISO 8601 <https://en.wikipedia.org/wiki/ISO_8601>`_.
* **restock**: *true* se a visita foi um reabastecimento; *false*, caso contrário.
* **cash_collect**: *true* se a visita foi uma coleta; *false*, caso contrário.
* **event_id**: o id do evento da vista.
* **location_id**: o id do local da visita.
* **machine_id**: o id da máquina da visita.
* **installation_id**: o id da instalação da visita.
* **place**: o local interno da instalação da visita.
* **bill_value**: o valor total de notas coletadas na visita. Este campo será null caso a visita não seja uma coleta.
* **coin_value**: o valor total de moedas coletadas na visita. Este campo será null caso a visita não seja uma coleta.
* **total_value**: o valor total coletado na visita. Este campo será null caso a visita não seja uma coleta.
* **location**: detalhes do local da visita.
* **machine**: detalhes da máquina da visita.
* **routes**: array com detalhes das rotas da instalação da visita.

Segue um exemplo de retorno de consulta:

::

    [
      {
        "id":12345,
        "previous_session_id":null,
        "occurred_at":"2019-06-03T19:28:39.000Z",
        "restock":true,
        "cash_collect":false,
        "event_id":12345679,
        "location_id":123,
        "machine_id":321,
        "installation_id":1234,
        "place":"Recepção",
        "bill_value":null,
        "coin_value":null,
        "total_value":null,
        "location":{
          "id":123,
          "name":"Local 1"
        },
        "machine":{
          "id":321,
          "asset_number":"1423"
        },
        "routes":[
          {
            "id":1,
            "name":"Rota 1"
          },
          {
            "id":2,
            "name":"Rota 2"
          }
        ]
      },
      {
        "id":12345,
        "previous_session_id":567,
        "occurred_at":"2019-06-03T19:11:45.000Z",
        "restock":true,
        "cash_collect":true,
        "event_id":12345678,
        "location_id":321,
        "machine_id":123,
        "installation_id":2345,
        "place":"1° andar",
        "bill_value":82.00,
        "coin_value":65.50,
        "total_value":147.50,
        "location":{
          "id":321,
          "name":"Local 3"
        },
        "machine":{
          "id":123,
          "asset_number":"8572"
        },
        "routes":[
          {
            "id":2,
            "name":"Rota 2"
          }
        ]
      }
    ]
