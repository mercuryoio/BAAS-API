***

1. [Steps](README.md#1-steps)
2. [Scheme](README.md#2-scheme)

***

#### 1. Steps

1. The Customer wants to sell crypto
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /lib/currencies`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies) - to show to the Custome available curencies.
4. Use method [`POST /b2b/sell/methods`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-SellMethods) to get avaliable sell methods
5. Use method [`GET /b2b/sell/rate`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-GetSellRate) to get rates.

***NB**: pay attention to the flag `is_total` which affects fee limits value.*

- if the Customer enters fiat value first, then converted crypto value must be counted with the commission `is_total=true`;
- if the Customer enters crypto value first, then converted fiat value must be counted with the commission `is_total=false`.

Rates are freezed and associated with `sell-token`.

6. You need to realize form on your side in which the Customer can choose his IBAN. 
7. Transaction will be completed on the Mercuryo side.
8. Use method [`GET /b2b/sell/:merch_trx_id:/status`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-SellTransactionStatus) to get transaction status

***

#### 2. Scheme

![sell]()
