#### 1. Sandbox

You should provide all your test personal/server IPs for whitelist to use Mercuryo’s sandbox. Contact your Mercuryo manager for it.

Test Adresses:

[`https://sandbox-partners.mrcr.io`](https://sandbox-partners.mrcr.io)

Ask Mercyruo manager to create login + pass. Tell him an email that you want to use as login. You can change password in settigs whenever you want.

***

#### 2. Phones

You may use your personal phone numbers to create test users. Or you can use virtual numbers to get an SMS.

***

#### 3. Card

Sandbox do not charge money from real cards. So you can use your own cards for transaction tests.

***

#### 4. SumSub

User need to pass KYS on the SumSub side. Ask your Mercuryo manager to help with this. 

This parameter is reqaried: `applicant_id`

You will get it in responthe from method `/b2b/user/kyc-access-token`

***

#### 5. Tokens

1. For authorization methods you need your `sdk-partner-token`. Ask your Mercuryo manager to get it.
2. All the methods in b2b domain have to be signed up with `b2b-bearer-token`. You can get it in authorization flow.

Table of the eternal tokens

| Parameter  | Value |
| ------------- | -------------  |
| `user_uuid4` | `913ac291-6fd8-4bcc-bfca-a5c7e38183a1` |
| `B2B-Bearer-Token` | `eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJtcmNyLmlvIiwiaWF0IjoxNjMxMTk1NDM5LCJqdGkiOiJZaXI3Q1d0RWswSk9nU0UraTlLXC9ZamFydGx2ZmFMZFdnTUpSOVpPWTFQdz0iLCJuYmYiOjE2MzExOTU0NDQsImRhdGEiOnsidXNlcl9pZCI6MzE3NSwiYWRkaXRpb25hbCI6eyJ3aWRnZXRfaWQiOiI0MzczOWQ2Yi02MzIzLTQ0OGEtYWM5Ny01MTVmNWI0MTk1YzMiLCJleGNoYW5nZV9wYXJ0bmVyX2lkIjo3MSwic2RrX3BhcnRuZXJfaWQiOjR9fX0.x5R7p7XqS2eLTsZWUgQWUU-avZTx9e_Lazi3M3v1lWA` |
| `buy_token` | `af1caddbe113bf227614b45f41bccb484361f679212e1048e96e97689600fbb2eyJ0IjoiMTYzMTE5NTQ3NiIsInR0Ijp0cnVlLCJjIjoiVVNEVCIsImEiOiI1Ni4xMTgwNjIiLCJmYyI6IlJVQiIsImZhIjoiNjAwMC4wMCIsImYiOiIxNjQ4LjA1IiwidGYiOiIwIiwic2YiOiIxNjQ4LjA1MDAwMDAwIiwiciI6Ijc3LjU0IiwiY2lkIjoiZGZlOThhMmM4ZjJmMTU0MzdjMDNmMjAyZGQ5NzdkM2UiLCJ3IjoiNDM3MzlkNmItNjMyMy00NDhhLWFjOTctNTE1ZjViNDE5NWMzIiwib3AiOiJidXkiLCJwYSI6ImNhcmQifQ==` |
| `init_token` | `06f48c2bb04e40597` |
