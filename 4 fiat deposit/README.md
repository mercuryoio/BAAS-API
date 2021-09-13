***

1. [Steps](README.md#1-steps)
2. [Scheme](README.md#2-scheme)

***

#### 1. Steps
The Customer wants to do fiat deposite on his IBAN. For this case you need to show the Customer his IBAN
1. You will need to authorize the Customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
2. Use method [`GET /b2b/user/iban-get`]() to get user IBAN.
3. Then show it to the Customer. The Customer will do deposite on his own side. If KYC2 is expired then Mercuryo cannot complite the deposite operation. In this case the Customer needs to pass KYC2 again.

***

#### 2. Scheme

![deposite_iban](https://github.com/mercuryoio/Commercial-API/blob/master/4%20fiat%20deposit/deposit%20IBAN.png)
