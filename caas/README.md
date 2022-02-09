Caas is option

### Methods

## Sign-in

Request:
`POST /sdk-partner/sign-in `

| Parameter | Description  | 
| ------------- | -------------  |
| `sdk-partner/sign-in` |	Authorization sdk partner token. |
| `phone` | SDK user's phone (for creating new user or login) |
| `accept` | required if get phone |
| `user_uuid4` | SDK user_uuid4 (for login) |

Response example:

`{
    "status": 200,
    "data": {
        "key": "74f490e26e20da1b713e41492b4343e952a4bd3d8faa301ff8ad6bce531522fcbG9naW4tdmVyaWZ5LXBob25lOONDI5-FSHL2EkGUkwF9C4pyv-16oxrh",
        "code_length": 4,
        "timeout": 20,
        "phone": "+7********96"
    }
}`

## KYC

Request:
`GET /b2b/user/kyc-access-token`

| Parameter | Description  | 
| ------------- | -------------  |
|  |  |

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

## Set e-mail

Request:
`GET /b2b/user/set-email`

| Parameter | Description  | 
| ------------- | -------------  |
| `email` | Email need to set |

Response example:

`{
    "status": 200
    "data": {
        "key": "fa50f86f1af9459fc53075ae85fd5661b009f5433a624023d401b9094cc9adb9Y2hhbmdlLWVtYWlsLXZlcmlmeS1waG9uZQ==Zfgd-Mu6xRix2YA-0YTLXFEXL4c9XZqF",
        "code_length": 4,
        "timeout": 20,
        "email": "d*****@list.ru"
    }
}`

## Verify e-mail

Request:
`GET /b2b/user/email-verify`

| Parameter | Description  | 
| ------------- | -------------  |
| `key` | Key from /b2b/user-email-verify |
| `code` | Code from email |

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
}`

## Verify phone

Request:
`GET /sdk-partner/phone-verify`


| Parameter | Description  | 
| ------------- | -------------  |
| `key` | From sdk-partner/sign-in |
| `code` | Code that sent on mobile |

Response example:

`{
   "status": 200,
   "data": {
       "user_uuid4": "3272133a-a683-4e80-8116-f219b1cf97c6",
       "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJtcmNyLmlvIiwiaWF0IjoxNjMyMTQ0NTQxLCJqdGkiOiJtY0pnaW1QMFwvNzJLOG9qR0lWd0xyZHZEclEyb1R6MTNIUWNjNTZkVzRtYz0iLCJuYmYiOjE2MzIxNDQ1NDYsImRhdGEiOnsidXNlcl9pZCI6MzE3MiwiYWRkaXRpb25hbCI6eyJ3aWRnZXRfaWQiOiI0MzczOWQ2Yi02MzIzLTQ0OGEtYWM5Ny01MTVmNWI0MTk1YzMiLCJleGNoYW5nZV9wYXJ0bmVyX2lkIjo3MSwic2RrX3BhcnRuZXJfaWQiOjV9fX0.BjchFtGtricBwcMnWwhfNeezyjHlapkWi8ePM2zfYXo",
       "timeout": 86400
   }
}
`
## Countries

Request:
`GET /lib/countries `

Response example:

`{
    "status": 200,
    "data": [
        {
            "code": "au",
            "title": "Australia",
            "code3": "aus",
            "phone_prefix": "7",
            "phone_mask": "999 999 9999"
        }
    ]
}`

## Transactions

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

Response example:
`{
     "status": 200,
     "total": 4,
     "next": null,
     "prev": null,
     "data": [
        {
             "id": "0737d94bac6808650",
             "transaction_id": "0737d956e71926059",
             "currency": "ETH",
             "status": "succeeded",
             "amount": "0.19",
             "created_at": "2021-10-30 15:03:39",
             "updated_at": "2021-10-30 15:04:01",
             "fiat_currency": "RUB",
             "fiat_amount": "67919.60",
             "vendor_id": "0737d9612a6823904",
             "url": "https://www.blockchair.com/ethereum/transaction/0737d9612a6823904?from=mercuryo",
             "type": "sell",
             "merchant_transaction_id": "0737a2abf2a6c3660"
        },
...`

## User data

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

##

Request:
`GET `

Example:
`GET `


| Parameter | Description  | 
| ------------- | -------------  |
|  |  |

Response example:

##

Request:
`GET `

Example:
`GET `


| Parameter | Description  | 
| ------------- | -------------  |
|  |  |

Response example:


### Shema

[imgcaas]()
