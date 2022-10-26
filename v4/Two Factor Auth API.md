  | Change Version | API Version | Change nots | Change Date | Author |Architect Team Reviewer | 
  | - | - | - | - | - |- |
  | 1.0 | v1 |Two Factor Auth API | 2022-10-13 | Leon|  Allon|
  
  ## Summary
  
### Comm100.2fa Function
 - CreateSecret -[Create the Secret Key](#create-a-secret-key).
 - VerifyCode - [verify the 2FA code](#verify-the-2fa-code).
 
### Partner Login API
- POST /partnerloginapi/endlogin - [verify the 2FA code](#verify-the-2fa-code-of-partner-user).
  
### Partner Global API
- GET /partnerglobal/2faSecret - [Get a 2FA secret key](#Get-a-2fa-secret-key-of-partner-user).
- GET /partnerglobal/2faConfig - [Get a 2FA config](#Get-the-2fa-config-of-partner-user).
- POST /partnerglobal/2faConfig - [Create a 2FA config](#create-a-2fa-config-of-partner-user).
- UPDATE /partnerglobal/2faConfig - [Update the 2FA config](#Update-the-2fa-config-of-partner-user). 
- DELETE /partnerglobal/2faConfig - [Delete the 2FA config](#Delete-the-2fa-config-of-partner-user). 
 
- POST /partnerglobal/2faBackupCode - [Create a 2FA Backup Code](#create-a-backup-code-of-partner-user).
- GET /partnerglobal/2faBackupCode - [Get the 2FA Backup Code](#get-the-backup-code-of-partner-user). 
- PUT /partnerglobal/2faBackupCode - [Update the 2FA Backup Code](#update-the-backup-code-of-partner-user). 
<!-- - DELETE /partnerglobal/2faBackupCode - [Delete the 2FA Backup Code](#delete-the-backup-code-of-partner-user). -->
    
### Login API
- POST /loginapi/login - [Agent Login](#agent-login).
<!-- - POST /loginapi/agentConsoleLogin - [Agent Console Login](#agent-console-login). -->
- POST /loginapi/endlogin - [verify the 2FA code](#verify-the-2fa-code-of-agent).

  
### Global API
- GET /global/2faSecret - [Get a 2FA secret key](#Get-a-2fa-secret-key-of-agent).
- GET /global/2faConfig - [Get a 2FA config](#Get-the-2fa-config-of-agent).
- POST /global/2faConfig - [Create a 2FA config](#create-a-2fa-config-of-agent).
- UPDATE /global/2faConfig - [Update the 2FA config](#Update-the-2fa-config-of-agent). 
- DELETE /global/2faConfig - [Delete the 2FA config](#delete-the-2fa-config-of-agent). 

- POST /global/2faBackupCode - [Create a 2FA Backup Code](#create-a-backup-code-of-agent).
- GET /global/2faBackupCode - [Get the 2FA Backup Code](#get-the-backup-code-of-agent). 
- PUT /global/2faBackupCode - [Update the 2FA Backup Code](#update-the-backup-code-of-agent). 
<!-- - DELETE /partnerglobal/2faBackupCode - [Delete the 2FA Backup Code](#delete-the-backup-code-of-agent).     -->

## Endpoints

### Create A Secret Key

When a user wants to setup two-factor auth (or, more correctly, multi-factor auth) you need to create a secret. 
```C# 
 Secret CreateSecret(string CompanyName,string UserAccount)
 public class Secret{
     string QrcodeUrl;
     string SecretKey;
 }
``` 
#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `CompanyName` | string | yes |  Company Name show in 2fa app|  
  | `UserAccount` | string | yes |  User Account show in 2fa app|  
  
The Response body contains data with the following 

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`SecretKey` |string |Yes| 2FA secret key |
|`otpauthUrl` |string |Yes|  otpauth Url of 2FA  |

### Verify The 2fa Code
VerifyCode() will return either true (the code was valid) or false (the code was invalid; no points for you!). 

```C# 
 bool VerifyCode(string SecretKey,string Code)
``` 
#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `SecretKey` | string | yes |  2fa secret key|  
  | `Code` | string | yes |   2fa code|  
  
The Response body is either true (the code was valid) or false (the code was invalid; no points for you!).  

<!-- ### Create A Secret Key
`POST /2fa/secretkey`
#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
|`secretKey` |string |Yes| 2FA secret key |
|`otpauthUrl` |string |Yes|  otpauth Url of 2FA  |
|`code` |string |Yes| verify code of 2FA  |
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`secretKey` |string |Yes| 2FA secret key |
|`otpauthUrl` |string |Yes|  otpauth Url of 2FA  |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "qrcodeUrl": "",
   "secretKey":"",
}
```


### Verify the 2FA Code
`POST /2fa/code:verify`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `secretKey` | string | yes |  2FA secret key |  
  | `code` | string | yes |  2FA code|  

  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`result` |string |Yes| `success`,`fail` |

```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "result": "success",
}
```

### Create 2FA Backup Codes
`POST /2fa/codes`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 


  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code|

```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "code": "23sdw4d234"
}
``` -->


### Verify the 2FA Code of Partner User
`POST /partnerloginapi/endlogin`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `preLoginToken` | string | yes | 2fa jwt token containing partner user id |  
  |`secretKey` |string |no| 2FA secret key |
  | `code` | string | yes |  2FA code or backup code|  

  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`result` |string |Yes| `success`,`fail` |
|`jwtToken` | string | no |  jwt token for logining | 
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "result": "success",
   "jwtToken":"sdfasdf3452t4werrtewr"
}
```

### Agent Login 
`POST /loginapi/login`


  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`preLoginToken` |string |No| prelogin jwt token,need when nextStep is isNeed2faVerify |
|`secretKey` |string |No| 2FA secret key,need when nextStep is isNeed2faSetup|
|`otpauthUrl` |string |No|  otpauth Url of 2FA,need when nextStep is isNeed2faSetup  |
|`nextStep` |enum |Yes| `isNeed2faVerify`,`isNeed2faSetup`,`noNeed` |
|`errCode` |enum |Yes| |

```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "preLoginToken": "dfghjklgvdxhfdhdsgdsg",
   "nextStep": "isNeed2faVerify"
}
```

<!-- ### Agent Console Login 
`POST /loginapi/agentConsoleLogin`


  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`2faToken` |string |No| 2fa jwt token |
|`isNeedVerify2faCode` |bool |Yes| is need to verify the 2fa code |

```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "2faRoken": "dfghjklgvdxhfdhdsgdsg",
   "isNeedVerifyThe2faCode":true
}
``` -->

### Verify the 2FA Code of Agent
`POST /loginapi/endlogin`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `2faToken` | string | yes | 2fa jwt token containing agent id |  
  |`secretKey` |string |no| 2FA secret key,when setup secretkey |
  | `code` | string | yes |  2FA code or backup code|  
  | `isSetCookie` | bool | yes | set token to cookie |  

  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`error` |string |no| `Timeout`,`times out of limit`，`account locked` |
|`message` |string |no| |
| `jwtToken` | string | no |  jwt token for logining | 
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "jwtToken":"sdfasdf3452t4werrtewr"
}

HTTP/1.1 400 OK
{
   "error": "Timeout",
   "message":"",
}
```

### Get A 2fa Secret Key of Partner User
`GET /partnerglobalapi/2faSecret`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`secretKey` |string |Yes| 2FA secret key |
|`otpauthUrl` |string |Yes|  otpauth Url of 2FA  |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "otpauthUrl": "otpauth://totp/leon%40comm100.com?secret=DQ6EXYKLD4TTJ7DY&issuer=Comm100&period=30&algorithm=SHA1&digits=6",
   "secretKey":"DQ6EXYKLD4TTJ7DY",
}
```

### Get the 2fa config of Partner User
`GET /partnerglobalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` |string |Yes| 2FA config Id |

```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "id": "DQ6EXYKLD4TTJ7DY",
}
```

### Create A 2fa config of Partner User
`POST /partnerglobalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `token` | string | yes |  token containing partner user id |
  |`secretKey` |string |Yes| 2FA secret key |
  | `code` | string | yes |  2FA code or backup code| 
  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`result` |string |Yes| `success`,`fail` |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "result":"success",
}
```

### Update the 2fa config of Partner User
`PUT /partnerglobalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `token` | string | yes |  token containing partner user id |
  |`secretKey` |string |Yes| 2FA secret key |
  | `code` | string | yes |  2FA code or backup code| 
  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`errcode` |int |Yes| 0 for success |
  |`message` |string |Yes|    |
  
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "errcode": 0,
   "message":"success",
}
```

### Delete the 2fa config of Partner User
`Delete /partnerglobalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
```Json 
  HTTP/1.1 200 OK
```

### Create A Backup Code of Partner User
`POST /partnerglobalapi/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "code": "DQ6EXYKLD4TTJ7DY",
}
```

### Get the Backup Code of Partner User
`GET /partnerglobalapi/user/{id}/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  partner user id |
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "code": "DQ6EXYKLD4TTJ7DY",
}
```

### Update the Backup Code of Partner User
`UPDATE /partnerglobalapi/user/{id}/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  partner user id |
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "code": "DQ6EXYKLD4TTJ7DY",
}
```

<!-- ### Delete the Backup Code of Partner User
`DELETE /partnerglobalapi/user/{id}/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  partner user id |
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
``` -->

### Get A 2fa Secret Key of Agent
`GET /partnerglobalapi/2faSecret`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`secretKey` |string |Yes| 2FA secret key |
|`otpauthUrl` |string |Yes|  otpauth Url of 2FA  |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "otpauthUrl": "otpauth://totp/leon%40comm100.com?secret=DQ6EXYKLD4TTJ7DY&issuer=Comm100&period=30&algorithm=SHA1&digits=6",
   "secretKey":"DQ6EXYKLD4TTJ7DY",
}
```

### Get the 2fa config of Agent
`GET /partnerglobalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` |string |Yes| 2FA config Id |

```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "id": "DQ6EXYKLD4TTJ7DY",
}
```

### Create A 2fa config of Agent
`POST /partnerglobalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `token` | string | yes |  token containing agent id |
  |`type` |string |Yes| `login`,`profile` |
  |`secretKey` |string |Yes| 2FA secret key |
  | `code` | string | yes |  2FA code or backup code| 
  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`errcode` |int |Yes| 0 for success |
  |`message` |string |Yes|    |
  | `jwtToken` | string | no |  jwt token for logining | 
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "errcode": 0,
   "message":"success",
   "jwtToken":"asdfasdf345345wfwerwe"
}
```

### Update the 2fa config of Agent
`POST /partnerglobalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `token` | string | yes |  token containing agent id |
  |`secretKey` |string |Yes| 2FA secret key |
  | `code` | string | yes |  2FA code or backup code| 
  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`errcode` |int |Yes| 0 for success |
  |`message` |string |Yes|    |
  
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "errcode": 0,
   "message":"success",
}
```

### Delete the 2fa of agent
`Delete /partnerglobalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
```Json 
  HTTP/1.1 200 OK
```

### Create A Backup Code of Agent
`POST /partnerglobalapi/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "code": "DQ6EXYKLD4TTJ7DY",
}
```
### Get the Backup Code of Agent
`GET /partnerglobalapi/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "code": "DQ6EXYKLD4TTJ7DY",
}
```

### Update the Backup Code of Agent
`UPDATE /partnerglobalapi/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "code": "DQ6EXYKLD4TTJ7DY",
}
```

### Delete the Backup Code of Agent
`DELETE /partnerglobalapi/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
```
