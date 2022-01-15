# Turret

View information about a Turret

## Get Turret Information

Returns basic information about the turret

### Request

```
GET /
```

### Responses

<details><summary>200 Success</summary>

| key | value |
| --- | --- |
| `turret` | `string` The public key of the turret owner |
| `network` | `string` The Stellar Network the turret is on. `TESTNET` or `PUBLIC` |
| `horizon` | `string` The Horizon API the turret uses |
| `version` | `string` The repository version and last commit |
| `fee` | `object (schemas)` |
| `divisor` | `object (schemas)` |

</details>

### Response Sample

```json
{
  "turret": "GB4OYM7TQTJSROWXHOJLKAX2IJ2QN4I6S6GCJH4MGWVTAO5Q5DPNADXX",
  "network": "TESTNET",
  "horizon": "https://horizon-testnet.stellar.org",
  "version": "v0.0.0-ff9e9750369cc8aed29af9f08ae34634594cbe41",
  "fee": {
    "min": 1,
    "max": 10,
    "days": 180
  },
  "divisor": {
    "upload": 1000,
    "run": 100000
  }
}
```

## Get the Turret's TOML file

Returns the `stellar.toml` file associated with the turret

### Request

```
GET /.well-known/stellar.toml
```

### Responses

<details><summary>200</summary>

A [Stellar TOML](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0001.md) file

</details>
