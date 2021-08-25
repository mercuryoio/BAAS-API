# Buying crypto on Partner side

**You can use Mercuryo API only with your partner token. Ask your Mercuryo manager to get it.**

[1. Steps](#steps)

[2. Scheme](#scheme)


<a name="steps"></a>
## 1. Steps 

1. The User wants buy crypto.

2. Use method [GET /lib/currencies](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies)

3. Use method [`POST /sdk-partner/sign-in`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKLogin) to authorize user. More about login is [here](login.md).

| Error | Text | Description|
|:--|:--|:--|
| 403004  | `User not found` | wrong uuid |
| 403005 | `invalid country by phone number`  | wrong countrycode  |
| 403005  | `Country `%s` is not active or not exist`  | country is inactive  |
| 403005  | `Country `%s` is in black list`  | country in black list  |
| 403010  | `Phone is invalid`  | Phone is invalid  |
| 403006  | `Accept cannot be blank for new users`  | there is no `acception` parameter  |
| 40304  | `Invalid uuid4 ` | wrong uuid format  |

4. Mercuryo API returns to you available payment methods.

5. You get rates using API-method [`GET /b2b/buy/rate`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-GetBuyRate).

While using this method pay attention to the flag which affects on fee limits value.

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

6. Accept payment details from the user. Use API-method [`GET /b2b/user/cards`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-User_cards). If you get an empty response, then add a new card. Adding cards and debit are on the Mercuryo side.

7. You need to redirect user to Mercuryo side by link. Link must contains this parameters:

| Parameter  |  Description  |
| ------------- | -------------  |
| `init_token` | your access token |
| `flow` | user's action: `buy`, `sell` etc |
| `scheme` | `dark` or `light`. This one is optional |
| `lang` | language. By default it is `en`. Supported languages: `en`, `zh`, `ru`, `fr`, `hi` , `id`, `ja`, `ko`, `pt`, `es`, `tr`, `vi`  |
| `success_url` | redirect to your site with successful result |
| `failure_url` | redirect to your site with failed result |

8. You will redirect the user back to the success or failed url that you specified in the [admin panel](ADD_LINK). And Mercury initiates a withdrawal transaction to the specified user wallet. User get transaction result from you.

9. Mercuryo API sends to you callback when transaction will be completed.

10. To show transaction status to user send request to Mercuryo API using method [`GET /b2b/buy/:merchant_trx_id/status`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-BuyTransactionStatus). Use this method before you get callback.

`merch_trx_id` - stands for transaction ID, by which you can find out its status or contact technical support. You can generate it by yourself, or Mercuryo can make it for you. We strongly recommend to save this parameter.


<a name="scheme"></a>
## 2. Scheme
![buy_scheme](scheme/buy.png)
