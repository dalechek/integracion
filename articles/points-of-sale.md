## 2. Generar punto(s) de venta
Para ciertas situaciones es necesaria la generación de un cobro para cada venta manteniendo el mismo QR. A esto le llamamos puntos de venta, estos pueden ser utilizados en comercios con múltiples cajas de pago.

Con el idToken generado en el paso 1 [Autenticación](autentication.md) debemos crear el punto de venta para crear cobros relacionados a él. El único campo obligatorio es el nombre (name). Si se desea agregar informacional adicional se puede hacer a través del campo additionalData, el cual debe ser un JSON. A diferencia de los cobros, los clientes no tendrán acceso a esta información.

```
curl -X POST \
  https://chek-payments-engine-staging.heypay.cl/pointsOfSales \
  -H 'Accept: */*' \
  -H 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IjA0NjUxMTM5ZDg4NzUyYjY0OTM0MjUzNGE2YjRhMDUxMjVkNzhmYmIiLCJ0eXAiOiJKV1QifQ.eyJjaGFubmVsIjoib3Blbi1hcGkiLCJhY2NvdW50c19wcml2aWxlZ2VzIjp7IjFFT2RVbkRnRHZkdXRSektHZ1VOIjpbImFkbWluIl19LCJpc3MiOiJodHRwczovL3NlY3VyZXRva2VuLmdvb2dsZS5jb20vY2hlay1hY2NvdW50cy1lbmdpbmUtc3RhZ2luZyIsImF1ZCI6ImNoZWstYWNjb3VudHMtZW5naW5lLXN0YWdpbmciLCJhdXRoX3RpbWUiOjE1NzU2MDY4NDksInVzZXJfaWQiOiJFdEVmVmE2QTRadUxCNkdvOWJETy1hZG1pbiIsInN1YiI6IkV0RWZWYTZBNFp1TEI2R285YkRPLWFkbWluIiwiaWF0IjoxNTc1NjA2ODQ5LCJleHAiOjE1NzU2MTA0NDksImZpcmViYXNlIjp7ImlkZW50aXRpZXMiOnt9LCJzaWduX2luX3Byb3ZpZGVyIjoiY3VzdG9tIn19.D-7niFV_3JJX5cnVXYKoUKyz6liHybNhsTTDdicr5Wajzg3oVuaQrnMMcyZjKSRKCtromQxqS6FQiWSK91L4cZlOOj9hMaXEHAqiobZL3z-KCKL6-9zNIWi7zcqhbHznBaTkhE3LR5wsnqRWIr0MQxvAfwRK6QA_3RtJ105yrhmhh7aYKKNNRB4DTpez5HDYS1yjXMSfcY42ODWx1X9Sq9zLkf6_x8mi-V9iVOsfC9r05cbFGftF4fa0Y3KM4X-XsNQFUEwgyK01dSf6SO2so9HZ4jxG0HNDDrMvAIhKUaUEmlzfZRuTuGo7snQAB9GW5uDlRcgL7yVp6VyMEqp88Q' \
  -H 'Connection: keep-alive' \
  -H 'Content-Length: 21' \
  -H 'Content-Type: application/json' \
  -H 'Host: chek-payments-engine-staging.heypay.cl' \
  -d '{
	"name": "Caja Ejemplo"
}'
```

Como respuesta obtendrás el **id** del punto de venta y la url con la que podras generar el código QR para imprimir y colocar en la caja:

```
{
    "id": "5QEkVOY3iHsPWGvK5xRU",
    "resource": "https://chek-payments-engine-staging.heypay.cl/pointsOfSales/5QEkVOY3iHsPWGvK5xRU"
}
```
