# Commercial-API

Mercuryo API is a set of crypto and fiat balances that allows users to quickly and easily exchange crypto to fiat and fiat to crypto, and top up and withdraw funds from fiat balance too.

If you have a crypto wallet or other crypto service, your users can create Mercuryo wallet and see an additional fiat balance in the interface. They can use Mercuryo wallet as simple as other that already exist in your service.

The Mercuryo API is structured around a your and user's wallets. Users create wallets and perform operations with them, and you monitors the transactions of these users and manages your own savings earned from each user transaction.

***

## Methods

You can find reference documentation with methods description [here](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html)

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

## Creating new IBAN for user

*Link Comming soon*

***

## Popular scenarios for using API:

1. [Buy crypto with card](https://github.com/mercuryoio/Commercial-API/tree/master/1%20Buy%20Card)
2. Buy crypto with bank transfer (Comming soon)
3. Buy crypto using user's IBAN (Comming soon)
4. Top Up user's IBAN (Comming soon)
5. [Sell crypto and withdraw fiat to card](https://github.com/mercuryoio/Commercial-API/blob/master/Sell/README.md)
6. Sell crypto and withdraw to random IBAN (Comming soon)
7. Sell crypto and withdraw to User's IBAN (Comming soon)
8. Withdraw from User's IBAN to random IBAN (Comming soon)

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

