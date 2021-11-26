*Note: US users can not use this flow.*

***

1. [Steps](README.md#1-steps)
2. [Scheme](README.md#2-scheme)

***

#### 1. Steps

1. The Customer wants to sell crypto
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /lib/currencies`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies) - to show to the Custome available curencies.
4. Use method [`POST /b2b/sell/methods`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-SellMethods) to get avaliable sell methods
5. Use method [`GET /b2b/sell/rate`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-GetSellRate) to get rates .

***NB**: pay attention to the flag `is_total` which affects fee limits value.*

- if the Customer enters fiat value first, then converted crypto value must be counted with the commission `is_total=true`;
- if the Customer enters crypto value first, then converted fiat value must be counted with the commission `is_total=false`.

| Parameter  |  Description  | Type | Oblygatory |
| ------------- | -------------  | -------------  | -------------  |
| `from` | transaction token | string | obligatory |
| `to` | crypto wallet address | string | obligatory |
| `amount` | amount to be converted | string | obligatory |
| `is_total` | amount with or without fee | boolean | obligatory |
| `payment` | payment method get form `/b2b/sell/methods` | string | obligatory |

Rates are freezed and associated with `sell-token`.

6. Payment Details.  
The Customer can use new card or saved card.  
To get list of saved cards use method [`GET /b2b/user/cards`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-User-UserCards).  
You will receive a list of masked customer's cards and `card_ids`.  
For the reason of PCI-DSS complience Mercuryo need to get payment details on Mercuryo side. In case of passing valid card_id in method `POST /b2b/sell` the Customer will be asked for CVV only.  
`wallet` partameter is oprional. This is wallet address for the refund. By default, it is users Mercuryo wallet
 
 7. Use method [`POST /b2b/sell`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-Sell) to initiate sell

`flow_id` has two options. You can give the customer an option to choose one of them or use the default method:
- The Customer needs to choose what to do: sell in any cases or refund if rate will change more than 5%. 
For this case, you need to integrate an interface for the Users on your side. 
- Do not give customer any options. By default, the chosen option is sell in any cases

| Parameter | Description | Value |
| ------------- | -------------  | -------------  |
| `flow_id` | sell in any cases | `payout` |
| `flow_id` | refund if rate will change more than 5% | `refund` |

`merch_tansaction_id` - transaction ID, by it you can find out its status. It is also needed to Mercuryo technical support if something going wrong. You can generate it by yourself, or Mercuryo can make it for you. Mercuryo strongly recommends you save this parameter.


8. You need to redirect the Customer to Mercuryo side by link.

Link example: `https://payments.mrcr.io/sell?parameters`

Link must contain these parameters:

| Parameter  |  Description  | Type |
| ------------- | -------------  | -------------  |
| `init_token` | your access token, you get it from method `POST /b2b/sell` | obligatory |
| `success_url` | [how to set](https://github.com/mercuryoio/Commercial-API/blob/master/admin.md) urlencoded JSON | obligatory |
| `failure_url` | [how to set](https://github.com/mercuryoio/Commercial-API/blob/master/admin.md) urlencoded JSON | obligatory |
| `status` | add to `failure_url` if the User taped on the back button or change payment method buttons - `status: back`, if you get an error as a response `status: fail` | obligatory |
| `msg` | string. This is a error message that you can get as a response from any api method | obligatory if `status: fail` |
| `scheme` | `dark` or `light` | optional |
| `lang` | language. By default it is `en`. Supported languages: `en`, `zh`, `ru`, `fr`, `hi` , `id`, `ja`, `ko`, `pt`, `es`, `tr`, `vi`  | optional |
| 'merchant_transaction_id` | merchant transaction id. You get this parameter from the response from `/b2b/sell` method | obligatory |
| 'address'| success address. You get this parameter from the response from `/b2b/sell` method | obligatory |

9. Mercuryo will redirect the user back to the success or failed url that you specified in the [admin panel](https://github.com/mercuryoio/Commercial-API/blob/master/admin.md). 
10. Redirect user to the page with the instructions how to create deposit on Mercury. The redirection link you get from method `POST /b2b/sell`. Customer needs to create a deposit on the Mercuryo side.
11. Transaction will be completed on the Mercuryo side.
12. Use method [`GET /b2b/sell/:merch_trx_id:/status`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-SellTransactionStatus) to get transaction status

***

#### 2. Scheme

![sell](https://github.com/mercuryoio/Commercial-API/blob/master/5%20Sell%20Card/sell.png)
