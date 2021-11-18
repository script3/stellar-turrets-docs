# txFunctions

Manage and run txFunctions on the Turret. A txFuntion is a JavaScript file that
outputs a valid Transaction Envelope XDR. The txFunction will be executed in a
node environment with the following default node_module packages:

* bignumber.js
* node-fetch
* stellar-sdk

## Upload a txFunction

Uploads a txFunction to the turret

### Request

```
POST /tx-functions
```

REQUEST BODY SCHEMA: multipart/form-data

| key | value |
| --- | --- |
| `txFunction` | `string` The source code to be uploaded |
| `txFunctionFields` | `string` A Base64 encoded array of json object of the input fields for the contract |
| `txFunctionFee` | `string` A signed, non-submitted transaction envelope XDR for a fee payment to the `TURRET_ADDRESS` that is greater than or equal to the byte length of the contract divided by the `UPLOAD_DIVISOR` set by the turret |

### Request Sample

```json
{
  "txFunction": "/some/path/txFunction.js",
  "txFunctionFields": "W3sibmFtZSI6ImRlc3RpbmF0aW9uIiwidHlwZSI6InN0cmluZyIsImRlc2NyaXB0aW9uIjoiU3RlbGxhciBwdWJsaWMga2V5IHlvdSdkIGxpa2UgdG8gcGF5IiwicnVsZSI6Ik11c3QgYmUgYSB2YWxpZCBhbmQgZnVuZGVkIFN0ZWxsYXIgcHVibGljIGtleSJ9XQ",
  "txFunctionFee": "AAAAAgAAAABTqjFHz0quLSka8SOrkw7R07aqDNUHAe+Qm5PX0jMiGwAAAGQAHfBZAAAADgAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAQAAAAB47DPzhNMoutc7krUC+kJ1BvEel4wkn4w1qzA7sOje0AAAAAAAAAAAAJiWgAAAAAAAAAAB0jMiGwAAAEAZjWTnxXY2lxVt0VSos6/Uvpoo3pXo6l+0Xk/P+sE5KDPwhAYkVQyXEBb8prEYprzp3aSlLF4TKcw3m/RM5IMK"
}
```

### Responses

<details><summary>200 txFunction uploaded</summary>

RESPONSE SCHEMA: application/json

| key | value |
| --- | --- |
| `hash` | `string` The SHA256 hash value of the contract |
| `signer` | `string` The public key of the signer the turret will use to sign the uploaded contract |

</details>

<details><summary>402 payment required</summary>

RESPONSE SCHEMA: application/json

| key | value |
| --- | --- |
| `message` | `string` Description of what failed |
| `turret` | `string` The public key of the turret requiring payment |
| `cost` | `string` The cost of the operation in lumens |

</details>

### Response Samples

#### 200 txFunction Uploaded

```
{
  "hash": "78565516a844fd4dfc5a7fc7da822028b04ee0aeaf981a4a914d4510906a7a32",
  "signer": "GB6VNMGXKHS4UTIXW7U23ZQFWD7UJIWCJNQZR7ISNKBTYNULCFQKKPIK"
}
```

#### 402 payment required

```
{
  "message": "Failed to process txFunctionFee",
  "turret": "GB4OYM7TQTJSROWXHOJLKAX2IJ2QN4I6S6GCJH4MGWVTAO5Q5DPNADXX",
  "cost": "0.2740000"
}
```
