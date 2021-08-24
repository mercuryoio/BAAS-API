*Note: US users can not use this flow.*

**You can use Mercuryo API only with your partner token. Ask your Mercuryo manager to get it**

***

1. [Steps](/commAPIsell.md#1-steps)
2. [Scheme](commAPIsell.md#2-scheme)

***

User can buy crypto on your side with Mercuryo API.

#### 1. Steps

1. The User want sell crypto
2. Use method [GET /lib/currencies]()
3. Use method [GET /lib/countries]()
4. Use method [POST /sdk-partner/sign-in]() to authorise user. More about login is [here]()
5. Use method [GET /b2b/sell/methods]()
6. Pass to Mercury parameters of crypto currency, fiat currency, etc from user to Mercuryo API by method [POST /b2b/sell/methods]()

Flow has two options. You can give user an option to choose one of them or using default method:
- The User needs to choose what to do: sell in any cases or refund if rate will change more than 5%.
For this case you need to integrate methods By default the refund adress is users's Mercuryo wallet
- Do not give user any options. By default the chosen option is sell in any cases

7. Redirect user to Mercuryo website. User will add his card on the Mercuryo side
8. Transaction operation will be completed on the Mercuryo side
9. Use method [GET /b2b/sell/:merch_trx_id:/status]() to get transactions statuses

***

#### 2. Scheme
