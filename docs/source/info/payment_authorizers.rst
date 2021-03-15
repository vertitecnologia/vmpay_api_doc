####################
Autorizadores QRCode
####################

Listar
======

::

  GET /api/v1/payment_authorizers

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
      "id": 1,
      "name": "VMpay"
    },
    {
      "id": 2,
      "name": "PicPay"
    },
    {
      "id": 3,
      "name": "Mercado Pago"
    }
  ]
