# Turret

View information about a Turret

## Get Turret Information

Returns basic information about the turret

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
