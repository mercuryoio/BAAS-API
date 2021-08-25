*Note: US users can not use this flow.*

***

1. [Steps](/README.md#1-steps)
2. [Scheme](/README.md#2-scheme)

***

#### 1. Steps

1. The Customer want sell crypto
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /lib/currencies`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies) - to show to the Custome available curencies.
4. Use method [`POST /b2b/sell/methods`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-SellMethods) to get avaliable sell methods
5. Use metod [`GET /b2b/sell/rate`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-GetSellRate) to get rates .

***NB**: pay attention to the flag `is_total` which affects on fee limits value.*

- if the User enter fiat value first, then converted crypto value must be counted with the commission `is_total=true`;
- if the User enter crypto value first, then converted fiat value must be counted with the commission `is_total=false`.

Rates are freezed and associated with `sell-token`.

6. Payment Details.  
The Customer can use new card or saved card.  
To get list of saved cards use method [`GET /b2b/user/cards`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-User-UserCards).  
You will receive a list of masked customer's cards and `card_ids`.  
For the reason of PCI-DSS complience Mercuryo need to get payment details on Mercuryo side. In case of passing valid card_id in method `POST /b2b/sell` the Customer will asked for CVV only.  
`wallet` partameter is oprional. This is wallet adress for refund. By default it is users Mercuryo wallet
 
 7. Use method [`POST /b2b/sell`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-Sell) to initiate sell

`flow_id` has two options. You can give user an option to choose one of them or use default method:
- The User needs to choose what to do: sell in any cases or refund if rate will change more than 5%. 
For this case you need to integrate interface for the Users on your side. 
- Do not give user any options. By default the chosen option is sell in any cases

| Parameter | Description | Value |
| ------------- | -------------  | -------------  |
| `flow_id` | sell in any cases | `payout` |
| `flow_id` | refund if rate will change more than 5% | `refund` |

`merch_trx_id` - transaction ID, by it you can find out its status. It is also needed to Mercuryo technical support if something going wrong. You can generate it by yourself, or Mercuryo can make it for you. We strongly recommend to save this parameter.


8. You need to redirect user to Mercuryo side by link.

Link example: `https://payments.mrcr.io/sell?parameters`

Link must contains this parameters:

| Parameter  |  Description  | Type |
| ------------- | -------------  | -------------  |
| `init_token` | your access token, you get it from method `POST /b2b/sell` | obligatory |
| `scheme` | `dark` or `light` | optional |
| `lang` | language. By default it is `en`. Supported languages: `en`, `zh`, `ru`, `fr`, `hi` , `id`, `ja`, `ko`, `pt`, `es`, `tr`, `vi`  | optional |

9. Mercuryo will redirect the user back to the success or failed url that you specified in the [admin panel](https://github.com/mercuryoio/Commercial-API/blob/master/admin.md). 
10. Redirect user to the page with the instructions how to create deposit on Mercury. The redirection link you get from method `POST /b2b/sell`. User neet to create deposit on the Mercuryo side.
11. Transaction will be completed on the Mercuryo side.
12. Use method [`GET /b2b/sell/:merch_trx_id:/status`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-SellTransactionStatus) to get transaction status

***

#### 2. Scheme
