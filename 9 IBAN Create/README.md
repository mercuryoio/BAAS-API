***

1. [Steps](README.md/#1-steps)
2. [Scheme](README.md/#2-scheme)

***

<a name="steps"></a>
#### 1. Steps

1. The Customer wants to create IBAN.
2. You will need to authorize customer and check if he can use Mercuryo API. Please check [this](https://github.com/mercuryoio/Commercial-API/blob/master/Login/README.md) for more information.
3. Use method [`GET /b2b/user/data`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_User-UserData) to get customer's status.
4. If the Customer has passed only KYC1 then he need to pass KYC2
5. Use method [`Get get/kyc-access-token2`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-User-UserData) to get KYC access token for KYC2. KYC2 statuses are the same with KYC statuses.
6. You need to redirect user to Mercuryo side by link.

Link example: `https://payments.mrcr.io/kyc?flow=ID%2BSelfie&access_token=your_token8&scheme=your_scheme&lang=lang_code`

Link must contains this parameters:

| Parameter  |  Description  | Type |
| ------------- | -------------  | -------------  |
| `access_token` | your access token, you get it from method `GET /b2b/kyc-access-token` | obligatory |
| `flow` |  `ID+Selfie`  | optional |
| `scheme` | `dark` or `light` | optional |
| `lang` | language. By default it is `en`. Supported languages: `en`, `zh`, `ru`, `fr`, `hi` , `id`, `ja`, `ko`, `pt`, `es`, `tr`, `vi`  | optional |
7. Then again use method [`GET b2b/user/data`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_User-UserData) to get customer's status. 
8. If KYC2 is passed use method [`GET /b2b/createIban`](https://sandbox-cryptosaas.mrcr.io/v1.6/comm-docs/index.html#api-B2B_User-IbanCreate) to create IBAN.
9. You need to realize a form on your side and show to the Customer his IBAN. 

***

#### 2. Scheme

![buy_iban](https://github.com/mercuryoio/Commercial-API/blob/master/9%20IBAN%20Create/IBAN%20create.png)
