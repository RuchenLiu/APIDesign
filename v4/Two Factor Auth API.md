  | Change Version | API Version | Change nots | Change Date | Author |Architect Team Reviewer | 
  | - | - | - | - | - |- |
  | 1.0 | v1 |Two Factor Auth API | 2022-10-13 | Leon|  Allon|
  
  ## Summary
  
  ### Two Factor Auth API
- POST /2fa/secretkey - [Create a 2FA secret key](#create-a-secret-key).
- POST /2fa/code:verify - [verify the 2FA code](#verify-the-2fa-code).
- POST /2fa/code - [Create the 2FA backup code](#create-2fa-backup-codes).
  
### Partner Login API
- POST /partnerloginapi/2fa:verify - [verify the 2FA code](#verify-the-2fa-code-of-partner-user).
  
### Partner Global API
- POST /partnerglobal/2faConfig - [Create a 2FA secret key](#create-a-secret-key-of-partner-user).
- GET /partnerglobal/2faConfig/{id} - [Get the 2FA secret key](#Get-the-secret-key-of-partner-user). 
- PUT /partnerglobal/2faConfig/{id} - [Update the 2FA secret key](#Get-the-secret-key-of-partner-user). 
- DELETE /partnerglobal/2faConfig/{id} - [Delete the 2FA secret key](#Delete-the-secret-key-agent).   
### Login API
- POST /global/2fa:verify - [verify the 2FA code](#verify-the-2fa-code-of-agent).
  
### Global API
- POST /global/2faConfig - [Create a 2FA secret key](#create-a-secret-key-of-agent).
- GET /global/2faConfig/{id} - [Get the 2FA secret key](#Get-the-secret-key-agent). 
- PUT /partnerglobal/2faConfig/{id} - [Update the 2FA secret key](#Get-the-secret-key-of-partner-user). 
- DELETE /global/2faConfig/{id} - [Delete the 2FA secret key](#Delete-the-secret-key-agent). 
## Endpoints

### Create A Secret Key
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
```


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
`POST /partnerglobalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `partneruserid` | string | yes |  partner user id |
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
   "secretKey":"b65cnh2y35vrkj2d",
}
```

### Create A Secret Key of Agent
`POST /globalapi/2faConfig`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  
  | `partneruserid` | string | yes |  partner user id |
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
   "secretKey":"b65cnh2y35vrkj2d",
}
```
