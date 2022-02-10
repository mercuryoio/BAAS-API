## CAAS

Crypto as a Service (CaaS) is an API based, fully white labelled solution.
CaaS will allow any bank, fintech and financial service provider to offer crypto services.

## Methods

### 1 Sign-in

#### 1.1 Sign-in

To sign in Customer

Request:
`POST /sdk-partner/sign-in `

| Parameter | Description  | 
| ------------- | -------------  |
| `sdk-partner/sign-in` |	Authorization sdk partner token. |
| `phone` | SDK user's phone (for creating new user or login) |
| `accept` | required if get phone |
| `user_uuid4` | SDK user_uuid4 (for login) |

#### 1.2 KYC

To get KYC access token for Customer

Request:
`GET /b2b/user/kyc-access-token`

Response example:

`HTTP/1.1 200 OK
{
    "status": 200
    "data": {
        "id": 4,
        "token": "_act-ca4dae41-0ecd-468d-86e2-02d5ca697b8d"
        "applicant_id": "_act-ca4dae41-0ecd-468d-86e2-02d5ca697b8d"
    }
}`



#### 1.3 Countries

to get list of available countries

Request:
`GET /lib/countries `

### 2 Transactions

#### 2.1 Transactions

To get list of transactions

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

##### 2.2 Transactions by merchant trx id

To sort transactions by merchant transaction id

Request:
`GET /b2b/:merchant_trx_id/status`


| Parameter | Description  | 
| ------------- | -------------  |
| `merchant_trx_id` | merchant transaction id you want sort by |


### 3 User data

Request:
`GET /b2b/user/data`

Example:
`GET /b2b/user/data `


| Parameter | Description  | 
| ------------- | -------------  |
|  |  |

Response example:
`{
    "status": 200,
    "data": {
        "first_name": "John",
        "last_name": "Smith",
        "country_code": "ru",
        "language_code": "ru-RU",
        "kyc1_status": "complete",
        "kyc2_status": "complete",
        "email_status": "confirmed",
        "user_status": "active"
        }
    }
}`

### 4 Limits

#### 4.1 User limit

Fiat and crypto currency limits for current user & partner

Request:
`POST /b2b/user/limit`

| Parameter | Description  | 
| ------------- | -------------  |
| currency | crypto currency |

### 5 Rates

#### 5.1 Buy rate

Request:
`GET /b2b/all/buy/rate`


| Parameter | Description  | 
| ------------- | -------------  |
| currency | fiat currency |

Response example:

`{

"data": 

       "ETH":"0.277700638",
       
       "BTC": "0.277700638",
       
...}`

#### 5.2 Sell rate

Request:
`GET /b2b/all/sell/rate`


| Parameter | Description  | 
| ------------- | -------------  |
| currency | fiat currency |

Response example:

`{

"data": 

       "ETH":"0.277700638",
       
       "BTC": "0.277700638",
       
...}`

### 6 Withdraw

#### 6.1 Estimate fee

Estimate fee for withdraw operation.

Request:
`GET /withdraw/estimate-fee`


| Parameter | Description  | 
| ------------- | -------------  |
| `currency` | crypto currency. Allowed values: `BTC`, `ETH`, `BAT`, `USDT` |

Response example:

#### 6.2 Withdraw

To create withdraw operation

Request:
`GET /withdraw`

| Parameter | Description  | 
| ------------- | -------------  |
| `currency` | crypto currency |
| `address` | withdraw address |
| `amount` | amount withou fee |
| `estimate_id` | estimate id |
| `client` | client. Allowed values: `web`,`ios`,`android`,`widget`|

Response example:

#### 6.3 Verify email

Thi method is to verify transaction by email.

Request:
`POST /withdraw/verify-email`


### 7 Buy

#### 7.1 Buy rate

To get buy rates and trx_token.

Request:
`GET /b2b/cs/buy/rate`

| Parameter | Description  | 
| ------------- | -------------  |
| `from` | currency to convert from. Allowed values: `EUR`, `USD`, `RUB`, `BTC`, `ETH`, `BAT`, `USDT`, `ALG`|
| `to`  | currency to convert to. Allowed values: `EUR`, `USD`, `RUB`, `BTC`, `ETH`, `BAT`, `USDT`, `ALG` |
| `amount` | amount to be converted |
| `is_total` | Is passed amount with fee |

#### 7.2 Buy

To create buy operation

Request:
`POST /b2b/cs/buy`


| Parameter | Description  | 
| ------------- | -------------  |
| `trx_token` | buy token returned by <code>/b2b/cs/buy/rate |
| `merchant_trx_id` | custom ID for check transaction status. If empty, it will be generated |

### 8 Sell

#### 8.1 Sell rate

To get sell rates and trx_token.

Request:
`GET /b2b/cs/sell/rate`

| Parameter | Description  | 
| ------------- | -------------  |
| `from` | currency to convert from. Allowed values: `EUR`, `USD`, `RUB`, `BTC`, `ETH`, `BAT`, `USDT`, `ALG`|
| `to`  | currency to convert to. Allowed values: `EUR`, `USD`, `RUB`, `BTC`, `ETH`, `BAT`, `USDT`, `ALG` |
| `amount` | amount to be converted |
| `is_total` | Is passed amount with fee |

#### 8.2 Sell 

To create sell operation

Request:
`POST /b2b/cs/sell`


| Parameter | Description  | 
| ------------- | -------------  |
| `trx_token` | buy token returned by <code>/b2b/cs/buy/rate |
| `merchant_trx_id` | custom ID for check transaction status. If empty, it will be generated |

## Schemas

### Buy 
    
![imgcaas1](https://github.com/mercuryoio/Commercial-API/blob/master/caas/img/b2b-cs-buy-external.svg)
    
### Sell 
    
![imgcaas2](https://github.com/mercuryoio/Commercial-API/blob/master/caas/img/b2b-cs-sell-external.svg)
    
### Withdraw
    
![imgcaas3](https://github.com/mercuryoio/Commercial-API/blob/master/caas/img/b2b-cs-send-external.svg)
