## 3. Generar Cobros (Charges)
A la hora de crear un cobro con QR es necesario definir el monto (amount), el mensaje (message), si se aceptan múltiples pagos (acceptsMultiplePayments), y si el QR es para múltiples ventas (keepAlive). En el caso de que el monto se envíe vacío, el cliente lo deberá ingresar a la hora de pagar.
Para el cobro remoto es necesario enviar el identificador del usuario, el monto y el mensaje. Solo el mensaje es opcional.
Si se requiere agregar información adicional al cobro se puede hacer a través del campo additionalData, el cual debe ser un JSON. Tener en cuenta que el cliente tendrá acceso a esta información.

Para generar un **charge** debes enviar:

```
curl -X POST \
  https://chek-payments-engine-staging.heypay.cl/charges \
  -H 'Accept: */*' \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer ID_TOKEN' \
  -H 'Cache-Control: no-cache' \
  -H 'Connection: keep-alive' \
  -H 'Content-Length: 161' \
  -H 'Content-Type: application/json' \
  -H 'Host: chek-payments-engine-staging.heypay.cl' \
  -d '{
	"currency": "CLP",
	"isAuthorization": false,
	"pointOfSaleId": "ID_DEL_PUNTO_DE_VENTA",
	"message": "Compra en comercio",
	"voidIn": 360000,
	"amount": 4990
}'
```
Obtendrás como respuesta:

```
{
    "id": "ID_DEL_CARGO",
    "resource": "https://chek-accounts-engine-staging.heypay.cl/charges/ID_DEL_CARGO"
}
```

### Consultar estado del **charge**

Luego que se crea el cobro se deberá consultar su estado múltiples veces hasta que el cliente realice el pago. Para verificar el estado de la transacción debes:

```
curl -X GET \
  https://chek-payments-engine-staging.heypay.cl/charges/ID_DEL_CARGO \
  -H 'Accept: */*' \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer ID_TOKEN' \
  -H 'Cache-Control: no-cache' \
  -H 'Connection: keep-alive' \
  -H 'Host: chek-payments-engine-staging.heypay.cl' \
```
Obtendrás como respuesta:
```
{
    "status": "pending",
    "redirectFromPointOfSales": false,
    "keepAlive": false,
    "createdAt": "2019-12-13T03:23:42.872Z",
    "requestTip": false,
    "fromAccountId": "CUENTA_DEL_CLIENTE",
    "voidIn": 360000,
    "updatedAt": "2019-12-13T03:23:42.872Z",
    "pointOfSalesId": "ID_DEL_PUNTO_DE_VENTA",
    "acceptsMultiplePayments": false,
    "commerceId": "ID_DEL_COMERCIO",
    "amount": 4990,
    "type": "ftf",
    "isAuthorization": false,
    "toAccountId": null,
    "additionalData": null,
    "message": "Compra en comercio",
    "payedAt": null,
    "capturedAt": null,
    "scheduledVoidAt": "2019-12-13T03:29:42.840Z",
    "payerInfo": null,
    "voidId": null,
    "onUpdateCallback": "https://chek-payments-engine-staging.heypay.cl/chargeUpdates",
    "currency": "CLP",
    "voidedAt": null,
    "rejectedAt": null,
    "requesterInfo": {
        "name": "Prueba",
        "type": "Cpmercio"
    },
    "authorizedAt": null,
    "authorizationId": null,
    "paymentId": null,
    "onCreateEventId": "Identificador",
    "transactionId": null
}
```
Descripción de los campos:
  
| Atributo | Tipo | Definición                               |
| -------- | ---- | ---------------------------------------- |
| acceptsMultiplePayments  | boolean | Acepta múltiples pagos por venta? El valor por defecto es false |
| amount | number |  Monto a cobrar. Si se deja vacío, permite que el cliente ingrese al pagar o autorizar |
| isAuthorization | boolean | Permite autorización directa o captura de fondos para autorización posterior. El valor por defecto es false |
| message | string | El asunto del cobro. Si se deja vacío, permite que el cliente lo ingrese al pagar o autorizar  |
| pointOfSalesId | Tipo | Identificador del punto de venta asociado al cobro |
| keepAlive | boolean | Permite el múltiples ventas sobre el mismo cargo. El valor por defecto es false.  |
| userPhoneNumber | string | Número de teléfono del usuario a cobrar en caso de realizar un cobro remoto. Ej: +56973981014 |
| voidIn | number | Milisegundos que deben pasar desde su creación para ser automáticamente anulado en caso que no se haya pagado (aunque esté autorizado). Su valor por defecto es 300000 (5 minutos). Si se envía null el cobro no se anulará automáticamente.  |
| keepAlive | boolean | Permite el múltiples ventas sobre el mismo cargo. El valor por defecto es false.  |

Al realizarse el pago, el identificador y la fecha del pago quedan guardados en el cobro. Con el identificador del pago se puede consultar la información respectiva a éste tales como la cuenta de origen y el perfil del cliente. En el caso que el cobro haya sido con el monto a definir por el cliente, este también se guardará en el cobro en el campo amount.

Los posibles estados de la transacción son:
  
| Status    | Definición                               |
| -------- | ---------------------------------------- |
| done  | El cargo fue realizado exitosamente en la cuenta Chek del cliente |
| pending | El cargo no ha sido confirmado por el cliente desde su app |
| voided | El cargo ha sido reversado porque se ha cumplido el tiempo parametrizado en el **voidIn**  |
| rejected | El cliente rechazó el cargo  |
| failed | Hubo un error al pagar |


Si deseas hacer un reembolso al cliente, debes llamar al [Reembolso (refund)](refund.md) o si deseas generar una reversa tecnica puedes llamar a la [Reversa (void)](void.md).


