*Note: US users can not use this flow.*

***

1. [Steps](/commAPIsell.md#1-steps)
2. [Scheme](commAPIsell.md#2-scheme)

***

#### 1. Steps

1. The User want sell crypto
2. Use method [`GET /lib/currencies`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-GetSellRate) - to show user available curencies.
3. Use method [`POST /sdk-partner/sign-in`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKLogin) to authorise user. More about login is [here](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md)
4. Use method [`POST /b2b/sell/methods`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-SellMethods) to get avaliable sell methods
5. Use metod [`GET /b2b/sell/rate`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-GetSellRate) to get rates .

***NB**: pay attention to the flag `is_total` which affects on fee limits value.*

- if the User enter fiat value first, then converted crypto value must be counted with the commission `is_total=true`;
- if the User enter crypto value first, then converted fiat value must be counted with the commission `is_total=false`.

Rates are freezed and associated with `sell-token`.

6. Use method `GET /b2b/user/cards` to get list of users card. If response is empty or if user want to add new card - user can add card on Mercuryo side

 `wallet` partameter is oprional. This is wallet adress to refund. By default it is users Mercuryo wallet
 
 7. Use method [`POST /b2b/sell`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-Sell) to initiate sell

`flow_id` has two options. You can give user an option to choose one of them or using default method:
- The User needs to choose what to do: sell in any cases or refund if rate will change more than 5%. 
For this case you need to integrate interface for the Users on your side. 
- Do not give user any options. By default the chosen option is sell in any cases

`merch_trx_id` - transaction ID, by it you can find out its status. It is also needed to Mercuryo technical support if something going wrong. You can generate it by yourself, or Mercuryo can make it for you. We strongly recommend to save this parameter.


8. You need to redirect user to Mercuryo side by link.

Link example: `https://payments.mrcr.io/sell?parameters`

Link must contains this parameters:

| Parameter  |  Description  | Type |
| ------------- | -------------  | -------------  |
| `init_token` | your access token, you get it from method `GET /b2b/kyc-access-token` | obligatory |
| `scheme` | `dark` or `light` | optional |
| `lang` | language. By default it is `en`. Supported languages: `en`, `zh`, `ru`, `fr`, `hi` , `id`, `ja`, `ko`, `pt`, `es`, `tr`, `vi`  | optional |

9. Transaction operation will be started on the Mercuryo side
10. Mercuryo will redirect the user back to the success or failed url that you specified in the [admin panel](ADD_LINK). 
11. Redirect user to the page with the instructions how to create deposit on the Mercury. The redirection link . User will create deposit on the Mercuryo side
12. Transaction operation will be ended on the Mercuryo side
13. Use method [`GET /b2b/sell/:merch_trx_id:/status`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-SellTransactionStatus) to get transaction status

***

#### 2. Scheme
