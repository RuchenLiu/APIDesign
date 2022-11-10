  | Change Version | API Version | Change nots | Change Date | Author |Architect Team Reviewer | 
  | - | - | - | - | - |- |
  | 1.0 | v1 |Two Factor Auth API | 2022-10-13 | Leon|  Allon|
  
  ## Summary
  
### Comm100.2fa Function
 - CreateSecret -[Create the Secret Key](#create-a-secret-key).
 - VerifyCode - [verify the 2FA code](#verify-the-2fa-code).
 
 
### Login API
- POST /global/jwtToken/login - [Agent Login](#agent-login).
<!-- - POST /loginapi/agentConsoleLogin - [Agent Console Login](#agent-console-login). -->
- POST /global/endlogin - [verify the 2FA code](#verify-the-2fa-code-of-agent).

  
### Global API
- GET /global/2faSecret - [Get a 2FA secret key](#Get-a-2fa-secret-key).

#### Agent2faConfig API
  
- GET /global/agent2faConfigs/{agentId} - [Get a Agent 2FA config](#Get-the-agent-2fa-config).
- GET /global/agent2faConfigs - [Get the list of Agent 2FA configs](#Get-the-list-of-agent-2fa-configs).
- POST /global/agent2faConfigs - [Create a Agent 2FA config](#create-a-2fa-agent-config).
- UPDATE /global/agent2faConfigs/{agentId} - [Update the Agent 2FA config](#Update-the-agent-2fa-config). 
<!-- - DELETE /global/agent2faConfigs/{agentId} - [Delete the 2FA config](#delete-the-2fa-config-of-agent).  -->

#### Agent2faBackupCode API
  
- POST /global/agent2faBackupCodes:generate - [Generate a Agent 2FA Backup Code](#Generate-a-agent-2fa-backup-code).
<!-- - GET /global/agent2faBackupCodes/{agentId} - [Get the Agent 2FA Backup Code](#get-the-backup-code-of-agent). 
- PUT /global/agent2faBackupCodes - [Update the Agent 2FA Backup Code](#update-the-backup-code-of-agent).  -->

#### SiteAuthenticationConfig API
  
- POST /global/siteAuthenticationConfigs - [Create a site authentication config](#create-a-site-authentication-config).
- GET /global/siteAuthenticationConfigs/{agentId} - [Get the site authentication config](#get-the-site-authentication-config). 
- PUT /global/siteAuthenticationConfigs - [Update the site authentication config](#update-the-site-authentication-config). 


### Partner Global API

#### Superagent2faConfig API
  
- GET /partnerglobal/superagent2faConfigs/{agentId} - [Get the Super Agent 2FA config](#Get-the-super-agent-2fa-config).
- GET /partnerglobal/superagent2faConfigs - [Get the list of Super Agent 2FA configs](#Get-the-list-of-super-agent-2fa-configs).
- POST /partnerglobal/superagent2faConfigs - [Create a Super Agent 2FA config](#create-a-super-agent-2fa-config).
- UPDATE /partnerglobal/superagent2faConfigs/{agentId} - [Update the Super Agent 2FA config](#Update-the-super-agent-2fa-config). 

#### Superagent2faBackupCode API
  
- POST /partnerglobal/superagent2fabackupcodes:generate - [Generate a Super agent 2FA Backup Code](#generate-a-super-agent-2fa-backup-code)
<!-- - DELETE /partnerglobal/2faBackupCode - [Delete the 2FA Backup Code](#delete-the-backup-code-of-agent).     -->
<!-- 
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
- PUT /partnerglobal/2faBackupCode - [Update the 2FA Backup Code](#update-the-backup-code-of-partner-user).  -->
<!-- - DELETE /partnerglobal/2faBackupCode - [Delete the 2FA Backup Code](#delete-the-backup-code-of-partner-user). -->
    


## Endpoints

### Create A Secret Key

When a user wants to setup two-factor auth (or, more correctly, multi-factor auth) you need to create a secret. 
```C# 
 Secret CreateSecret(string CompanyName,string UserAccount)
 public class Secret{
     string OtpauthUrl;
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
|`OtpauthUrl` |string |Yes|  otpauth Url of 2FA  |

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


<!-- ### Verify the 2FA Code of Partner User
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
``` -->

### Agent Login 
`POST /global/jwtToken/login`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `partnerId` | int | yes |  |     
  | `siteId` | int | no |  |  
  | `email` |string |yes|  |
  | `password` | string | yes | |  
  | `verificationCode` | string | no | |  
  | `isMobile` | bool | no |  |  
  | `ip` | string | no |  | 
  | `isAutoLoginForRegistration` | bool | no |  | 
  | `Verifiedtoken` | string | no |Verified token containing `2fa verified time`|
  

  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`preLoginToken` |string |No| prelogin jwt token containing agent id,login time.need when nextStep is isNeed2faVerify |
|`secretKey` |string |No| 2FA secret key,need when nextStep is isNeed2faSetup|
|`otpauthUrl` |string |No|  otpauth Url of 2FA,need when nextStep is isNeed2faSetup  |
|`nextStep` |enum |Yes| `isNeed2faVerify`,`isNeed2faSetup`,`noNeed` |
|`isShowSkip2fa` |bool |Yes| if `true` show option skip 2fa |
|`errorCode` |enum |Yes| |
|`errorMessage` |string |No| |
|`url` |string |No| |
|`siteId` |int |Yes| |
|`agentId` |guid |Yes| |
|`email` |string |Yes| |
|`jwtToken` |string |Yes| |
|`expireTime` |datetime |No| |
|`showVerificationCode` |bool |Yes| |
|`verificationCode` |string |Yes| |
|`hasMutipleSite` |bool |Yes| |
|`siteIds` |int[] |Yes| |
|`isFirstLogin` |bool |Yes| |
|`superAgentId` |guid |Yes| |
|`days` |int |Yes| |
|`trialInfo` |object |Yes| |

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
`POST /global/endlogin`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `preLoginToken` | string | yes | 2fa jwt token containing agent id,login time |  
  |`secretKey` |string |no| 2FA secret key,when setup secretkey |
  | `code` | string | yes |  2FA code or backup code|  
  | `isSetCookie` | bool | yes | set token to cookie |  
  | `isSKip2fa` | bool | yes |if `true` Don't ask again on this computer for 14 days | 
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`error` |string |no| `code verify failed`,`Timeout`,`Number of retries exceeded`，`account locked` |
|`message` |string |no| |
| `Verifiedtoken` | string | no |Verified token containing `2fa verified time`|
|`jwtToken` | string | no |  jwt token for logining | 
|`retryRemainingNumber` | string | no | 2FA code retry Remaining Number | 
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "Verifiedtoken":"sdfasdf3452tsdfsd4werrtewr"
   "jwtToken":"sdfasdf3452t4werrtewr"
}

HTTP/1.1 400 OK
{
   "error": "Timeout",
   "message":"",
}
```

<!-- ### Get A 2fa Secret Key of Partner User
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
``` -->

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

 ### Get a 2fa Secret Key
`GET /global/2faSecret`

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

### Get the Agent 2fa config
`GET /global/agent2faConfigs/{agentId}`

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
### Get the list of agent 2fa configs
`GET /global/agent2faConfigs`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | siteId | int | yes | site Id |  
    
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` |string |Yes| 2FA config Id |

```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
[
  {
     "id": "DQ6EXYKLD4TTJ7DY",
     "agentId":"324234",
  }
]
```

### Create A Agent 2fa config
`POST /global/agent2faConfigs`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  |`secretKey` |string |Yes| 2FA secret key |
  | `code` | string | yes |  2FA code or backup code| 
  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - |   
  |`error` |string |no| `code verify failed`,`secretKey have exited` |
  |`message` |string |no| |
```Json 
  HTTP/1.1 200 OK
  
 
  HTTP/1.1 400 OK
  {
     "error": "code verify failed",
     "message":"code verify failed",
  }
```

### Update the Agent 2fa config
`Put /global/agent2faConfigs/{agentId}`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  |`secretKey` |string |Yes| 2FA secret key |
  | `code` | string | yes |  2FA code or backup code| 
  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`error` |string |Yes|`code verify failed`  |
  |`message` |string |Yes|    |
  
```Json 
  HTTP/1.1 200 OK
  
  HTTP/1.1 400 OK
  {
     "error": "code verify failed",
     "message":"code verify failed",
  }
```

<!-- ### Delete the 2fa of agent
`Delete /global/agent2faConfigs/{agentId}`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
```Json 
  HTTP/1.1 200 OK
``` -->

### Generate A Agent 2fa Backup Code
`POST /global/agent2faBackupCode:generate`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | agentId | int | yes | agent Id | 
  
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
### Get the Agent 2fa Backup Code
`GET /global/agent2faBackupCode`

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

### Update the Agent 2fa Backup Code
`UPDATE /global/agent2faBackupCode`

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

### Delete the Agent 2fa Backup Code
`DELETE /global/agent2faBackupCode`

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

``` 

### Create a site authentication config
`POST /global/siteAuthenticationConfigs`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `2FARequirement` | int | yes |  0: Every login,1: Allow to skip in trusted devices for 14 days. |
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `siteId` | int | yes |  site Id |
  | `2FARequirement` | int | yes |  0: Every login,1: Allow to skip in trusted devices for 14 days. |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
  "siteId":10000,
  "2FARequirement":1
}
```
### Get the site authentication config
`Get /global/siteAuthenticationConfigs/{siteId}`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |    
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `siteId` | int | yes |  site Id |
  | `2FARequirement` | int | yes |  0: Every login,1: Allow to skip in trusted devices for 14 days. |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
  "siteId":10000,
  "2FARequirement":1
}
```

### Update the site authentication config
`Put /global/siteAuthenticationConfigs`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `2FARequirement` | int | yes |  0: Every login,1: Allow to skip in trusted devices for 14 days. |
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  | `siteId` | int | yes |  site Id |
  | `2FARequirement` | int | yes |  0: Every login,1: Allow to skip in trusted devices for 14 days. |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
  "siteId":10000,
  "2FARequirement":1
}
```

### Get the Super Agent 2fa config
`GET /partnerglobal/superagent2faConfigs/{superagentId}`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  |superagentId | int | yes | superagentId |  
    
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

### Get the list of Super agent 2fa configs
`GET /partnerglobal/superagent2faConfigs`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | partnerId | int | yes | partnerId|  
    
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`id` |string |Yes| 2FA config Id |
  |`superagentid` |string |Yes| superagentid |
  
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
[
  {
     "id": "DQ6EXYKLD4TTJ7DY",
     "superagentid":"324234",
  }
]
```

### Create A Super Agent 2fa config
`POST /partnerglobal/superagent2faConfigs`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  |`secretKey` |string |Yes| 2FA secret key |
  | `code` | string | yes |  2FA code or backup code| 
  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - |   
  |`error` |string |no| `code verify failed`,`secretKey have exited` |
  |`message` |string |no| |
```Json 
  HTTP/1.1 200 OK
  
 
  HTTP/1.1 400 OK
  {
     "error": "code verify failed",
     "message":"code verify failed",
  }
```

### Update the Super Agent 2fa config
`Put /partnerglobal/superagent2faConfigs/{superagentId}`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  |`secretKey` |string |Yes| 2FA secret key |
  | `code` | string | yes |  2FA code or backup code| 
  
#### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
  |`error` |string |Yes|`code verify failed`  |
  |`message` |string |Yes|    |
  
```Json 
  HTTP/1.1 200 OK
  
  HTTP/1.1 400 OK
  {
     "error": "code verify failed",
     "message":"code verify failed",
  }
```

### Generate a Super Agent 2fa backup code
`Post /partnerglobal/superagents2fabackupcodes:generate`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |
  |`partnerId` | int | yes |  partnerId |
  |`superAgentId` |int |Yes| superAgentId |
  
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK

``` 

