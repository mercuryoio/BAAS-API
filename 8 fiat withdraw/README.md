***

1. [Steps](README.md/#1-steps)
2. [Scheme](README.md/#2-scheme)

***

<a name="steps"></a>
#### 1. Steps

1. The Customer wants to withdraw from his IBAN.
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /b2b/user/iban`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_User-IbanGet) to get customer's IBAN. Parameter fiat_balance contains IBAN's balance data
4. Show it to the Customer. You need to realize a form on your side in which the Customer can choose his IBAN and how much he want to withdraw.
5. Use method [`GET /b2b/fiat/withdraw`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_User-IbanWithdraw) to start withdrawal operation.
6. Show a operation's status to the Customer

***

#### 2. Scheme

![buy_withdraw](https://github.com/mercuryoio/Commercial-API/blob/master/8%20fiat%20withdraw/IBAN%20withdraw.png)
