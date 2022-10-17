  | Change Version | API Version | Change nots | Change Date | Author |Architect Team Reviewer | 
  | - | - | - | - | - |- |
  | 1.0 | v1 |Two Factor Auth API | 2022-10-13 | Leon|  Allon|
  
  ## Summary
  
  ### Two Factor Auth API
- POST /bot/2fa/secretkey - [Create a 2FA secret key](#create-a-secret-key).
- POST /bot/2fa/code:verify - [Verify the 2FA code](#verify-the-2fa-code).
- POST /bot/2fa/code - [Create the 2FA backup code](#create-2fa-backup-codes).

## Endpoints
### Create A Secret Key
`POST /bot/2fa/secretkey`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - |  

  #### Response
The Response body contains data with the following 
  | Name  | Type | Required  | Description |     
  | - | - | - | - | 
|`secret_key` |string |Yes| 2FA secret key |
|`qrcode_url` |string |Yes|  qrcode image url of 2FA secret key  |
```Json 
  HTTP/1.1 200 OK
  Content-Type: application/json
{
   "qrcode_url": "",
   "secret_key":"",
}
```

### Verify the 2FA Code
`POST /bot/2fa/code:verify`

#### Parameters
  | Name | Type | Required  | Description |     
  | - | - | - | - | 
  | `secret_key` | string | yes |  2FA secret key |  
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
`POST /bot/2fa/codes`

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
