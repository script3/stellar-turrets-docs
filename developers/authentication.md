# Authentication

## XdrToken

The Turret XDR Token is a signed transaction envelope XDR that is signed by the
account seeking authentication's public key. The signed XDR, or XDR Token, is
provided as a Authorization Bearer token to the Turret.

### XdrToken Structure

The Xdr Token Transaction is a Stellar transaction that authenticates public key
ownership against a Turret. It MUST have a Sequence Number of 0 to ensure the
transaction is not malicious and is unable to be submitted. The following
information will be pulled from the Xdr Token Transaction:

* Sequence Number
  * Verify the sequence number is 0 - if not, reject the token.
* Source account
  * The account that is paying fees in to the turret through the claimable balance
* Timebounds
  * The max time of the timebounds will be the absolute UNIX expiration time of the token.
* Operations
  * ClaimClaimableBalance
    * The Balance Id of the Claimable Fee Balance (of the structure show below) of the fee payment to the turret.
  * ManageData
    * Used to pass token parameters into the turret
    * Valid parameters
      * Entry name = "txFunction" (If no txFunctions parameters are passed in, the turret does not limit any txFunctions to run)
        * Value = the hash of the txFunction that the user is allowing the turret to run
* Signature
  * The Fee Transaction is signed by the account that is the source account of the transaction

### Example

This [RunKit Example](https://runkit.com/mootz12/60d1f69582e0580013bb591e)
showcases how to generate a XDR Token. It creates, signs, and generates a valid
Authorization token.

| | |
| --- | --- |
| **Security Scheme Type** | HTTP |
| **HTTP Authorization Scheme** | bearer |
| **Bearer Format** | "XDR" |
