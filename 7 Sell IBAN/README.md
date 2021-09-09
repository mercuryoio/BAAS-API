***

1. [Steps](README.md#1-steps)
2. [Scheme](README.md#2-scheme)

***

#### 1. Steps

1. The Customer wants to sell crypto
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /lib/currencies`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies) - to show to the Custome available curencies.
4. Use method [`POST /b2b/sell/methods`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-SellMethods) to get avaliable sell methods. You need to realize a form on your side in which the Customer can choose one of available methods.
5. Use method [`GET /b2b/sell/rate`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-GetSellRate) to get rates.

***NB**: pay attention to the flag `is_total` which affects fee limits value.*

- if the Customer enters fiat value first, then converted crypto value must be counted with the commission `is_total=true`;
- if the Customer enters crypto value first, then converted fiat value must be counted with the commission `is_total=false`.

Rates are freezed and associated with `sell-token`.

6. You need to realize form on your side in which the Customer can type any IBAN he wants to. 
7. Use method [`POST /b2b/sell`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-Sell) to initiate sell

`flow_id` has two options. You can give the customer an option to choose one of them or use the default method:
- The Customer needs to choose what to do: sell in any cases or refund if rate will change more than 5%. 
For this case, you need to integrate an interface for the Users on your side. 
- Do not give customer any options. By default, the chosen option is sell in any cases

| Parameter | Description | Value |
| ------------- | -------------  | -------------  |
| `flow_id` | sell in any cases | `payout` |
| `flow_id` | refund if rate will change more than 5% | `refund` |

`merch_trx_id` - transaction ID, by it you can find out its status. It is also needed to Mercuryo technical support if something going wrong. You can generate it by yourself, or Mercuryo can make it for you. Mercuryo strongly recommends you save this parameter.

8. Transaction will be completed on the Mercuryo side.
9. Use method [`GET /b2b/sell/:merch_trx_id:/status`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-Sell-SellTransactionStatus) to get transaction status

***

#### 2. Scheme

![sell]()
