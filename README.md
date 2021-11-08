# Commercial-API

Mercuryo API is a set of crypto and fiat balances that allows users to quickly and easily exchange crypto to fiat and fiat to crypto, and top up and withdraw funds from fiat balance too.

If you have a crypto wallet or other crypto service, your users can create Mercuryo wallet and see an additional fiat balance in the interface. They can use Mercuryo wallet as simple as other that already exist in your service.

The Mercuryo API is structured around a your and user's wallets. Users create wallets and perform operations with them, and you monitors the transactions of these users and manages your own savings earned from each user transaction.

***

## Methods

You can find reference documentation with methods description [here](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html)

All the methods in b2b domain have to be signed up with `b2b-bearer-token`. You can get it in authorization flow described here.

***

## Sign up/ Log in

*Note: For authorization you need your `sdk-partner-token`. Ask your Mercuryo manager to get it.*

[Sign up/Log in](https://github.com/mercuryoio/Commercial-API/tree/master/0%20Login)


***

## KYC

There are two types of KYC: KYC and KYC2.
1. The Customer need to pass KYC to start using Mercuryo. If the Customer passed KYC he can:
 - Buy or Sell with a card
 - Buy crypto with bank transfer
2. The Customer need to pass KYC2 too to make operations with IBAN.
3. The Customer can get information about his IBAN number and balance with expired KYC.

*NB: KYC and KYC2 can expire. In this case the Customer will need to pass it again.*

**NB: The customer does not pass the KYC instantly. It is failed if KYC takes more than 15 minutes. SO try to get KYC status during this time.**

## Creating new IBAN for user

IBANs is available only for EU users.

The Customer can create IBAN. [Here](https://github.com/mercuryoio/Commercial-API/blob/master/9%20IBAN%20Create/README.md) is the instruction.

***

## Popular scenarios for using API:

1. [Buy crypto with card](https://github.com/mercuryoio/Commercial-API/tree/master/1%20Buy%20Card)
2. [Buy crypto with bank transfer](https://github.com/mercuryoio/Commercial-API/blob/master/2%20Buy%20Invoice/README.md)
3. [Buy crypto using user's IBAN](https://github.com/mercuryoio/Commercial-API/blob/master/3%20Buy%20IBAN/README.md)
4. [Top Up user's IBAN](https://github.com/mercuryoio/Commercial-API/blob/master/4%20fiat%20deposit/README.md)
5. [Sell crypto and withdraw fiat to card](https://github.com/mercuryoio/Commercial-API/blob/master/5%20Sell%20Card/README.md)
6. Sell crypto and withdraw to random IBAN - tbd
7. [Withdraw from User's IBAN to random IBAN](https://github.com/mercuryoio/Commercial-API/blob/master/8%20fiat%20withdraw/README.md)

***

##  Transaction status types 

#### BUY
There are two internal operations "buy" and "withdraw" per 1 transaction. They are the same for cards and IBANs

**Type: `buy`**

| Status  | Description  | 
| ------------- | -------------  |
| `new` | transaction initiated |
| `pending` | waiting for any action from the user to continue the transaction (waiting for 3ds input or descriptor) |
| `cancelled` | transaction cancelled (usually due to timeout of descriptor or 3ds) |
| `paid` | transaction completed successfully (money debited from the card) |
| `order_failed` | transaction was rejected by the issuer bank |
| `descriptor_failed` | the user entered an invalid descriptor three times |
| `failed_exchange' | exchange is failed |
| `order_scheduled` | transaction is successful, the money is held off/frozen on the card by the bank, Mercuryo are waiting for the client to pass KYC. As soon as the client passes KYC crypto will be sent to the address, if the client fails KYC transaction will be canceled within 1 hour abd client’s bank will return money to the card.|

**Type: `withdraw`**

| Status  | Description  |
| ------------- | -------------  | 
| `new` | transaction initiated |
| `pending` | transaction in progress |
| `failed` | completed unsuccessfully (this is rare) |
| `failed_exchange` | exchange is failed | 
| `completed` | successfully completed (received transaction hash) |

#### SELL

There are two internal operations "deposit" and "payout"\"iban-payout" per 1 transaction. Payout is different for cards or IBAN

**Type:** `deposit`

| Status  | Description  | 
| ------------- | -------------  |
| `new` | new deposit |
| `pending`| deposit in progress |
| `succeeded` | deposit is done |
| `failed` | something went wrong |
| `payout_failed` | |

**Type:** `payout` This one is for card operation

| Status  | Description  | 
| ------------- | -------------  |
| `new` | transaction created |
| `pending` | transaction in progress |
| `completed` | successfully completed (money transferred to the card) |
| `failed` | not completed successfully (crypto is refunded to `refund_address`) |

**Type:** `iban-payout` This one is  for IBAN operation

| Status  | Description  | 
| ------------- | -------------  |
| `new` | this status is shown before IBAN transaction has created |
| `pending` | transaction in progress |
| `completed` | successfully completed (money transferred to the card) |
| `failed` | not completed successfully (crypto is refunded to `refund_address`) |
| `cancelled` | transaction is cancelled | 
| `hold` | smth going wrong. Users fiat is holded |

***

## Errors

| Error code  | Description  | 
| ------------- | -------------  |
| 2xx | all is okay. The request was successfully received, understood, and accepted |
| 4xx | most of them are a part of our normal flow, so all of those codes are coming from the backend and processed normally by our frontend. Don’t care much if you see any of those in your logs, as they don’t indicate any serious problem related with service |
| 5xx | server errors. Mercuryo team have already seen them in monitor and already chasing the problem, this is normally resolved as quickly as possible, because it might affects all Mercuryo partners. So if you see that error was detected 3 days ago or even half day ago — 100% it’s fixed |


**Most common cases of 4xx**

| Error code  | Description  | 
| ------------- | -------------  |
| 400 | validation error. Wrong parameters etc | 
| 401 | unauthorized, client token authentication timeout |
| 403 | access  error |
| 404 |  method not found |

