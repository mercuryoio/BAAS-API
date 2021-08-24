**You can use Mercuryo API only with your partner token. Ask your Mercuryo manager to get it**

***

**In Mercuryo users can be registrated and verificated only with phone. US users need to verificate their e-mail too. Users can be authorised with phone and uuid. uuid - uniq user id. As a partner you will get it as a response for sign-in method and we recommend to save it to user account on your side.**

***

**Acceptance**

1. You need to add to your Terms and Policy agreement to share user data with Mercuryo.
2. You need to make an agreement with Mercuryo that Mercuryo will use the data for registration and will use it to third parties.
3. You need to ask users to accept the Mercurio term in your interface before signing user in.
4. If you create a new user you need to pass user acception to Mercuryo API. When the user is new for Mercuryo `acception` parameter is required.

***
***

**Cases**

1. [Sign up](login.md/#1-sign-up)
2. [Partner has phone sign up](login.md/#2-partner-has-phone-sign-up)
3. [User from US](login.md/#3-user-from-us)
4. [Log in by uuid](login.md/#4-log-in-by-uuid)
5. [Log in by phone](login.md/#5-log-in-by-phone)

***

#### 1. Sing up

**Case:**

User want to by crypto on your side. You do not have information about users phone. User have not got Mercuryo account. `acception` parameter is required.

**Steps:**

1. Ask user about phone
2. Use method [`POST /sdk-partner/sign-in`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKLogin) to pass user's phone to Mercuryo API

| Error  | Text | Description  | 
| ------------- | -------------  | -------------  |
| 403004 | `User not found.` | wrong uuid |
| 403005 | `invalid country by phone number` |  wrong countrycode |
| 403005 | `Country `%s` is not active or not exist.` | country is inactive |
| 403005 | `Country `%s` is in black list.` | country in black list |
| 403010 | `Phone is invalid` | phone is invalid |
| 403006 | `Accept cannot be blank for new users` | there is no `acception` parameter |


4. Get verification code from user
5. Use method [`POST /sdk-partner/phone-verify`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKPhone_verify) to give Mercuryo API user's phone and verification code


| Error  | Text | Description  | 
| ------------- | -------------  | -------------  |
| 403001 | `Verification failed.` | wrong key  |
| 403002 | `Verification failed.` |  wrong code |

6. User need to pass KYC. Use method [`GET /b2b/kyc-access-token`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-UserKycAccessToken) to get user's KYC token

| Error  | Text | Description  | 
| ------------- | -------------  | -------------  | 
| 403004 | `User not found.` | user not found |


7. You need to redirect user to Mercuryo side by link. 

Link example: `https://payments.mrcr.io/buy?init_token=123&scheme=dark`

Link must contains this parameters: 

| Parameter | Description  | 
| ------------- | -------------  | 
| 403004 | `User not found.` |

| Parameter  |  Description  | 
| ------------- | -------------  | 
| `access_token` | your access token | 
| `flow` | user's action: `buy`, `sell` etc |
| `scheme` | `dark` or `light`. This one is optional |
| `lang` | language. By default it is `en`. Supported languages: `en`, `zh`, `ru`, `fr`, `hi` , `id`, `ja`, `ko`, `pt`, `es`, `tr`, `vi`  | 
| `success_url` | redirect to your site with successful result |
| `failure_url` | redirect to your site with failed result |

8. Use [`GET /b2b/user/data`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-B2B-UserData) to get info about user's status

| Error  | Text | Description  | 
| ------------- | -------------  | -------------  |
| 500001 | `try later` | smth going wrong |


What to do if user still inactive:
1. Check if all parameters are filled
2. Ask user's e-mail. US users need to verify their e-mail
3. User need to pass KYC successful. 
4. If user status is `temporary-blocked` user will be able to use Mercuryo in 15 min.
5. If user sill has problem -- ask Mercuryo support

![img](https://github.com/mercuryoio/Commercial-API/blob/master/Sing%20up.png)

***

#### 2. Partner has phone sign-up

**Case:**

User want to by crypto on your side. You have information about users phone. User have not got Mercuryo account. `acception` parameter is required.

**Steps:**

If you have users phone there are some differences with previous case:

1. You do not need to ask user about his phone. Just transfer `phone` parameter to Mercuryo API
2. If users phone is already verificated on your side - skip phone verification

All other steps are same with previous case

***

#### 3. User from US

**Case:**

User want to by crypto on your side. User have not got Mercuryo account. User from US

**Steps:**

US users need to verificate their e-mail too

1. Use  method [`POST /b2b/user/set-email`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKLogin) to send user e-mail to Mercuryo API

| Error  | Text | Description  | 
| ------------- | -------------  | -------------  |
| 403006 | `Email cannot be blank.` |  wrong e-mail |
| 403006 | `Email is not a valid email address.` | invalid e-mail |
| 403006 | `Email "ff@dd.dd" has already been taken.` | e-mail is already taken |

3. Use method [`POST /b2b/user/email-verify`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKLogin) to give Mercuryo API user's phone and verification code

| Error  | Text | Description  | 
| ------------- | -------------  | -------------  |
| 403007 | `Token somehow contains invalid data.` | token data is invalid |
| 401008 | `Verification failed.` | invalid token |
| 401009 | `Verification failed.` | code is invalid |

4. Mercuryo API response with user status

![img]( https://github.com/mercuryoio/Commercial-API/blob/master/User%20from%20US.png)

***

#### 4. Log in by uuid

**Case:**

User want to by crypto on your side. User have Mercuryo account. Login by uuid. `acception` parameter isn't required becouse uuid have only already registrated users

**Steps:**

1. Use  method [`POST /sdk-partner/sign-in`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKLogin) to initiate login by uuid

| Error  | Text | Description  | 
| ------------- | -------------  | -------------  |
| 403004 | `User not found.` | wrong uuid |
| 400305 | `invalid country by phone number` |  wrong countrycode |
| 403005 | `Country `%s` is not active or not exist.` | country is inactive |
| 403005 | `Country `%s` is in black list.` | country in black list |
| 403005 | `Phone is invalid` | phone is invalid |
| 403005 | `Invalid uuid4` | wrong uuid format |

2. If as a responce you get user's token - you do not need to verify user's phone. If as a response you get `code length` you need to verify user's phone by method [`POST /sdk-partner/phone-verify`](https://u3-1-api.mrcr.io/v1.6/comm-docs/index.html#api-SDK-SDKPhone_verify) to give Mercuryo API user's phone and verefication code

3. Then Mercuryo API will send users status to you

![img](https://github.com/mercuryoio/Commercial-API/blob/master/Log%20In.png)


***

#### 5. Log in by phone

**Case:**

User want to by crypto on your side. User have Mercuryo account. Login by phone. If you are not shure is user already registrated or not - pass `acception` parameter to Mercuryo API

**Steps:**

Flow is the same with log in by uuid but with little diffenrences:

1. Use method `POST /sdk-partner/sign-in`
2. User do not need to verificate his phone

