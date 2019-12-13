## Reembolso (refund)

Necesitas enviar el **idToken** (en el header de la petición) para ejecutar una petición a la **API de refund** de la siguiente forma:

```
curl -X POST \
  https://chek-payments-engine-staging.heypay.cl/refunds \
  -H 'Accept: */*' \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer ID_TOKEN' \
  -H 'Cache-Control: no-cache' \
  -H 'Connection: keep-alive' \
  -H 'Content-Length: 80' \
  -H 'Content-Type: application/json' \
  -H 'Host: chek-payments-engine-staging.heypay.cl' \
  -H 'cache-control: no-cache' \
  -d '{
	"amount": 4990,
	"paymentId": "ID_DEL_PAGO",
	"transactionId": "001"
}'
```
Obtendras como respuesta:

```

```
