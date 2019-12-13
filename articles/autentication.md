## 1. Autenticación

Una vez completes el registro de tu Comercio, te entregaremos credenciales para que te puedas autenticar en el sistema:

**"commerceId"** y **"apiKey"**

Con estas podrás llamar a la API **tokens** así:

```
curl -X POST \
  https://chek-payments-engine-staging.heypay.cl/tokens \
  -H 'Content-Type: application/json' \
  -d '{
	"commerceId": "ID DEL COMERCIO",
	"apiKey": "LLAVE DEL COMERCIO"
}'
```

> Debes reemplazar **ID DEL COMERCIO** y **LLAVE DEL COMERCIO** por los entregados al confirmar el alta.

Como respuesta obtendrás el **token**:

```
{
    "token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL2lkZW50aXR5dG9vbGtpdC5nb29nbGVhcGlzLmNvbS9nb29nbGUuaWRlbnRpdHkuaWRlbnRpdHl0b29sa2l0LnYxLklkZW50aXR5VG9vbGtpdCIsImlhdCI6MTU3NjIwNDU1MSwiZXhwIjoxNTc2MjA4MTUxLCJpc3MiOiJjaGVrLWFjY291bnRzLWVuZ2luZS1zdGFnaW5nQGFwcHNwb3QuZ3NlcnZpY2VhY2NvdW50LmNvbSIsInN1YiI6ImNoZWstYWNjb3VudHMtZW5naW5lLXN0YWdpbmdAYXBwc3BvdC5nc2VydmljZWFjY291bnQuY29tIiwidWlkIjoiRXRFZlZhNkE0WnVMQjZHbzliRE8tYWRtaW4iLCJjbGFpbXMiOnsiY2hhbm5lbCI6Im9wZW4tYXBpIiwiYWNjb3VudHNfcHJpdmlsZWdlcyI6eyIxRU9kVW5EZ0R2ZHV0UnpLR2dVTiI6WyJhZG1pbiJdfX19.OiZhQ9IybZYYYkllSuFcTyfjG5globHBIBl3lQMru-rkQiK7A66tFPPWYngRi-sXC-il54o1-hhnw24R_Fk-W85hrXJgVv0NipTFszHfQ7jdhTNDL-l_RKueDR4FQA6t_2nY1pSSaW8xTU1wT7-5IQVuFf0xnoG6gaDBd8DStQUP9FBusFs5_xknDs1tncXMAotWmZ0LFt6juDTErTYg7CaO420RrXuwM15D8MLUKwLS3UtKE5rleAN2g0iONv-KnUWLtQ47Gi0jLFlm-6SLtlpQgnXM1CUB3cfII_uUaeD9Anzy37mET-6GC3eYGAk0txH515XNX30Dn9UasQ_Fwg"
}
```

### Para disminuir el uso de tus credenciales, y con esto aumentar la seguridad en las llamadas a nuestras APIs debes llamar al **idToken** a partir del **token** generado en el paso anterior.

Generar **idToken**:

```
curl -X POST \
  https://chek-payments-engine-staging.heypay.cl/idTokens \
  -H 'Accept: */*' \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Connection: keep-alive' \
  -H 'Content-Length: 911' \
  -H 'Content-Type: application/json' \
  -H 'Host: chek-payments-engine-staging.heypay.cl' \
  -H 'Postman-Token: b2a0ca15-3c39-4058-8e1d-2e196a69ca5e,c32273d0-525d-4c33-87d3-8f6922c89300' \
  -d '{
	"token":"TOKEN"
```

Obtendrás como respuesta:

```
{
    "idToken": "ID_TOKEN",
    "refreshToken": "REFRESH_TOKEN",
    "expiresIn": 3600
}
```
Con este **idToken** podrás autenticarte en todas nuestras APIs.


> Si deseas evitar recurrencia en la generación del **idToken**, puedes refrescarlo constantemente llamando al **refreshToken** así:

```
curl -X POST \
  https://chek-payments-engine-staging.heypay.cl/refreshTokens \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
	"refreshToken":"REFRESH_TOKEN"
}'
```
Recursos

| Método   | Definición | Atributo | Tipo   | Descripción         |
| -------- | ---------- |--------- |------- |-------------------- |
| POST     | Request    | apiKey   | string |Api key del comercio |

commerceId
string
Identificador del comercio.
readOnly
boolean
Si brindar solo permisos de lectura a los idTokens generados por el token a crear. El valor por defecto es false.
Response
token
string
Token que permite autentificarse en la API.


Ir al paso [2. Generar Punto(s) de venta](points-of-sale.md)
