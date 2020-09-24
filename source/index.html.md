---
title: API Spec V1.0 v1.0
language_tabs:
  - javascript: Javascript
language_clients:
  - javascript: ""
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2
generator: widdershins v4.0.1

---

<h1 id="api-spec-v1-0">FIO API Spec</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

FIO Protocol API spec

Base URLs:

* <a href="http://testnet.fioprotocol.io/v1/chain/">http://testnet.fioprotocol.io/v1/chain/</a>

Email: <a href="mailto:getinfo@fio.foundation">FIO</a> Web: <a href="http://fio.foundation">FIO</a> 
 License: MIT

<h1 id="api-spec-v1-0-default">Get FIO Info</h1>

## FIO Address lookup

<a id="opIdget_pub_address"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_address": "string",
  "chain_code": "string",
  "token_code": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_pub_address',
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

`/get_pub_address`

Returns a public address for specified token code and FIO Address.

> Body parameter

```json
{
  "fio_address": "string",
  "chain_code": "string",
  "token_code": "string"
}
```

<h3 id="fio-address-lookup-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» fio_address|body|string|true|none|
|» chain_code|body|string|true|none|
|» token_code|body|string|true|none|

> Example responses

```json
{
  "public_address": "0xab5801a7d398351b8be11c439e05c5b3259aec9b"
}
```

> Possible error messages:
* 	"Invalid FIO Address"
* 	"Invalid Chain Code"
* 	"Invalid Token Code"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "public_address",
      "value": "",
      "error": "Invalid public address format"
    }
  ]
}
```

> Possible error messages:
* "Public address not found"

```json
{
  "message": "Public address not found"
}
```

<h3 id="fio-address-lookup-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* 	"Invalid FIO Address"
* 	"Invalid Chain Code"
* 	"Invalid Token Code"|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Possible error messages:
* "Public address not found"|Inline|

<h3 id="fio-address-lookup-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» public_address|string|false|none|Public address for requested FIO Address and token.|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **404**

*Error 404*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## FIO Address or Domain availability check

<a id="opIdavail_check"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_name": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/avail_check',
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

`POST /avail_check`

Checks if a FIO Address or FIO Domain is available for registration.

> Body parameter

```json
{
  "fio_name": "string"
}
```

<h3 id="fio-address-or-domain-availability-check-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» fio_name|body|string|true|FIO Address or FIO Domain to check.|

> Example responses

```json
{
  "is_registered": 1
}
```

> Possible error messages:
* "Invalid FIO Name"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_name",
      "value": "_.@",
      "error": "Invalid FIO Name"
    }
  ]
}
```

<h3 id="fio-address-or-domain-availability-check-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Name"|Inline|

<h3 id="fio-address-or-domain-availability-check-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» is_registered|integer|false|none|* 1 - FIO Address or Domain is registered<br />* 0 - FIO Address or Domain is not registered|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## Get FIO Names

<a id="opIdget_fio_names"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_public_key": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_fio_names',
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

`POST /get_fio_names`

Returns FIO Addresses and FIO Domains owned by this public key.

> Body parameter

```json
{
  "fio_public_key": "string"
}
```

<h3 id="get-fio-names-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» fio_public_key|body|string|true|Valid WIF Public Key with FIO Prefix|

> Example responses

```json
{
  "fio_domains": [
    {
      "fio_domain": "alice",
      "expiration": "2020-09-11T18:30:56",
      "is_public": 0
    }
  ],
  "fio_addresses": [
    {
      "fio_address": "purse@alice",
      "expiration": "2020-09-11T18:30:56"
    }
  ]
}
```

> Possible error messages:
* "Invalid FIO Public Key"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_public_key",
      "value": "FIO123",
      "error": "Invalid FIO Public Key"
    }
  ]
}
```

> Possible error messages:
* "No FIO names"

```json
{
  "message": "No FIO names"
}
```

<h3 id="get-fio-names-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Public Key"|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Possible error messages:
* "No FIO names"|Inline|

<h3 id="get-fio-names-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» fio_domains|[object]|false|none|none|
|»» fio_domain|string|false|none|none|
|»» expiration|string(date-time)|false|none|none|
|»» is_public|integer|false|none|* 0 - domain is not public<br />* 1 - domain is public|
|» fio_addresses|[object]|false|none|none|
|»» fio_address|string|false|none|none|
|»» expiration|string(date-time)|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **404**

*Error 404*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Get pending FIO Requests

<a id="opIdget_pending_fio_requests"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_public_key": "string",
  "limit": 0,
  "offset": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_pending_fio_requests',
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

`POST /get_pending_fio_requests`

Pending requests call polls for any pending requests sent to a receiver.

> Body parameter

```json
{
  "fio_public_key": "string",
  "limit": 0,
  "offset": 0
}
```

<h3 id="get-pending-fio-requests-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» fio_public_key|body|string|true|Valid WIF Public Key with FIO Prefix|
|» limit|body|integer|false|Number of requests to return. If omitted, all requests will be returned.|
|» offset|body|integer|false|First request from list to return. If omitted, 0 is assumed.|

> Example responses

```json
{
  "requests": [
    {
      "fio_request_id": "10",
      "payer_fio_address": "purse@alice",
      "payee_fio_address": "crypto@bob",
      "payer_fio_public_key": "FIO7167ErgCveJvuonvrEvVGhdWnkP4AEMfqvEd8s8raMkbbAXqhx",
      "payee_fio_public_key": "FIO7KGdMYj4ZMY2nUX9EaZu3G3GxZhTNXUq1tsNqC5rcP9rcmvWHq",
      "content": "...",
      "time_stamp": "2020-09-11T18:30:56"
    }
  ],
  "more": 0
}
```

> Possible error messages:
* "Invalid FIO Public Key"
* "Invalid limit"
* "Invalid offset"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_public_key",
      "value": "FIO123",
      "error": "Invalid FIO Public Key"
    }
  ]
}
```

> Possible error messages:
* "No pending FIO Requests"

```json
{
  "message": "No pending FIO Requests"
}
```

<h3 id="get-pending-fio-requests-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Public Key"
* "Invalid limit"
* "Invalid offset"|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Possible error messages:
* "No pending FIO Requests"|Inline|

<h3 id="get-pending-fio-requests-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» requests|[object]|false|none|Multiple requests may be returned. All requests are returned.|
|»» fio_request_id|string|false|none|Id of that funds request.|
|»» payer_fio_address|string|false|none|FIO Address of the payer. This address initiated payment.|
|»» payee_fio_address|string|false|none|FIO Address of the payee. This address is receiving payment.|
|»» payer_fio_public_key|string|false|none|FIO public key of the payer.|
|»» payee_fio_public_key|string|false|none|FIO public key of the payee.|
|»» content|object|false|none|Certain content inside FIO Request is encrypted and packed into this field.<br /><br />Min 64 characters<br />Max 296 characters|
|»»» payee_public_address|object|true|none|This is the public address on another blockchain. Both integrated addresses as well as URI Scheme are supported.<br /><br />**Integrated Address**<br />If the blockchain supports it, an integrated address may be passed in just like standard public address. The FIO protocol does not perform validation on the passed string.<br /><br />**URI Scheme**<br />FIO Protocol will support formatting of public addresses using URI were certain attributes are appended to the public address following a '?' and delimited with '&'. To allow inter-wallet operability, the following standardized parameters will be supported in official FIO Protocol SDKs.<br /><br />**Parameters**<br />* dt - Ripple<br />* memo - Any - use as generic memo field<br />* memo_id -	Stellar<br />* memo_text -	Stellar<br />* memo_hash -	Stellar<br />* memo_return -	Stellar<br />* payment_id - Monero|
|»»» amount|string|true|none|Amount requested.|
|»»» token_code|string|true|none|none|
|»»» memo|string|true|none|none|
|»»» hash|string|true|none|none|
|»»» offline_url|string|true|none|none|
|»»» future_use1|string|true|none|none|
|»»» future_use2|string|true|none|none|
|»»» future_use3|string|true|none|none|
|»»» future_use4|string|true|none|none|
|»»» future_use5|string|true|none|none|
|»» time_stamp|string|false|none|Timestamp of request|
|» more|integer|false|none|0 - no more results<br />1 - more results|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **404**

*Error 404*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Get FIO balance

<a id="opIdget_fio_balance"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_public_key": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_fio_balance',
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

`POST /get_fio_balance`

Retrieves balance of FIO tokens.

> Body parameter

```json
{
  "fio_public_key": "string"
}
```

<h3 id="get-fio-balance-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» fio_public_key|body|string|true|Valid WIF Public Key with FIO Prefix|

> Example responses

```json
{
  "balance": 100000000000
}
```

> Possible error messages:
* "Invalid FIO Public Key"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_public_key",
      "value": "FIO123",
      "error": "Invalid FIO Public Key"
    }
  ]
}
```

> Possible error messages:
* "Public key not found"

```json
{
  "message": "Public key not found"
}
```

<h3 id="get-fio-balance-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Public Key"|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Possible error messages:
* "Public key not found"|Inline|

<h3 id="get-fio-balance-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» balance|integer|false|none|SUF balance associated with supplied public key.|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **404**

*Error 404*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Get fee amount

<a id="opIdget_fee"></a>

> Code samples

```javascript
const inputBody = '{
  "end_point": "string",
  "fio_address": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_fee',
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

`POST /get_fee`

Computes and returns fee amount for specific call and specific user.

> Body parameter

```json
{
  "end_point": "string",
  "fio_address": "string"
}
```

<h3 id="get-fee-amount-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|Valid FIO Address required on the following calls:|
|» end_point|body|string|true|Name of API call end point, e.g. add_pub_address|
|» fio_address|body|string|true|none|

#### Detailed descriptions

**body**: Valid FIO Address required on the following calls:
* add_pub_address
* new_funds_request
* reject_funds_request
* record_obt_data

> Example responses

```json
{
  "fee": 100000000
}
```

> Possible error messages:
* "Invalid end point"
* "Invalid FIO Address"
* "No such FIO Address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "end_point",
      "value": "blah",
      "error": "Invalid end point"
    }
  ]
}
```

<h3 id="get-fee-amount-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid end point"
* "Invalid FIO Address"
* "No such FIO Address"|Inline|

<h3 id="get-fee-amount-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» fee|integer|false|none|Amount of fee in SUFs|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## Get FIO blockchain information

<a id="opIdget_info"></a>

> Code samples

```javascript

const headers = {
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_info',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`POST /get_info`

Retrieves information about the FIO blockchain.

> Example responses

```json
{
  "server_version": "8578680f",
  "chain_id": "cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f",
  "head_block_num": 1201696,
  "last_irreversible_block_num": 1201656,
  "last_irreversible_block_id": "001255f8d3e90e4573265d5ee71a64d6a20dccee5226a0c2e30b4c0a1b082068",
  "head_block_id": "00125620fac409486e7fea1bebb0b506f8beb679b250a76e95e6f50d02e85d3f",
  "head_block_time": "2019-09-27T15:28:43.500",
  "head_block_producer": "5spujqoyq4ie",
  "virtual_block_cpu_limit": 200000000,
  "virtual_block_net_limit": 1048576000,
  "block_cpu_limit": 199900,
  "block_net_limit": 1048576,
  "server_version_string": "v1.2.1-2421-g92993a283"
}
```

<h3 id="get-fio-blockchain-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

<h3 id="get-fio-blockchain-information-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» server_version|string|false|none|none|
|» chain_id|string|false|none|none|
|» head_block_num|integer|false|none|none|
|» last_irreversible_block_num|integer|false|none|none|
|» last_irreversible_block_id|string|false|none|none|
|» head_block_id|string|false|none|none|
|» head_block_time|string|false|none|none|
|» head_block_producer|string|false|none|none|
|» virtual_block_cpu_limit|integer|false|none|none|
|» virtual_block_net_limit|integer|false|none|none|
|» block_cpu_limit|integer|false|none|none|
|» block_net_limit|integer|false|none|none|
|» server_version_string|string|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## Get block information

<a id="opIdget_block"></a>

> Code samples

```javascript
const inputBody = '{
  "block_num_or_id": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_block',
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

`POST /get_block`

Retrieves information about the specific block.

> Body parameter

```json
{
  "block_num_or_id": "string"
}
```

<h3 id="get-block-information-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» block_num_or_id|body|string|true|last_irreversible_block_num or last_irreversible_block_id from /get_info|

> Example responses

```json
{
  "timestamp": "2019-09-27T15:28:23.500",
  "producer": "5spujqoyq4ie",
  "confirmed": 0,
  "previous": "001255f72bd0a154355dddec8391de0f20a3619ee6802535e6bd8f4ea2caf0df",
  "transaction_mroot": "0000000000000000000000000000000000000000000000000000000000000000",
  "action_mroot": "d8552b686d6b520d39bf27c3bb49968b5ca52e370467962e42edc151437d01c6",
  "schedule_version": 2,
  "new_producers": null,
  "header_extensions": [],
  "producer_signature": "SIG_K1_K5WD9qbSfJwMz1doYBn5znfFsPh9UiV2p9XAbkDDV2nvpQXq2D23EU6vuGSndSZ7FATqkNn5dqZFtaBricHRJvtgGFZ9pG",
  "transactions": [],
  "block_extensions": [],
  "id": "001255f8d3e90e4573265d5ee71a64d6a20dccee5226a0c2e30b4c0a1b082068",
  "block_num": 1201656,
  "ref_block_prefix": 1583162995
}
```

<h3 id="get-block-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

<h3 id="get-block-information-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» timestamp|string|false|none|none|
|» producer|string|false|none|none|
|» confirmed|integer|false|none|none|
|» previous|string|false|none|none|
|» transaction_mroot|string|false|none|none|
|» action_mroot|string|false|none|none|
|» schedule_version|integer|false|none|none|
|» new_producers|any|false|none|none|
|» header_extensions|[object]|false|none|none|
|» producer_signature|string|false|none|none|
|» transactions|[object]|false|none|none|
|» block_extensions|[object]|false|none|none|
|» id|string|false|none|none|
|» block_num|integer|false|none|none|
|» ref_block_prefix|integer|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## Get ABI for specific account name

<a id="opIdget_raw_abi"></a>

> Code samples

```javascript
const inputBody = '{
  "account_name": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_raw_abi',
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

`POST /get_raw_abi`

The ABI is required to properly pack content of signed calls.

> Body parameter

```json
{
  "account_name": "string"
}
```

<h3 id="get-abi-for-specific-account-name-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» account_name|body|string|true|Account name. Check request definition for specific call.|

> Example responses

```json
{
  "account_name": "fio.system",
  "code_hash": "0e5e404480e07b5b1c9d0d8cfbe4f04b8f3fd3477a42251bab8191e6e6c241a8",
  "abi_hash": "d98bbfa97018efcdfbbf42b62406707bc17498e630f58e4529029af71042d861",
  "abi": "DmVvc2lvOjphYmkvMS4wABMHZmlvbmFtZQAIBG5hbWUGc3RyaW5nCG5hbWVoYXNoBnVpbnQ2NAZkb21haW4Gc3RyaW5nCmRvbWFpbmhhc2gGdWludDY0CmV4cGlyYXRpb24GdWludDY0DW93bmVyX2FjY291bnQEbmFtZQlhZGRyZXNzZXMIc3RyaW5nW10XYnVuZGxlZWxpZ2libGVjb3VudGRvd24GdWludDY0BmRvbWFpbgAFBG5hbWUGc3RyaW5nCmRvbWFpbmhhc2gGdWludDY0CWlzX3B1YmxpYwV1aW50OApleHBpcmF0aW9uBnVpbnQzMgdhY2NvdW50BnVpbnQ2NAljaGFpbkxpc3QAAwRuYW1lBnN0cmluZwJpZAZ1aW50NjQJY2hhaW5oYXNoBnVpbnQzMgplb3Npb19uYW1lAAMHYWNjb3VudARuYW1lCWNsaWVudGtleQZzdHJpbmcHa2V5aGFzaAZ1aW50NjQJY2hhaW5wYWlyAAMFaW5kZXgGdWludDY0CWNoYWlubmFtZQZzdHJpbmcJY2hhaW5oYXNoBnVpbnQ2NApyZWdhZGRyZXNzAAULZmlvX2FkZHJlc3MGc3RyaW5nFG93bmVyX2Zpb19wdWJsaWNfa2V5BnN0cmluZwdtYXhfZmVlBnVpbnQ2NAVhY3RvcgRuYW1lBHRwaWQGc3RyaW5nCmFkZGFkZHJlc3MABgtmaW9fYWRkcmVzcwZzdHJpbmcKdG9rZW5fY29kZQZzdHJpbmcOcHVibGljX2FkZHJlc3MGc3RyaW5nB21heF9mZWUGdWludDY0BWFjdG9yBG5hbWUEdHBpZAZzdHJpbmcJcmVnZG9tYWluAAUKZmlvX2RvbWFpbgZzdHJpbmcUb3duZXJfZmlvX3B1YmxpY19rZXkGc3RyaW5nB21heF9mZWUGdWludDY0BWFjdG9yBG5hbWUEdHBpZAZzdHJpbmcLcmVuZXdkb21haW4ABApmaW9fZG9tYWluBnN0cmluZwdtYXhfZmVlBnVpbnQ2NAR0cGlkBnN0cmluZwVhY3RvcgRuYW1lDHJlbmV3YWRkcmVzcwAEC2Zpb19hZGRyZXNzBnN0cmluZwdtYXhfZmVlBnVpbnQ2NAR0cGlkBnN0cmluZwVhY3RvcgRuYW1lCWV4cGRvbWFpbgACBWFjdG9yBG5hbWUGZG9tYWluBnN0cmluZwxleHBhZGRyZXNzZXMABAVhY3RvcgRuYW1lBmRvbWFpbgZzdHJpbmcOYWRkcmVzc19wcmVmaXgGc3RyaW5nF251bWJlcl9hZGRyZXNzZXNfdG9fYWRkBnVpbnQ2NAxzZXRkb21haW5wdWIABQpmaW9fZG9tYWluBnN0cmluZwlpc19wdWJsaWMFdWludDgHbWF4X2ZlZQZ1aW50NjQFYWN0b3IEbmFtZQR0cGlkBnN0cmluZwtidXJuZXhwaXJlZAAACnJlbW92ZW5hbWUAAAxyZW1vdmVkb21haW4AAApybXZhZGRyZXNzAAALZGVjcmNvdW50ZXIAAQtmaW9fYWRkcmVzcwZzdHJpbmcKYmluZDJlb3NpbwADB2FjY291bnQEbmFtZQpjbGllbnRfa2V5BnN0cmluZwhleGlzdGluZwRib29sDQAAxuqmZJi6CnJlZ2FkZHJlc3MAAADG6qZkUjIKYWRkYWRkcmVzcwAAAJjOSJqYuglyZWdkb21haW4AAKYzkiauproLcmVuZXdkb21haW4AgLG6KRmuproMcmVuZXdhZGRyZXNzAAAAmM5ImmpXCWV4cGRvbWFpbgCAFcbqpmRqVwxleHBhZGRyZXNzZXMAAJK6rnY1rz4LYnVybmV4cGlyZWQAAICSZqpNpboKcmVtb3ZlbmFtZQAwnZE0qU2lugxyZW1vdmVkb21haW4AAADG6qZktrwKcm12YWRkcmVzcwBwdJ3OSJqywgxzZXRkb21haW5wdWIAAAB1mCqRpjsKYmluZDJlb3NpbwAEAAAAWEkzqVsDaTY0AQRuYW1lAQZzdHJpbmcHZmlvbmFtZQAAAABPZyRNA2k2NAEEbmFtZQEGc3RyaW5nBmRvbWFpbgAAAADg6UxDA2k2NAEEbmFtZQEGc3RyaW5nCWNoYWluTGlzdABANTJPTREyA2k2NAEHYWNjb3VudAEGdWludDY0CmVvc2lvX25hbWUAAAAA="
}
```

<h3 id="get-abi-for-specific-account-name-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

<h3 id="get-abi-for-specific-account-name-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» account_name|string|false|none|none|
|» code_hash|string|false|none|none|
|» abi_hash|string|false|none|none|
|» abi|string|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## Get a list of current block producers

<a id="opIdget_producers"></a>

> Code samples

```javascript
const inputBody = '{
  "limit": "string",
  "lower_bound": "string",
  "json": true
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_producers',
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

`POST /get_producers`

This call returns all block producers and their scaled votes.

> Body parameter

```json
{
  "limit": "string",
  "lower_bound": "string",
  "json": true
}
```

<h3 id="get-a-list-of-current-block-producers-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» limit|body|string|false|Total number of producers to retrieve|
|» lower_bound|body|string|false|none|
|» json|body|boolean|false|Return result in JSON format?|

> Example responses

```json
{
  "producers": [
    {
      "owner": "fioproducerd",
      "fio_address": "",
      "total_votes": "4999000000000.00000000000000000",
      "producer_fio_public_key": "FIO79vbwYtjhBVnBRYDjhCyxRFVr6JsFfVrLVhUKoqFTnceZtPvAU",
      "is_active": 1,
      "url": "",
      "unpaid_blocks": 302361,
      "last_claim_time": "2019-09-20T16:35:26.000",
      "location": 0
    },
    {
      "owner": "fioproducerc",
      "fio_address": "",
      "total_votes": "3999000000000.00000000000000000",
      "producer_fio_public_key": "FIO79vbwYtjhBVnBRYDjhCyxRFVr6JsFfVrLVhUKoqFTnceZtPvAU",
      "is_active": 1,
      "url": "",
      "unpaid_blocks": 302349,
      "last_claim_time": "2019-09-20T16:35:25.500",
      "location": 0
    },
    {
      "owner": "fioproducerb",
      "fio_address": "",
      "total_votes": "2999000000000.00000000000000000",
      "producer_fio_public_key": "FIO79vbwYtjhBVnBRYDjhCyxRFVr6JsFfVrLVhUKoqFTnceZtPvAU",
      "is_active": 1,
      "url": "",
      "unpaid_blocks": 302352,
      "last_claim_time": "2019-09-20T16:35:25.500",
      "location": 0
    },
    {
      "owner": "5spujqoyq4ie",
      "fio_address": "",
      "total_votes": "1999000000000.00000000000000000",
      "producer_fio_public_key": "FIO77odcm3LYr6YduUxf83a4jp4pQ4YvKAjBkHJnLxq2SsgNSc13u",
      "is_active": 1,
      "url": "",
      "unpaid_blocks": 302364,
      "last_claim_time": "2019-09-20T16:35:25.500",
      "location": 0
    },
    {
      "owner": "2ugokdhavqow",
      "fio_address": "pawel366688@woohoo56311",
      "total_votes": "0.00000000000000000",
      "producer_fio_public_key": "FIO1111111111111111111111111111111114T1Anm",
      "is_active": 0,
      "url": "h",
      "unpaid_blocks": 0,
      "last_claim_time": "2019-09-26T22:40:30.000",
      "location": 80
    },
    {
      "owner": "gev2yeim1cjy",
      "fio_address": "pawel554427@woohoo56311",
      "total_votes": "998769980000000.00000000000000000",
      "producer_fio_public_key": "FIO1111111111111111111111111111111114T1Anm",
      "is_active": 0,
      "url": "",
      "unpaid_blocks": 0,
      "last_claim_time": "2019-09-26T22:40:22.000",
      "location": 80
    }
  ],
  "total_producer_vote_weight": "1012765980000000.00000000000000000",
  "more": ""
}
```

> Possible error messages:
* "Invalid limit"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "limit",
      "value": "-100",
      "error": "Invalid limit"
    }
  ]
}
```

<h3 id="get-a-list-of-current-block-producers-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid limit"|None|

<h3 id="get-a-list-of-current-block-producers-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» producers|[object]|false|none|none|
|»» owner|string|false|none|none|
|»» fio_address|string|false|none|none|
|»» total_votes|string|false|none|none|
|»» producer_fio_public_key|string|false|none|none|
|»» is_active|integer|false|none|none|
|»» url|string|false|none|none|
|»» unpaid_blocks|integer|false|none|none|
|»» last_claim_time|string|false|none|none|
|»» location|integer|false|none|none|
|» total_producer_vote_weight|string|false|none|none|
|» more|string|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Register FIO Address

<a id="opIdregister_fio_address"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/register_fio_address',
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

`POST /register_fio_address`

Registers a FIO Address on the FIO blockchain.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-register-fio-address-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **Contents** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "84409d5141043921be9384cd62ddff80d6e9435273cd5c95f96b6ba19c2137cd",
  "processed": {
    "id": "84409d5141043921be9384cd62ddff80d6e9435273cd5c95f96b6ba19c2137cd",
    "block_num": 1201721,
    "block_time": "2019-09-27T15:28:56.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 2403,
      "net_usage_words": 17
    },
    "elapsed": 2403,
    "net_usage": 136,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.address",
          "response": "{\"expiration\":\"2020-09-26T15:28:56\",\"fee_collected\":5000000000,\"status\":\"OK\"}",
          "act_digest": "51b6825f1b8c639a3071c0267d29d6ff40b11a9cbcd094885dcd69da92d2a6a1",
          "global_sequence": 1212122,
          "recv_sequence": 42,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              75
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.address",
          "name": "regaddress",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_address": "pawel554427@woohoo56311",
            "owner_fio_public_key": "",
            "max_fee": 5000000000,
            "actor": "gev2yeim1cjy",
            "tpid": ""
          },
          "hex_data": "17706177656c3535343432373a776f6f686f6f35363331310000f2052a01000000e01f0ad2292fb66200"
        },
        "context_free": false,
        "elapsed": 1913,
        "console": "OWNER:gev2yeim1cjy...Value:7112924518142320608...Key:FIO8PRe4WRZJj5mkem6qVGKyvNFgPsNnjNN6kPhh6EaCpzCVin5Jj...hash:18446744073642438656\n1601134136 INSIDE.   2020   TESTINSIDE.   5000000000\nfionamefound: \nCannot register TPID or FIO Address not found. The transaction will continue without TPID payment.\n",
        "trx_id": "84409d5141043921be9384cd62ddff80d6e9435273cd5c95f96b6ba19c2137cd",
        "block_num": 1201721,
        "block_time": "2019-09-27T15:28:56.000",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "fio.address",
            "delta": 646
          }
        ],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "41051fa782f88f79085466aa9f1aff1f918a69b8a3a82a0554060aaf1e8ea5d2",
              "global_sequence": 1212123,
              "recv_sequence": 84,
              "auth_sequence": [
                [
                  "gev2yeim1cjy",
                  76
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "gev2yeim1cjy",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "gev2yeim1cjy",
                "to": "fio.treasury",
                "quantity": "5.000000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00f2052a010000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 129,
            "console": "",
            "trx_id": "84409d5141043921be9384cd62ddff80d6e9435273cd5c95f96b6ba19c2137cd",
            "block_num": 1201721,
            "block_time": "2019-09-27T15:28:56.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "41051fa782f88f79085466aa9f1aff1f918a69b8a3a82a0554060aaf1e8ea5d2",
                  "global_sequence": 1212124,
                  "recv_sequence": 19,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "5.000000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00f2052a010000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 3,
                "console": "",
                "trx_id": "84409d5141043921be9384cd62ddff80d6e9435273cd5c95f96b6ba19c2137cd",
                "block_num": 1201721,
                "block_time": "2019-09-27T15:28:56.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "41051fa782f88f79085466aa9f1aff1f918a69b8a3a82a0554060aaf1e8ea5d2",
                  "global_sequence": 1212125,
                  "recv_sequence": 113,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "5.000000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00f2052a010000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 11,
                "console": "",
                "trx_id": "84409d5141043921be9384cd62ddff80d6e9435273cd5c95f96b6ba19c2137cd",
                "block_num": 1201721,
                "block_time": "2019-09-27T15:28:56.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "1a7775344923ca0ff6340e6c0ae2d246ef2899f908a550741d0cfe02d4ce2c0d",
              "global_sequence": 1212126,
              "recv_sequence": 114,
              "auth_sequence": [
                [
                  "fio.system",
                  51
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "00e1f50500000000"
            },
            "context_free": false,
            "elapsed": 51,
            "console": "",
            "trx_id": "84409d5141043921be9384cd62ddff80d6e9435273cd5c95f96b6ba19c2137cd",
            "block_num": 1201721,
            "block_time": "2019-09-27T15:28:56.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "f549782fb7ac5903d111ca2e52dd25599b4220ff6958431da5c493cdc97cefca",
              "global_sequence": 1212127,
              "recv_sequence": 115,
              "auth_sequence": [
                [
                  "fio.system",
                  52
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bppoolupdate",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "0011102401000000"
            },
            "context_free": false,
            "elapsed": 34,
            "console": "",
            "trx_id": "84409d5141043921be9384cd62ddff80d6e9435273cd5c95f96b6ba19c2137cd",
            "block_num": 1201721,
            "block_time": "2019-09-27T15:28:56.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid FIO address"
* "FIO address already registered"
* "FIO Domain not registered"
* "FIO Domain expired"
* "FIO Domain is not public. Only owner can create FIO Addresses."
* "Invalid FIO Public Key"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_address",
      "value": "purse@alice",
      "error": "FIO address already registered"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-register-fio-address-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO address"
* "FIO address already registered"
* "FIO Domain not registered"
* "FIO Domain expired"
* "FIO Domain is not public. Only owner can create FIO Addresses."
* "Invalid FIO Public Key"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-register-fio-address-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Register FIO Address

<a id="opIdregister_fio_address_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_address": "string",
  "owner_fio_public_key": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/register_fio_address',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /register_fio_address`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.address"
* name: "regaddress"

> Body parameter

```json
{
  "fio_address": "string",
  "owner_fio_public_key": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}
```

<h3 id="[content]-register-fio-address-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_address|body|string|true|See [FIO Address format](https://kb.fioprotocol.io/fio-protocol/fio-addresses/format)|
|» owner_fio_public_key|body|string|true|Valid WIF Public Key with FIO Prefix|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» tpid|body|string|true|* FIO Address of the wallet which generates this transaction.|
|» actor|body|string|true|See [Generating actor](/actor)|

#### Detailed descriptions

**» fio_address**: See [FIO Address format](https://kb.fioprotocol.io/fio-protocol/fio-addresses/format)

Please note that FIO Address is case insensitive. If upper case characters are passed in, they will be converted to lower case.

**» tpid**: * FIO Address of the wallet which generates this transaction.
* This FIO Address will be paid 10% of the fee.
* See FIO Protocol#TPIDs for details.
* Set to empty if not known.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "expiration": "2020-09-11T18:30:56",
  "fee_collected": 30000000000
}
```

<h3 id="[content]-register-fio-address-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-register-fio-address-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» expiration|string(date-time)|false|none|none|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Register FIO Domain

<a id="opIdregister_fio_domain"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/register_fio_domain',
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

`POST /register_fio_domain`

Registers a FIO Domain on the FIO blockchain.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-register-fio-domain-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response. 

```json
{
  "transaction_id": "cae721ba5b7a57bc7d78d86ffa2a09128f363834fbad4e553ddba8e5985a54f1",
  "processed": {
    "id": "cae721ba5b7a57bc7d78d86ffa2a09128f363834fbad4e553ddba8e5985a54f1",
    "block_num": 1201716,
    "block_time": "2019-09-27T15:28:53.500",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1637,
      "net_usage_words": 24
    },
    "elapsed": 1637,
    "net_usage": 192,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.address",
          "response": "{\"expiration\":\"2020-09-26T15:28:53\",\"fee_collected\":80000000000,\"status\":\"OK\"}",
          "act_digest": "46051a043bff16287d3712717b5158727d3614be6704befd359a3a056db30b80",
          "global_sequence": 1212111,
          "recv_sequence": 41,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              71
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.address",
          "name": "regdomain",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_domain": "woohoo56311",
            "owner_fio_public_key": "FIO8PRe4WRZJj5mkem6qVGKyvNFgPsNnjNN6kPhh6EaCpzCVin5Jj",
            "max_fee": 80000000000,
            "actor": "gev2yeim1cjy",
            "tpid": "blahblah@blahblah"
          },
          "hex_data": "0b776f6f686f6f35363331313546494f385052653457525a4a6a356d6b656d367156474b79764e466750734e6e6a4e4e366b50686836456143707a4356696e354a6a00205fa012000000e01f0ad2292fb66211626c6168626c61683a626c6168626c6168"
        },
        "context_free": false,
        "elapsed": 1154,
        "console": "hashed account name from the owner_fio_public_key gev2yeim1cjy\n1601134133 INSIDE.   2020   TESTINSIDE.   80000000000\nfionamefound: \nCannot register TPID or FIO Address not found. The transaction will continue without TPID payment.\n",
        "trx_id": "cae721ba5b7a57bc7d78d86ffa2a09128f363834fbad4e553ddba8e5985a54f1",
        "block_num": 1201716,
        "block_time": "2019-09-27T15:28:53.500",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "fio.address",
            "delta": 405
          }
        ],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "c9742e89b5997def70807b5fc2b2495fce6125683e9493310fc282a8bfc99b9e",
              "global_sequence": 1212112,
              "recv_sequence": 83,
              "auth_sequence": [
                [
                  "gev2yeim1cjy",
                  72
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "gev2yeim1cjy",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "gev2yeim1cjy",
                "to": "fio.treasury",
                "quantity": "80.000000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00205fa0120000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 142,
            "console": "",
            "trx_id": "cae721ba5b7a57bc7d78d86ffa2a09128f363834fbad4e553ddba8e5985a54f1",
            "block_num": 1201716,
            "block_time": "2019-09-27T15:28:53.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "c9742e89b5997def70807b5fc2b2495fce6125683e9493310fc282a8bfc99b9e",
                  "global_sequence": 1212113,
                  "recv_sequence": 18,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "80.000000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00205fa0120000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 2,
                "console": "",
                "trx_id": "cae721ba5b7a57bc7d78d86ffa2a09128f363834fbad4e553ddba8e5985a54f1",
                "block_num": 1201716,
                "block_time": "2019-09-27T15:28:53.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "c9742e89b5997def70807b5fc2b2495fce6125683e9493310fc282a8bfc99b9e",
                  "global_sequence": 1212114,
                  "recv_sequence": 110,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "80.000000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00205fa0120000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 10,
                "console": "",
                "trx_id": "cae721ba5b7a57bc7d78d86ffa2a09128f363834fbad4e553ddba8e5985a54f1",
                "block_num": 1201716,
                "block_time": "2019-09-27T15:28:53.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "15584c15ca31252be83a82ddb18390727b0964075d3d137835314638302f9daa",
              "global_sequence": 1212115,
              "recv_sequence": 111,
              "auth_sequence": [
                [
                  "fio.system",
                  49
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "00105e5f00000000"
            },
            "context_free": false,
            "elapsed": 43,
            "console": "",
            "trx_id": "cae721ba5b7a57bc7d78d86ffa2a09128f363834fbad4e553ddba8e5985a54f1",
            "block_num": 1201716,
            "block_time": "2019-09-27T15:28:53.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "71601241e042c849fc61481de448c75f38856c59999827560fc1cae061839c60",
              "global_sequence": 1212116,
              "recv_sequence": 112,
              "auth_sequence": [
                [
                  "fio.system",
                  50
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bppoolupdate",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "0010014112000000"
            },
            "context_free": false,
            "elapsed": 35,
            "console": "",
            "trx_id": "cae721ba5b7a57bc7d78d86ffa2a09128f363834fbad4e553ddba8e5985a54f1",
            "block_num": 1201716,
            "block_time": "2019-09-27T15:28:53.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid FIO domain"
* "FIO domain already registered"
* "Invalid FIO Public Key"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "max_fee",
      "value": "200",
      "error": "Fee exceeds supplied maximum."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-register-fio-domain-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO domain"
* "FIO domain already registered"
* "Invalid FIO Public Key"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-register-fio-domain-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Register FIO Domain

<a id="opIdregister_fio_domain_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_domain": "string",
  "owner_fio_public_key": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/register_fio_domain',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /register_fio_domain`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.address"
* name: "regdomain"

> Body parameter

```json
{
  "fio_domain": "string",
  "owner_fio_public_key": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}
```

<h3 id="[content]-register-fio-domain-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_domain|body|string|true|See [FIO Domain format](https://kb.fioprotocol.io/fio-protocol/fio-addresses/format)|
|» owner_fio_public_key|body|string|true|Valid WIF Public Key with FIO Prefix|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» tpid|body|string|true|* FIO Address of the wallet which generates this transaction.|
|» actor|body|string|true|See [Generating actor](/actor)|

#### Detailed descriptions

**» fio_domain**: See [FIO Domain format](https://kb.fioprotocol.io/fio-protocol/fio-addresses/format)

Please note that FIO Domain is case insensitive. If upper case characters are passed in, they will be converted to lower case.

**» tpid**: * FIO Address of the wallet which generates this transaction.
* This FIO Address will be paid 10% of the fee.
* See FIO Protocol#TPIDs for details.
* Set to empty if not known.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "expiration": "2020-09-11T18:30:56",
  "fee_collected": 2000000000
}
```

<h3 id="[content]-register-fio-domain-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-register-fio-domain-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» expiration|string(date-time)|false|none|none|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Renew FIO Domain

<a id="opIdrenew_fio_domain"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/renew_fio_domain',
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

`POST /renew_fio_domain`

When a domain is renewed 365 days are added to its expiration date.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-renew-fio-domain-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response. 

```json
{
  "transaction_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
  "processed": {
    "id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
    "block_num": 1201737,
    "block_time": "2019-09-27T15:29:04.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1674,
      "net_usage_words": 18
    },
    "elapsed": 1674,
    "net_usage": 144,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.address",
          "response": "{\"expiration\":\"2021-09-26T15:28:53\",\"fee_collected\":40000000000,\"status\":\"OK\"}",
          "act_digest": "88bd9192985f8c7f9bc91096f5638b46dbd773353c4131b1ea40583d67b4030c",
          "global_sequence": 1212187,
          "recv_sequence": 46,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              87
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.address",
          "name": "renewdomain",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_domain": "woohoo56311",
            "max_fee": 40000000000,
            "tpid": "pawel366688@woohoo56311",
            "actor": "gev2yeim1cjy"
          },
          "hex_data": "0b776f6f686f6f353633313100902f500900000017706177656c3336363638383a776f6f686f6f3536333131e01f0ad2292fb662"
        },
        "context_free": false,
        "elapsed": 815,
        "console": "40000000000\nfionamefound: pawel366688@woohoo56311\n\nBounties: 29321500000\n\nBounty payout: 26000000000\n\nTest Bucket Update Amount: 35200000000\n1632670133 INSIDE.   2021   TESTINSIDE.   ",
        "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
        "block_num": 1201737,
        "block_time": "2019-09-27T15:29:04.000",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "1809af2b5b77df44949c1597443fcf2ff35763e8c08f6c5624c3c08141debec2",
              "global_sequence": 1212188,
              "recv_sequence": 97,
              "auth_sequence": [
                [
                  "gev2yeim1cjy",
                  88
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "gev2yeim1cjy",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "gev2yeim1cjy",
                "to": "fio.treasury",
                "quantity": "40.000000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00902f50090000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 133,
            "console": "",
            "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
            "block_num": 1201737,
            "block_time": "2019-09-27T15:29:04.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "1809af2b5b77df44949c1597443fcf2ff35763e8c08f6c5624c3c08141debec2",
                  "global_sequence": 1212189,
                  "recv_sequence": 22,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "40.000000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00902f50090000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 3,
                "console": "",
                "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
                "block_num": 1201737,
                "block_time": "2019-09-27T15:29:04.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "1809af2b5b77df44949c1597443fcf2ff35763e8c08f6c5624c3c08141debec2",
                  "global_sequence": 1212190,
                  "recv_sequence": 128,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "40.000000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00902f50090000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 8,
                "console": "",
                "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
                "block_num": 1201737,
                "block_time": "2019-09-27T15:29:04.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "79ecc4b63c3c5de749b1edf5ba91ba1bd924f9c16c99b87867f200c0748253ab",
              "global_sequence": 1212191,
              "recv_sequence": 129,
              "auth_sequence": [
                [
                  "fio.system",
                  63
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "0008af2f00000000"
            },
            "context_free": false,
            "elapsed": 40,
            "console": "",
            "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
            "block_num": 1201737,
            "block_time": "2019-09-27T15:29:04.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "92a56b9179c3b3dedda6cad12463699d38cab17831113902602c2d6faf063e47",
              "global_sequence": 1212192,
              "recv_sequence": 98,
              "auth_sequence": [
                [
                  "fio.treasury",
                  45
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "mintfio",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "amount": 26000000000
              },
              "hex_data": "0084b80d06000000"
            },
            "context_free": false,
            "elapsed": 40,
            "console": "\n\nMintfio called\n",
            "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
            "block_num": 1201737,
            "block_time": "2019-09-27T15:29:04.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "fio.token",
                  "response": "",
                  "act_digest": "745dc00cff6a2f8ec9322471bf66655afb5a7bd03e64b495b2e6ad9fc166fc25",
                  "global_sequence": 1212193,
                  "recv_sequence": 99,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "issue",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "to": "fio.treasury",
                    "quantity": "26.000000000 FIO",
                    "memo": "New tokens produced from reserves"
                  },
                  "hex_data": "e0afc646dd0ca85b0084b80d060000000946494f00000000214e657720746f6b656e732070726f64756365642066726f6d207265736572766573"
                },
                "context_free": false,
                "elapsed": 77,
                "console": "",
                "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
                "block_num": 1201737,
                "block_time": "2019-09-27T15:29:04.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": [
                  {
                    "receipt": "[Object]",
                    "act": "[Object]",
                    "context_free": false,
                    "elapsed": 122,
                    "console": "",
                    "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
                    "block_num": 1201737,
                    "block_time": "2019-09-27T15:29:04.000",
                    "producer_block_id": null,
                    "account_ram_deltas": "[Object]",
                    "except": null,
                    "inline_traces": "[Object]"
                  }
                ]
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.tpid",
              "response": "",
              "act_digest": "73d9ff58d742db86ee3c5ff0e5a2a75a33156fb4eec5a9fd90ff422e9605b594",
              "global_sequence": 1212197,
              "recv_sequence": 25,
              "auth_sequence": [
                [
                  "fio.treasury",
                  46
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.tpid",
              "name": "updatebounty",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "amount": 26000000000
              },
              "hex_data": "0084b80d06000000"
            },
            "context_free": false,
            "elapsed": 32,
            "console": "",
            "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
            "block_num": 1201737,
            "block_time": "2019-09-27T15:29:04.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.tpid",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.tpid",
              "response": "",
              "act_digest": "2fb98d182b18da247ca115fe8f2bf4101b17af5b4726b63ded7391ca3601abba",
              "global_sequence": 1212198,
              "recv_sequence": 26,
              "auth_sequence": [
                [
                  "fio.system",
                  64
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.tpid",
              "name": "updatetpid",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": {
                "tpid": "pawel366688@woohoo56311",
                "owner": "fio.system",
                "amount": 30000000000
              },
              "hex_data": "17706177656c3336363638383a776f6f686f6f3536333131008054197b0ca85b00ac23fc06000000"
            },
            "context_free": false,
            "elapsed": 105,
            "console": "calling updatetpid with tpid pawel366688@woohoo56311 owner fio.system amount 30000000000\n\ntpidfound: pawel366688@woohoo56311\nUpdating TPID.pawel366688@woohoo56311\n",
            "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
            "block_num": 1201737,
            "block_time": "2019-09-27T15:29:04.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "64ec87801586ad31f43048d96d1cf06acd73519749bf1f4940da8e87efa8b26c",
              "global_sequence": 1212199,
              "recv_sequence": 131,
              "auth_sequence": [
                [
                  "fio.system",
                  65
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bppoolupdate",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "0060153208000000"
            },
            "context_free": false,
            "elapsed": 34,
            "console": "",
            "trx_id": "15e4c6caeab6fe2664310bd7cfc510876baf10820b6290dc4b16aba653b7b1a1",
            "block_num": 1201737,
            "block_time": "2019-09-27T15:29:04.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid FIO domain"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "max_fee",
      "value": "200",
      "error": "Fee exceeds supplied maximum."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-renew-fio-domain-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO domain"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-renew-fio-domain-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Renew FIO Domain

<a id="opIdrenew_fio_domain_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_domain": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/renew_fio_domain',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /renew_fio_domain`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.address"
* name: "renewdomain"

> Body parameter

```json
{
  "fio_domain": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}
```

<h3 id="[content]-renew-fio-domain-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_domain|body|string|true|none|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» tpid|body|string|true|* FIO Address of the wallet which generates this transaction.|
|» actor|body|string|true|See [Generating actor](/actor)|

#### Detailed descriptions

**» tpid**: * FIO Address of the wallet which generates this transaction.
* This FIO Address will be paid 10% of the fee.
* See FIO Protocol#TPIDs for details.
* Set to empty if not known.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "expiration": "2020-09-11T18:30:56",
  "fee_collected": 30000000000
}
```

<h3 id="[content]-renew-fio-domain-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-renew-fio-domain-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» expiration|string(date-time)|false|none|none|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Renew FIO Address

<a id="opIdrenew_fio_address"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/renew_fio_address',
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

`POST /renew_fio_address`

When a domain is renewed:
* 365 days are added to the current expiration date (not date when renewal is ran)
* New bundle of transactions is added to the existing count.
* Example:
	* Bundled transaction before renewal: 20
	* Assuming every address gets 500 bundled transactions
	* Bundled transaction after renewal: 20

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-renew-fio-address-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response. 

```json
{
  "transaction_id": "955bffdb6695bb5a5e05413c2863d2b2b2bccaac7c8f079f8e43d522a5fa02f4",
  "processed": {
    "id": "955bffdb6695bb5a5e05413c2863d2b2b2bccaac7c8f079f8e43d522a5fa02f4",
    "block_num": 1201740,
    "block_time": "2019-09-27T15:29:05.500",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1071,
      "net_usage_words": 17
    },
    "elapsed": 1071,
    "net_usage": 136,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.address",
          "response": "{\"expiration\":\"2021-09-26T15:28:56\",\"fee_collected\":5000000000,\"status\":\"OK\"}",
          "act_digest": "e76bf94890e7273726d5020aee9af1910f8b1613672b265510678faab38ad6e3",
          "global_sequence": 1212203,
          "recv_sequence": 47,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              91
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.address",
          "name": "renewaddress",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_address": "pawel554427@woohoo56311",
            "max_fee": 5000000000,
            "tpid": "",
            "actor": "gev2yeim1cjy"
          },
          "hex_data": "17706177656c3535343432373a776f6f686f6f353633313100f2052a0100000000e01f0ad2292fb662"
        },
        "context_free": false,
        "elapsed": 875,
        "console": "5000000000\nfionamefound: \nCannot register TPID or FIO Address not found. The transaction will continue without TPID payment.\n1632670136 INSIDE.   2021   TESTINSIDE.   ",
        "trx_id": "955bffdb6695bb5a5e05413c2863d2b2b2bccaac7c8f079f8e43d522a5fa02f4",
        "block_num": 1201740,
        "block_time": "2019-09-27T15:29:05.500",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "1a7775344923ca0ff6340e6c0ae2d246ef2899f908a550741d0cfe02d4ce2c0d",
              "global_sequence": 1212204,
              "recv_sequence": 132,
              "auth_sequence": [
                [
                  "fio.system",
                  66
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "00e1f50500000000"
            },
            "context_free": false,
            "elapsed": 48,
            "console": "",
            "trx_id": "955bffdb6695bb5a5e05413c2863d2b2b2bccaac7c8f079f8e43d522a5fa02f4",
            "block_num": 1201740,
            "block_time": "2019-09-27T15:29:05.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "f549782fb7ac5903d111ca2e52dd25599b4220ff6958431da5c493cdc97cefca",
              "global_sequence": 1212205,
              "recv_sequence": 133,
              "auth_sequence": [
                [
                  "fio.system",
                  67
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bppoolupdate",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "0011102401000000"
            },
            "context_free": false,
            "elapsed": 35,
            "console": "",
            "trx_id": "955bffdb6695bb5a5e05413c2863d2b2b2bccaac7c8f079f8e43d522a5fa02f4",
            "block_num": 1201740,
            "block_time": "2019-09-27T15:29:05.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid FIO address"
* "FIO Domain expired"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "max_fee",
      "value": "200",
      "error": "Fee exceeds supplied maximum."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-renew-fio-address-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO address"
* "FIO Domain expired"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-renew-fio-address-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Renew FIO Address

<a id="opIdrenew_fio_address_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_address": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/renew_fio_address',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /renew_fio_address`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.address"
* name: "renewaddress"

> Body parameter

```json
{
  "fio_address": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}
```

<h3 id="[content]-renew-fio-address-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_address|body|string|true|none|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» tpid|body|string|true|* FIO Address of the wallet which generates this transaction.|
|» actor|body|string|true|See [Generating actor](/actor)|

#### Detailed descriptions

**» tpid**: * FIO Address of the wallet which generates this transaction.
* This FIO Address will be paid 10% of the fee.
* See FIO Protocol#TPIDs for details.
* Set to empty if not known.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "expiration": "2020-09-11T18:30:56",
  "fee_collected": 30000000000
}
```

<h3 id="[content]-renew-fio-address-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-renew-fio-address-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» expiration|string(date-time)|false|none|none|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Add public address

<a id="opIdadd_pub_address"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/add_pub_address',
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

`POST /add_pub_address`

This call allows a public address of the specific blockchain type to be added to the FIO Address, so that it can be returned using /pub_address_lookup

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-add-public-address-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "b8a66bca177ac9ba2060676abe2e60a02d3f81c6edc4c33ca9a7bed859a8ba73",
  "processed": {
    "id": "b8a66bca177ac9ba2060676abe2e60a02d3f81c6edc4c33ca9a7bed859a8ba73",
    "block_num": 1201783,
    "block_time": "2019-09-27T15:29:27.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 987,
      "net_usage_words": 27
    },
    "elapsed": 987,
    "net_usage": 216,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.address",
          "response": "{\"fee_collected\":0,\"status\":\"OK\"}",
          "act_digest": "cb4f2a246dbc26c93df7fed16db910b68e52fd34476848908e05eddabc3b143c",
          "global_sequence": 1212257,
          "recv_sequence": 53,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              94
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.address",
          "name": "addaddress",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_address": "pawel554427@woohoo56311",
            "token_code": "FIO",
            "public_address": "FIO59nUcEk5oasnQ2kBDhu6dK1i5cSn4zUqEfXhKHYpBxo5TGn9qo",
            "max_fee": 0,
            "actor": "gev2yeim1cjy",
            "tpid": "pawel554427@woohoo56311"
          },
          "hex_data": "17706177656c3535343432373a776f6f686f6f35363331310346494f3546494f35396e5563456b356f61736e51326b4244687536644b31693563536e347a5571456658684b48597042786f3554476e39716f0000000000000000e01f0ad2292fb66217706177656c3535343432373a776f6f686f6f3536333131"
        },
        "context_free": false,
        "elapsed": 891,
        "console": "",
        "trx_id": "b8a66bca177ac9ba2060676abe2e60a02d3f81c6edc4c33ca9a7bed859a8ba73",
        "block_num": 1201783,
        "block_time": "2019-09-27T15:29:27.000",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": []
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid Chain Code"
* "Invalid token code format"
* "Invalid public address format"
* "Min 1, Max 5 public addresses are allowed"
* "FIO Address expired"
* "FIO Domain expired"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"
* "Maximum token codes mapped to single FIO Address reached. Only 100 can be mapped."

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "token_code",
      "value": "BTC!",
      "error": "Invalid token code format"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

> Possible error messages:
* "FIO Address not found"

```json
{
  "message": "FIO Address not found"
}
```

<h3 id="[signed]-add-public-address-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid Chain Code"
* "Invalid token code format"
* "Invalid public address format"
* "Min 1, Max 5 public addresses are allowed"
* "FIO Address expired"
* "FIO Domain expired"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"
* "Maximum token codes mapped to single FIO Address reached. Only 100 can be mapped."|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Possible error messages:
* "FIO Address not found"|None|

<h3 id="[signed]-add-public-address-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Add public address

<a id="opIdadd_pub_address_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_address": "string",
  "public_addresses": [
    {
      "chain_code": "string",
      "token_code": "string",
      "public_address": {}
    }
  ],
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/add_pub_address',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /add_pub_address`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.address"
* name: "addaddress"

> Body parameter

```json
{
  "fio_address": "string",
  "public_addresses": [
    {
      "chain_code": "string",
      "token_code": "string",
      "public_address": {}
    }
  ],
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}
```

<h3 id="[content]-add-public-address-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_address|body|string|true|none|
|» public_addresses|body|[object]|true|Maximum of 5 token codes can be mapped to single FIO Address at any one time. See [Mapping Public Addresses](/wallet-integration-guide/mapping-pub-addresses) for details.|
|»» chain_code|body|string|true|Chain code identifies the blockchain, while token code identifies a token on that blockchain. For example: for USDC: chain_code = ETH and token_code = USDC, for BTC: chain_code = BTC and token_code = BTC. For list of chain codes you can refer to [SLIP-44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) and for list of token code refer to the specific blockchain.|
|»» token_code|body|string|true|Chain code identifies the blockchain, while token code identifies a token on that blockchain. For example: for USDC: chain_code = ETH and token_code = USDC, for BTC: chain_code = BTC and token_code = BTC. For list of chain codes you can refer to [SLIP-44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) and for list of token code refer to the specific blockchain.|
|»» public_address|body|object|true|This is the public address on another blockchain. Both integrated addresses as well as URI Scheme are supported.|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» tpid|body|string|true|* FIO Address of the wallet which generates this transaction.|
|» actor|body|string|true|See [Generating actor](/actor)|

#### Detailed descriptions

**body**: This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.

Please read [Mapping Public Addresses](/wallet-integration-guide/mapping-pub-addresses) to better understand how public address mappings work.

**»» public_address**: This is the public address on another blockchain. Both integrated addresses as well as URI Scheme are supported.

**Integrated Address**
If the blockchain supports it, an integrated address may be passed in just like standard public address. The FIO protocol does not perform validation on the passed string.

**URI Scheme**
FIO Protocol will support formatting of public addresses using URI were certain attributes are appended to the public address following a '?' and delimited with '&'. To allow inter-wallet operability, the following standardized parameters will be supported in official FIO Protocol SDKs.

**Parameters**
* dt - Ripple
* memo - Any - use as generic memo field
* memo_id -	Stellar
* memo_text -	Stellar
* memo_hash -	Stellar
* memo_return -	Stellar
* payment_id - Monero

**» tpid**: * FIO Address of the wallet which generates this transaction.
* This FIO Address will be paid 10% of the fee.
* See FIO Protocol#TPIDs for details.
* Set to empty if not known.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "fee_collected": 0
}
```

<h3 id="[content]-add-public-address-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-add-public-address-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Set FIO Domain's public flag

<a id="opIdset_fio_domain_public"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/set_fio_domain_public',
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

`POST /set_fio_domain_public`

By default all FIO Domains are non-public, meaning only the owner can register FIO Addresses on that domain. Setting them to public allows anyone to register a FIO Address on that domain.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-set-fio-domain's-public-flag-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response. 

```json
{
  "transaction_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
  "processed": {
    "id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
    "block_num": 1201732,
    "block_time": "2019-09-27T15:29:01.500",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1641,
      "net_usage_words": 19
    },
    "elapsed": 1641,
    "net_usage": 152,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.address",
          "response": "{\"expiration\":1601134133,\"fee_collected\":100000000,\"status\":\"OK\"}",
          "act_digest": "06e84db773a73f38f8855ae18f66f2a7493d1ea7ce1a71de9f6b9d72db8003d2",
          "global_sequence": 1212154,
          "recv_sequence": 44,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              83
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.address",
          "name": "setdomainpub",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_domain": "woohoo56311",
            "is_public": 1,
            "max_fee": 100000000,
            "actor": "gev2yeim1cjy",
            "tpid": "pawel554427@woohoo56311"
          },
          "hex_data": "0b776f6f686f6f35363331310100e1f50500000000e01f0ad2292fb66217706177656c3535343432373a776f6f686f6f3536333131"
        },
        "context_free": false,
        "elapsed": 761,
        "console": "100000000\nfionamefound: pawel554427@woohoo56311\n\nBounties: 26006500000\n\nBounty payout: 65000000\n\nTest Bucket Update Amount: 88000000\n",
        "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
        "block_num": 1201732,
        "block_time": "2019-09-27T15:29:01.500",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "8033a021142d625b56a360f4f92eb3172dd3a9ec144edf56887983ae9316b636",
              "global_sequence": 1212155,
              "recv_sequence": 89,
              "auth_sequence": [
                [
                  "gev2yeim1cjy",
                  84
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "gev2yeim1cjy",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "gev2yeim1cjy",
                "to": "fio.treasury",
                "quantity": "0.100000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00e1f505000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 122,
            "console": "",
            "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
            "block_num": 1201732,
            "block_time": "2019-09-27T15:29:01.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "8033a021142d625b56a360f4f92eb3172dd3a9ec144edf56887983ae9316b636",
                  "global_sequence": 1212156,
                  "recv_sequence": 21,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "0.100000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00e1f505000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 2,
                "console": "",
                "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
                "block_num": 1201732,
                "block_time": "2019-09-27T15:29:01.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "8033a021142d625b56a360f4f92eb3172dd3a9ec144edf56887983ae9316b636",
                  "global_sequence": 1212157,
                  "recv_sequence": 120,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "0.100000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00e1f505000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 8,
                "console": "",
                "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
                "block_num": 1201732,
                "block_time": "2019-09-27T15:29:01.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "6b32ed9f1442401dac9e11681bd627de8f3f361691107eb24466e6e3c9d81c73",
              "global_sequence": 1212158,
              "recv_sequence": 121,
              "auth_sequence": [
                [
                  "fio.system",
                  56
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "80841e0000000000"
            },
            "context_free": false,
            "elapsed": 40,
            "console": "",
            "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
            "block_num": 1201732,
            "block_time": "2019-09-27T15:29:01.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "070b84207f7ec9f800928d7dc8dae37091a0180ce040497e97808a972ee929f8",
              "global_sequence": 1212159,
              "recv_sequence": 90,
              "auth_sequence": [
                [
                  "fio.treasury",
                  41
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "mintfio",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "amount": 65000000
              },
              "hex_data": "40d2df0300000000"
            },
            "context_free": false,
            "elapsed": 41,
            "console": "\n\nMintfio called\n",
            "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
            "block_num": 1201732,
            "block_time": "2019-09-27T15:29:01.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "fio.token",
                  "response": "",
                  "act_digest": "6af6f9909d4a58b569ce1da89763b096c696d838cda34d9dc2a4a665d3c82cc9",
                  "global_sequence": 1212160,
                  "recv_sequence": 91,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "issue",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "to": "fio.treasury",
                    "quantity": "0.065000000 FIO",
                    "memo": "New tokens produced from reserves"
                  },
                  "hex_data": "e0afc646dd0ca85b40d2df03000000000946494f00000000214e657720746f6b656e732070726f64756365642066726f6d207265736572766573"
                },
                "context_free": false,
                "elapsed": 79,
                "console": "",
                "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
                "block_num": 1201732,
                "block_time": "2019-09-27T15:29:01.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": [
                  {
                    "receipt": "[Object]",
                    "act": "[Object]",
                    "context_free": false,
                    "elapsed": 110,
                    "console": "",
                    "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
                    "block_num": 1201732,
                    "block_time": "2019-09-27T15:29:01.500",
                    "producer_block_id": null,
                    "account_ram_deltas": "[Object]",
                    "except": null,
                    "inline_traces": "[Object]"
                  }
                ]
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.tpid",
              "response": "",
              "act_digest": "22b343e04f560596657caa707f143d46d1bbfe4f82e3c977c3877bad577cf5c3",
              "global_sequence": 1212164,
              "recv_sequence": 21,
              "auth_sequence": [
                [
                  "fio.treasury",
                  42
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.tpid",
              "name": "updatebounty",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "amount": 65000000
              },
              "hex_data": "40d2df0300000000"
            },
            "context_free": false,
            "elapsed": 39,
            "console": "",
            "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
            "block_num": 1201732,
            "block_time": "2019-09-27T15:29:01.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.tpid",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.tpid",
              "response": "",
              "act_digest": "9a5abe3cad6dc41b58cfb87825290b810a4a0061d2ffce986a29250b7c5bdfdc",
              "global_sequence": 1212165,
              "recv_sequence": 22,
              "auth_sequence": [
                [
                  "fio.system",
                  57
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.tpid",
              "name": "updatetpid",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": {
                "tpid": "pawel554427@woohoo56311",
                "owner": "fio.system",
                "amount": 75000000
              },
              "hex_data": "17706177656c3535343432373a776f6f686f6f3536333131008054197b0ca85bc068780400000000"
            },
            "context_free": false,
            "elapsed": 92,
            "console": "calling updatetpid with tpid pawel554427@woohoo56311 owner fio.system amount 75000000\n\ntpidfound: pawel554427@woohoo56311\nUpdating TPID.pawel554427@woohoo56311\n",
            "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
            "block_num": 1201732,
            "block_time": "2019-09-27T15:29:01.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "9bfc4ff9f88833f90ba5cf7139d963d9f1d1c0760c0d9179c028761080a1bcd8",
              "global_sequence": 1212166,
              "recv_sequence": 123,
              "auth_sequence": [
                [
                  "fio.system",
                  58
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bprewdupdate",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": "00c63e0500000000"
            },
            "context_free": false,
            "elapsed": 35,
            "console": "",
            "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
            "block_num": 1201732,
            "block_time": "2019-09-27T15:29:01.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "eosio",
              "response": "",
              "act_digest": "a1b8416ef696397bf36ce938aa6b0d45ec3e9cfefd98701475bae3bb58d3b37e",
              "global_sequence": 1212167,
              "recv_sequence": 1201866,
              "auth_sequence": [
                [
                  "fio.system",
                  59
                ]
              ],
              "code_sequence": 2,
              "abi_sequence": 2
            },
            "act": {
              "account": "eosio",
              "name": "updatepower",
              "authorization": [
                {
                  "actor": "fio.system",
                  "permission": "active"
                }
              ],
              "data": {
                "voter": "gev2yeim1cjy",
                "updateonly": 1
              },
              "hex_data": "e01f0ad2292fb66201"
            },
            "context_free": false,
            "elapsed": 63,
            "console": " called update power.\n",
            "trx_id": "fae9ef14f9b0b7dca4512abfe8e2236d02da620863454ab4dfd3ebe748df4db9",
            "block_num": 1201732,
            "block_time": "2019-09-27T15:29:01.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid FIO domain"
* "FIO Domain expired"
* "Only 0 or 1 allowed"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "max_fee",
      "value": "200",
      "error": "Fee exceeds supplied maximum."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-set-fio-domain's-public-flag-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO domain"
* "FIO Domain expired"
* "Only 0 or 1 allowed"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-set-fio-domain's-public-flag-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Set FIO Domain's public flag

<a id="opIdset_fio_domain_public_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_domain": "string",
  "is_public": 0,
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/set_fio_domain_public',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /set_fio_domain_public`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.address"
* name: "setdomainpub"

> Body parameter

```json
{
  "fio_domain": "string",
  "is_public": 0,
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}
```

<h3 id="[content]-set-fio-domain's-public-flag-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_domain|body|string|true|none|
|» is_public|body|integer|true|* 1 - allows anyone to register FIO Address|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» tpid|body|string|true|* FIO Address of the wallet which generates this transaction.|
|» actor|body|string|true|See [Generating actor](/actor)|

#### Detailed descriptions

**» is_public**: * 1 - allows anyone to register FIO Address
* 0 - only owner of domain can register FIO Address

**» tpid**: * FIO Address of the wallet which generates this transaction.
* This FIO Address will be paid 10% of the fee.
* See FIO Protocol#TPIDs for details.
* Set to empty if not known.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "fee_collected": 10000000
}
```

<h3 id="[content]-set-fio-domain's-public-flag-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-set-fio-domain's-public-flag-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Create new funds request

<a id="opIdnew_funds_request"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/new_funds_request',
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

`POST /new_funds_request`

This api method will create a new funds request on the FIO chain.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-create-new-funds-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "864e31d9ba2c31b9cf0307e33b339447689d2d604ff79c4f3a1a8175e28caed6",
  "processed": {
    "id": "864e31d9ba2c31b9cf0307e33b339447689d2d604ff79c4f3a1a8175e28caed6",
    "block_num": 1201809,
    "block_time": "2019-09-27T15:29:40.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1435,
      "net_usage_words": 25
    },
    "elapsed": 1435,
    "net_usage": 200,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.reqobt",
          "response": "{\"fee_collected\":0,\"fio_request_id\":3,\"status\":\"requested\"}",
          "act_digest": "f832fd5879f3fec51b960c3032959e27cc4d3f4bda359927b590fae1e96a466e",
          "global_sequence": 1212288,
          "recv_sequence": 8,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              97
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.reqobt",
          "name": "newfundsreq",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "payer_fio_address": "pawel366688@woohoo56311",
            "payee_fio_address": "pawel554427@woohoo56311",
            "content": "blahblah",
            "max_fee": 0,
            "actor": "gev2yeim1cjy",
            "tpid": "pawel554427@woohoo56311"
          },
          "hex_data": "17706177656c3336363638383a776f6f686f6f353633313117706177656c3535343432373a776f6f686f6f353633313108626c6168626c616800000000000000000c676576327965696d31636a7917706177656c3535343432373a776f6f686f6f3536333131"
        },
        "context_free": false,
        "elapsed": 1117,
        "console": "account: 7112924518142320608 actor: gev2yeim1cjy\n",
        "trx_id": "864e31d9ba2c31b9cf0307e33b339447689d2d604ff79c4f3a1a8175e28caed6",
        "block_num": 1201809,
        "block_time": "2019-09-27T15:29:40.000",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "fio.reqobt",
            "delta": 457
          }
        ],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.system",
              "response": "",
              "act_digest": "ff38b9fd6fa5929f91b48870520fb2dd20fa06ff94657289194eec6009ee971d",
              "global_sequence": 1212289,
              "recv_sequence": 58,
              "auth_sequence": [
                [
                  "fio.reqobt",
                  11
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.system",
              "name": "decrcounter",
              "authorization": [
                {
                  "actor": "fio.reqobt",
                  "permission": "active"
                }
              ],
              "data": "17706177656c3535343432373a776f6f686f6f3536333131"
            },
            "context_free": false,
            "elapsed": 198,
            "console": "",
            "trx_id": "864e31d9ba2c31b9cf0307e33b339447689d2d604ff79c4f3a1a8175e28caed6",
            "block_num": 1201809,
            "block_time": "2019-09-27T15:29:40.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "No such FIO Address"
* "FIO Address expired"
* "FIO Domain expired"
* "Requires min 64 max 296 size"
* "Invalid fee value"
* "Fee exceeds maximum"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "payer_fio_address",
      "value": "asdfg@pqowieuryt67",
      "error": "No such FIO Address"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor
* Payee FIO Address not owned by FIO Public Key in signature

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-create-new-funds-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "No such FIO Address"
* "FIO Address expired"
* "FIO Domain expired"
* "Requires min 64 max 296 size"
* "Invalid fee value"
* "Fee exceeds maximum"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor
* Payee FIO Address not owned by FIO Public Key in signature|Inline|

<h3 id="[signed]-create-new-funds-request-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Create new funds request

<a id="opIdnew_funds_request_model"></a>

> Code samples

```javascript
const inputBody = '{
  "payer_fio_address": "string",
  "payee_fio_address": "string",
  "content": {
    "payee_public_address": "string",
    "amount": "string",
    "chain_code": "string",
    "token_code": "string",
    "memo": "string",
    "hash": "string",
    "offline_url": "string",
    "future_use1": "string",
    "future_use2": "string",
    "future_use3": "string",
    "future_use4": "string",
    "future_use5": "string"
  },
  "max_fee": 0,
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/new_funds_request',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /new_funds_request`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.reqobt"
* name: "newfundsreq"

> Body parameter

```json
{
  "payer_fio_address": "string",
  "payee_fio_address": "string",
  "content": {
    "payee_public_address": "string",
    "amount": "string",
    "chain_code": "string",
    "token_code": "string",
    "memo": "string",
    "hash": "string",
    "offline_url": "string",
    "future_use1": "string",
    "future_use2": "string",
    "future_use3": "string",
    "future_use4": "string",
    "future_use5": "string"
  },
  "max_fee": 0,
  "actor": "string"
}
```

<h3 id="[content]-create-new-funds-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» payer_fio_address|body|string|true|none|
|» payee_fio_address|body|string|true|none|
|» content|body|object|true|Certain content inside FIO Request is encrypted and packed into this field.|
|»» payee_public_address|body|string|true|This is the public address on another blockchain. Both integrated addresses as well as URI Scheme are supported.|
|»» amount|body|string|true|Amount requested.|
|»» chain_code|body|string|true|Chain code identifies the blockchain, while token code identifies a token on that blockchain. For example: for USDC: chain_code = ETH and token_code = USDC, for BTC: chain_code = BTC and token_code = BTC. For list of chain codes you can refer to [SLIP-44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) and for list of token code refer to the specific blockchain.|
|»» token_code|body|string|true|Chain code identifies the blockchain, while token code identifies a token on that blockchain. For example: for USDC: chain_code = ETH and token_code = USDC, for BTC: chain_code = BTC and token_code = BTC. For list of chain codes you can refer to [SLIP-44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) and for list of token code refer to the specific blockchain.|
|»» memo|body|string|true|Free-form text to pass to Payer.|
|»» hash|body|string|true|Hash of off-chain data.|
|»» offline_url|body|string|true|Url of where to find off-chain data.|
|»» future_use1|body|string|true|Do not use|
|»» future_use2|body|string|true|Do not use|
|»» future_use3|body|string|true|Do not use|
|»» future_use4|body|string|true|Do not use|
|»» future_use5|body|string|true|Do not use|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» actor|body|string|true|See [Generating actor](/actor)|

#### Detailed descriptions

**» content**: Certain content inside FIO Request is encrypted and packed into this field.

Min 64 characters
Max 296 characters

See [Encrypting FIO Data](/wallet-integration-guide/encrypting-fio-data) for more information.

**»» payee_public_address**: This is the public address on another blockchain. Both integrated addresses as well as URI Scheme are supported.

**Integrated Address**
If the blockchain supports it, an integrated address may be passed in just like standard public address. The FIO protocol does not perform validation on the passed string.

**URI Scheme**
FIO Protocol will support formatting of public addresses using URI were certain attributes are appended to the public address following a '?' and delimited with '&'. To allow inter-wallet operability, the following standardized parameters will be supported in official FIO Protocol SDKs.

**Parameters**
* dt - Ripple
* memo - Any - use as generic memo field
* memo_id -	Stellar
* memo_text -	Stellar
* memo_hash -	Stellar
* memo_return -	Stellar
* payment_id - Monero

**»» memo**: Free-form text to pass to Payer.

Use either memo or hash/offline_url, but not both.

**»» hash**: Hash of off-chain data.

Use either memo or hash/offline_url, but not both.

**»» offline_url**: Url of where to find off-chain data.

Use either memo or hash/offline_url, but not both.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "fio_request_id": 10,
  "status": "requested",
  "fee_collected": 0
}
```

<h3 id="[content]-create-new-funds-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-create-new-funds-request-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» fio_request_id|integer|false|none|ID of FIO Request created|
|» status|string|false|none|Status of FIO Request|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

#### Enumerated Values

|Property|Value|
|---|---|
|status|requested|
|status|request_rejected|
|status|sent_to_blockchain|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Reject funds request

<a id="opIdreject_funds_request"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/reject_funds_request',
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

`POST /reject_funds_request`

Reject funds request.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-reject-funds-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "7926ae661fff4be977cb0d24cc7f2dc593c6a9bc90512acc6f540eb3c7f96b4d",
  "processed": {
    "id": "7926ae661fff4be977cb0d24cc7f2dc593c6a9bc90512acc6f540eb3c7f96b4d",
    "block_num": 1201821,
    "block_time": "2019-09-27T15:29:46.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1297,
      "net_usage_words": 15
    },
    "elapsed": 1297,
    "net_usage": 120,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.reqobt",
          "response": "{\"fee_collected\":0,\"status\":\"request_rejected\"}",
          "act_digest": "35caa21c5cfe80537b7e8447457eb030ed1fe5e00f30b219bb593d6b1f85c7b2",
          "global_sequence": 1212308,
          "recv_sequence": 12,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              98
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.reqobt",
          "name": "rejectfndreq",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_request_id": "4",
            "max_fee": 0,
            "actor": "gev2yeim1cjy",
            "tpid": ""
          },
          "hex_data": "013400000000000000000c676576327965696d31636a7900"
        },
        "context_free": false,
        "elapsed": 858,
        "console": "call new funds request\naccount: 7112924518142320608 actor: gev2yeim1cjy\n",
        "trx_id": "7926ae661fff4be977cb0d24cc7f2dc593c6a9bc90512acc6f540eb3c7f96b4d",
        "block_num": 1201821,
        "block_time": "2019-09-27T15:29:46.000",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "fio.reqobt",
            "delta": 273
          }
        ],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.system",
              "response": "",
              "act_digest": "ff38b9fd6fa5929f91b48870520fb2dd20fa06ff94657289194eec6009ee971d",
              "global_sequence": 1212309,
              "recv_sequence": 62,
              "auth_sequence": [
                [
                  "fio.reqobt",
                  15
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.system",
              "name": "decrcounter",
              "authorization": [
                {
                  "actor": "fio.reqobt",
                  "permission": "active"
                }
              ],
              "data": "17706177656c3535343432373a776f6f686f6f3536333131"
            },
            "context_free": false,
            "elapsed": 201,
            "console": "",
            "trx_id": "7926ae661fff4be977cb0d24cc7f2dc593c6a9bc90512acc6f540eb3c7f96b4d",
            "block_num": 1201821,
            "block_time": "2019-09-27T15:29:46.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "No such FIO Request"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "FIO Address expired"
* "FIO Domain expired"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_request_id",
      "value": "10000000000",
      "error": "No such FIO Request"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor
* Payer's FIO Address in specified fio_request_id is not owned by the public key in signature

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-reject-funds-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "No such FIO Request"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "FIO Address expired"
* "FIO Domain expired"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor
* Payer's FIO Address in specified fio_request_id is not owned by the public key in signature|Inline|

<h3 id="[signed]-reject-funds-request-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Reject funds request

<a id="opIdreject_funds_request_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_request_id": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/reject_funds_request',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /reject_funds_request`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.reqobt"
* name: "rejectfndreq"

> Body parameter

```json
{
  "fio_request_id": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}
```

<h3 id="[content]-reject-funds-request-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_request_id|body|string|true|none|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» tpid|body|string|true|* FIO Address of the wallet which generates this transaction.|
|» actor|body|string|true|See [Generating actor](/actor)|

#### Detailed descriptions

**» tpid**: * FIO Address of the wallet which generates this transaction.
* This FIO Address will be paid 10% of the fee.
* See FIO Protocol#TPIDs for details.
* Set to empty if not known.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "request_rejected",
  "fee_collected": 0
}
```

<h3 id="[content]-reject-funds-request-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-reject-funds-request-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|Status of FIO Request|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

#### Enumerated Values

|Property|Value|
|---|---|
|status|requested|
|status|request_rejected|
|status|sent_to_blockchain|

<aside class="success">
This operation does not require authentication
</aside>

## Get FIO Requests sent out

<a id="opIdget_sent_fio_requests"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_public_key": "string",
  "limit": 0,
  "offset": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_sent_fio_requests',
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

`POST /get_sent_fio_requests`

Sent requests call polls for any requests sent by provided FIO public key.

> Body parameter

```json
{
  "fio_public_key": "string",
  "limit": 0,
  "offset": 0
}
```

<h3 id="get-fio-requests-sent-out-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» fio_public_key|body|string|true|Valid WIF Public Key with FIO Prefix|
|» limit|body|integer|false|Number of requests to return. If omitted, all requests will be returned.|
|» offset|body|integer|false|First request from list to return. If omitted, 0 is assumed.|

> Example responses

```json
{
  "requests": [
    {
      "fio_request_id": "309753b6b0aca9ba107c06332c4294ec2d8a270133a17239f07bc62b704ccb87",
      "payer_fio_address": "purse@alice",
      "payee_fio_address": "crypto@bob",
      "payer_fio_public_key": "FIO7167ErgCveJvuonvrEvVGhdWnkP4AEMfqvEd8s8raMkbbAXqhx",
      "payee_fio_public_key": "FIO7KGdMYj4ZMY2nUX9EaZu3G3GxZhTNXUq1tsNqC5rcP9rcmvWHq",
      "content": "...",
      "time_stamp": "2020-09-11T18:30:56",
      "status": "rejected"
    }
  ],
  "more": 0
}
```

> Possible error messages:
* "Invalid FIO Public Key"
* "Invalid limit"
* "Invalid offset"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_public_key",
      "value": "FIO123",
      "error": "Invalid FIO Public Key"
    }
  ]
}
```

> Possible error messages:
* "No FIO Requests"

```json
{
  "message": "No FIO Requests"
}
```

<h3 id="get-fio-requests-sent-out-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Public Key"
* "Invalid limit"
* "Invalid offset"|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|Possible error messages:
* "No FIO Requests"|Inline|

<h3 id="get-fio-requests-sent-out-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» requests|[object]|false|none|Multiple requests may be returned. All requests are returned.|
|»» fio_request_id|string|false|none|Id of that funds request.|
|»» payer_fio_address|string|false|none|FIO Address of the payer. This address initiated payment.|
|»» payee_fio_address|string|false|none|FIO Address of the payee. This address is receiving payment.|
|»» payer_fio_public_key|string|false|none|FIO public key of the payer.|
|»» payee_fio_public_key|string|false|none|FIO public key of the payee.|
|»» content|object|false|none|Certain content inside FIO Request is encrypted and packed into this field.<br /><br />Min 64 characters<br />Max 296 characters|
|»»» payee_public_address|object|true|none|This is the public address on another blockchain. Both integrated addresses as well as URI Scheme are supported.<br /><br />**Integrated Address**<br />If the blockchain supports it, an integrated address may be passed in just like standard public address. The FIO protocol does not perform validation on the passed string.<br /><br />**URI Scheme**<br />FIO Protocol will support formatting of public addresses using URI were certain attributes are appended to the public address following a '?' and delimited with '&'. To allow inter-wallet operability, the following standardized parameters will be supported in official FIO Protocol SDKs.<br /><br />**Parameters**<br />* dt - Ripple<br />* memo - Any - use as generic memo field<br />* memo_id -	Stellar<br />* memo_text -	Stellar<br />* memo_hash -	Stellar<br />* memo_return -	Stellar<br />* payment_id - Monero|
|»»» amount|string|true|none|Amount requested.|
|»»» token_code|string|true|none|none|
|»»» memo|string|true|none|none|
|»»» hash|string|true|none|none|
|»»» offline_url|string|true|none|none|
|»»» future_use1|string|true|none|none|
|»»» future_use2|string|true|none|none|
|»»» future_use3|string|true|none|none|
|»»» future_use4|string|true|none|none|
|»»» future_use5|string|true|none|none|
|»» time_stamp|string|false|none|Timestamp of request|
|»» status|string|false|none|Status of FIO Request|
|» more|integer|false|none|0 - no more results<br />1 - more results|

#### Enumerated Values

|Property|Value|
|---|---|
|status|requested|
|status|sent_to_blockchain|
|status|rejected|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **404**

*Error 404*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Records other blockchain transaction data on another blockchain

<a id="opIdrecord_obt_data"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/record_obt_data',
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

`POST /record_obt_data`

This call is made to record Other Blockchain Transaction (OBT) data on the FIO blockchain, e.g. 1 BTC was sent on Bitcoin Blockchain, and both sender and receiver have FIO Addresses.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-records-other-blockchain-transaction-data-on-another-blockchain-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "26fe8a771f10a090af9f768df298532af9437fa5791bdf09a3a8cc2ad8a46963",
  "processed": {
    "id": "26fe8a771f10a090af9f768df298532af9437fa5791bdf09a3a8cc2ad8a46963",
    "block_num": 1201815,
    "block_time": "2019-09-27T15:29:43.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1474,
      "net_usage_words": 22
    },
    "elapsed": 1474,
    "net_usage": 176,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.reqobt",
          "response": "{\"fee_collected\":0,\"status\":\"sent_to_blockchain\"}",
          "act_digest": "ebdc19ee477b844a62281d345785a5d329516f313675e4b169c3b1d8e87cfa82",
          "global_sequence": 1212298,
          "recv_sequence": 10,
          "auth_sequence": [
            [
              "2ugokdhavqow",
              26
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.reqobt",
          "name": "recordsend",
          "authorization": [
            {
              "actor": "2ugokdhavqow",
              "permission": "active"
            }
          ],
          "data": {
            "fio_request_id": "3",
            "payer_fio_address": "pawel366688@woohoo56311",
            "payee_fio_address": "pawel554427@woohoo56311",
            "content": "blahblah",
            "max_fee": 0,
            "actor": "2ugokdhavqow",
            "tpid": ""
          },
          "hex_data": "013317706177656c3336363638383a776f6f686f6f353633313117706177656c3535343432373a776f6f686f6f353633313108626c6168626c616800000000000000000c3275676f6b64686176716f7700"
        },
        "context_free": false,
        "elapsed": 1089,
        "console": "account: 1628412066821679552 actor: 2ugokdhavqow\n",
        "trx_id": "26fe8a771f10a090af9f768df298532af9437fa5791bdf09a3a8cc2ad8a46963",
        "block_num": 1201815,
        "block_time": "2019-09-27T15:29:43.000",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "fio.reqobt",
            "delta": 273
          }
        ],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.system",
              "response": "",
              "act_digest": "bcdbc290d77ef37aeff34a75a651abf1520630fadeea82efafaa1bec7cc97cfb",
              "global_sequence": 1212299,
              "recv_sequence": 60,
              "auth_sequence": [
                [
                  "fio.reqobt",
                  13
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.system",
              "name": "decrcounter",
              "authorization": [
                {
                  "actor": "fio.reqobt",
                  "permission": "active"
                }
              ],
              "data": "17706177656c3336363638383a776f6f686f6f3536333131"
            },
            "context_free": false,
            "elapsed": 202,
            "console": "",
            "trx_id": "26fe8a771f10a090af9f768df298532af9437fa5791bdf09a3a8cc2ad8a46963",
            "block_num": 1201815,
            "block_time": "2019-09-27T15:29:43.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "No such FIO Address"
* "FIO Address expired"
* "FIO Domain expired"
* "Requires min 64 max 432 size"
* "No such FIO Request"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "payee_fio_address",
      "value": "asdfg@pqowieuryt67",
      "error": "No such FIO Address"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor
* Payer's FIO Address not owned by FIO Public Key in signature

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-records-other-blockchain-transaction-data-on-another-blockchain-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "No such FIO Address"
* "FIO Address expired"
* "FIO Domain expired"
* "Requires min 64 max 432 size"
* "No such FIO Request"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor
* Payer's FIO Address not owned by FIO Public Key in signature|Inline|

<h3 id="[signed]-records-other-blockchain-transaction-data-on-another-blockchain-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Records send on another blockchain

<a id="opIdrecord_obt_data_model"></a>

> Code samples

```javascript
const inputBody = '{
  "payer_fio_address": "string",
  "payee_fio_address": "string",
  "content": {
    "payer_public_address": "string",
    "payee_public_address": "string",
    "amount": "string",
    "chain_code": "string",
    "token_code": "string",
    "status": "string",
    "obt_id": "string",
    "memo": "string",
    "hash": "string",
    "offline_url": "string"
  },
  "fio_request_id": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/record_obt_data',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /record_obt_data`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.reqobt"
* name: "recordobt"

> Body parameter

```json
{
  "payer_fio_address": "string",
  "payee_fio_address": "string",
  "content": {
    "payer_public_address": "string",
    "payee_public_address": "string",
    "amount": "string",
    "chain_code": "string",
    "token_code": "string",
    "status": "string",
    "obt_id": "string",
    "memo": "string",
    "hash": "string",
    "offline_url": "string"
  },
  "fio_request_id": "string",
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}
```

<h3 id="[content]-records-send-on-another-blockchain-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» payer_fio_address|body|string|true|FIO Address of the payer. This address initiated payment. Also MUST be the same one signing the transaction|
|» payee_fio_address|body|string|true|FIO Address of the payee. This address is receiving payment.|
|» content|body|object|true|Certain content inside FIO Data is encrypted and packed into this field.|
|»» payer_public_address|body|string|true|Public address on other blockchain of user sending funds.|
|»» payee_public_address|body|string|true|Public address on other blockchain of user receiving funds.|
|»» amount|body|string|true|Amount sent.|
|»» chain_code|body|string|true|Chain code identifies the blockchain, while token code identifies a token on that blockchain. For example: for USDC: chain_code = ETH and token_code = USDC, for BTC: chain_code = BTC and token_code = BTC. For list of chain codes you can refer to [SLIP-44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) and for list of token code refer to the specific blockchain.|
|»» token_code|body|string|true|Chain code identifies the blockchain, while token code identifies a token on that blockchain. For example: for USDC: chain_code = ETH and token_code = USDC, for BTC: chain_code = BTC and token_code = BTC. For list of chain codes you can refer to [SLIP-44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) and for list of token code refer to the specific blockchain.|
|»» status|body|string|true|Status of this OBT. Allowed statuses are:|
|»» obt_id|body|string|true|Other Blockchain Transaction ID (OBT ID), i.e Bitcoin transaction ID|
|»» memo|body|string|true|Free-form text to pass to Payee.|
|»» hash|body|string|true|Hash of off-chain data.|
|»» offline_url|body|string|true|Url of where to find off-chain data.|
|» fio_request_id|body|string|true|* Send empty if no FIO Request ID|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» tpid|body|string|true|* FIO Address of the wallet which generates this transaction.|
|» actor|body|string|true|See [Generating actor](/actor)|

#### Detailed descriptions

**» content**: Certain content inside FIO Data is encrypted and packed into this field.

Min 64 characters
Max 432 characters

See [Encrypting FIO Data](/wallet-integration-guide/encrypting-fio-data) for more information.

**»» status**: Status of this OBT. Allowed statuses are:
* sent_to_blockchain

**»» memo**: Free-form text to pass to Payee.

Use either memo or hash/offline_url, but not both.

**»» hash**: Hash of off-chain data.

Use either memo or hash/offline_url, but not both.

**»» offline_url**: Url of where to find off-chain data.

Use either memo or hash/offline_url, but not both.

**» fio_request_id**: * Send empty if no FIO Request ID
* ID of FIO Request, if this Record Send transaction is in response to a previously received FIO Request.

**» tpid**: * FIO Address of the wallet which generates this transaction.
* This FIO Address will be paid 10% of the fee.
* See FIO Protocol#TPIDs for details.
* Set to empty if not known.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "sent_to_blockchain",
  "fee_collected": 0
}
```

<h3 id="[content]-records-send-on-another-blockchain-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-records-send-on-another-blockchain-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|sent_to_blockchain|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Transfer FIO tokens

<a id="opIdtransfer_tokens_pub_key"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/transfer_tokens_pub_key',
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

`POST /transfer_tokens_pub_key`

This call transfers FIO tokens using FIO public key

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-transfer-fio-tokens-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
  "processed": {
    "id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
    "block_num": 1201702,
    "block_time": "2019-09-27T15:28:46.500",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1931,
      "net_usage_words": 23
    },
    "elapsed": 1931,
    "net_usage": 184,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.token",
          "response": "{\"fee_collected\":250000000,\"status\":\"OK\"}",
          "act_digest": "3cd952d84e9000f76f98c532e71d4fe87c1fdf7d8cb23e5df498fba0fd8fa72e",
          "global_sequence": 1212081,
          "recv_sequence": 81,
          "auth_sequence": [
            [
              "r41zuwovtn44",
              39
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.token",
          "name": "trnsfiopubky",
          "authorization": [
            {
              "actor": "r41zuwovtn44",
              "permission": "active"
            }
          ],
          "data": {
            "payee_public_key": "FIO8PRe4WRZJj5mkem6qVGKyvNFgPsNnjNN6kPhh6EaCpzCVin5Jj",
            "amount": "1000000000000",
            "max_fee": 250000000,
            "actor": "r41zuwovtn44",
            "tpid": ""
          },
          "hex_data": "3546494f385052653457525a4a6a356d6b656d367156474b79764e466750734e6e6a4e4e366b50686836456143707a4356696e354a6a0d3130303030303030303030303080b2e60e0000000040c8cc9b72fd03b900"
        },
        "context_free": false,
        "elapsed": 1301,
        "console": "hashed account name from the payee_public_key gev2yeim1cjy\nCollecting FIO API fees: 0.250000000 FIO\nfionamefound: \nCannot register TPID or FIO Address not found. The transaction will continue without TPID payment.\n",
        "trx_id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
        "block_num": 1201702,
        "block_time": "2019-09-27T15:28:46.500",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "r41zuwovtn44",
              "response": "{\"fee_collected\":250000000,\"status\":\"OK\"}",
              "act_digest": "3cd952d84e9000f76f98c532e71d4fe87c1fdf7d8cb23e5df498fba0fd8fa72e",
              "global_sequence": 1212082,
              "recv_sequence": 12,
              "auth_sequence": [
                [
                  "r41zuwovtn44",
                  40
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "trnsfiopubky",
              "authorization": [
                {
                  "actor": "r41zuwovtn44",
                  "permission": "active"
                }
              ],
              "data": {
                "payee_public_key": "FIO8PRe4WRZJj5mkem6qVGKyvNFgPsNnjNN6kPhh6EaCpzCVin5Jj",
                "amount": "1000000000000",
                "max_fee": 250000000,
                "actor": "r41zuwovtn44",
                "tpid": ""
              },
              "hex_data": "3546494f385052653457525a4a6a356d6b656d367156474b79764e466750734e6e6a4e4e366b50686836456143707a4356696e354a6a0d3130303030303030303030303080b2e60e0000000040c8cc9b72fd03b900"
            },
            "context_free": false,
            "elapsed": 5,
            "console": "",
            "trx_id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
            "block_num": 1201702,
            "block_time": "2019-09-27T15:28:46.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "{\"fee_collected\":250000000,\"status\":\"OK\"}",
              "act_digest": "3cd952d84e9000f76f98c532e71d4fe87c1fdf7d8cb23e5df498fba0fd8fa72e",
              "global_sequence": 1212083,
              "recv_sequence": 104,
              "auth_sequence": [
                [
                  "r41zuwovtn44",
                  41
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "trnsfiopubky",
              "authorization": [
                {
                  "actor": "r41zuwovtn44",
                  "permission": "active"
                }
              ],
              "data": {
                "payee_public_key": "FIO8PRe4WRZJj5mkem6qVGKyvNFgPsNnjNN6kPhh6EaCpzCVin5Jj",
                "amount": "1000000000000",
                "max_fee": 250000000,
                "actor": "r41zuwovtn44",
                "tpid": ""
              },
              "hex_data": "3546494f385052653457525a4a6a356d6b656d367156474b79764e466750734e6e6a4e4e366b50686836456143707a4356696e354a6a0d3130303030303030303030303080b2e60e0000000040c8cc9b72fd03b900"
            },
            "context_free": false,
            "elapsed": 16,
            "console": "",
            "trx_id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
            "block_num": 1201702,
            "block_time": "2019-09-27T15:28:46.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "gev2yeim1cjy",
              "response": "{\"fee_collected\":250000000,\"status\":\"OK\"}",
              "act_digest": "3cd952d84e9000f76f98c532e71d4fe87c1fdf7d8cb23e5df498fba0fd8fa72e",
              "global_sequence": 1212084,
              "recv_sequence": 16,
              "auth_sequence": [
                [
                  "r41zuwovtn44",
                  42
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "trnsfiopubky",
              "authorization": [
                {
                  "actor": "r41zuwovtn44",
                  "permission": "active"
                }
              ],
              "data": {
                "payee_public_key": "FIO8PRe4WRZJj5mkem6qVGKyvNFgPsNnjNN6kPhh6EaCpzCVin5Jj",
                "amount": "1000000000000",
                "max_fee": 250000000,
                "actor": "r41zuwovtn44",
                "tpid": ""
              },
              "hex_data": "3546494f385052653457525a4a6a356d6b656d367156474b79764e466750734e6e6a4e4e366b50686836456143707a4356696e354a6a0d3130303030303030303030303080b2e60e0000000040c8cc9b72fd03b900"
            },
            "context_free": false,
            "elapsed": 3,
            "console": "",
            "trx_id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
            "block_num": 1201702,
            "block_time": "2019-09-27T15:28:46.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "efcccf217b786e16ddd9b413a87c540d0d91c38bf251153f4b62b4831fe91d5f",
              "global_sequence": 1212085,
              "recv_sequence": 105,
              "auth_sequence": [
                [
                  "fio.token",
                  18
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "fio.token",
                  "permission": "active"
                }
              ],
              "data": "404b4c0000000000"
            },
            "context_free": false,
            "elapsed": 63,
            "console": "",
            "trx_id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
            "block_num": 1201702,
            "block_time": "2019-09-27T15:28:46.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "ef00f54eaa4fa31188e86466202e9c14b66ebe1f7248ce7f5f84ef70239f0bbc",
              "global_sequence": 1212086,
              "recv_sequence": 106,
              "auth_sequence": [
                [
                  "fio.token",
                  19
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bprewdupdate",
              "authorization": [
                {
                  "actor": "fio.token",
                  "permission": "active"
                }
              ],
              "data": "40679a0e00000000"
            },
            "context_free": false,
            "elapsed": 39,
            "console": "",
            "trx_id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
            "block_num": 1201702,
            "block_time": "2019-09-27T15:28:46.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "eosio",
              "response": "",
              "act_digest": "876d569e8178704513e2339c7e09b24a0d484cfdcc1fb379987c793490283301",
              "global_sequence": 1212087,
              "recv_sequence": 1201829,
              "auth_sequence": [
                [
                  "fio.token",
                  20
                ]
              ],
              "code_sequence": 2,
              "abi_sequence": 2
            },
            "act": {
              "account": "eosio",
              "name": "updatepower",
              "authorization": [
                {
                  "actor": "fio.token",
                  "permission": "active"
                }
              ],
              "data": {
                "voter": "r41zuwovtn44",
                "updateonly": 1
              },
              "hex_data": "40c8cc9b72fd03b901"
            },
            "context_free": false,
            "elapsed": 164,
            "console": " called update power.\ncalled update votes.\n",
            "trx_id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
            "block_num": 1201702,
            "block_time": "2019-09-27T15:28:46.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "eosio",
              "response": "",
              "act_digest": "a92e4acaf4435ac5ee7178ae49d05818c3a4934b2e5aca63ccd32ec59acd1180",
              "global_sequence": 1212088,
              "recv_sequence": 1201830,
              "auth_sequence": [
                [
                  "fio.token",
                  21
                ]
              ],
              "code_sequence": 2,
              "abi_sequence": 2
            },
            "act": {
              "account": "eosio",
              "name": "updatepower",
              "authorization": [
                {
                  "actor": "fio.token",
                  "permission": "active"
                }
              ],
              "data": {
                "voter": "gev2yeim1cjy",
                "updateonly": 1
              },
              "hex_data": "e01f0ad2292fb66201"
            },
            "context_free": false,
            "elapsed": 62,
            "console": " called update power.\n",
            "trx_id": "55970f427fd326922eb522445d29979e54a8cf7ca09ef6b79dbd7e880a6843b9",
            "block_num": 1201702,
            "block_time": "2019-09-27T15:28:46.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid FIO Public Key"
* "Invalid amount value"
* "Insufficient balance"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "amount",
      "value": "100000000000000000",
      "error": "Insufficient balance"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-transfer-fio-tokens-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Public Key"
* "Invalid amount value"
* "Insufficient balance"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-transfer-fio-tokens-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Transfer FIO tokens

<a id="opIdtransfer_tokens_pub_key_model"></a>

> Code samples

```javascript
const inputBody = '{
  "payee_public_key": "string",
  "amount": 0,
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/transfer_tokens_pub_key',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /transfer_tokens_pub_key`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.token"
* name: "trnsfiopubky"

> Body parameter

```json
{
  "payee_public_key": "string",
  "amount": 0,
  "max_fee": 0,
  "tpid": "string",
  "actor": "string"
}
```

<h3 id="[content]-transfer-fio-tokens-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» payee_public_key|body|string|false|Valid WIF Public Key with FIO Prefix|
|» amount|body|integer|false|Amount sent in SUFs|
|» max_fee|body|integer|false|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» tpid|body|string|false|* FIO Address of the wallet which generates this transaction.|
|» actor|body|string|false|See [Generating actor](/actor)|

#### Detailed descriptions

**» tpid**: * FIO Address of the wallet which generates this transaction.
* This FIO Address will be paid 10% of the fee.
* See FIO Protocol#TPIDs for details.
* Set to empty if not known.

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "fee_collected": 250000000
}
```

<h3 id="[content]-transfer-fio-tokens-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-transfer-fio-tokens-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Burn expired FIO Addresses and Domains

<a id="opIdburn_expired"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/burn_expired',
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

`POST /burn_expired`

This is a maintenance call and is intended to burn FIO Addresses and Domains which have passed their expiration date and need to be removed from state. It is envisioned that this call will be made by BPs as good stewards of the blockchain and to free-up state file. This is a signed call, but is free to make.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-burn-expired-fio-addresses-and-domains-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "83495e1a218678a8ad4ad55e2ff1d21b0e0700e9e3f0f95e2d6ba3390a523498",
  "processed": {
    "id": "83495e1a218678a8ad4ad55e2ff1d21b0e0700e9e3f0f95e2d6ba3390a523498",
    "block_num": 1201857,
    "block_time": "2019-09-27T15:30:04.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 599,
      "net_usage_words": 12
    },
    "elapsed": 599,
    "net_usage": 96,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.address",
          "response": "{\"items_burned\":2,\"status\":\"OK\"}",
          "act_digest": "4edeb0f57403c8f0669b87e6d427751515caf54640a6e8691318f29d4056a732",
          "global_sequence": 1212351,
          "recv_sequence": 65,
          "auth_sequence": [
            [
              "r41zuwovtn44",
              49
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.address",
          "name": "burnexpired",
          "authorization": [
            {
              "actor": "r41zuwovtn44",
              "permission": "active"
            }
          ],
          "data": ""
        },
        "context_free": false,
        "elapsed": 465,
        "console": " found expired domain woohoo56311exp expiration 1411918146 domain hash 9221400986991824896\n",
        "trx_id": "83495e1a218678a8ad4ad55e2ff1d21b0e0700e9e3f0f95e2d6ba3390a523498",
        "block_num": 1201857,
        "block_time": "2019-09-27T15:30:04.000",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "fio.system",
            "delta": -1004
          }
        ],
        "except": null,
        "inline_traces": []
      }
    ],
    "except": null
  }
}
```

> Possible triggers:
* No work to be performed

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "burnexpired",
      "value": "burnexpired",
      "error": "No work."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-burn-expired-fio-addresses-and-domains-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible triggers:
* No work to be performed|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-burn-expired-fio-addresses-and-domains-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Burn expired FIO Addresses and Domains

<a id="opIdburn_expired_model"></a>

> Code samples

```javascript

const headers = {
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/burn_expired',
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

`GET /burn_expired`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.address"
* name: "burnexpired"

> Example responses

```json
{
  "status": "OK",
  "items_burned": 100
}
```

<h3 id="[content]-burn-expired-fio-addresses-and-domains-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

<h3 id="[content]-burn-expired-fio-addresses-and-domains-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» items_burned|integer|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Pay rewards to TPIDs

<a id="opIdpay_tpid_rewards"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/pay_tpid_rewards',
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

`POST /pay_tpid_rewards`

This is a maintenance call and is intended to pay TPIDs. It is envisioned that this call will be made by BPs as good stewards of the blockchain and to free-up state file. This is a signed call, but is free to make.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-pay-rewards-to-tpids-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response. 

```json
{
  "transaction_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
  "processed": {
    "id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
    "block_num": 1201946,
    "block_time": "2019-09-27T15:30:48.500",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1118,
      "net_usage_words": 13
    },
    "elapsed": 1118,
    "net_usage": 104,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.treasury",
          "response": "{\"status\":\"OK\",\"tpids_paid\":5}",
          "act_digest": "80841cf787105299daf990bc60433ecaa318e05804992470dfcf16237daf040c",
          "global_sequence": 1212534,
          "recv_sequence": 176,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              136
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.treasury",
          "name": "tpidclaim",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "actor": "gev2yeim1cjy"
          },
          "hex_data": "e01f0ad2292fb662"
        },
        "context_free": false,
        "elapsed": 526,
        "console": "pawel554427@woohoo56311 has 3825000000 rewards.\npawel366688@woohoo56311 has 33750000000 rewards.\n",
        "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
        "block_num": 1201946,
        "block_time": "2019-09-27T15:30:48.500",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "99a441eefe226bbe098893a4632c2edbb0b3af96905ffd99d5d3387fdf0e8c01",
              "global_sequence": 1212535,
              "recv_sequence": 116,
              "auth_sequence": [
                [
                  "fio.treasury",
                  54
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "fio.treasury",
                "to": "gev2yeim1cjy",
                "quantity": "3.825000000 FIO",
                "memo": "Paying TPID from treasury."
              },
              "hex_data": "e0afc646dd0ca85be01f0ad2292fb66240defce3000000000946494f000000001a506179696e6720545049442066726f6d2074726561737572792e"
            },
            "context_free": false,
            "elapsed": 127,
            "console": "",
            "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
            "block_num": 1201946,
            "block_time": "2019-09-27T15:30:48.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "99a441eefe226bbe098893a4632c2edbb0b3af96905ffd99d5d3387fdf0e8c01",
                  "global_sequence": 1212536,
                  "recv_sequence": 177,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "fio.treasury",
                    "to": "gev2yeim1cjy",
                    "quantity": "3.825000000 FIO",
                    "memo": "Paying TPID from treasury."
                  },
                  "hex_data": "e0afc646dd0ca85be01f0ad2292fb66240defce3000000000946494f000000001a506179696e6720545049442066726f6d2074726561737572792e"
                },
                "context_free": false,
                "elapsed": 9,
                "console": "",
                "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
                "block_num": 1201946,
                "block_time": "2019-09-27T15:30:48.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "99a441eefe226bbe098893a4632c2edbb0b3af96905ffd99d5d3387fdf0e8c01",
                  "global_sequence": 1212537,
                  "recv_sequence": 32,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "fio.treasury",
                    "to": "gev2yeim1cjy",
                    "quantity": "3.825000000 FIO",
                    "memo": "Paying TPID from treasury."
                  },
                  "hex_data": "e0afc646dd0ca85be01f0ad2292fb66240defce3000000000946494f000000001a506179696e6720545049442066726f6d2074726561737572792e"
                },
                "context_free": false,
                "elapsed": 2,
                "console": "",
                "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
                "block_num": 1201946,
                "block_time": "2019-09-27T15:30:48.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.tpid",
              "response": "",
              "act_digest": "771c329082eb1c32f04dc55ba129695082ae267e6c3b6ebfe86b84aaf7a4f950",
              "global_sequence": 1212538,
              "recv_sequence": 27,
              "auth_sequence": [
                [
                  "fio.treasury",
                  57
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.tpid",
              "name": "rewardspaid",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "tpid": "pawel554427@woohoo56311"
              },
              "hex_data": "17706177656c3535343432373a776f6f686f6f3536333131"
            },
            "context_free": false,
            "elapsed": 59,
            "console": "",
            "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
            "block_num": 1201946,
            "block_time": "2019-09-27T15:30:48.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "806ce2add057f84333bcfb99e289dea31d692394cad2da4a8cd7230f317de771",
              "global_sequence": 1212539,
              "recv_sequence": 117,
              "auth_sequence": [
                [
                  "fio.treasury",
                  58
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "fio.treasury",
                "to": "2ugokdhavqow",
                "quantity": "33.750000000 FIO",
                "memo": "Paying TPID from treasury."
              },
              "hex_data": "e0afc646dd0ca85bc0a9dda6254899168021a8db070000000946494f000000001a506179696e6720545049442066726f6d2074726561737572792e"
            },
            "context_free": false,
            "elapsed": 125,
            "console": "",
            "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
            "block_num": 1201946,
            "block_time": "2019-09-27T15:30:48.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "806ce2add057f84333bcfb99e289dea31d692394cad2da4a8cd7230f317de771",
                  "global_sequence": 1212540,
                  "recv_sequence": 178,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "fio.treasury",
                    "to": "2ugokdhavqow",
                    "quantity": "33.750000000 FIO",
                    "memo": "Paying TPID from treasury."
                  },
                  "hex_data": "e0afc646dd0ca85bc0a9dda6254899168021a8db070000000946494f000000001a506179696e6720545049442066726f6d2074726561737572792e"
                },
                "context_free": false,
                "elapsed": 8,
                "console": "",
                "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
                "block_num": 1201946,
                "block_time": "2019-09-27T15:30:48.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "2ugokdhavqow",
                  "response": "",
                  "act_digest": "806ce2add057f84333bcfb99e289dea31d692394cad2da4a8cd7230f317de771",
                  "global_sequence": 1212541,
                  "recv_sequence": 10,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "fio.treasury",
                    "to": "2ugokdhavqow",
                    "quantity": "33.750000000 FIO",
                    "memo": "Paying TPID from treasury."
                  },
                  "hex_data": "e0afc646dd0ca85bc0a9dda6254899168021a8db070000000946494f000000001a506179696e6720545049442066726f6d2074726561737572792e"
                },
                "context_free": false,
                "elapsed": 3,
                "console": "",
                "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
                "block_num": 1201946,
                "block_time": "2019-09-27T15:30:48.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.tpid",
              "response": "",
              "act_digest": "aea9a09096651636ca75bb1e48a3fa6c42b28a9a18909d44d628525b1dde6969",
              "global_sequence": 1212542,
              "recv_sequence": 28,
              "auth_sequence": [
                [
                  "fio.treasury",
                  61
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.tpid",
              "name": "rewardspaid",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "tpid": "pawel366688@woohoo56311"
              },
              "hex_data": "17706177656c3336363638383a776f6f686f6f3536333131"
            },
            "context_free": false,
            "elapsed": 46,
            "console": "",
            "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
            "block_num": 1201946,
            "block_time": "2019-09-27T15:30:48.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "313622ac2bcaf5fac2168cdb23fe17dc06b5de7f8a6ff77b719acc76d4bc8333",
              "global_sequence": 1212543,
              "recv_sequence": 179,
              "auth_sequence": [
                [
                  "fio.treasury",
                  62
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "updateclock",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": ""
            },
            "context_free": false,
            "elapsed": 45,
            "console": "",
            "trx_id": "c005378bcd5bdb4ae3a880aa05f69ad1cbb78d300af76a2db12b557dcb41205c",
            "block_num": 1201946,
            "block_time": "2019-09-27T15:30:48.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible triggers:
* No work to perform

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "tpidclaim",
      "value": "tpidclaim",
      "error": "No work."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-pay-rewards-to-tpids-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible triggers:
* No work to perform|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-pay-rewards-to-tpids-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Pay rewards to TPIDs

<a id="opIdpay_tpid_rewards_model"></a>

> Code samples

```javascript
const inputBody = '{
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/pay_tpid_rewards',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /pay_tpid_rewards`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.treasury"
* name: "tpidclaim"

> Body parameter

```json
{
  "actor": "string"
}
```

<h3 id="[content]-pay-rewards-to-tpids-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» actor|body|string|false|See [Generating actor](/actor)|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "tpids_paid": 100
}
```

<h3 id="[content]-pay-rewards-to-tpids-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-pay-rewards-to-tpids-responseschema">Response Schema</h3>

Status Code **202**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» tpids_paid|integer|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Pay BP rewards

<a id="opIdclaim_bp_rewards"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/claim_bp_rewards',
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

`POST /claim_bp_rewards`

This is a maintenance call and is intended to pay the calling BP. This call can only be made by BPs once every 24 hours. This is a signed call, but is free to make.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-pay-bp-rewards-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
  "processed": {
    "id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
    "block_num": 1201940,
    "block_time": "2019-09-27T15:30:45.500",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1755,
      "net_usage_words": 16
    },
    "elapsed": 1755,
    "net_usage": 128,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.treasury",
          "response": "{\"amount\":25408885514,\"status\":\"OK\"}",
          "act_digest": "f7b2b8d1d664446084155b51e2cb39f15aed1c77194a4d5630037c08ed53a68c",
          "global_sequence": 1212514,
          "recv_sequence": 170,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              131
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.treasury",
          "name": "bpclaim",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_address": "pawel554427@woohoo56311",
            "actor": "gev2yeim1cjy"
          },
          "hex_data": "17706177656c3535343432373a776f6f686f6f3536333131e01f0ad2292fb662"
        },
        "context_free": false,
        "elapsed": 1228,
        "console": "\nPay schedule erased... \nCreating new pay schedule... \nNOW rewards is 37129227933\n365 rewards is 254783232877\nAfter receiving 1/365 of 365 rewards, NOW rewards is 37827264187\nBy this much:  698036254\nAfter receiving 1/365 of 365 rewards, 365 rewards is 254085196623\nbpcount: 5\nbpcount: 5\ntostandbybps: 22696358512\n:toactivebps: 15130905674Pay schedule created...\n",
        "trx_id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
        "block_num": 1201940,
        "block_time": "2019-09-27T15:30:45.500",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "fio.treasury",
            "delta": 0
          }
        ],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "63f5621af5c582b81291c3f576f2935756b1d35276e095bd3795254af510a973",
              "global_sequence": 1212515,
              "recv_sequence": 113,
              "auth_sequence": [
                [
                  "fio.treasury",
                  47
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "fio.treasury",
                "to": "gev2yeim1cjy",
                "quantity": "25.408885514 FIO",
                "memo": "Paying producer from treasury."
              },
              "hex_data": "e0afc646dd0ca85be01f0ad2292fb6620ad37cea050000000946494f000000001e506179696e672070726f64756365722066726f6d2074726561737572792e"
            },
            "context_free": false,
            "elapsed": 140,
            "console": "",
            "trx_id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
            "block_num": 1201940,
            "block_time": "2019-09-27T15:30:45.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "63f5621af5c582b81291c3f576f2935756b1d35276e095bd3795254af510a973",
                  "global_sequence": 1212516,
                  "recv_sequence": 171,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "fio.treasury",
                    "to": "gev2yeim1cjy",
                    "quantity": "25.408885514 FIO",
                    "memo": "Paying producer from treasury."
                  },
                  "hex_data": "e0afc646dd0ca85be01f0ad2292fb6620ad37cea050000000946494f000000001e506179696e672070726f64756365722066726f6d2074726561737572792e"
                },
                "context_free": false,
                "elapsed": 9,
                "console": "",
                "trx_id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
                "block_num": 1201940,
                "block_time": "2019-09-27T15:30:45.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "63f5621af5c582b81291c3f576f2935756b1d35276e095bd3795254af510a973",
                  "global_sequence": 1212517,
                  "recv_sequence": 30,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "fio.treasury",
                    "to": "gev2yeim1cjy",
                    "quantity": "25.408885514 FIO",
                    "memo": "Paying producer from treasury."
                  },
                  "hex_data": "e0afc646dd0ca85be01f0ad2292fb6620ad37cea050000000946494f000000001e506179696e672070726f64756365722066726f6d2074726561737572792e"
                },
                "context_free": false,
                "elapsed": 2,
                "console": "",
                "trx_id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
                "block_num": 1201940,
                "block_time": "2019-09-27T15:30:45.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.system",
              "response": "",
              "act_digest": "e7222d441572f810ac45660d3ee6187935abcbccaa2e6df0cc9c37a62eee998f",
              "global_sequence": 1212518,
              "recv_sequence": 66,
              "auth_sequence": [
                [
                  "fio.treasury",
                  50
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.system",
              "name": "resetclaim",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": "e01f0ad2292fb662"
            },
            "context_free": false,
            "elapsed": 11,
            "console": "",
            "trx_id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
            "block_num": 1201940,
            "block_time": "2019-09-27T15:30:45.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "7c2e0ffa08492e53e9caecf64f5a8088af382c6a8f6e045de3593932373c4cb2",
              "global_sequence": 1212519,
              "recv_sequence": 114,
              "auth_sequence": [
                [
                  "fio.treasury",
                  51
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "fio.treasury",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "fio.treasury",
                "to": "fio.foundatn",
                "quantity": "3.418800000 FIO",
                "memo": "Paying foundation from treasury."
              },
              "hex_data": "e0afc646dd0ca85b30b34953d305a85b80bfc6cb000000000946494f0000000020506179696e6720666f756e646174696f6e2066726f6d2074726561737572792e"
            },
            "context_free": false,
            "elapsed": 112,
            "console": "",
            "trx_id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
            "block_num": 1201940,
            "block_time": "2019-09-27T15:30:45.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "7c2e0ffa08492e53e9caecf64f5a8088af382c6a8f6e045de3593932373c4cb2",
                  "global_sequence": 1212520,
                  "recv_sequence": 172,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "fio.treasury",
                    "to": "fio.foundatn",
                    "quantity": "3.418800000 FIO",
                    "memo": "Paying foundation from treasury."
                  },
                  "hex_data": "e0afc646dd0ca85b30b34953d305a85b80bfc6cb000000000946494f0000000020506179696e6720666f756e646174696f6e2066726f6d2074726561737572792e"
                },
                "context_free": false,
                "elapsed": 8,
                "console": "",
                "trx_id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
                "block_num": 1201940,
                "block_time": "2019-09-27T15:30:45.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.foundatn",
                  "response": "",
                  "act_digest": "7c2e0ffa08492e53e9caecf64f5a8088af382c6a8f6e045de3593932373c4cb2",
                  "global_sequence": 1212521,
                  "recv_sequence": 2,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "fio.treasury",
                    "to": "fio.foundatn",
                    "quantity": "3.418800000 FIO",
                    "memo": "Paying foundation from treasury."
                  },
                  "hex_data": "e0afc646dd0ca85b30b34953d305a85b80bfc6cb000000000946494f0000000020506179696e6720666f756e646174696f6e2066726f6d2074726561737572792e"
                },
                "context_free": false,
                "elapsed": 3,
                "console": "",
                "trx_id": "3f320a718c9cf23f80fdf46a42a2d7899989d99f73af31c124db703d780eaba8",
                "block_num": 1201940,
                "block_time": "2019-09-27T15:30:45.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid FIO Address"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not producer or nothing payable"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_address",
      "value": "purse@alice",
      "error": "FIO Address expired"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-pay-bp-rewards-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Address"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not producer or nothing payable"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature|Inline|

<h3 id="[signed]-pay-bp-rewards-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Pay BP rewards

<a id="opIdclaim_bp_rewards_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_address": "string",
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/claim_bp_rewards',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /claim_bp_rewards`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.treasury"
* name: "bpclaim"

> Body parameter

```json
{
  "fio_address": "string",
  "actor": "string"
}
```

<h3 id="[content]-pay-bp-rewards-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_address|body|string|false|none|
|» actor|body|string|false|See [Generating actor](/actor)|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "amount": 100000000000
}
```

<h3 id="[content]-pay-bp-rewards-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-pay-bp-rewards-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» amount|integer|false|none|Amount of payment in SUFs|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Registers a block producer

<a id="opIdregister_producer"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/register_producer',
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

`POST /register_producer`

This call registers an entity as a block producer, so that they can be voted on.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-registers-a-block-producer-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "985f6e859605ad847fc6fde42663b8cdd32c2a21ac87148851965dfb80da0989",
  "processed": {
    "id": "985f6e859605ad847fc6fde42663b8cdd32c2a21ac87148851965dfb80da0989",
    "block_num": 1201937,
    "block_time": "2019-09-27T15:30:44.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1244,
      "net_usage_words": 20
    },
    "elapsed": 1244,
    "net_usage": 160,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "eosio",
          "response": "{\"fee_collected\":10000000000,\"status\":\"OK\"}",
          "act_digest": "ed4f64088598d67c69520ff47c14e3969923f3a54e5ff65dee0316f83df2e871",
          "global_sequence": 1212505,
          "recv_sequence": 1202087,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              127
            ]
          ],
          "code_sequence": 2,
          "abi_sequence": 2
        },
        "act": {
          "account": "eosio",
          "name": "regproducer",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_address": "pawel554427@woohoo56311",
            "url": "http://fio.foundation",
            "location": 80,
            "actor": "gev2yeim1cjy",
            "max_fee": 10000000000
          },
          "hex_data": "17706177656c3535343432373a776f6f686f6f353633313115687474703a2f2f66696f2e666f756e646174696f6e5000e01f0ad2292fb66200e40b5402000000"
        },
        "context_free": false,
        "elapsed": 861,
        "console": "10000000000",
        "trx_id": "985f6e859605ad847fc6fde42663b8cdd32c2a21ac87148851965dfb80da0989",
        "block_num": 1201937,
        "block_time": "2019-09-27T15:30:44.000",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "gev2yeim1cjy",
            "delta": 5
          }
        ],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "91f342eda25401553fd371db7f5101ddf5cc6f7a07191a1c3580f05dcd6927ed",
              "global_sequence": 1212506,
              "recv_sequence": 112,
              "auth_sequence": [
                [
                  "gev2yeim1cjy",
                  128
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "gev2yeim1cjy",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "gev2yeim1cjy",
                "to": "fio.treasury",
                "quantity": "10.000000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00e40b54020000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 143,
            "console": "",
            "trx_id": "985f6e859605ad847fc6fde42663b8cdd32c2a21ac87148851965dfb80da0989",
            "block_num": 1201937,
            "block_time": "2019-09-27T15:30:44.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "91f342eda25401553fd371db7f5101ddf5cc6f7a07191a1c3580f05dcd6927ed",
                  "global_sequence": 1212507,
                  "recv_sequence": 29,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "10.000000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00e40b54020000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 2,
                "console": "",
                "trx_id": "985f6e859605ad847fc6fde42663b8cdd32c2a21ac87148851965dfb80da0989",
                "block_num": 1201937,
                "block_time": "2019-09-27T15:30:44.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "91f342eda25401553fd371db7f5101ddf5cc6f7a07191a1c3580f05dcd6927ed",
                  "global_sequence": 1212508,
                  "recv_sequence": 167,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "10.000000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b00e40b54020000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 10,
                "console": "",
                "trx_id": "985f6e859605ad847fc6fde42663b8cdd32c2a21ac87148851965dfb80da0989",
                "block_num": 1201937,
                "block_time": "2019-09-27T15:30:44.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "990cedeb8db76d8ccfe7426b24b96f428357965e560eccfd285abc9604990f65",
              "global_sequence": 1212509,
              "recv_sequence": 168,
              "auth_sequence": [
                [
                  "eosio",
                  1212044
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bprewdupdate",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "0022204802000000"
            },
            "context_free": false,
            "elapsed": 44,
            "console": "",
            "trx_id": "985f6e859605ad847fc6fde42663b8cdd32c2a21ac87148851965dfb80da0989",
            "block_num": 1201937,
            "block_time": "2019-09-27T15:30:44.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "eb5d6f1154b5de28fd01d085272ed856a5016b42223ed12bebac5f5b9bdadf68",
              "global_sequence": 1212510,
              "recv_sequence": 169,
              "auth_sequence": [
                [
                  "eosio",
                  1212045
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "00c2eb0b00000000"
            },
            "context_free": false,
            "elapsed": 34,
            "console": "",
            "trx_id": "985f6e859605ad847fc6fde42663b8cdd32c2a21ac87148851965dfb80da0989",
            "block_num": 1201937,
            "block_time": "2019-09-27T15:30:44.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Already registered as producer"
* "Invalid FIO Public Key"
* "Invalid url"
* "Invalid location"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "Already registered as producer"
* "TPID must be empty or valid FIO address"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "max_fee",
      "value": "200",
      "error": "Fee exceeds supplied maximum."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-registers-a-block-producer-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Already registered as producer"
* "Invalid FIO Public Key"
* "Invalid url"
* "Invalid location"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "Already registered as producer"
* "TPID must be empty or valid FIO address"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature|Inline|

<h3 id="[signed]-registers-a-block-producer-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Registers a block producer

<a id="opIdregister_producer_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_address": "string",
  "fio_pub_key": "string",
  "url": "string",
  "location": 0,
  "actor": "string",
  "max_fee": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/register_producer',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /register_producer`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "eosio"
* name: "regproducer"

> Body parameter

```json
{
  "fio_address": "string",
  "fio_pub_key": "string",
  "url": "string",
  "location": 0,
  "actor": "string",
  "max_fee": 0
}
```

<h3 id="[content]-registers-a-block-producer-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_address|body|string|true|none|
|» fio_pub_key|body|string|true|Valid WIF Public Key with FIO Prefix|
|» url|body|string|true|Url of block producer website|
|» location|body|integer|true|Location ID of where BPs servers are located. See table below.|
|» actor|body|string|true|See [Generating actor](/actor)|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|

#### Detailed descriptions

**» location**: Location ID of where BPs servers are located. See table below.

Locations
* 10	East Asia
* 20	Australia
* 30	West Asia
* 40	Africa
* 50	Europe
* 60	East North America
* 70	South America
* 80	West North America

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "fee_collected": 10000000000
}
```

<h3 id="[content]-registers-a-block-producer-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-registers-a-block-producer-responseschema">Response Schema</h3>

Status Code **202**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Unregister a block producer

<a id="opIdunregister_producer"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/unregister_producer',
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

`POST /unregister_producer`

This call unregisters an entity as a block producer.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-unregister-a-block-producer-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "91537c23ae5f5f0729032d44336672dbf34cda7e031aef596fbff2bd6c0307f6",
  "processed": {
    "id": "91537c23ae5f5f0729032d44336672dbf34cda7e031aef596fbff2bd6c0307f6",
    "block_num": 1201943,
    "block_time": "2019-09-27T15:30:47.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1333,
      "net_usage_words": 17
    },
    "elapsed": 1333,
    "net_usage": 136,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "eosio",
          "response": "{\"fee_collected\":10000000,\"status\":\"OK\"}",
          "act_digest": "328fb6006277725e85665cc2aaece99f867a833e3af77745c8a53de8709cd781",
          "global_sequence": 1212525,
          "recv_sequence": 1202094,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              132
            ]
          ],
          "code_sequence": 2,
          "abi_sequence": 2
        },
        "act": {
          "account": "eosio",
          "name": "unregprod",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_address": "pawel554427@woohoo56311",
            "actor": "gev2yeim1cjy",
            "max_fee": 1000000000
          },
          "hex_data": "17706177656c3535343432373a776f6f686f6f3536333131e01f0ad2292fb66200ca9a3b00000000"
        },
        "context_free": false,
        "elapsed": 886,
        "console": "10000000",
        "trx_id": "91537c23ae5f5f0729032d44336672dbf34cda7e031aef596fbff2bd6c0307f6",
        "block_num": 1201943,
        "block_time": "2019-09-27T15:30:47.000",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "d07631ada5bb023b024215ca9cfb62fc5331fcbdb635b7ea25f9764107c38004",
              "global_sequence": 1212526,
              "recv_sequence": 115,
              "auth_sequence": [
                [
                  "gev2yeim1cjy",
                  133
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "gev2yeim1cjy",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "gev2yeim1cjy",
                "to": "fio.treasury",
                "quantity": "0.010000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 127,
            "console": "",
            "trx_id": "91537c23ae5f5f0729032d44336672dbf34cda7e031aef596fbff2bd6c0307f6",
            "block_num": 1201943,
            "block_time": "2019-09-27T15:30:47.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "d07631ada5bb023b024215ca9cfb62fc5331fcbdb635b7ea25f9764107c38004",
                  "global_sequence": 1212527,
                  "recv_sequence": 31,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 3,
                "console": "",
                "trx_id": "91537c23ae5f5f0729032d44336672dbf34cda7e031aef596fbff2bd6c0307f6",
                "block_num": 1201943,
                "block_time": "2019-09-27T15:30:47.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "d07631ada5bb023b024215ca9cfb62fc5331fcbdb635b7ea25f9764107c38004",
                  "global_sequence": 1212528,
                  "recv_sequence": 173,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 9,
                "console": "",
                "trx_id": "91537c23ae5f5f0729032d44336672dbf34cda7e031aef596fbff2bd6c0307f6",
                "block_num": 1201943,
                "block_time": "2019-09-27T15:30:47.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "a8364da36a3496b6f7f2599c034cfc8259cbae98da8a5d38085557ccb0c51052",
              "global_sequence": 1212529,
              "recv_sequence": 174,
              "auth_sequence": [
                [
                  "eosio",
                  1212052
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bprewdupdate",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "4089950000000000"
            },
            "context_free": false,
            "elapsed": 43,
            "console": "",
            "trx_id": "91537c23ae5f5f0729032d44336672dbf34cda7e031aef596fbff2bd6c0307f6",
            "block_num": 1201943,
            "block_time": "2019-09-27T15:30:47.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "81b6b654162b4fc2904c46d2f10e58f16eee0e33ba0eee558f90da876f89cc5d",
              "global_sequence": 1212530,
              "recv_sequence": 175,
              "auth_sequence": [
                [
                  "eosio",
                  1212053
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "400d030000000000"
            },
            "context_free": false,
            "elapsed": 35,
            "console": "",
            "trx_id": "91537c23ae5f5f0729032d44336672dbf34cda7e031aef596fbff2bd6c0307f6",
            "block_num": 1201943,
            "block_time": "2019-09-27T15:30:47.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "Not registered as producer"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "max_fee",
      "value": "200",
      "error": "Fee exceeds supplied maximum."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-unregister-a-block-producer-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "Not registered as producer"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature|Inline|

<h3 id="[signed]-unregister-a-block-producer-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Unregister a block producer

<a id="opIdunregister_producer_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_address": "string",
  "actor": "string",
  "max_fee": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/unregister_producer',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /unregister_producer`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "eosio"
* name: "unregprod"

> Body parameter

```json
{
  "fio_address": "string",
  "actor": "string",
  "max_fee": 0
}
```

<h3 id="[content]-unregister-a-block-producer-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_address|body|string|true|none|
|» actor|body|string|true|See [Generating actor](/actor)|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "fee_collected": 10000000
}
```

<h3 id="[content]-unregister-a-block-producer-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-unregister-a-block-producer-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Vote on block producers

<a id="opIdvote_producer"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/vote_producer',
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

`POST /vote_producer`

This call submits votes on block producers.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-vote-on-block-producers-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "e50296e79c1fc71aa2666341af63613cc1f05f90148c20d0bd58e5d4e4c37a7b",
  "processed": {
    "id": "e50296e79c1fc71aa2666341af63613cc1f05f90148c20d0bd58e5d4e4c37a7b",
    "block_num": 1748869,
    "block_time": "2019-09-30T19:28:30.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1310,
      "net_usage_words": 17
    },
    "elapsed": 1310,
    "net_usage": 136,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "eosio",
          "response": "{\"fee_collected\":10000000,\"status\":\"OK\"}",
          "act_digest": "437c8e51311f982f4b2cbd9a3323b01997941be80ad0976be22e9e61e0cf8159",
          "global_sequence": 1764156,
          "recv_sequence": 1749041,
          "auth_sequence": [
            [
              "r41zuwovtn44",
              73
            ]
          ],
          "code_sequence": 2,
          "abi_sequence": 2
        },
        "act": {
          "account": "eosio",
          "name": "voteproducer",
          "authorization": [
            {
              "actor": "r41zuwovtn44",
              "permission": "active"
            }
          ],
          "data": {
            "producers": [
              "pawel242295@woohoo719202"
            ],
            "actor": "r41zuwovtn44",
            "max_fee": 100000000
          },
          "hex_data": "0118706177656c3234323239353a776f6f686f6f37313932303240c8cc9b72fd03b900e1f50500000000"
        },
        "context_free": false,
        "elapsed": 847,
        "console": "called update votes.\n10000000",
        "trx_id": "e50296e79c1fc71aa2666341af63613cc1f05f90148c20d0bd58e5d4e4c37a7b",
        "block_num": 1748869,
        "block_time": "2019-09-30T19:28:30.000",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "7d5931d460b243c3ff7bd3c6da860f82f0e18f651037f0fa65dca13b685b2bbc",
              "global_sequence": 1764157,
              "recv_sequence": 146,
              "auth_sequence": [
                [
                  "r41zuwovtn44",
                  74
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "r41zuwovtn44",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "r41zuwovtn44",
                "to": "fio.treasury",
                "quantity": "0.010000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "40c8cc9b72fd03b9e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 124,
            "console": "",
            "trx_id": "e50296e79c1fc71aa2666341af63613cc1f05f90148c20d0bd58e5d4e4c37a7b",
            "block_num": 1748869,
            "block_time": "2019-09-30T19:28:30.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "r41zuwovtn44",
                  "response": "",
                  "act_digest": "7d5931d460b243c3ff7bd3c6da860f82f0e18f651037f0fa65dca13b685b2bbc",
                  "global_sequence": 1764158,
                  "recv_sequence": 21,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "r41zuwovtn44",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "40c8cc9b72fd03b9e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 3,
                "console": "",
                "trx_id": "e50296e79c1fc71aa2666341af63613cc1f05f90148c20d0bd58e5d4e4c37a7b",
                "block_num": 1748869,
                "block_time": "2019-09-30T19:28:30.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "7d5931d460b243c3ff7bd3c6da860f82f0e18f651037f0fa65dca13b685b2bbc",
                  "global_sequence": 1764159,
                  "recv_sequence": 234,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "r41zuwovtn44",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "40c8cc9b72fd03b9e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 10,
                "console": "",
                "trx_id": "e50296e79c1fc71aa2666341af63613cc1f05f90148c20d0bd58e5d4e4c37a7b",
                "block_num": 1748869,
                "block_time": "2019-09-30T19:28:30.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "a8364da36a3496b6f7f2599c034cfc8259cbae98da8a5d38085557ccb0c51052",
              "global_sequence": 1764160,
              "recv_sequence": 235,
              "auth_sequence": [
                [
                  "eosio",
                  1763530
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bprewdupdate",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "4089950000000000"
            },
            "context_free": false,
            "elapsed": 45,
            "console": "",
            "trx_id": "e50296e79c1fc71aa2666341af63613cc1f05f90148c20d0bd58e5d4e4c37a7b",
            "block_num": 1748869,
            "block_time": "2019-09-30T19:28:30.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "81b6b654162b4fc2904c46d2f10e58f16eee0e33ba0eee558f90da876f89cc5d",
              "global_sequence": 1764161,
              "recv_sequence": 236,
              "auth_sequence": [
                [
                  "eosio",
                  1763531
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "400d030000000000"
            },
            "context_free": false,
            "elapsed": 35,
            "console": "",
            "trx_id": "e50296e79c1fc71aa2666341af63613cc1f05f90148c20d0bd58e5d4e4c37a7b",
            "block_num": 1748869,
            "block_time": "2019-09-30T19:28:30.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Invalid or duplicated producers"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "max_fee",
      "value": "200",
      "error": "Fee exceeds supplied maximum."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-vote-on-block-producers-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid or duplicated producers"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-vote-on-block-producers-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Vote on block producers

<a id="opIdvote_producer_model"></a>

> Code samples

```javascript
const inputBody = '{
  "producers": [
    "string"
  ],
  "fio_address": "string",
  "actor": "string",
  "max_fee": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/vote_producer',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /vote_producer`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "eosio"
* name: "voteproducer"

> Body parameter

```json
{
  "producers": [
    "string"
  ],
  "fio_address": "string",
  "actor": "string",
  "max_fee": 0
}
```

<h3 id="[content]-vote-on-block-producers-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» producers|body|[string]|true|List of FIO Addresses of block producers to vote on.|
|»» FIO Address|body|string|false|none|
|» fio_address|body|string|true|none|
|» actor|body|string|true|See [Generating actor](/actor)|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "fee_collected": 10000000
}
```

<h3 id="[content]-vote-on-block-producers-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-vote-on-block-producers-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Register a FIO Address as proxy

<a id="opIdregister_proxy"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/register_proxy',
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

`POST /register_proxy`

This call registers an entity as a proxy.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-register-a-fio-address-as-proxy-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "56cfafe349a2f32da1d2d313fb6e5d4e1561b88c4944fa215717b0b57114b7e2",
  "processed": {
    "id": "56cfafe349a2f32da1d2d313fb6e5d4e1561b88c4944fa215717b0b57114b7e2",
    "block_num": 1748823,
    "block_time": "2019-09-30T19:28:07.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1278,
      "net_usage_words": 17
    },
    "elapsed": 1278,
    "net_usage": 136,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "eosio",
          "response": "{\"fee_collected\":10000000,\"status\":\"OK\"}",
          "act_digest": "7f63df4daf4759f749999f884696490a1d077ffda6a04a4052bc5eb91408f20a",
          "global_sequence": 1764061,
          "recv_sequence": 1748987,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              174
            ]
          ],
          "code_sequence": 2,
          "abi_sequence": 2
        },
        "act": {
          "account": "eosio",
          "name": "regproxy",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_address": "pawel242295@woohoo719202",
            "actor": "gev2yeim1cjy",
            "max_fee": 10000000
          },
          "hex_data": "18706177656c3234323239353a776f6f686f6f373139323032e01f0ad2292fb6628096980000000000"
        },
        "context_free": false,
        "elapsed": 844,
        "console": "called regiproxy with proxy gev2yeim1cjy isproxy true\n10000000",
        "trx_id": "56cfafe349a2f32da1d2d313fb6e5d4e1561b88c4944fa215717b0b57114b7e2",
        "block_num": 1748823,
        "block_time": "2019-09-30T19:28:07.000",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "d07631ada5bb023b024215ca9cfb62fc5331fcbdb635b7ea25f9764107c38004",
              "global_sequence": 1764062,
              "recv_sequence": 139,
              "auth_sequence": [
                [
                  "gev2yeim1cjy",
                  175
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "gev2yeim1cjy",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "gev2yeim1cjy",
                "to": "fio.treasury",
                "quantity": "0.010000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 130,
            "console": "",
            "trx_id": "56cfafe349a2f32da1d2d313fb6e5d4e1561b88c4944fa215717b0b57114b7e2",
            "block_num": 1748823,
            "block_time": "2019-09-30T19:28:07.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "d07631ada5bb023b024215ca9cfb62fc5331fcbdb635b7ea25f9764107c38004",
                  "global_sequence": 1764063,
                  "recv_sequence": 41,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 2,
                "console": "",
                "trx_id": "56cfafe349a2f32da1d2d313fb6e5d4e1561b88c4944fa215717b0b57114b7e2",
                "block_num": 1748823,
                "block_time": "2019-09-30T19:28:07.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "d07631ada5bb023b024215ca9cfb62fc5331fcbdb635b7ea25f9764107c38004",
                  "global_sequence": 1764064,
                  "recv_sequence": 213,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 11,
                "console": "",
                "trx_id": "56cfafe349a2f32da1d2d313fb6e5d4e1561b88c4944fa215717b0b57114b7e2",
                "block_num": 1748823,
                "block_time": "2019-09-30T19:28:07.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "a8364da36a3496b6f7f2599c034cfc8259cbae98da8a5d38085557ccb0c51052",
              "global_sequence": 1764065,
              "recv_sequence": 214,
              "auth_sequence": [
                [
                  "eosio",
                  1763472
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bprewdupdate",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "4089950000000000"
            },
            "context_free": false,
            "elapsed": 46,
            "console": "",
            "trx_id": "56cfafe349a2f32da1d2d313fb6e5d4e1561b88c4944fa215717b0b57114b7e2",
            "block_num": 1748823,
            "block_time": "2019-09-30T19:28:07.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "81b6b654162b4fc2904c46d2f10e58f16eee0e33ba0eee558f90da876f89cc5d",
              "global_sequence": 1764066,
              "recv_sequence": 215,
              "auth_sequence": [
                [
                  "eosio",
                  1763473
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "400d030000000000"
            },
            "context_free": false,
            "elapsed": 36,
            "console": "",
            "trx_id": "56cfafe349a2f32da1d2d313fb6e5d4e1561b88c4944fa215717b0b57114b7e2",
            "block_num": 1748823,
            "block_time": "2019-09-30T19:28:07.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messgaes:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "Already registered as proxy"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_address",
      "value": "purse@alice",
      "error": "Already registered as proxy. "
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-register-a-fio-address-as-proxy-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messgaes:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "Already registered as proxy"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature|Inline|

<h3 id="[signed]-register-a-fio-address-as-proxy-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Register a FIO Address as proxy

<a id="opIdregister_proxy_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_address": "string",
  "actor": "string",
  "max_fee": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/register_proxy',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /register_proxy`

## This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "eosio"
* name: "regproxy"

> Body parameter

```json
{
  "fio_address": "string",
  "actor": "string",
  "max_fee": 0
}
```

<h3 id="[content]-register-a-fio-address-as-proxy-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_address|body|string|false|none|
|» actor|body|string|false|See [Generating actor](/actor)|
|» max_fee|body|integer|false|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "fee_collected": 10000000
}
```

<h3 id="[content]-register-a-fio-address-as-proxy-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-register-a-fio-address-as-proxy-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Unregisters a FIO Address as proxy

<a id="opIdunregister_proxy"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/unregister_proxy',
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

`POST /unregister_proxy`

This call unregisters an entity as a proxy.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-unregisters-a-fio-address-as-proxy-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response. 

```json
{
  "transaction_id": "e7fc199764b905dde3177c0b76f2c1d903814e78fba5760e2be2a55918cbb0ef",
  "processed": {
    "id": "e7fc199764b905dde3177c0b76f2c1d903814e78fba5760e2be2a55918cbb0ef",
    "block_num": 1748833,
    "block_time": "2019-09-30T19:28:12.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1172,
      "net_usage_words": 17
    },
    "elapsed": 1172,
    "net_usage": 136,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "eosio",
          "response": "{\"fee_collected\":10000000,\"status\":\"OK\"}",
          "act_digest": "9e58a87c36d3e899ec4459325da340dcbdda8c843ae1a686bd1e57dbe622ed30",
          "global_sequence": 1764091,
          "recv_sequence": 1749001,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              178
            ]
          ],
          "code_sequence": 2,
          "abi_sequence": 2
        },
        "act": {
          "account": "eosio",
          "name": "unregproxy",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fio_address": "pawel242295@woohoo719202",
            "actor": "gev2yeim1cjy",
            "max_fee": 100000000
          },
          "hex_data": "18706177656c3234323239353a776f6f686f6f373139323032e01f0ad2292fb66200e1f50500000000"
        },
        "context_free": false,
        "elapsed": 825,
        "console": "called regiproxy with proxy gev2yeim1cjy isproxy false\n10000000",
        "trx_id": "e7fc199764b905dde3177c0b76f2c1d903814e78fba5760e2be2a55918cbb0ef",
        "block_num": 1748833,
        "block_time": "2019-09-30T19:28:12.000",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "d07631ada5bb023b024215ca9cfb62fc5331fcbdb635b7ea25f9764107c38004",
              "global_sequence": 1764092,
              "recv_sequence": 142,
              "auth_sequence": [
                [
                  "gev2yeim1cjy",
                  179
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "gev2yeim1cjy",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "gev2yeim1cjy",
                "to": "fio.treasury",
                "quantity": "0.010000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 126,
            "console": "",
            "trx_id": "e7fc199764b905dde3177c0b76f2c1d903814e78fba5760e2be2a55918cbb0ef",
            "block_num": 1748833,
            "block_time": "2019-09-30T19:28:12.000",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "gev2yeim1cjy",
                  "response": "",
                  "act_digest": "d07631ada5bb023b024215ca9cfb62fc5331fcbdb635b7ea25f9764107c38004",
                  "global_sequence": 1764093,
                  "recv_sequence": 42,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 2,
                "console": "",
                "trx_id": "e7fc199764b905dde3177c0b76f2c1d903814e78fba5760e2be2a55918cbb0ef",
                "block_num": 1748833,
                "block_time": "2019-09-30T19:28:12.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "d07631ada5bb023b024215ca9cfb62fc5331fcbdb635b7ea25f9764107c38004",
                  "global_sequence": 1764094,
                  "recv_sequence": 222,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "gev2yeim1cjy",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "e01f0ad2292fb662e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 10,
                "console": "",
                "trx_id": "e7fc199764b905dde3177c0b76f2c1d903814e78fba5760e2be2a55918cbb0ef",
                "block_num": 1748833,
                "block_time": "2019-09-30T19:28:12.000",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "a8364da36a3496b6f7f2599c034cfc8259cbae98da8a5d38085557ccb0c51052",
              "global_sequence": 1764095,
              "recv_sequence": 223,
              "auth_sequence": [
                [
                  "eosio",
                  1763486
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bprewdupdate",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "4089950000000000"
            },
            "context_free": false,
            "elapsed": 44,
            "console": "",
            "trx_id": "e7fc199764b905dde3177c0b76f2c1d903814e78fba5760e2be2a55918cbb0ef",
            "block_num": 1748833,
            "block_time": "2019-09-30T19:28:12.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "81b6b654162b4fc2904c46d2f10e58f16eee0e33ba0eee558f90da876f89cc5d",
              "global_sequence": 1764096,
              "recv_sequence": 224,
              "auth_sequence": [
                [
                  "eosio",
                  1763487
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "400d030000000000"
            },
            "context_free": false,
            "elapsed": 35,
            "console": "",
            "trx_id": "e7fc199764b905dde3177c0b76f2c1d903814e78fba5760e2be2a55918cbb0ef",
            "block_num": 1748833,
            "block_time": "2019-09-30T19:28:12.000",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messgaes:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "Not registered as proxy"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "max_fee",
      "value": "200",
      "error": "Fee exceeds supplied maximum."
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-unregisters-a-fio-address-as-proxy-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messgaes:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "Not registered as proxy"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor
* FIO Address not owned by FIO Public Key in signature|Inline|

<h3 id="[signed]-unregisters-a-fio-address-as-proxy-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Unregisters a FIO Address as proxy

<a id="opIdunregister_proxy_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_address": "string",
  "actor": 0,
  "max_fee": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/unregister_proxy',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /unregister_proxy`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "eosio"
* name: "unregproxy"

> Body parameter

```json
{
  "fio_address": "string",
  "actor": 0,
  "max_fee": 0
}
```

<h3 id="[content]-unregisters-a-fio-address-as-proxy-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fio_address|body|string|true|none|
|» actor|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "fee_collected": 10000000
}
```

<h3 id="[content]-unregisters-a-fio-address-as-proxy-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-unregisters-a-fio-address-as-proxy-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Proxy votes

<a id="opIdproxy_vote"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/proxy_vote',
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

`POST /proxy_vote`

This call proxies votes of caller to a designated proxy.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-proxy-votes-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "69cfecc2ef7217a1dc8f97918849cb3717459d01adb8d03c8898ae5a87970f7a",
  "processed": {
    "id": "69cfecc2ef7217a1dc8f97918849cb3717459d01adb8d03c8898ae5a87970f7a",
    "block_num": 1748830,
    "block_time": "2019-09-30T19:28:10.500",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1229,
      "net_usage_words": 17
    },
    "elapsed": 1229,
    "net_usage": 136,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "eosio",
          "response": "{\"fee_collected\":10000000,\"status\":\"OK\"}",
          "act_digest": "9c0b22abc66491f5c7c129506eb349ec0c688ef31fa80a865792d2767397737b",
          "global_sequence": 1764082,
          "recv_sequence": 1748997,
          "auth_sequence": [
            [
              "2ugokdhavqow",
              50
            ]
          ],
          "code_sequence": 2,
          "abi_sequence": 2
        },
        "act": {
          "account": "eosio",
          "name": "voteproxy",
          "authorization": [
            {
              "actor": "2ugokdhavqow",
              "permission": "active"
            }
          ],
          "data": {
            "fio_address": "pawel242295@woohoo719202",
            "actor": "2ugokdhavqow",
            "max_fee": 100000000
          },
          "hex_data": "18706177656c3234323239353a776f6f686f6f373139323032c0a9dda62548991600e1f50500000000"
        },
        "context_free": false,
        "elapsed": 878,
        "console": "called update votes.\n10000000",
        "trx_id": "69cfecc2ef7217a1dc8f97918849cb3717459d01adb8d03c8898ae5a87970f7a",
        "block_num": 1748830,
        "block_time": "2019-09-30T19:28:10.500",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "fio.token",
              "response": "",
              "act_digest": "c634e77cb03b1ae53d940eb69b09229e5e6941846211c9b022d65ed0aee04868",
              "global_sequence": 1764083,
              "recv_sequence": 141,
              "auth_sequence": [
                [
                  "2ugokdhavqow",
                  51
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.token",
              "name": "transfer",
              "authorization": [
                {
                  "actor": "2ugokdhavqow",
                  "permission": "active"
                }
              ],
              "data": {
                "from": "2ugokdhavqow",
                "to": "fio.treasury",
                "quantity": "0.010000000 FIO",
                "memo": "FIO API fees. Thank you."
              },
              "hex_data": "c0a9dda625489916e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
            },
            "context_free": false,
            "elapsed": 123,
            "console": "",
            "trx_id": "69cfecc2ef7217a1dc8f97918849cb3717459d01adb8d03c8898ae5a87970f7a",
            "block_num": 1748830,
            "block_time": "2019-09-30T19:28:10.500",
            "producer_block_id": null,
            "account_ram_deltas": [],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "2ugokdhavqow",
                  "response": "",
                  "act_digest": "c634e77cb03b1ae53d940eb69b09229e5e6941846211c9b022d65ed0aee04868",
                  "global_sequence": 1764084,
                  "recv_sequence": 12,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "2ugokdhavqow",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "c0a9dda625489916e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 2,
                "console": "",
                "trx_id": "69cfecc2ef7217a1dc8f97918849cb3717459d01adb8d03c8898ae5a87970f7a",
                "block_num": 1748830,
                "block_time": "2019-09-30T19:28:10.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              },
              {
                "receipt": {
                  "receiver": "fio.treasury",
                  "response": "",
                  "act_digest": "c634e77cb03b1ae53d940eb69b09229e5e6941846211c9b022d65ed0aee04868",
                  "global_sequence": 1764085,
                  "recv_sequence": 219,
                  "auth_sequence": [
                    "[Object]"
                  ],
                  "code_sequence": 1,
                  "abi_sequence": 1
                },
                "act": {
                  "account": "fio.token",
                  "name": "transfer",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "2ugokdhavqow",
                    "to": "fio.treasury",
                    "quantity": "0.010000000 FIO",
                    "memo": "FIO API fees. Thank you."
                  },
                  "hex_data": "c0a9dda625489916e0afc646dd0ca85b80969800000000000946494f000000001846494f2041504920666565732e205468616e6b20796f752e"
                },
                "context_free": false,
                "elapsed": 10,
                "console": "",
                "trx_id": "69cfecc2ef7217a1dc8f97918849cb3717459d01adb8d03c8898ae5a87970f7a",
                "block_num": 1748830,
                "block_time": "2019-09-30T19:28:10.500",
                "producer_block_id": null,
                "account_ram_deltas": [],
                "except": null,
                "inline_traces": []
              }
            ]
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "a8364da36a3496b6f7f2599c034cfc8259cbae98da8a5d38085557ccb0c51052",
              "global_sequence": 1764086,
              "recv_sequence": 220,
              "auth_sequence": [
                [
                  "eosio",
                  1763481
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "bprewdupdate",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "4089950000000000"
            },
            "context_free": false,
            "elapsed": 45,
            "console": "",
            "trx_id": "69cfecc2ef7217a1dc8f97918849cb3717459d01adb8d03c8898ae5a87970f7a",
            "block_num": 1748830,
            "block_time": "2019-09-30T19:28:10.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          },
          {
            "receipt": {
              "receiver": "fio.treasury",
              "response": "",
              "act_digest": "81b6b654162b4fc2904c46d2f10e58f16eee0e33ba0eee558f90da876f89cc5d",
              "global_sequence": 1764087,
              "recv_sequence": 221,
              "auth_sequence": [
                [
                  "eosio",
                  1763482
                ]
              ],
              "code_sequence": 1,
              "abi_sequence": 1
            },
            "act": {
              "account": "fio.treasury",
              "name": "fdtnrwdupdat",
              "authorization": [
                {
                  "actor": "eosio",
                  "permission": "active"
                }
              ],
              "data": "400d030000000000"
            },
            "context_free": false,
            "elapsed": 35,
            "console": "",
            "trx_id": "69cfecc2ef7217a1dc8f97918849cb3717459d01adb8d03c8898ae5a87970f7a",
            "block_num": 1748830,
            "block_time": "2019-09-30T19:28:10.500",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "fio.treasury",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": []
          }
        ]
      }
    ],
    "except": null
  }
}
```

> Possible error messgaes:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "This address is not a proxy"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_address",
      "value": "pawel379538@woohoo719202",
      "error": "This address is not a proxy"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-proxy-votes-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messgaes:
* "Invalid FIO Address format"
* "FIO Address expired"
* "FIO Domain expired"
* "FIO Address not registered"
* "Invalid fee value"
* "Insufficient funds to cover fee"
* "Fee exceeds supplied maximum"
* "This address is not a proxy"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-proxy-votes-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Proxy votes

<a id="opIdproxy_vote_model"></a>

> Code samples

```javascript
const inputBody = '{
  "proxy": "string",
  "fio_address": "string",
  "actor": "string",
  "max_fee": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/proxy_vote',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /proxy_vote`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "eosio"
* name: "voteproxy"

> Body parameter

```json
{
  "proxy": "string",
  "fio_address": "string",
  "actor": "string",
  "max_fee": 0
}
```

<h3 id="[content]-proxy-votes-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» proxy|body|string|true|none|
|» fio_address|body|string|true|none|
|» actor|body|string|true|See [Generating actor](/actor)|
|» max_fee|body|integer|true|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK",
  "fee_collected": 10000000
}
```

<h3 id="[content]-proxy-votes-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-proxy-votes-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|
|» fee_collected|integer|false|none|Amount of SUFs collected as fee|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Set fee ratios

<a id="opIdsubmit_fee_ratios"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/submit_fee_ratios',
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

`POST /submit_fee_ratios`

This call is only allowed to be made by active BPs and is designed to submit fee ratios. It has no fee.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-set-fee-ratios-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "1cbd812645f98a47d40434dd0e026bcd9164543bbce4a394da8a9a6877c9d112",
  "processed": {
    "id": "1cbd812645f98a47d40434dd0e026bcd9164543bbce4a394da8a9a6877c9d112",
    "block_num": 1748841,
    "block_time": "2019-09-30T19:28:16.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 3098,
      "net_usage_words": 65
    },
    "elapsed": 3098,
    "net_usage": 520,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.fee",
          "response": "{\"status\":\"OK\"}",
          "act_digest": "2695e2cd4c213efad1fe26e2b7af19ccf2ed8b6edf7d05ffd7dc823f12ffb239",
          "global_sequence": 1764117,
          "recv_sequence": 14484,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              190
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.fee",
          "name": "setfeevote",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "fee_ratios": [
              {
                "end_point": "register_fio_domain",
                "value": 40000000000
              },
              {
                "end_point": "renew_fio_domain",
                "value": 40000000000
              },
              {
                "end_point": "register_fio_address",
                "value": 5000000000
              },
              {
                "end_point": "renew_fio_address",
                "value": 5000000000
              },
              {
                "end_point": "add_pub_address",
                "value": 10000000
              },
              {
                "end_point": "set_fio_domain_public",
                "value": 100000000
              },
              {
                "end_point": "transfer_tokens_pub_key",
                "value": 250000000
              },
              {
                "end_point": "new_funds_request",
                "value": 10000000
              },
              {
                "end_point": "reject_funds_request",
                "value": 10000000
              },
              {
                "end_point": "record_send",
                "value": 10000000
              },
              {
                "end_point": "register_producer",
                "value": 10000000000
              },
              {
                "end_point": "unregister_producer",
                "value": 10000000
              },
              {
                "end_point": "vote_producer",
                "value": 10000000
              },
              {
                "end_point": "register_proxy",
                "value": 10000000
              },
              {
                "end_point": "unregister_proxy",
                "value": 10000000
              },
              {
                "end_point": "proxy_vote",
                "value": 10000000
              }
            ],
            "actor": "gev2yeim1cjy"
          },
          "hex_data": "101372656769737465725f66696f5f646f6d61696e00902f50090000001072656e65775f66696f5f646f6d61696e00902f50090000001472656769737465725f66696f5f6164647265737300f2052a010000001172656e65775f66696f5f6164647265737300f2052a010000000f6164645f7075625f616464726573738096980000000000157365745f66696f5f646f6d61696e5f7075626c696300e1f50500000000177472616e736665725f746f6b656e735f7075625f6b657980b2e60e00000000116e65775f66756e64735f7265717565737480969800000000001472656a6563745f66756e64735f7265717565737480969800000000000b7265636f72645f73656e6480969800000000001172656769737465725f70726f647563657200e40b540200000013756e72656769737465725f70726f647563657280969800000000000d766f74655f70726f647563657280969800000000000e72656769737465725f70726f7879809698000000000010756e72656769737465725f70726f787980969800000000000a70726f78795f766f746580969800000000000c676576327965696d31636a79"
        },
        "context_free": false,
        "elapsed": 2966,
        "console": "\nendPointHash: 6320586559841969920\n\nendPointHash: 6305032876858408960\n\nendPointHash: 6320586559823699376\n\nendPointHash: 6305032867503890432\n\nendPointHash: 1467915364214133552\n\nendPointHash: 16122877859051077632\n\nendPointHash: 3384455117283786752\n\nendPointHash: 16140186920813297664\n\nendPointHash: 6149663896362532288\n\nendPointHash: 10468328247948707840\n\nendPointHash: 6320586478202077184\n\nendPointHash: 13357356466700647680\n\nendPointHash: 8018079897198338048\n\nendPointHash: 2700246986718681344\n\nendPointHash: 13357356466698780672\n\nendPointHash: 4693833169073295440\ncalled update fees.\n",
        "trx_id": "1cbd812645f98a47d40434dd0e026bcd9164543bbce4a394da8a9a6877c9d112",
        "block_num": 1748841,
        "block_time": "2019-09-30T19:28:16.000",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "fio.fee",
            "delta": 0
          }
        ],
        "except": null,
        "inline_traces": []
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Not an active BP"
* "Value cannot be negative"
* "Invalid end_point"
* "Too soon since last call"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "value",
      "value": "-2",
      "error": "Value cannot be negative"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-set-fee-ratios-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Not an active BP"
* "Value cannot be negative"
* "Invalid end_point"
* "Too soon since last call"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-set-fee-ratios-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Set fee ratios

<a id="opIdsubmit_fee_ratios_model"></a>

> Code samples

```javascript
const inputBody = '{
  "fee_ratios": [
    {
      "end_point": "string",
      "value": 0
    }
  ],
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/submit_fee_ratios',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /submit_fee_ratios`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.fee"
* name: "setfeevote"

> Body parameter

```json
{
  "fee_ratios": [
    {
      "end_point": "string",
      "value": 0
    }
  ],
  "actor": "string"
}
```

<h3 id="[content]-set-fee-ratios-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» fee_ratios|body|[object]|false|Array of fees and corresponding ratios.|
|»» end_point|body|string|false|Name of endpoint for which fee is being set.|
|»» value|body|integer|false|Fee in SUFs which will be multiplied by multiplier.|
|» actor|body|string|false|See [Generating actor](/actor)|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK"
}
```

<h3 id="[content]-set-fee-ratios-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-set-fee-ratios-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Set fee multiplier

<a id="opIdsubmit_fee_multiplier"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/submit_fee_multiplier',
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

`POST /submit_fee_multiplier`

This call is only allowed to be made by active BPs and is designed to submit fee multiplier. It has no fee.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-set-fee-multiplier-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response. 

```json
{
  "transaction_id": "2cdec7f9f0772d8d831e27375125eb3ad8952212d856e487a0dced40587c5db2",
  "processed": {
    "id": "2cdec7f9f0772d8d831e27375125eb3ad8952212d856e487a0dced40587c5db2",
    "block_num": 1748843,
    "block_time": "2019-09-30T19:28:17.000",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1695,
      "net_usage_words": 15
    },
    "elapsed": 1695,
    "net_usage": 120,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.fee",
          "response": "{\"status\":\"OK\"}",
          "act_digest": "410be298e40fb5880fad1a2d3c8354f10f3dbf004f56a524ca433bebd4361875",
          "global_sequence": 1764120,
          "recv_sequence": 14485,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              191
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.fee",
          "name": "setfeemult",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "multiplier": "1.00000000000000000",
            "actor": "gev2yeim1cjy"
          },
          "hex_data": "000000000000f03f0c676576327965696d31636a79"
        },
        "context_free": false,
        "elapsed": 1562,
        "console": "called setfeemult.\ncalled update fees.\ndone setfeemult.\n",
        "trx_id": "2cdec7f9f0772d8d831e27375125eb3ad8952212d856e487a0dced40587c5db2",
        "block_num": 1748843,
        "block_time": "2019-09-30T19:28:17.000",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": []
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Not an active BP"
* "Must be positive"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "multiplier",
      "value": "-2.000000",
      "error": " Must be positive"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-set-fee-multiplier-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Not an active BP"
* "Must be positive"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-set-fee-multiplier-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Set fee multiplier

<a id="opIdsubmit_fee_multiplier_model"></a>

> Code samples

```javascript
const inputBody = '{
  "multiplier": 0,
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/submit_fee_multiplier',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /submit_fee_multiplier`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.fee"
* name: "setfeemult"

> Body parameter

```json
{
  "multiplier": 0,
  "actor": "string"
}
```

<h3 id="[content]-set-fee-multiplier-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» multiplier|body|integer|true|Multiplier|
|» actor|body|string|true|See [Generating actor](/actor)|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK"
}
```

<h3 id="[content]-set-fee-multiplier-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-set-fee-multiplier-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|

<aside class="success">
This operation does not require authentication
</aside>

## [SIGNED] Set bundled transaction count

<a id="opIdsubmit_bundled_transaction"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/submit_bundled_transaction',
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

`POST /submit_bundled_transaction`

This call is only allowed to be made by active BPs and is designed to submit bundled transaction amount which should be allocated to new FIO Address registrations. It has no fee.

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="[signed]-set-bundled-transaction-count-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This request needs to be packed and signed. See **[CONTENT]** for the definition of the object before it's packed and signed.|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.

```json
{
  "transaction_id": "3091e858a9b8f6f895d868c6793e38031763ca49d97835cf1a21bac690aa541a",
  "processed": {
    "id": "3091e858a9b8f6f895d868c6793e38031763ca49d97835cf1a21bac690aa541a",
    "block_num": 1748848,
    "block_time": "2019-09-30T19:28:19.500",
    "producer_block_id": null,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 530,
      "net_usage_words": 15
    },
    "elapsed": 530,
    "net_usage": 120,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "fio.fee",
          "response": "{\"status\":\"OK\"}",
          "act_digest": "93aca1763f952e634fa47b7f68a16b692a40b0d6aeb2880126451c3d02ac5968",
          "global_sequence": 1764126,
          "recv_sequence": 14486,
          "auth_sequence": [
            [
              "gev2yeim1cjy",
              192
            ]
          ],
          "code_sequence": 1,
          "abi_sequence": 1
        },
        "act": {
          "account": "fio.fee",
          "name": "bundlevote",
          "authorization": [
            {
              "actor": "gev2yeim1cjy",
              "permission": "active"
            }
          ],
          "data": {
            "bundled_transactions": "500.00000000000000000",
            "actor": "gev2yeim1cjy"
          },
          "hex_data": "0000000000407f400c676576327965696d31636a79"
        },
        "context_free": false,
        "elapsed": 315,
        "console": "called bundlevote.\ndone bundlevote.\n",
        "trx_id": "3091e858a9b8f6f895d868c6793e38031763ca49d97835cf1a21bac690aa541a",
        "block_num": 1748848,
        "block_time": "2019-09-30T19:28:19.500",
        "producer_block_id": null,
        "account_ram_deltas": [],
        "except": null,
        "inline_traces": []
      }
    ],
    "except": null
  }
}
```

> Possible error messages:
* "Not an active BP"
* "Must be positive int"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "actor",
      "value": "gev2yeim1cjy",
      "error": " Not an active BP"
    }
  ]
}
```

> Possible triggers:
* Signer's FIO Public Key does not match actor

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}
```

<h3 id="[signed]-set-bundled-transaction-count-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|202|[Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)|This is a generic Signed call response. The specific response to this call is contained in processed->action_traces->receipt->response. See **[CONTENT]** for definition of the that response.|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Not an active BP"
* "Must be positive int"|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|Possible triggers:
* Signer's FIO Public Key does not match actor|Inline|

<h3 id="[signed]-set-bundled-transaction-count-responseschema">Response Schema</h3>

Status Code **202**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **403**

*Error 403*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## [CONTENT] Set bundled transaction count

<a id="opIdsubmit_bundled_transaction_model"></a>

> Code samples

```javascript
const inputBody = '{
  "bundled_transactions": 0,
  "actor": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/submit_bundled_transaction',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /submit_bundled_transaction`

### This is not an actual api endpoint
This section defines the object which needs to be created before it's packed and signed and the response object returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual request and response.
### "actions" parameters
* account: "fio.fee"
* name: "bundlevote"

> Body parameter

```json
{
  "bundled_transactions": 0,
  "actor": "string"
}
```

<h3 id="[content]-set-bundled-transaction-count-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|This section defines the object which needs to be created before it's packed and signed. See Signed call section for the definition of the actual request.|
|» bundled_transactions|body|integer|true|Number of bundled transactions which should be included with every FIO Address.|
|» actor|body|string|true|See [Generating actor](/actor)|

> Example responses

> This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.

```json
{
  "status": "OK"
}
```

<h3 id="[content]-set-bundled-transaction-count-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|This section defines only the contents of the response returned in processed->action_traces->receipt->response string. See Signed call section for the definition of the actual response.|Inline|

<h3 id="[content]-set-bundled-transaction-count-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» status|string|false|none|OK|

<aside class="success">
This operation does not require authentication
</aside>

## Get OBT data

<a id="opIdget_obt_data"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_public_key": "string",
  "limit": 0,
  "offset": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_obt_data',
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

`POST /get_obt_data`

Retrives Other Blockchain Transaction (OBT) metadata data stored using /record_obt_data. This call will return all metadata relevant to the provided FIO Public key, including:
* Outbound data. Payer's FIO Address is owned by provided FIO Public key
* Inbound data. Payee's FIO Address is owned by provided FIO Public key

> Body parameter

```json
{
  "fio_public_key": "string",
  "limit": 0,
  "offset": 0
}
```

<h3 id="get-obt-data-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» fio_public_key|body|string|true|Valid WIF Public Key with FIO Prefix|
|» limit|body|integer|false|Number of requests to return. If omitted, all requests will be returned.|
|» offset|body|integer|false|First request from list to return. If omitted, 0 is assumed.|

> Example responses

```json
{
  "obt_data_records": [
    {
      "payer_fio_address": "purse@alice",
      "payee_fio_address": "crypto@bob",
      "payer_fio_public_key": "FIO7167ErgCveJvuonvrEvVGhdWnkP4AEMfqvEd8s8raMkbbAXqhx",
      "payee_fio_public_key": "FIO7KGdMYj4ZMY2nUX9EaZu3G3GxZhTNXUq1tsNqC5rcP9rcmvWHq",
      "content": "...",
      "fio_request_id": 10,
      "status": "sent_to_blockchain",
      "time_stamp": "2020-09-11T18:30:56"
    }
  ],
  "more": 0
}
```

> Possible error messages:
* "Invalid FIO Public Key"
* "Invalid limit"
* "Invalid offset"

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "fio_public_key",
      "value": "FIO123",
      "error": "Invalid FIO Public Key"
    }
  ]
}
```

```json
{
  "message": "No OBT data records"
}
```

<h3 id="get-obt-data-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Possible error messages:
* "Invalid FIO Public Key"
* "Invalid limit"
* "Invalid offset"|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|none|Inline|

<h3 id="get-obt-data-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» obt_data_records|[object]|false|none|Multiple OBT Data Records may be returned.|
|»» payer_fio_address|string|false|none|FIO Address of the payer. This address initiated payment.|
|»» payee_fio_address|string|false|none|FIO Address of the payee. This address is receiving payment.|
|»» payer_fio_public_key|string|false|none|FIO public key of the payer.|
|»» payee_fio_public_key|string|false|none|FIO public key of the payee.|
|»» content|object|false|none|Certain content inside FIO Data is encrypted and packed into this field.<br /><br />Min 64 characters<br />Max 432 characters|
|»»» payer_public_address|string|true|none|Public address on other blockchain of user sending funds.|
|»»» payee_public_address|string|true|none|Public address on other blockchain of user receiving funds.|
|»»» amount|string|true|none|Amount sent.|
|»»» token_code|string|true|none|none|
|»»» status|string|true|none|Status of this OBT. Allowed statuses are:<br />* sent_to_blockchain|
|»»» obt_id|string|true|none|Other Blockchain Transaction ID (OBT ID), i.e Bitcoin transaction ID|
|»»» memo|string|true|none|memo field|
|»»» hash|string|true|none|none|
|»»» offline_url|string|true|none|none|
|»» fio_request_id|integer|false|none|Id of FIO Request, if in response to FIO Request.|
|»» status|string|false|none|In current version alwasy sent_to_blockchain|
|»» time_stamp|string|false|none|Timestamp of transaction|
|» more|integer|false|none|0 - no more results<br />1 - more results|

Status Code **400**

*Error 400*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» type|string|false|none|none|
|» message|string|false|none|none|
|» fields|[object]|false|none|none|
|»» name|string|false|none|none|
|»» value|string|false|none|none|
|»» error|string|false|none|none|

Status Code **404**

*Error 404*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|

<aside class="success">
This operation does not require authentication
</aside>

## Push transaction

<a id="opIdpush_transaction"></a>

> Code samples

```javascript
const inputBody = '{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/push_transaction',
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

`POST /push_transaction`

Allows advance user to send their own content directly to FIO contracts

> Body parameter

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}
```

<h3 id="push-transaction-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» signatures|body|[string]|false|none|
|» compression|body|string|false|none|
|» packed_context_free_data|body|string|false|none|
|» packed_trx|body|string|false|none|

> Example responses

> 200 Response

```json
{
  "transaction_id": "string",
  "processed": {
    "id": "string",
    "block_num": 0,
    "block_time": "string",
    "producer_block_id": null,
    "receipt": {
      "status": "string",
      "cpu_usage_us": 0,
      "net_usage_words": 0
    },
    "elapsed": 0,
    "net_usage": 0,
    "scheduled": true,
    "action_traces": [
      {
        "receipt": {
          "receiver": "string",
          "response": "string",
          "act_digest": "string",
          "global_sequence": 0,
          "recv_sequence": 0,
          "auth_sequence": [
            0
          ],
          "code_sequence": 0,
          "abi_sequence": 0
        },
        "act": {
          "account": "string",
          "name": "string",
          "authorization": [
            {
              "actor": "string",
              "permission": "string"
            }
          ],
          "data": {
            "fio_domain": "string",
            "owner_fio_public_key": "string",
            "max_fee": 0,
            "actor": "string",
            "tpid": "string"
          },
          "hex_data": "string"
        },
        "context_free": true,
        "elapsed": 0,
        "console": "string",
        "trx_id": "string",
        "block_num": 0,
        "block_time": "string",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "string",
            "delta": 0
          }
        ],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "string",
              "response": "string",
              "act_digest": "string",
              "global_sequence": 0,
              "recv_sequence": 0,
              "auth_sequence": [
                0
              ],
              "code_sequence": 0,
              "abi_sequence": 0
            },
            "act": {
              "account": "string",
              "name": "string",
              "authorization": [
                {
                  "actor": "string",
                  "permission": "string"
                }
              ],
              "data": {},
              "hex_data": "string"
            },
            "context_free": true,
            "elapsed": 0,
            "console": "string",
            "trx_id": "string",
            "block_num": 0,
            "block_time": "string",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "string",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "string",
                  "response": "string",
                  "act_digest": "string",
                  "global_sequence": 0,
                  "recv_sequence": 0,
                  "auth_sequence": [
                    0
                  ],
                  "code_sequence": 0,
                  "abi_sequence": 0
                },
                "act": {
                  "account": "string",
                  "name": "string",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "string",
                    "to": "string",
                    "quantity": "string",
                    "memo": "string"
                  },
                  "hex_data": "string"
                },
                "context_free": true,
                "elapsed": 0,
                "console": "string",
                "trx_id": "string",
                "block_num": 0,
                "block_time": "string",
                "producer_block_id": null,
                "account_ram_deltas": [
                  {}
                ],
                "except": null,
                "inline_traces": [
                  {}
                ]
              }
            ]
          }
        ]
      }
    ],
    "except": null
  }
}
```

<h3 id="push-transaction-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

<h3 id="push-transaction-responseschema">Response Schema</h3>

Status Code **200**

*Signed transaction response*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» transaction_id|string|false|none|none|
|» processed|object|false|none|none|
|»» id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» receipt|object|false|none|none|
|»»» status|string|false|none|none|
|»»» cpu_usage_us|integer|false|none|none|
|»»» net_usage_words|integer|false|none|none|
|»» elapsed|integer|false|none|none|
|»» net_usage|integer|false|none|none|
|»» scheduled|boolean|false|none|none|
|»» action_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» fio_domain|string|false|none|none|
|»»»»» owner_fio_public_key|string|false|none|none|
|»»»»» max_fee|integer|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» tpid|string|false|none|none|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|object|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»»» *anonymous*|string|false|none|none|

*continued*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» delta|integer|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|»»»»» receipt|object|false|none|none|
|»»»»»» receiver|string|false|none|none|
|»»»»»» response|string|false|none|none|
|»»»»»» act_digest|string|false|none|none|
|»»»»»» global_sequence|integer|false|none|none|
|»»»»»» recv_sequence|integer|false|none|none|
|»»»»»» auth_sequence|[integer]|false|none|none|
|»»»»»» code_sequence|integer|false|none|none|
|»»»»»» abi_sequence|integer|false|none|none|
|»»»»» act|object|false|none|none|
|»»»»»» account|string|false|none|none|
|»»»»»» name|string|false|none|none|
|»»»»»» authorization|[object]|false|none|none|
|»»»»»»» actor|string|false|none|none|
|»»»»»»» permission|string|false|none|none|
|»»»»»» data|object|false|none|none|
|»»»»»»» from|string|false|none|none|
|»»»»»»» to|string|false|none|none|
|»»»»»»» quantity|string|false|none|none|
|»»»»»»» memo|string|false|none|none|
|»»»»»» hex_data|string|false|none|none|
|»»»»» context_free|boolean|false|none|none|
|»»»»» elapsed|integer|false|none|none|
|»»»»» console|string|false|none|none|
|»»»»» trx_id|string|false|none|none|
|»»»»» block_num|integer|false|none|none|
|»»»»» block_time|string|false|none|none|
|»»»»» producer_block_id|any|false|none|none|
|»»»»» account_ram_deltas|[object]|false|none|none|
|»»»»» except|any|false|none|none|
|»»»»» inline_traces|[object]|false|none|none|
|»» except|any|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## Get actor from public key

<a id="opIdget_actor"></a>

> Code samples

```javascript
const inputBody = '{
  "fio_public_key": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_actor',
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

`POST /get_actor`

Convenience method, which returns [actor](/api/actor) for supplied FIO Public Key. The FIO Chain is not checked for existence of this actor, it simply converts the key to actor using [hash function](/api/actor).

> Body parameter

```json
{
  "fio_public_key": "string"
}
```

<h3 id="get-actor-from-public-key-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» fio_public_key|body|string|true|Valid WIF Public Key with FIO Prefix|

> Example responses

```json
{
  "actor": "gev2yeim1cjy"
}
```

<h3 id="get-actor-from-public-key-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

<h3 id="get-actor-from-public-key-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» actor|string|true|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## Get state table content

<a id="opIdget_table_rows"></a>

> Code samples

```javascript
const inputBody = '{
  "code": "string",
  "scope": "string",
  "table": "string",
  "lower_bound": "string",
  "upper_bound": "string",
  "key_type": "string",
  "index_position": "string",
  "limit": 0,
  "json": true,
  "reverse": true
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_table_rows',
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

`POST /get_table_rows`

This call can be used to return any data from the state table.

## Returning all public addresses example
Here's an advance example of a query returning all public addresses mapped to a single FIO Address.

The data is contained in *fionames* table in *fio.address* contract and *fio.address* scope.

The FIO Address is index position *5* of index_type *i128*.

### Compute index
The hash is a truncated sha1 hash, in big-endian order, as a hex-string.
1. Calculate the sha1 sum of the address
2. Take the first 16 bytes
3. Reverse the byte order
4. Convert to a hexadecimal string, and prepend "0x"

Example for "test@fiotestnet"
1. sha1 hash: 58df646ca7a4c9be1e1436b9ae1608eb62e653a0
2. First 16 bytes: 58df646ca7a4c9be1e1436b9ae1608eb
3. Reverse byte order (big endian): eb0816aeb936141ebec9a4a76c64df58
4. Prepend 0x

```
function nameHash(name) {
    const hash = require('crypto').createHash('sha1')
    return '0x' + hash.update(name).digest().slice(0,16).reverse().toString("hex")
}

console.log( nameHash('test@fiotestnet') )
// outputs: 0xeb0816aeb936141ebec9a4a76c64df58
```

### Query table
To query the table, specify index 5, with a type of i128, using the hash as the upper and lower bounds:
```
{
	"code": "fio.address",
	"scope": "fio.address",
	"table": "fionames",
	"lower_bound": "0xeb0816aeb936141ebec9a4a76c64df58",
	"upper_bound": "0xeb0816aeb936141ebec9a4a76c64df58",
	"key_type": "i128",
	"index_position": "5",
	"json": true
}
```

> Body parameter

```json
{
  "code": "string",
  "scope": "string",
  "table": "string",
  "lower_bound": "string",
  "upper_bound": "string",
  "key_type": "string",
  "index_position": "string",
  "limit": 0,
  "json": true,
  "reverse": true
}
```

<h3 id="get-state-table-content-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» code|body|string|true|The name of the smart contract that controls the provided table.|
|» scope|body|string|true|The account to which this data belongs.|
|» table|body|string|true|The name of the table as specified by the contract abi.|
|» lower_bound|body|string|false|Filters results to return the first element that is not less than provided value in set.|
|» upper_bound|body|string|false|Filters results to return the first element that is greater than provided value in set.|
|» key_type|body|string|false|Type of key specified by index_position (for example - uint64_t or name).|
|» index_position|body|string|false|Position of the index used.|
|» limit|body|integer|false|Number of rows to return. If omitted, all requests will be returned.|
|» json|body|boolean|false|Get the response as json.|
|» reverse|body|boolean|false|Return data in reverse order.|

> Example responses

```json
{
  "rows": [
    {
      "id": 10070,
      "name": "referral@fio",
      "namehash": "0xc3bf40257f090f2887271c515ebac1dc",
      "domain": "fio",
      "domainhash": "0x8d9d3bd8a6fb22345ce8fa3c416a28e5",
      "expiration": 1624985778,
      "owner_account": "534jl4ye5oai",
      "addresses": [
        {
          "token_code": "FIO",
          "chain_code": "FIO",
          "public_address": "FIO6dZx1TeggbrDemzVNdvuVJdgZ4RXAtGMBm5xcHJZVYgPFRQmpk"
        }
      ],
      "bundleeligiblecountdown": 100
    }
  ],
  "more": true
}
```

<h3 id="get-state-table-content-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

<h3 id="get-state-table-content-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» rows|[any]|false|none|Rows from table. Format depands on table queried.|
|» more|boolean|false|none|Indicates if more results are available.|

<aside class="success">
This operation does not require authentication
</aside>

## Get account information

<a id="opIdget_account"></a>

> Code samples

```javascript
const inputBody = '{
  "account_name": "string"
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json'
};

fetch('http://testnet.fioprotocol.io/v1/chain/get_account',
{
  method: 'GET',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

`GET /get_account`

Returns information about the [account](https://developers.fioprotocol.io/fio-protocol/accounts), such as creation date and permissions.

If you are trying to use this method to get FIO Public Key from an account, please note that users have the options of swapping their key, for example to create a multisig, see tw4tjkmo4eyd

> Body parameter

```json
{
  "account_name": "string"
}
```

<h3 id="get-account-information-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|object|false|none|
|» account_name|body|string|true|none|

> Example responses

```json
{
  "account_name": "qkx1keadtwau",
  "head_block_num": 30682251,
  "head_block_time": "2020-09-18T14:45:02.500",
  "privileged": false,
  "last_code_update": "1970-01-01T00:00:00.000",
  "created": "2020-08-31T14:41:54.000",
  "ram_quota": 26112,
  "net_weight": -1,
  "cpu_weight": -1,
  "net_limit": {
    "used": -1,
    "available": -1,
    "max": -1
  },
  "cpu_limit": {
    "used": -1,
    "available": -1,
    "max": -1
  },
  "ram_usage": 2996,
  "permissions": [
    {
      "perm_name": "active",
      "parent": "owner",
      "required_auth": {
        "threshold": 1,
        "keys": [
          {
            "key": "FIO5nejysoKY5U9fxGicT6oR2ztW6CPazJRZBoPR1Dh3oJUGssqJE",
            "weight": 1
          }
        ],
        "accounts": [],
        "waits": []
      }
    },
    {
      "perm_name": "owner",
      "parent": "",
      "required_auth": {
        "threshold": 1,
        "keys": [
          {
            "key": "FIO5nejysoKY5U9fxGicT6oR2ztW6CPazJRZBoPR1Dh3oJUGssqJE",
            "weight": 1
          }
        ],
        "accounts": [],
        "waits": []
      }
    }
  ],
  "total_resources": {
    "owner": "qkx1keadtwau",
    "net_weight": "0.000000000 FIO",
    "cpu_weight": "0.000000000 FIO",
    "ram_bytes": 0
  },
  "self_delegated_bandwidth": null,
  "refund_request": null,
  "voter_info": null
}
```

<h3 id="get-account-information-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

<h3 id="get-account-information-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» account_name|string|false|none|none|
|» head_block_num|integer|false|none|none|
|» head_block_time|string|false|none|none|
|» privileged|boolean|false|none|none|
|» last_code_update|string|false|none|none|
|» created|string|false|none|none|
|» ram_quota|integer|false|none|none|
|» net_weight|integer|false|none|none|
|» cpu_weight|integer|false|none|none|
|» net_limit|object|false|none|none|
|»» used|integer|false|none|none|
|»» available|integer|false|none|none|
|»» max|integer|false|none|none|
|» cpu_limit|object|false|none|none|
|»» used|integer|false|none|none|
|»» available|integer|false|none|none|
|»» max|integer|false|none|none|
|» ram_usage|integer|false|none|none|
|» permissions|[object]|false|none|none|
|»» perm_name|string|false|none|none|
|»» parent|string|false|none|none|
|»» required_auth|object|false|none|none|
|»»» threshold|integer|false|none|none|
|»»» keys|[object]|false|none|none|
|»»»» key|string|false|none|none|
|»»»» weight|integer|false|none|none|
|»»» accounts|[object]|false|none|none|
|»»» waits|[object]|false|none|none|
|» total_resources|object|false|none|none|
|»» owner|string|false|none|none|
|»» net_weight|string|false|none|none|
|»» cpu_weight|string|false|none|none|
|»» ram_bytes|integer|false|none|none|
|» self_delegated_bandwidth|any|false|none|none|
|» refund_request|any|false|none|none|
|» voter_info|any|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocS_error-400">error-400</h2>

<a id="schemaerror-400"></a>
<a id="schema_error-400"></a>
<a id="tocSerror-400"></a>
<a id="tocserror-400"></a>

```json
{
  "type": "invalid_input",
  "message": "An invalid request was sent in, please check the nested errors for details.",
  "fields": [
    {
      "name": "string",
      "value": "string",
      "error": "string"
    }
  ]
}

```

Error 400

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|true|none|invalid_input|
|message|string|true|none|An invalid request was sent in, please check the nested errors for details.|
|fields|[object]|true|none|none|
|» name|string|false|none|Name of the field which triggered the error|
|» value|string|false|none|Value which was sent in and which triggered the error|
|» error|string|false|none|Error message|

<h2 id="tocS_tpid">tpid</h2>

<a id="schematpid"></a>
<a id="schema_tpid"></a>
<a id="tocStpid"></a>
<a id="tocstpid"></a>

```json
"string"

```

TPID

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|TPID|string|false|none|See [Technology Provider ID](/fio-protocol/tpid)|

<h2 id="tocS_actor">actor</h2>

<a id="schemaactor"></a>
<a id="schema_actor"></a>
<a id="tocSactor"></a>
<a id="tocsactor"></a>

```json
"string"

```

Actor

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Actor|string|false|none|See [Generating actor](/api/actor)|

<h2 id="tocS_fio-address">fio-address</h2>

<a id="schemafio-address"></a>
<a id="schema_fio-address"></a>
<a id="tocSfio-address"></a>
<a id="tocsfio-address"></a>

```json
"string"

```

FIO Address

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|FIO Address|string|false|none|none|

<h2 id="tocS_date-time">date-time</h2>

<a id="schemadate-time"></a>
<a id="schema_date-time"></a>
<a id="tocSdate-time"></a>
<a id="tocsdate-time"></a>

```json
"2019-08-24T14:15:22Z"

```

Date/time

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Date/time|string(date-time)|false|none|none|

<h2 id="tocS_fee-collected">fee-collected</h2>

<a id="schemafee-collected"></a>
<a id="schema_fee-collected"></a>
<a id="tocSfee-collected"></a>
<a id="tocsfee-collected"></a>

```json
0

```

Fee collected

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Fee collected|integer|false|none|Amount of SUFs collected as fee|

<h2 id="tocS_error-403">error-403</h2>

<a id="schemaerror-403"></a>
<a id="schema_error-403"></a>
<a id="tocSerror-403"></a>
<a id="tocserror-403"></a>

```json
{
  "type": "invalid_signature",
  "message": "Request signature not valid or not allowed."
}

```

Error 403

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|true|none|Type of 403 error|
|message|string|true|none|Message associated with the 403 type|

<h2 id="tocS_error-404">error-404</h2>

<a id="schemaerror-404"></a>
<a id="schema_error-404"></a>
<a id="tocSerror-404"></a>
<a id="tocserror-404"></a>

```json
{
  "message": "Public address not found"
}

```

Error 404

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|message|string|false|none|Call specific error message.|

<h2 id="tocS_fio-domain">fio-domain</h2>

<a id="schemafio-domain"></a>
<a id="schema_fio-domain"></a>
<a id="tocSfio-domain"></a>
<a id="tocsfio-domain"></a>

```json
"string"

```

FIO Domain

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|FIO Domain|string|false|none|none|

<h2 id="tocS_signed-request">signed-request</h2>

<a id="schemasigned-request"></a>
<a id="schema_signed-request"></a>
<a id="tocSsigned-request"></a>
<a id="tocssigned-request"></a>

```json
{
  "signatures": [
    "string"
  ],
  "compression": "string",
  "packed_context_free_data": "string",
  "packed_trx": "string"
}

```

Signed transaction request

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|signatures|[string]|false|none|none|
|compression|string|false|none|none|
|packed_context_free_data|string|false|none|none|
|packed_trx|string|false|none|none|

<h2 id="tocS_signed-response">signed-response</h2>

<a id="schemasigned-response"></a>
<a id="schema_signed-response"></a>
<a id="tocSsigned-response"></a>
<a id="tocssigned-response"></a>

```json
{
  "transaction_id": "string",
  "processed": {
    "id": "string",
    "block_num": 0,
    "block_time": "string",
    "producer_block_id": null,
    "receipt": {
      "status": "string",
      "cpu_usage_us": 0,
      "net_usage_words": 0
    },
    "elapsed": 0,
    "net_usage": 0,
    "scheduled": true,
    "action_traces": [
      {
        "receipt": {
          "receiver": "string",
          "response": "string",
          "act_digest": "string",
          "global_sequence": 0,
          "recv_sequence": 0,
          "auth_sequence": [
            0
          ],
          "code_sequence": 0,
          "abi_sequence": 0
        },
        "act": {
          "account": "string",
          "name": "string",
          "authorization": [
            {
              "actor": "string",
              "permission": "string"
            }
          ],
          "data": {
            "fio_domain": "string",
            "owner_fio_public_key": "string",
            "max_fee": 0,
            "actor": "string",
            "tpid": "string"
          },
          "hex_data": "string"
        },
        "context_free": true,
        "elapsed": 0,
        "console": "string",
        "trx_id": "string",
        "block_num": 0,
        "block_time": "string",
        "producer_block_id": null,
        "account_ram_deltas": [
          {
            "account": "string",
            "delta": 0
          }
        ],
        "except": null,
        "inline_traces": [
          {
            "receipt": {
              "receiver": "string",
              "response": "string",
              "act_digest": "string",
              "global_sequence": 0,
              "recv_sequence": 0,
              "auth_sequence": [
                0
              ],
              "code_sequence": 0,
              "abi_sequence": 0
            },
            "act": {
              "account": "string",
              "name": "string",
              "authorization": [
                {
                  "actor": "string",
                  "permission": "string"
                }
              ],
              "data": {},
              "hex_data": "string"
            },
            "context_free": true,
            "elapsed": 0,
            "console": "string",
            "trx_id": "string",
            "block_num": 0,
            "block_time": "string",
            "producer_block_id": null,
            "account_ram_deltas": [
              {
                "account": "string",
                "delta": 0
              }
            ],
            "except": null,
            "inline_traces": [
              {
                "receipt": {
                  "receiver": "string",
                  "response": "string",
                  "act_digest": "string",
                  "global_sequence": 0,
                  "recv_sequence": 0,
                  "auth_sequence": [
                    0
                  ],
                  "code_sequence": 0,
                  "abi_sequence": 0
                },
                "act": {
                  "account": "string",
                  "name": "string",
                  "authorization": [
                    "[Object]"
                  ],
                  "data": {
                    "from": "string",
                    "to": "string",
                    "quantity": "string",
                    "memo": "string"
                  },
                  "hex_data": "string"
                },
                "context_free": true,
                "elapsed": 0,
                "console": "string",
                "trx_id": "string",
                "block_num": 0,
                "block_time": "string",
                "producer_block_id": null,
                "account_ram_deltas": [
                  {}
                ],
                "except": null,
                "inline_traces": [
                  {}
                ]
              }
            ]
          }
        ]
      }
    ],
    "except": null
  }
}

```

Signed transaction response

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|transaction_id|string|false|none|none|
|processed|object|false|none|none|
|» id|string|false|none|none|
|» block_num|integer|false|none|none|
|» block_time|string|false|none|none|
|» producer_block_id|any|false|none|none|
|» receipt|object|false|none|none|
|»» status|string|false|none|none|
|»» cpu_usage_us|integer|false|none|none|
|»» net_usage_words|integer|false|none|none|
|» elapsed|integer|false|none|none|
|» net_usage|integer|false|none|none|
|» scheduled|boolean|false|none|none|
|» action_traces|[object]|false|none|none|
|»» receipt|object|false|none|none|
|»»» receiver|string|false|none|none|
|»»» response|string|false|none|none|
|»»» act_digest|string|false|none|none|
|»»» global_sequence|integer|false|none|none|
|»»» recv_sequence|integer|false|none|none|
|»»» auth_sequence|[integer]|false|none|none|
|»»» code_sequence|integer|false|none|none|
|»»» abi_sequence|integer|false|none|none|
|»» act|object|false|none|none|
|»»» account|string|false|none|none|
|»»» name|string|false|none|none|
|»»» authorization|[object]|false|none|none|
|»»»» actor|string|false|none|none|
|»»»» permission|string|false|none|none|
|»»» data|object|false|none|none|
|»»»» fio_domain|string|false|none|none|
|»»»» owner_fio_public_key|string|false|none|none|
|»»»» max_fee|integer|false|none|none|
|»»»» actor|string|false|none|none|
|»»»» tpid|string|false|none|none|
|»»» hex_data|string|false|none|none|
|»» context_free|boolean|false|none|none|
|»» elapsed|integer|false|none|none|
|»» console|string|false|none|none|
|»» trx_id|string|false|none|none|
|»» block_num|integer|false|none|none|
|»» block_time|string|false|none|none|
|»» producer_block_id|any|false|none|none|
|»» account_ram_deltas|[object]|false|none|none|
|»»» account|string|false|none|none|
|»»» delta|integer|false|none|none|
|»» except|any|false|none|none|
|»» inline_traces|[object]|false|none|none|
|»»» receipt|object|false|none|none|
|»»»» receiver|string|false|none|none|
|»»»» response|string|false|none|none|
|»»»» act_digest|string|false|none|none|
|»»»» global_sequence|integer|false|none|none|
|»»»» recv_sequence|integer|false|none|none|
|»»»» auth_sequence|[integer]|false|none|none|
|»»»» code_sequence|integer|false|none|none|
|»»»» abi_sequence|integer|false|none|none|
|»»» act|object|false|none|none|
|»»»» account|string|false|none|none|
|»»»» name|string|false|none|none|
|»»»» authorization|[object]|false|none|none|
|»»»»» actor|string|false|none|none|
|»»»»» permission|string|false|none|none|
|»»»» data|object|false|none|none|
|»»»»» from|string|false|none|none|
|»»»»» to|string|false|none|none|
|»»»»» quantity|string|false|none|none|
|»»»»» memo|string|false|none|none|

oneOf

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» *anonymous*|object|false|none|none|

xor

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»»» *anonymous*|string|false|none|none|

continued

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|»»»» hex_data|string|false|none|none|
|»»» context_free|boolean|false|none|none|
|»»» elapsed|integer|false|none|none|
|»»» console|string|false|none|none|
|»»» trx_id|string|false|none|none|
|»»» block_num|integer|false|none|none|
|»»» block_time|string|false|none|none|
|»»» producer_block_id|any|false|none|none|
|»»» account_ram_deltas|[object]|false|none|none|
|»»»» account|string|false|none|none|
|»»»» delta|integer|false|none|none|
|»»» except|any|false|none|none|
|»»» inline_traces|[object]|false|none|none|
|»»»» receipt|object|false|none|none|
|»»»»» receiver|string|false|none|none|
|»»»»» response|string|false|none|none|
|»»»»» act_digest|string|false|none|none|
|»»»»» global_sequence|integer|false|none|none|
|»»»»» recv_sequence|integer|false|none|none|
|»»»»» auth_sequence|[integer]|false|none|none|
|»»»»» code_sequence|integer|false|none|none|
|»»»»» abi_sequence|integer|false|none|none|
|»»»» act|object|false|none|none|
|»»»»» account|string|false|none|none|
|»»»»» name|string|false|none|none|
|»»»»» authorization|[object]|false|none|none|
|»»»»»» actor|string|false|none|none|
|»»»»»» permission|string|false|none|none|
|»»»»» data|object|false|none|none|
|»»»»»» from|string|false|none|none|
|»»»»»» to|string|false|none|none|
|»»»»»» quantity|string|false|none|none|
|»»»»»» memo|string|false|none|none|
|»»»»» hex_data|string|false|none|none|
|»»»» context_free|boolean|false|none|none|
|»»»» elapsed|integer|false|none|none|
|»»»» console|string|false|none|none|
|»»»» trx_id|string|false|none|none|
|»»»» block_num|integer|false|none|none|
|»»»» block_time|string|false|none|none|
|»»»» producer_block_id|any|false|none|none|
|»»»» account_ram_deltas|[object]|false|none|none|
|»»»» except|any|false|none|none|
|»»»» inline_traces|[object]|false|none|none|
|» except|any|false|none|none|

<h2 id="tocS_max-fee">max-fee</h2>

<a id="schemamax-fee"></a>
<a id="schema_max-fee"></a>
<a id="tocSmax-fee"></a>
<a id="tocsmax-fee"></a>

```json
0

```

Max fee

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Max fee|integer|false|none|Maximum amount of SUFs the user is willing to pay for fee. Should be preceded by /get_fee for correct value.|

<h2 id="tocS_token-code">token-code</h2>

<a id="schematoken-code"></a>
<a id="schema_token-code"></a>
<a id="tocStoken-code"></a>
<a id="tocstoken-code"></a>

```json
"string"

```

Token/chain code

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|Token/chain code|string|false|none|Chain code identifies the blockchain, while token code identifies a token on that blockchain. For example: for USDC: chain_code = ETH and token_code = USDC, for BTC: chain_code = BTC and token_code = BTC. For list of chain codes you can refer to [SLIP-44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md) and for list of token code refer to the specific blockchain.|

<h2 id="tocS_fio-request-ecrypted-content">fio-request-ecrypted-content</h2>

<a id="schemafio-request-ecrypted-content"></a>
<a id="schema_fio-request-ecrypted-content"></a>
<a id="tocSfio-request-ecrypted-content"></a>
<a id="tocsfio-request-ecrypted-content"></a>

```json
{
  "payee_public_address": {},
  "amount": "string",
  "token_code": "string",
  "memo": "string",
  "hash": "string",
  "offline_url": "string",
  "future_use1": "string",
  "future_use2": "string",
  "future_use3": "string",
  "future_use4": "string",
  "future_use5": "string"
}

```

FIO Request encrypted content

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|payee_public_address|object|true|none|This is the public address on another blockchain. Both integrated addresses as well as URI Scheme are supported.<br /><br />**Integrated Address**<br />If the blockchain supports it, an integrated address may be passed in just like standard public address. The FIO protocol does not perform validation on the passed string.<br /><br />**URI Scheme**<br />FIO Protocol will support formatting of public addresses using URI were certain attributes are appended to the public address following a '?' and delimited with '&'. To allow inter-wallet operability, the following standardized parameters will be supported in official FIO Protocol SDKs.<br /><br />**Parameters**<br />* dt - Ripple<br />* memo - Any - use as generic memo field<br />* memo_id -	Stellar<br />* memo_text -	Stellar<br />* memo_hash -	Stellar<br />* memo_return -	Stellar<br />* payment_id - Monero|
|amount|string|true|none|Amount requested.|
|token_code|string|true|none|none|
|memo|string|true|none|none|
|hash|string|true|none|none|
|offline_url|string|true|none|none|
|future_use1|string|true|none|none|
|future_use2|string|true|none|none|
|future_use3|string|true|none|none|
|future_use4|string|true|none|none|
|future_use5|string|true|none|none|

<h2 id="tocS_fio_request-status">fio_request-status</h2>

<a id="schemafio_request-status"></a>
<a id="schema_fio_request-status"></a>
<a id="tocSfio_request-status"></a>
<a id="tocsfio_request-status"></a>

```json
"requested"

```

FIO Request status

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|FIO Request status|string|false|none|Status of FIO Request|

#### Enumerated Values

|Property|Value|
|---|---|
|FIO Request status|requested|
|FIO Request status|request_rejected|
|FIO Request status|sent_to_blockchain|

<h2 id="tocS_fio-data-encrypted-content">fio-data-encrypted-content</h2>

<a id="schemafio-data-encrypted-content"></a>
<a id="schema_fio-data-encrypted-content"></a>
<a id="tocSfio-data-encrypted-content"></a>
<a id="tocsfio-data-encrypted-content"></a>

```json
{
  "payer_public_address": "string",
  "payee_public_address": "string",
  "amount": "string",
  "token_code": "string",
  "status": "string",
  "obt_id": "string",
  "memo": "string",
  "hash": "string",
  "offline_url": "string"
}

```

FIO Data encrypted content

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|payer_public_address|string|true|none|Public address on other blockchain of user sending funds.|
|payee_public_address|string|true|none|Public address on other blockchain of user receiving funds.|
|amount|string|true|none|Amount sent.|
|token_code|string|true|none|none|
|status|string|true|none|Status of this OBT. Allowed statuses are:<br />* sent_to_blockchain|
|obt_id|string|true|none|Other Blockchain Transaction ID (OBT ID), i.e Bitcoin transaction ID|
|memo|string|true|none|memo field|
|hash|string|true|none|none|
|offline_url|string|true|none|none|

<h2 id="tocS_fio-public-key">fio-public-key</h2>

<a id="schemafio-public-key"></a>
<a id="schema_fio-public-key"></a>
<a id="tocSfio-public-key"></a>
<a id="tocsfio-public-key"></a>

```json
"string"

```

FIO Public Key

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|FIO Public Key|string|false|none|Valid WIF Public Key with FIO Prefix|

<h2 id="tocS_nbpa">nbpa</h2>

<a id="schemanbpa"></a>
<a id="schema_nbpa"></a>
<a id="tocSnbpa"></a>
<a id="tocsnbpa"></a>

```json
{}

```

Native Blockchain Public Address

### Properties

*None*

