# Credit

## Credit Resource

The `Credit` resource represents the credits created on behalf of the customer `Account`. Credits are tracked inside invoices, as a specical kind of
of invoice item. The credits are visible at the level of the `Account`, i.e account credit, and those will automatically be consumed by the system on
subsequent invoices to bring the balance to zero -- or reduce the balance if there is not enough credit to pay the full amount.

The attributes are the following:

* **`creditId`** <span style="color:#32A9C7">*[System generated, immutable]*</span>: The `ID` allocated by Kill Bill upon creation.
* **`invoiceId`** <span style="color:#32A9C7">*[System or User generated, immutable]*</span>. If the `ID` is specified during creation, the credit will go against a specific invoice, provided this invoice has not yet been `COMMITTED`.
* **`accountId`** <span style="color:#32A9C7">*[System generated, immutable]*</span>. The `ID` allocated by Kill Bill upon creation.
* **`creditAmount`** <span style="color:#32A9C7">*[User generated]*</span>. 
* **`currency`** <span style="color:#32A9C7">*[User generated]*</span>
* **`invoiceNumber`** <span style="color:#32A9C7">*[System generated, immutable]*</span>
* **`effectiveDate`** <span style="color:#32A9C7">*[User generated]*</span>
* **`description`** <span style="color:#32A9C7">*[User generated]*</span>
* **`itemDetails`** <span style="color:#32A9C7">*[User or system generated]*</span>


## Create a credit

**HTTP Request** 

`POST http://example.com/1.0/kb/credits`

> Example Request:

```shell
TODO	
```

```java
import org.killbill.billing.client.api.gen.CreditApi;
protected CreditApi creditApi;

UUID accountId = UUID.fromString("864c1418-e768-4cd5-a0db-67537144b685");

Credit credit = new Credit();
credit.setAccountId(accountId);
credit.setCreditAmount(BigDecimal.ONE);
credit.setDescription("description");
credit.setItemDetails("itemDetails");

Boolean autoCommit = false;
Map<String, String> pluginProperty = null;

creditApi.createCredit(credit, 
                       autoCommit,
                       pluginProperty,
                       requestOptions);
```

```ruby
credit_item                 = KillBillClient::Model::Credit.new()
credit_item.account_id      = 'da3769a8-58c4-4dc0-b4e8-7b534e349624'
credit_item.credit_amount   = 50.0
credit_item.currency        = 'USD'
credit_item.description     = 'description'

auto_commit = true

credit_item.create(auto_commit, 
                   user,
                   reason,
                   comment,
                   options)
```

```python
creditApi = killbill.api.CreditApi()
body = Credit(account_id=account_id, 
              credit_amount=50.0, 
              currency='USD', 
              description='example')

creditApi.create_credit(body, created_by, api_key, api_secret)
```

> Example Response:

```java
class Credit {
    org.killbill.billing.client.model.gen.Credit@a32400a5
    creditId: d2edf4c0-9929-4e2f-b3a9-feb9bd9d60ba
    creditAmount: 1.00
    currency: USD
    invoiceId: 41c87837-ec1d-4095-8d20-a56e6237cb0c
    invoiceNumber: 3
    effectiveDate: 2012-09-26
    accountId: 7cf30d01-84f1-4d9d-94c2-3a3277374960
    description: description
    itemDetails: itemDetails
    auditLogs: []
}
```
```ruby
{
   "creditId":"fd5669a8-68c1-8dl0-m4e8-8y535e349324"
   "creditAmount":50.0,
   "currency":"USD",
   "invoiceId":"c57e1a2b-1a6b-4053-be2c-cc5fad2b5cbf",
   "invoiceNumber":"1285",
   "effectiveDate":"2013-08-01",
   "accountId":"da3769a8-58c4-4dc0-b4e8-7b534e349624",
   "description":"description"
}
```
```python
no content
```

**Query Parameters**

| Name | Type | Required | Description |
| ---- | -----| -------- | ----------- |
| **autoCommit** | boolean | true | auto commit |

**Returns**

Returns a credit object.

## Retrieve a credit by id

**HTTP Request** 

`GET http://example.com/1.0/kb/credits/{creditId}`

> Example Request:

```shell
TODO	
```

```java
import org.killbill.billing.client.api.gen.CreditApi;
protected CreditApi creditApi;

UUID creditId = UUID.fromString("d2edf4c0-9929-4e2f-b3a9-feb9bd9d60ba");

Credit result = creditApi.getCredit(creditId, requestOptions)
```

```ruby
credit_id = 'fd5669a8-68c1-8dl0-m4e8-8y535e349324'

KillBillClient::Model::Credit.find_by_id(credit_id , options)
```

```python
creditApi = killbill.api.CreditApi()
        
creditApi.get_credit(credit_id, api_key, api_secret)
```
> Example Response:

```java
class Credit {
    org.killbill.billing.client.model.gen.Credit@a32400a5
    creditId: d2edf4c0-9929-4e2f-b3a9-feb9bd9d60ba
    creditAmount: 1.00
    currency: USD
    invoiceId: 41c87837-ec1d-4095-8d20-a56e6237cb0c
    invoiceNumber: 3
    effectiveDate: 2012-09-26
    accountId: 7cf30d01-84f1-4d9d-94c2-3a3277374960
    description: description
    itemDetails: itemDetails
    auditLogs: []
}
```
```ruby
{
   "creditId":"fd5669a8-68c1-8dl0-m4e8-8y535e349324"
   "creditAmount":50.0,
   "currency":"USD",
   "invoiceId":"c57e1a2b-1a6b-4053-be2c-cc5fad2b5cbf",
   "invoiceNumber":"1285",
   "effectiveDate":"2013-08-01",
   "accountId":"da3769a8-58c4-4dc0-b4e8-7b534e349624",
   "description":"description"
}
```
```python
{'credit_id' : 'fd5669a8-68c1-8dl0-m4e8-8y535e349328'
 'account_id': 'da3769a8-58c4-4dc0-b4e8-7b534e349624',
 'credit_amount': 50.0,
 'currency': 'USD',
 'description': 'example',
 'effective_date': datetime.datetime(2018, 5, 3, 15, 53, 44, tzinfo=tzutc()),,
 'invoice_id': 'c57e1a2b-1a6b-4053-be2c-cc5fad2b5cbf',
 'invoice_number': '1285'
}
```

**Query Parameters**

None.

**Returns**

Returns a credit object.