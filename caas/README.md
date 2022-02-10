## CAAS

Crypto as a Service (CaaS) is an API based, fully white labelled solution.
CaaS will allow any bank, fintech and financial service provider to offer crypto services.

****

## Methods

1. [Login](/caas/README.md/#1-login)

   1.1. [Login](/caas/README.md/#11-login)
 
   1.2. [KYC](/caas/README.md/#12-kyc)

   1.3. [Countries](/caas/README.md/#13-countries)
2. [Transaction status](/caas/README.md/#2-transaction-status)

   2.1 [Transactions](/caas/README.md/#21-еransactions)

   2.2 [Transactions by merchant trx ide](/caas/README.md/#22-transactions-by-merchant-trx-id)

3. [User data](/caas/README.md/#3-user-data)
4. [Limits](/caas/README.md/#4-limits)
5. [Rates](/caas/README.md/#5-rates)

   5.1 [Buy rate](/caas/README.md/#71-buy-rate)

   5.2 [Sell rate](/caas/README.md/#72-sell-rate)

6. [Withdraw](/caas/README.md/#6-withdraw)

   6.1 [Estimate fee](/caas/README.md/#61-estimate-fee)

   6.2 [Withdraw](/caas/README.md/#62-withdraw)

   6.3 [Verify email](/caas/README.md/#63-verify-email)

7. [Buy](/caas/README.md/#7-buy)

   8.1 [Buy rates](/caas/README.md/#71-buy-rates)

   8.2 [Buy](/caas/README.md/#72-buy)

8. [Sell](/caas/README.md/#8-sell)

   8.1 [Sell rates](/caas/README.md/#81-sell-rates)

   8.2 [Sell](/caas/README.md/#82-sell)

***

### 1 Login

#### 1.1 Login

This method is to sign in Customer

Request:
`POST /sdk-partner/sign-in `

| Parameter | Description  | 
| ------------- | -------------  |
| `sdk-partner/sign-in` |	Authorization sdk partner token. |
| `phone` | SDK user's phone (for creating new user or login) |
| `accept` | required if get phone |
| `user_uuid4` | SDK user_uuid4 (for login) |

#### 1.2 KYC

This method is to get KYC access token for Customer

Request:
`GET /b2b/user/kyc-access-token`

#### 1.3 Countries

This method is to get list of available countries

Request:
`GET /lib/countries `

***

### 2 Transaction status

#### 2.1 Transactions

This method is to get list of transactions

Request:
`GET /b2b/transactions`


| Parameter | Description  | 
| ------------- | -------------  |
| `merchant_transaction_id` | Merchant transaction id. Default value: null |
| `date_start` | Unix Timestamp search from. Default value: null|
| `date_end` | Unix Timestamp search end. Default value: null |
| `status` | Transaction status. Default value: null |
| `limit` | Limit of rows max 50, min 5. Default value: 50 |
| `offset` | Type of client. Default value: 0|

#### 2.2 Transactions by merchant trx id

This method is to sort transactions by merchant transaction id

Request:
`GET /b2b/:merchant_trx_id/status`

***

### 3 User data

This method is to get Customers data

Request:
`GET /b2b/user/data`

***

### 4 Limits

#### 4.1 User limit

This method is to get fiat and crypto currency limits for current user & partner

Request:
`POST /b2b/user/limit`

| Parameter | Description  | 
| ------------- | -------------  |
| currency | crypto currency |

***

### 5 Rates

This methods are to get rates for 1 crypto token with Partners fee

#### 5.1 Buy rate

Request:
`GET /b2b/all/buy/rate`


| Parameter | Description  | 
| ------------- | -------------  |
| currency | fiat currency |


#### 5.2 Sell rate

Request:
`GET /b2b/all/sell/rate`


| Parameter | Description  | 
| ------------- | -------------  |
| currency | fiat currency |

***

### 6 Withdraw

#### 6.1 Estimate fee

This method is to get estimate fee for withdraw operation.

Request:
`GET /withdraw/estimate-fee`


| Parameter | Description  | 
| ------------- | -------------  |
| `currency` | crypto currency. Allowed values: `BTC`, `ETH`, `BAT`, `USDT` |


#### 6.2 Withdraw

This method is to create withdraw operation

Request:
`GET /withdraw`

| Parameter | Description  | 
| ------------- | -------------  |
| `currency` | crypto currency |
| `address` | withdraw address |
| `amount` | amount withou fee |
| `estimate_id` | estimate id |
| `client` | client. Allowed values: `web`,`ios`,`android`,`widget`|


#### 6.3 Verify email

This method is to verify transaction by email.

Request:
`POST /withdraw/verify-email`

***

### 7 Buy

#### 7.1 Buy rate

This method is to get buy rates and trx_token.

Request:
`GET /b2b/cs/buy/rate`

| Parameter | Description  | 
| ------------- | -------------  |
| `from` | currency to convert from. Allowed values: `EUR`, `USD`, `RUB`, `BTC`, `ETH`, `BAT`, `USDT`, `ALG`|
| `to`  | currency to convert to. Allowed values: `EUR`, `USD`, `RUB`, `BTC`, `ETH`, `BAT`, `USDT`, `ALG` |
| `amount` | amount to be converted |
| `is_total` | Is passed amount with fee |

#### 7.2 Buy

This method is to create buy operation

Request:
`POST /b2b/cs/buy`


| Parameter | Description  | 
| ------------- | -------------  |
| `trx_token` | buy token returned by <code>/b2b/cs/buy/rate |
| `merchant_trx_id` | custom ID for check transaction status. If empty, it will be generated |
    
***

### 8 Sell

#### 8.1 Sell rate

This method is to get sell rates and trx_token.

Request:
`GET /b2b/cs/sell/rate`

| Parameter | Description  | 
| ------------- | -------------  |
| `from` | currency to convert from. Allowed values: `EUR`, `USD`, `RUB`, `BTC`, `ETH`, `BAT`, `USDT`, `ALG`|
| `to`  | currency to convert to. Allowed values: `EUR`, `USD`, `RUB`, `BTC`, `ETH`, `BAT`, `USDT`, `ALG` |
| `amount` | amount to be converted |
| `is_total` | Is passed amount with fee |

#### 8.2 Sell 

This method is to create sell operation

Request:
`POST /b2b/cs/sell`


| Parameter | Description  | 
| ------------- | -------------  |
| `trx_token` | buy token returned by <code>/b2b/cs/buy/rate |
| `merchant_trx_id` | custom ID for check transaction status. If empty, it will be generated |
    
****

## Schemas

### Withdraw
    
![imgcaas3](https://github.com/mercuryoio/Commercial-API/blob/master/caas/img/b2b-cs-send-external.svg)   
    
### Buy 
    
![imgcaas1](https://github.com/mercuryoio/Commercial-API/blob/master/caas/img/b2b-cs-buy-external.svg)
    
### Sell 
    
![imgcaas2](https://github.com/mercuryoio/Commercial-API/blob/master/caas/img/b2b-cs-sell-external.svg)

