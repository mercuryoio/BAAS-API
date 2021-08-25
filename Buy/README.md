# Buying crypto on Partner side

**You can use Mercuryo API only with your partner token. Ask your Mercuryo manager to get it.**


[1. Steps to buy crypto](#steps)

[2. Scheme](#scheme)


<a name="steps"></a>
## 1. Steps to buy crypto

**User can buy crypto on your side.**

1. User wants buy crypto.

2. Use method [GET /lib/currencies](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies)

3. Use method [`POST /sdk-partner/sign-in`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKLogin) to authorize user. More about login is [here](login.md).

4. Mercuryo API returns to you available payment methods.

5. You get rates using API-method [`GET /b2b/buy/rate`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-GetBuyRate).

While using this method pay attention to the flag `is total` which affects on fee limits value:

* if user is buying crypto and enter fiat value first, then converted crypto value must be counted with the commission `is total=true`;
* if user is buying crypto and enter crypto value first, then converted fiat value must be counted with the commission `is_total=false`.

Rates are freezed and associated with buy-token.

| Error | Text | Description|
|:--|:--|:--|
| 403011  | `From cannot be blank`  | parameter **From** not set  |
| 403012   | `To cannot be blank`  | parameter **To** not set |
| 403013   | `Amount cannot be blank` or `Unable to find currency options` | parameter **Amount** not set or the value is not valid  |
| 403014  | `Invalid widget` | parameter **widget_id** not set or widget not found  |
| 403015 | `Invalid payment flow`  | non-existent flow specified  |
| 500001  | `try later`  | Failed to get rates for various reasons  |
| 500002  | amount off limits  | Failed to get rates  |

6. Use method [`GET /b2b/user/cards`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-User_cards). to get list of users card. If response is empty or if user want to add new card - user can add card on Mercuryo side.
7. Use method [`POST /b2b/buy`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-Buy) to initiate buy
`merch_trx_id` - transaction ID, by it you can find out its status. It is also needed to Mercuryo technical support if something going wrong. You can generate it by yourself, or Mercuryo can make it for you. We strongly recommend to save this parameter.

7. You need to redirect user to Mercuryo side by link. The User will add his card on the Mercuryo side

Link example: `https://payments.mrcr.io/buy?parameters`

Link must contains this parameters:

| Parameter  |  Description  | Type |
| ------------- | -------------  | -------------  |
| `init_token` | your access token, you get it from method `GET /b2b/kyc-access-token` | obligatory |
| `scheme` | `dark` or `light` | optional |
| `lang` | language. By default it is `en`. Supported languages: `en`, `zh`, `ru`, `fr`, `hi` , `id`, `ja`, `ko`, `pt`, `es`, `tr`, `vi`  | optional |

8. Mercuryo will redirect the User back to the success or failed url that you specified in the [admin panel](ADD_LINK). Mercuryo  will initiate a withdrawal transaction to the specified user wallet. The User get transaction result from you.

9. Mercuryo API will send callback to you  when transaction will be completed.

10. To show transaction status to user before you get the callback with status use method [`GET /b2b/buy/:merchant_trx_id/status`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-BuyTransactionStatus). 

`merch_trx_id` - transaction ID, by it you can find out its status. It is also needed to Mercuryo technical support if something going wrong. You can generate it by yourself, or Mercuryo can make it for you. We strongly recommend to save this parameter.


<a name="scheme"></a>
## 2. Scheme
![buy_scheme](scheme/buy.png)
