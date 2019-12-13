## Reversa técnica (void)

Necesitas enviar el **idToken** (en el header de la petición) para ejecutar una petición a la **API void** de la siguiente forma:

```
curl -X POST \
  https://chek-payments-engine-staging.heypay.cl/voids \
  -H 'Accept: */*' \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer ID_TOKEN' \
  -H 'Cache-Control: no-cache' \
  -H 'Connection: keep-alive' \
  -H 'Content-Length: 39' \
  -H 'Content-Type: application/json' \
  -H 'Host: chek-payments-engine-staging.heypay.cl' \
  -H 'cache-control: no-cache' \
  -d '{
	"chargeId": "ID_DEL_CARGO"
}'
```
Obtendras como respuesta:

```

```
