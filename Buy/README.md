

1. [Steps](README.md/#1-steps)
2. [Scheme](README.md/#2-scheme)

***

<a name="steps"></a>
#### 1. Steps

1. The Customer wants buy crypto.
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /lib/currencies`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies) - to show to the Custome available curencies.
4. Use method [`GET /b2b/buy/methods`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Buy-BuyMethods) to get avaliable buy methods.
5. Use method [`GET /b2b/buy/rate`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Buy-GetBuyRate) to get rates.

While using this method pay attention to the flag `is total` which affects on fee limits value:

* if the Customer is buying crypto and enter fiat value first, then converted crypto value must be counted with the commission `is total=true`;
* if the Customer is buying crypto and enter crypto value first, then converted fiat value must be counted with the commission `is_total=false`.

Rates are freezed and associated with buy-token.

| Error | Text | Description|
|:--|:--|:--|
| 403011  | `From cannot be blank`  | parameter **From** not set  |
| 403012   | `To cannot be blank`  | parameter **To** not set |
| 403013   | `Amount cannot be blank` or `Unable to find currency options` | parameter **Amount** not set or the value is not valid  |
| 403015 | `Invalid payment flow`  | non-existent flow specified  |
| 500001  | `try later`  | failed to get rates for various reasons  |
| 500002  | amount off limits  | failed to get rates  |

6. Payment Details.  
The Customer can use new card or saved card.  
To get list of saved cards use method [`GET /b2b/user/cards`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-User-UserCards).  
You will receive a list of masked customer's cards and `card_ids`.  
For the reason of PCI-DSS complience Mercuryo need to get payment details on Mercuryo side. In case of passing valid card_id in method [`POST /b2b/buy`] the Customer will asked for CVV only.  

7. Use method [`POST /b2b/buy`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Buy-Buy) to initiate buy. 

`merch_trx_id` - transaction ID, using it you can find out the transaction status. It is also needed to Mercuryo technical support if something going wrong. You can generate it by yourself, or Mercuryo can make it for you. We strongly recommend you to save this parameter.

8. You need to redirect the Customer to Mercuryo side by link. The User will add his card on the Mercuryo side

Link example: `https://payments.mrcr.io/buy?parameters`

Link must contains this parameters:

| Parameter  |  Description  | Type |
| ------------- | -------------  | -------------  |
| `init_token` | your access token, you get it from method `POST /b2b/buy` | obligatory |
| `scheme` | `dark` or `light` | optional |
| `lang` | language. By default it is `en`. Supported languages: `en`, `zh`, `ru`, `fr`, `hi` , `id`, `ja`, `ko`, `pt`, `es`, `tr`, `vi`  | optional |

9. Mercuryo will redirect the Customer back to the success or failed url that you specified in the [admin panel](https://github.com/mercuryoio/Commercial-API/blob/master/admin.md). Mercuryo will initiate a withdrawal transaction to the specified Customer's wallet. 

10. Mercuryo API will send callback to you  when transaction will be completed.

11. To show transaction status to the Customer before you get the callback with status use method [`GET /b2b/buy/:merchant_trx_id/status`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Buy-BuyTransactionStatus).

***

<a name="scheme"></a>
#### 2. Scheme
![buy_scheme](scheme/buy.png)
