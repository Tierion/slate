---
title: Boltwall API
language_tabs:
  - go: Go
  - http: HTTP
  - javascript: JavaScript
  - javascript--nodejs: Node.JS
  - python: Python
  - ruby: Ruby
toc_footers:
  - '<a href="https://tierion.github.io/boltwall/">External documentation</a>'
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<h1 id="boltwall-api">Boltwall API v2.0.0-beta-oas3</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

API Documentation for Boltwall - A middleware to enable self-sovereign paywalls for the new internet

Base URLs:

* <a href="https://tierion-boltwall.tierion.now.sh/">https://tierion-boltwall.tierion.now.sh/</a>

Email: <a href="mailto:buck@tierion.com">Support</a> 
License: <a href="https://opensource.org/licenses/MIT">MIT</a>

# Authentication

- HTTP Authentication, scheme: bearer LSAT Authorization header which requires prefix 'LSAT' followed by base64 encoded macaroon and the proof of payment (invoice preimage), separated by a colon

<h1 id="boltwall-api-default">Default</h1>

## getNodeInfo

<a id="opIdgetNodeInfo"></a>

> Code samples

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://tierion-boltwall.tierion.now.sh/api/node", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```http
GET https://tierion-boltwall.tierion.now.sh/api/node HTTP/1.1
Host: tierion-boltwall.tierion.now.sh
Accept: application/json

```

```javascript
var headers = {
  'Accept':'application/json'

};

$.ajax({
  url: 'https://tierion-boltwall.tierion.now.sh/api/node',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json'

};

fetch('https://tierion-boltwall.tierion.now.sh/api/node',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```python
import requests
headers = {
  'Accept': 'application/json'
}

r = requests.get('https://tierion-boltwall.tierion.now.sh/api/node', params={

}, headers = headers)

print r.json()

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json'
}

result = RestClient.get 'https://tierion-boltwall.tierion.now.sh/api/node',
  params: {
  }, headers: headers

p JSON.parse(result)

```

`GET /api/node`

*get information about the node*

Get information about the lightning node that is receiving payments. This is useful to get p2p level information, e.g. to create a direct channel with the node.

> Example responses

> 200 Response

```json
{
  "pubKey": "03cb9e0a30f17a7b75f3ac9e9f39909811805be22ad6044953220a3c35d2809418",
  "alias": "foobar node",
  "socket": "123.45.67.87:10009",
  "activeChannelsCount": 2,
  "peersCount": 1
}
```

<h3 id="getnodeinfo-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Useful information about the node.|[NodeInfo](#schemanodeinfo)|

<aside class="success">
This operation does not require authentication
</aside>

## getInvoice

<a id="opIdgetInvoice"></a>

> Code samples

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "id": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://tierion-boltwall.tierion.now.sh/api/invoice", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```http
GET https://tierion-boltwall.tierion.now.sh/api/invoice HTTP/1.1
Host: tierion-boltwall.tierion.now.sh
Accept: application/json
id: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'id':'string'

};

$.ajax({
  url: 'https://tierion-boltwall.tierion.now.sh/api/invoice',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'id':'string'

};

fetch('https://tierion-boltwall.tierion.now.sh/api/invoice',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'id': 'string'
}

r = requests.get('https://tierion-boltwall.tierion.now.sh/api/invoice', params={

}, headers = headers)

print r.json()

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'id' => 'string'
}

result = RestClient.get 'https://tierion-boltwall.tierion.now.sh/api/invoice',
  params: {
  }, headers: headers

p JSON.parse(result)

```

`GET /api/invoice`

*get status of a given invoice based on request LSAT*

Given an LSAT and invoice id, get the status of an invoice (i.e. is it paid or not)

<h3 id="getinvoice-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|id|header|string|false|Hex encoded string of invoice id. Can be optional if request has a cookie that contains a root macaroon attached which should include data referencing an invoice id.|

#### Detailed descriptions

**id**: Hex encoded string of invoice id. Can be optional if request has a cookie that contains a root macaroon attached which should include data referencing an invoice id.

> Example responses

> 200 Response

```json
{
  "id": "7cef93f2c51aa65208bec1447fc38fc58d9bce1375a532edb0dcd290a2c330ae",
  "payreq": "lntb10u1pw7kfm8pp50nhe8uk9r2n9yz97c9z8lsu0ckxehnsnwkjn9mdsmnffpgkrxzhqdq5w3jhxapqd9h8vmmfvdjscqzpg llq2qvdlgkllc27kpd87lz8pdfsfmtteyc3kwq734jpwnvqt96e4nuy0yauzdrtkumxsvawgda8dlljxu3nnjlhs6w75390wy7ukj6cpfmygah",
  "createdAt": "2020-01-09T18:13:31.241Z",
  "amount": 30,
  "status": "paid",
  "description": "example invoice description"
}
```

<h3 id="getinvoice-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Status of invoice and payreq string for reference|[InvoiceResponse](#schemainvoiceresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Missing invoice id, problem getting invoice|[ErrorMessage](#schemaerrormessage)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Request sent with an invalid LSAT|[ErrorMessage](#schemaerrormessage)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Invoice with given ID does not exist|[ErrorMessage](#schemaerrormessage)|

<aside class="success">
This operation does not require authentication
</aside>

## generateInvoice

<a id="opIdgenerateInvoice"></a>

> Code samples

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://tierion-boltwall.tierion.now.sh/api/invoice", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```http
POST https://tierion-boltwall.tierion.now.sh/api/invoice HTTP/1.1
Host: tierion-boltwall.tierion.now.sh
Content-Type: application/json
Accept: application/json

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

$.ajax({
  url: 'https://tierion-boltwall.tierion.now.sh/api/invoice',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');
const inputBody = '{
  "title": "string",
  "amount": 0,
  "time": 0,
  "expiresAt": "string",
  "appName": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'

};

fetch('https://tierion-boltwall.tierion.now.sh/api/invoice',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json'
}

r = requests.post('https://tierion-boltwall.tierion.now.sh/api/invoice', params={

}, headers = headers)

print r.json()

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json'
}

result = RestClient.post 'https://tierion-boltwall.tierion.now.sh/api/invoice',
  params: {
  }, headers: headers

p JSON.parse(result)

```

`POST /api/invoice`

*generate a new lightning invoice*

Given a set of metadata and a price, generate a new lightning invoice for sending a payment to.

> Body parameter

```json
{
  "title": "string",
  "amount": 0,
  "time": 0,
  "expiresAt": "string",
  "appName": "string"
}
```

<h3 id="generateinvoice-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[body](#schemabody)|false|creates a new invoice in our lightning node|

> Example responses

> 200 Response

```json
{
  "id": "7cef93f2c51aa65208bec1447fc38fc58d9bce1375a532edb0dcd290a2c330ae",
  "payreq": "lntb10u1pw7kfm8pp50nhe8uk9r2n9yz97c9z8lsu0ckxehnsnwkjn9mdsmnffpgkrxzhqdq5w3jhxapqd9h8vmmfvdjscqzpg llq2qvdlgkllc27kpd87lz8pdfsfmtteyc3kwq734jpwnvqt96e4nuy0yauzdrtkumxsvawgda8dlljxu3nnjlhs6w75390wy7ukj6cpfmygah",
  "createdAt": "2020-01-09T18:13:31.242Z",
  "amount": 30,
  "status": "paid",
  "description": "example invoice description"
}
```

<h3 id="generateinvoice-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A valid Invoice Response|[InvoiceResponse](#schemainvoiceresponse)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|error creating the invoice against a lightning node|None|

<aside class="success">
This operation does not require authentication
</aside>

## get__[protected]

> Code samples

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"*/*"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://tierion-boltwall.tierion.now.sh/[protected]", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

```http
GET https://tierion-boltwall.tierion.now.sh/[protected] HTTP/1.1
Host: tierion-boltwall.tierion.now.sh
Accept: */*

```

```javascript
var headers = {
  'Accept':'*/*'

};

$.ajax({
  url: 'https://tierion-boltwall.tierion.now.sh/[protected]',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'*/*'

};

fetch('https://tierion-boltwall.tierion.now.sh/[protected]',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```python
import requests
headers = {
  'Accept': '*/*'
}

r = requests.get('https://tierion-boltwall.tierion.now.sh/[protected]', params={

}, headers = headers)

print r.json()

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => '*/*'
}

result = RestClient.get 'https://tierion-boltwall.tierion.now.sh/[protected]',
  params: {
  }, headers: headers

p JSON.parse(result)

```

`GET /[protected]`

*protected path (applies to all method verbs- GET/PUT/POST/DELETE)*

A middleware that checks for a valid authorizing LSAT on all requests. Any middleware or router that comes _after_ boltwall will have this check performed on it. 
Invoice information will be contained in the LSAT WWW-Authenticate header. When an invoice is paid, a valid LSAT can usually
be constructed (depending on if there are other caveats on the macaroon)

**NOTE: The invoice can be paid by anyone from any node**. While authorization itself is tied to the specific session, payment is not. This allows for _accountless_ authorization.

> Example responses

> 200 Response

<h3 id="get__[protected]-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This is just a dummy response. In reality it depends on whatever endpoints the developer is protecting.|[inline_response_200](#schemainline_response_200)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Problem checking authorization in macaroon or checking invoice|[ErrorMessage](#schemaerrormessage)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Provided LSAT is unauthorized for access e.g. due to expiration or caveat validation error|[UnauthorizedError](#schemaunauthorizederror)|
|402|[Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2)|Payment required. Request has not been authorized with payment yet. Sent when a authorization is missing or somehow invalid.|[PaymentRequiredError](#schemapaymentrequirederror)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Server side error|[ErrorMessage](#schemaerrormessage)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|402|X-WWW-Authenticate|string|base64|none|

<aside class="warning">
To perform this operation, you must be authenticated by means of one of the following methods:
None ( Scopes: LSAT )
</aside>

# Schemas

<h2 id="tocSlsat-challenge">LSAT-Challenge</h2>

<a id="schemalsat-challenge"></a>

```json
"LSAT macaroon=\"MDAyM2xvY2F0aW9uIGh0dHA6Ly9sb2NhbGhvc3Q6MzAwMAowMDk0aWRlbnRpZmllciAwMDAwN2NlZjkzZjJjNTFhYTY1MjA4YmVjMTQ0N2ZjMzhmYzU4ZDliY2UxMzc1YTUzMmVkYjBkY2QyOTBhMmMzMzBhZWVhNDM5YWU1ZTg2Mjk1YTUwZmQ4MTRiODMyZTQ3NjRjNWMyYTRmM2YzYzUzZGNiOTRlNmM1ZTIwMjllNWRhNjcKMDAyZnNpZ25hdHVyZSAT8u5IrVmkydhKyFw3RzHNjL3FOzUsU33p6ghPVxZ83Ao\", invoice=\"lntb10u1pw7kfm8pp50nhe8uk9r2n9yz97c9z8lsu0ckxehnsnwkjn9mdsmnffpgkrxzhqdq5w3jhxapqd9h8vmmfvdjscqzpgllq2qvdlgkllc27kpd87lz8pdfsfmtteyc3kwq734jpwnvqt96e4nuy0yauzdrtkumxsvawgda8dlljxu3nnjlhs6w75390wy7ukj6cpfmygah\""

```

*The challenge issued by boltwall with a 402 Response in a WWW-Authenticate header, base64 encoded  with macaroon and invoice to be paid*

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string(base64)|false|none|The challenge issued by boltwall with a 402 Response in a WWW-Authenticate header, base64 encoded  with macaroon and invoice to be paid|

<h2 id="tocSlsat">LSAT</h2>

<a id="schemalsat"></a>

```json
"LSAT MDAxNmxvY2F0aW9uIGxvY2F0aW9uCjAwOTRpZGVudGlmaWVyIDAwMDA3Y2VmOTNmMmM1MWFhNjUyMDhiZWMxNDQ3ZmMzOGZjNThkOWJjZTEzNzVhNTMyZWRiMGRjZDI5MGEyYz MzMGFlOWMzMzNjOGM3N2MyNzU0YmI4NWJjMDc4YmY5N2Y2NGE5NTBjNDRhYjg0NTFjM2VmZmIyZTk0OTQ5MmQ0ZjRmZgowMDJmc2lnbmF0dXJlIJ0cCih9DapeVzWrq5AGX643eJC4y9 OdIF-yde_va0HjCg:2ca931a1c36b48f54948b898a271a53ed91ff7d0081939a5fa511249e81cba5c"

```

*Base64 encoded LSAT token, prefixed with the type (LSAT) and a macaroon and optional secret, separated with a colon*

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string(base64)|false|none|Base64 encoded LSAT token, prefixed with the type (LSAT) and a macaroon and optional secret, separated with a colon|

<h2 id="tocSnodeinfo">NodeInfo</h2>

<a id="schemanodeinfo"></a>

```json
{
  "pubKey": "03cb9e0a30f17a7b75f3ac9e9f39909811805be22ad6044953220a3c35d2809418",
  "alias": "foobar node",
  "socket": "123.45.67.87:10009",
  "activeChannelsCount": 2,
  "peersCount": 1
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|pubKey|string|true|none|none|
|alias|string|false|none|Alias of lightning node|
|socket|string|true|none|host and port where node can be reached|
|activeChannelsCount|number|false|none|Active channels on the node|
|peersCount|number|false|none|total number of peers connected to node|

<h2 id="tocSpaymentrequest">PaymentRequest</h2>

<a id="schemapaymentrequest"></a>

```json
"lntb10u1pw7kfm8pp50nhe8uk9r2n9yz97c9z8lsu0ckxehnsnwkjn9mdsmnffpgkrxzhqdq5w3jhxapqd9h8vmmfvdjscqzpg llq2qvdlgkllc27kpd87lz8pdfsfmtteyc3kwq734jpwnvqt96e4nuy0yauzdrtkumxsvawgda8dlljxu3nnjlhs6w75390wy7ukj6cpfmygah"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|string(<BOLT 11 Encoded Payment Request String>)|false|none|none|

<h2 id="tocSpaymentrequirederror">PaymentRequiredError</h2>

<a id="schemapaymentrequirederror"></a>

```json
{
  "message": "Payment required"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|true|none|none|

<h2 id="tocSunauthorizederror">UnauthorizedError</h2>

<a id="schemaunauthorizederror"></a>

```json
{
  "message": "Unauthorized: LSAT invalid"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|true|none|none|

<h2 id="tocSerrormessage">ErrorMessage</h2>

<a id="schemaerrormessage"></a>

```json
{
  "message": "_generic error message_"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|true|none|none|

<h2 id="tocSinvoiceresponse">InvoiceResponse</h2>

<a id="schemainvoiceresponse"></a>

```json
{
  "id": "7cef93f2c51aa65208bec1447fc38fc58d9bce1375a532edb0dcd290a2c330ae",
  "payreq": "lntb10u1pw7kfm8pp50nhe8uk9r2n9yz97c9z8lsu0ckxehnsnwkjn9mdsmnffpgkrxzhqdq5w3jhxapqd9h8vmmfvdjscqzpg llq2qvdlgkllc27kpd87lz8pdfsfmtteyc3kwq734jpwnvqt96e4nuy0yauzdrtkumxsvawgda8dlljxu3nnjlhs6w75390wy7ukj6cpfmygah",
  "createdAt": "2020-01-09T18:13:31.244Z",
  "amount": 30,
  "status": "paid",
  "description": "example invoice description"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string(hex)|false|none|Payment hash hex string|
|payreq|[PaymentRequest](#schemapaymentrequest)|false|none|none|
|createdAt|string(date-time)|false|none|none|
|amount|integer|false|none|Amount (in satoshis) of payment|
|status|string|false|none|One of "paid", "unpaid", or "held"|
|description|string|false|none|none|

<h2 id="tocSbody">body</h2>

<a id="schemabody"></a>

```json
{
  "title": "string",
  "amount": 0,
  "time": 0,
  "expiresAt": "string",
  "appName": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|title|string|false|none|Title of data being requested. Will be used in invoice metadata|
|amount|integer|true|none|none|
|time|integer|false|none|For time based APIs. Can be superceded by the `amount` property|
|expiresAt|string|false|none|Optional expiry for the invoice to timeout at in valid UTC string format.|
|appName|string|false|none|Optional name for identifying the app that is requesting the invoice.|

<h2 id="tocSinline_response_200">inline_response_200</h2>

<a id="schemainline_response_200"></a>

```json
{
  "message": "I am protected content. You can only see me if you've paid the price."
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|false|none|none|

<h2 id="tocSinline_response_402">inline_response_402</h2>

<a id="schemainline_response_402"></a>

```json
{
  "message": "Payment required"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|false|none|none|

