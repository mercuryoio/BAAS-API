# Buying crypto with card on Partner side

[1. Steps to buy crypto](#steps)

[2. Scheme](#scheme)


<a name="steps"></a>
## 1. Steps to buy crypto

**User can buy crypto on your side with Mercuryo API.**

1. On your side user wants to buy crypto with card.

2. You will need to authorize user and check if he can use Mercuryo API. Please check (link to ligin md here ) for more information.

3. Use method [GET /lib/currencies](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies) - to show user available cuurencies.

4. After that you need to log in Mercuryo API with [`POST /sdk-partner/sign-in`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKLogin).

| Error | Text | Description|
|:--|:--|:--|
| 403004  | `User not found` | wrong uuid |
| 403005 | `invalid country by phone number`  | wrong countrycode  |
| 403005  | `Country `%s` is not active or not exist`  | country is inactive  |
| 403005  | `Country `%s` is in black list`  | country in black list  |
| 403010  | `Phone is invalid`  | Phone is invalid  |
| 403006  | `Accept cannot be blank for new users`  | there is no `acception` parameter  |
| 40304  | `Invalid uuid4 ` | wrong uuid format  |


5. Mercuryo API returns to you available payment methods.

6. On your side user selects paramenters to buy crypto.

7. You send users's data to Mercuryo API using API-method [`/b2b/buy/rate`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-GetBuyRate).


| Error | Text | Description|
|:--|:--|:--|
| 403011  | `From cannot be blank`  | parameter **From** not set  |
| 403012   | `To cannot be blank`  | parameter **To** not set |
| 403013   | `Amount cannot be blank` or `Unable to find currency options` | parameter **Amount** not set or the value is not valid  |
| 403014  | `Invalid widget` | parameter **widget_id** not set or widget not found  |
| 403015 | `Invalid payment flow`  | non-existent flow specified  |
| 500001  | `try later`  | Failed to get rates for various reasons  |
| 500002  | amount off limits  | Failed to get rates  |

8. Mercuryo API returns to you buy-token.

**While the transaction is in progress, the user is redirected to the 3D-secure page of his bank to confirm the payment.**

9. Mercuryo API sends to you callback.

10. The response to this callback must have a status of the transaction using API-method [`/b2b/buy/:merch_trx_id:/status`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-BuyTransactionStatus).

11. Mercuryo API sends to you trx status array.

12. User get transaction result from you.

<a name="scheme"></a>
## 2. Scheme

![buy_scheme](img/buy_scheme_edit.png)
