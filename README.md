# BAAS API

Mercuryo API is a set of crypto and fiat balances that allows users to exchange crypto to fiat and fiat to crypto quickly and easily, and top up and withdraw funds from fiat balance too.

If you have a crypto wallet or other crypto service, your users can create Mercuryo wallet and see an additional fiat balance in the interface. They can use Mercuryo wallet as simple as others that already exist in your service.

The Mercuryo API has structured around your and users' wallets. Users create wallets and perform operations with them, and you monitor the transactions of these users and manage your own savings earned from each user transaction.

***

## Methods

You can find reference documentation with methods description [in sandbox](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html).

All the methods in b2b domain have to be signed up with `b2b-bearer-token`. You can get it in the authorization flow described in [New sign in ](new-sign-in/README.md).

***

## Sign up/ Sign in

*Note: For authorization, you need your `sdk-partner-token`. Ask your Mercuryo manager to get it.*

[Sign up/Sign in](new-sign-in/README.md)


***

## KYC

There are two types of KYC: KYC and KYC2.
1. The Customer need to pass KYC to start using Mercuryo. If the Customer passed KYC he can:
 - Buy or Sell with a card.
 - Buy crypto by bank transfer.
2. The Customer needs to pass KYC2 too to make operations with IBAN.
3. The Customer can get information about his IBAN and balance with expired KYC.

*NB: KYC and KYC2 can expire. In this case, the Customer will need to pass it again.*

**NB: The customer does not pass the KYC instantly. It is failed if KYC takes more than 15 minutes. SO try to get KYC status during this time.**

## Creating new IBAN for user

IBANs are available only for EU users.

The Customer can create IBAN. [Here](9-iban-create/README.md) is the instruction.

***

## Popular scenarios for using API:

1. [Buy crypto with card](1-buy-card/README.md)
2. [Buy crypto with bank transfer](2-buy-invoice/README.md)
3. [Buy crypto using user's IBAN](3-buy-iban/README.md)
4. [Top Up user's IBAN](4-fiat-deposit/README.md)
5. [Sell crypto and withdraw fiat to card](5-sell-card/README.md)
6. Sell crypto and withdraw to random IBAN - TBD
7. [Withdraw from User's IBAN to random IBAN](8-fiat-withdraw/README.md)

***

## Transactions

| Transaction  | Type  |
| :-- | :--  |
| buy crypto with a card| `buy_card` |
| buy crypto using user's IBAN | `buy_iban` |
| buy crypto by invoice | `buy_iban_invoice` |
| sell crypto with a card | `sell_card` |
| sell crypto using user's IBAN | `sell_iban` |
| top up user's IBAN | `deposit` |
| withdraw from user's IBAN | `withdraw` |

| Transaction  | trx_type  |
| :-- | :--  |
| pending  | transaction is in progress |
| failed | transaction is failed |
| success | transaction is successfully completed |

Fail flow:

1. Buy: fiat would be returned to the users card\IBAN\etc.
2. Sell: crypto would be returned to the users `refund_address`.

Request example:

`GET https://sandbox-cryptosaas.mrcr.io/v1.6/b2b/transactions?merchant_transaction_id=123456789&date_start=1606210749&date_end=1637833150`

| Parameter  | Description  | Obligatory |
| :-- | :--  | :--  |
| merchant_transaction_id | filter by transaction ID | optional |
| date_start | start of a date period | optional |
| date_end | end of a date period | optional |

Response example:

```
  "status": 200,
  "total": 1,
  "next": null,
  "prev": null,
  "data": [
    {
      "id": 123456789",
      "parent_id": "123456789",
      "user_id": 1234,
      "currency": "USDT",
      "status": "succeeded",
      "amount": "110",
      "fiat_amount": "0",
      "created_at": "2021-10-26 08:25:28",
      "updated_at": "2021-10-26 08:27:20",
      "fiat_currency": "EUR",
      "type": "buy_card",
      "merchant_transaction_id": "123456789"
    ]}
```

***

## Errors

| Error code  | Description  |
| :-- | :--  |
| 2xx | all is okay. The request was successfully received, understood, and accepted |
| 4xx | most of them are a part of our normal flow, so all of those codes are coming from the backend and processed normally by our frontend. Don’t care much if you see any of those in your logs, as they don’t indicate any serious problem related with service |
| 5xx | server errors. Mercuryo team have already seen them in monitor and already chasing the problem, this is normally resolved as quickly as possible, because it might affects all Mercuryo partners. So if you see that error was detected 3 days ago or even half day ago — 100% it’s fixed |


**Most common cases of 4xx**

| Error code  | Description  |
| :-- | :--  |
| 400 | validation error. Wrong parameters etc |
| 401 | unauthorized, client token authentication timeout |
| 403 | access  error |
| 404 |  method not found |
