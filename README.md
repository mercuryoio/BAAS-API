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

[Sign up/Log in](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md)


***


## Creating new IBAN for user

*Link Comming soon*

***

## Popular scenarios for using API:

1. [Buy crypto with card](https://github.com/mercuryoio/Commercial-API/blob/master/Buy/README.md)
2. Buy crypto with bank transfer (Comming soon)
3. Buy crypto using user's IBAN (Comming soon)
4. Top Up user's IBAN (Comming soon)
5. [Sell crypto and withdraw fiat to card](https://github.com/mercuryoio/Commercial-API/blob/master/Sell/README.md)
6. Sell crypto and withdraw to random IBAN (Comming soon)
7. Sell crypto and withdraw to User's IBAN (Comming soon)
8. Withdraw from User's IBAN to random IBAN (Comming soon)
