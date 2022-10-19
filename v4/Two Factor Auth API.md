  | Change Version | API Version | Change nots | Change Date | Author |Architect Team Reviewer | 
  | - | - | - | - | - |- |
  | 1.0 | v1 |Two Factor Auth API | 2022-10-13 | Leon|  Allon|
  
  ## Summary
  
### Comm100.2fa Function
 - CreateSecret -[Create the Secret Key](#create-a-secret-key).
 - VerifyCode - [verify the 2FA code](#verify-the-2fa-code).
 
### Partner Login API
- POST /partnerloginapi/2fa:verify - [verify the 2FA code](#verify-the-2fa-code-of-partner-user).
  
### Partner Global API
- POST /partnerglobal/user/{id}/2faConfig - [Create a 2FA secret key](#create-a-secret-key-of-partner-user).
- DELETE /partnerglobal/user/{id}/2faConfig - [Delete the 2FA secret key](#Delete-the-secret-key-of-partner-user). 
 
- POST /partnerglobal/2faBackupCode - [Create a 2FA Backup Code](#create-a-backup-code-of-partner-user).
- GET /partnerglobal/2faBackupCode/{id} - [Get the 2FA Backup Code](#get-the-backup-code-of-partner-user). 
- PUT /partnerglobal/2faBackupCode/{id} - [Update the 2FA Backup Code](#update-the-backup-code-of-partner-user). 
- DELETE /partnerglobal/2faBackupCode/{id} - [Delete the 2FA Backup Code](#delete-the-backup-code-of-partner-user).
    
### Login API
- POST /global/2fa:verify - [verify the 2FA code](#verify-the-2fa-code-of-agent).
  
### Global API
- POST /global/2faConfig - [Create a 2FA secret key](#create-a-secret-key-of-agent).
- DELETE /global/2faConfig/{id} - [Delete the 2FA secret key](#delete-the-secret-key-of-agent). 

- POST /partnerglobal/2faBackupCode - [Create a 2FA Backup Code](#create-a-backup-code-of-agent).
- GET /partnerglobal/2faBackupCode/{id} - [Get the 2FA Backup Code](#get-the-backup-code-of-agent). 
- PUT /partnerglobal/2faBackupCode/{id} - [Update the 2FA Backup Code](#update-the-backup-code-of-agent). 
- DELETE /partnerglobal/2faBackupCode/{id} - [Delete the 2FA Backup Code](#delete-the-backup-code-of-agent).    

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
  | `UserAccount` | string | yes |  User Email show in 2fa app|  
  
The Response body contains data with the following 

  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`SecretKey` |string |Yes| 2FA secret key |
|`QrcodeUrl` |string |Yes|  qrcode text url of 2FA  |

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

  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`secretKey` |string |Yes| 2FA secret key |
|`qrcodeUrl` |string |Yes|  qrcode image url of 2FA secret key  |
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
`POST /partnerloginapi/2fa:verify`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `partneruserid` | string | yes |  partner user id |  
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
   "result": "success",
}
```

### Verify the 2FA Code of Agent
`POST /loginapi/2fa:verify`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `agentid` | string | yes |  partner user id |  
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
   "result": "success",
}
```

### Create A Secret Key of Partner User
`POST /partnerglobalapi/user/{id}/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  partner user id |
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`secretKey` |string |Yes| 2FA secret key |
|`qrcodeUrl` |string |Yes|  qrcode image text url of 2FA information |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "qrcodeUrl": "otpauth://totp/leon%40comm100.com?secret=DQ6EXYKLD4TTJ7DY&issuer=Comm100&period=30&algorithm=SHA1&digits=6",
   "secretKey":"DQ6EXYKLD4TTJ7DY",
}
```
### Delete the Secret Key of Partner User
`Delete /partnerglobalapi/user/{id}/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  partner user id |
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
```Json 
  HTTP/1.1 200 OK
```
### Create A Backup Code of Partner User
`POST /partnerglobalapi/user/{id}/2faBackupCode`

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

### Delete the Backup Code of Partner User
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
```

### Create A Secret Key of Agent
`POST /partnerglobalapi/agent/{id}/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  agent id |
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`secretKey` |string |Yes| 2FA secret key |
|`qrcodeUrl` |string |Yes|  qrcode image text url of 2FA information |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "qrcodeUrl": "otpauth://totp/leon%40comm100.com?secret=DQ6EXYKLD4TTJ7DY&issuer=Comm100&period=30&algorithm=SHA1&digits=6",
   "secretKey":"DQ6EXYKLD4TTJ7DY",
}
```
### Delete the Secret Key of agent
`Delete /partnerglobalapi/agent/{id}/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  agent id |
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
```Json 
  HTTP/1.1 200 OK
```

### Create A Backup Code of Agent
`POST /partnerglobalapi/user/{id}/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  agent id |
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
`GET /partnerglobalapi/user/{id}/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  agent id |
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
`UPDATE /partnerglobalapi/user/{id}/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  agent id |
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
`DELETE /partnerglobalapi/user/{id}/2faBackupCode`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `id` | string | yes |  agent id |
  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`code` |string |Yes| 2FA Backup Code |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
```
