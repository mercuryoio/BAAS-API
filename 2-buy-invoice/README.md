
1. [Steps](README.md/#steps)
2. [Scheme](README.md/#scheme)

***

<a name="steps"></a>
#### 1. Steps

1. The Customer wants to buy crypto.
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /lib/currencies`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies) - to show to the Customer available currencies.
4. Use method [`GET /b2b/fiat/buy-methods`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_Buy-BuyMethods) to get available buy methods. You need to implement a form on your side in which the Customer can choose one of available methods.
5. Use method [`GET /b2b/fiat/buy-rates`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_Buy-GetBuyRate) to get rates.

While using this method pay attention to the flag `is total` which affects on fee limits value:

* if the Customer enters fiat value first, then converted crypto value must be counted with the commission `is total=true`;
* if the Customer enters crypto value first, then converted fiat value must be counted with the commission `is_total=false`.

| Parameter  |  Description  | Type | Obligatory |
| :-- | :--  | :--  | :--  |
| `from` | transaction token | string | obligatory |
| `to` | crypto wallet address | string | obligatory |
| `amount` | Amount to be converted | string | obligatory |
| `is_total` | amount with or without fee | boolean | obligatory |
| `payment` | payment method get form `/b2b/fiat/buy-methods` | string | obligatory |

Rates are frozen and associated with buy-token.

| Error | Text | Description|
|:--|:--|:--|
| 403011  | `From cannot be blank`  | parameter **From** not set  |
| 403012   | `To cannot be blank`  | parameter **To** not set |
| 403013   | `Amount cannot be blank` or `Unable to find currency options` | parameter **Amount** not set or the value is not valid  |
| 403015 | `Invalid payment flow`  | non-existent flow specified  |
| 500001  | `try later`  | failed to get rates for various reasons  |
| 500002  | amount off limits  | failed to get rates  |

6. You need to implement a form on your side in which the Customer can type his wallet.
7. Use method [`POST /b2b/fiat/buy`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_Buy-Buy) to initiate buy.

`merch_tansaction_id` - transaction ID, using it you can find out the transaction status. It is also needed to Mercuryo technical support if something going wrong. You can generate it by yourself, or Mercuryo can make it for you. We strongly recommend you save this parameter.

| Parameter  |  Description  | Type | Obligatory |
| :-- | :--  | :--  | :--  |
| `trx_token` | transaction token | string | obligatory |
| `address` | crypto wallet address | string | obligatory |
| `merchant_transaction_id` | transaction ID | string | optional |

8. Use method [`GET /b2b/transactions/:merchant_trx_id`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_Sell-SellTransactionStatus) to get transaction status.

***

<a name="scheme"></a>
#### 2. Scheme

![new-invoice](new-invoice.png)
