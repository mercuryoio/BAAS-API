***

1. [Steps](README.md/#1-steps)
2. [Scheme](README.md/#2-scheme)

***

<a name="steps"></a>
#### 1. Steps

1. The Customer wants to withdraw from his IBAN.
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /b2b/user/iban-get`]() to get customer's IBAN.
4. Use method [`GET /b2b/user/iban-balance`]() to get customer's balance on his IBAN.
5. Show it to the Customer. You need to realize a form on your side in which the Customer can choose his IBAN and how much he want to withdraw.
6. Use method [`GET /b2b/user/iban-withdraw`]() to start withdrawal operation.
7. Show a operation's status to the Customer

***

#### 2. Scheme

![buy_withdraw](https://github.com/mercuryoio/Commercial-API/blob/master/8%20fiat%20withdraw/IBAN%20withdraw.png)
