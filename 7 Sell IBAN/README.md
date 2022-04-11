***

1. [Steps](README.md#1-steps)
2. [Scheme](README.md#2-scheme)

***

#### 1. Steps

1. The Customer wants to sell crypto.
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /lib/currencies`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-Public-PublicCurrencies) - to show to the Custome available curencies.
4. Use method [`POST /b2b/sell/methods`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_Sell-SellMethods) to get avaliable sell methods. You need to implement a form on your side in which the Customer can choose one of available methods.
5. Use method [`GET /b2b/sell/rate`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_Sell-GetSellRate) to get rates.

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

6. You need to implement form on your side in which the Customer can type any IBAN he wants to. 
7. Use method [`POST /b2b/sell`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_Sell-Sell) to initiate sell

`flow_id` has two options. You can give the customer an option to choose one of them or use the default method:
- The Customer needs to choose what to do: sell in any cases or refund if rate will change more than 5%. 
For this case, you need to integrate an interface for the Users on your side. 
- Do not give customer any options. By default, the chosen option is sell in any cases

| Parameter | Description | Value |
| ------------- | -------------  | -------------  |
| `flow_id` | sell in any cases | `payout` |
| `flow_id` | refund if rate will change more than 5% | `refund` |

`merch_tansaction_id` - transaction ID, by it you can find out its status. It is also needed to Mercuryo technical support if something going wrong. You can generate it by yourself, or Mercuryo can make it for you. Mercuryo strongly recommends you save this parameter.

8. Transaction will be completed on the Mercuryo side.
9. Use method [`GET /b2b/sell/:merch_trx_id:/status`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-Sell-SellTransactionStatus) to get transaction status

***

#### 2. Scheme

![sell](https://github.com/mercuryoio/Commercial-API/blob/master/7%20Sell%20IBAN/sell%20IBAN2.png)
