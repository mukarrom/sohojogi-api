---
title: sohojogi api
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
code_clipboard: true
highlight_theme: darkula
headingLevel: 2
generator: "@tarslib/widdershins v4.0.30"

---

# sohojogi api

Provider endpoints for profile, KYC, services, availability, location, and device fingerprinting.

Base URLs:

* <a href="https://server.sohojogi.com.bd/api/v1">Testing Env: https://server.sohojogi.com.bd/api/v1</a>

# Authentication

- HTTP Authentication, scheme: bearer

- HTTP Authentication, scheme: bearer

# Health Check

<a id="opIde_webdev_sohojogi-server_bruno_health_check_health_check_yml"></a>

## GET Health Check

GET /health

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|None|

# Auth

<a id="opIde_webdev_sohojogi-server_bruno_auth_request_otp_yml"></a>

## POST request_otp

POST /auth/otp/request

> Body Parameters

```json
"{\n    \"mobile\": \"01909037017\",\n    \"role\": \"PROVIDER\" // ADMIN, CUSTOMER, SUPER_ADMIN\n}"
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|Content-Type|header|string| yes |none|
|body|body|[request_otp](#schemarequest_otp)| yes |none|

> Response Examples

> 200 Response

```json
{
  "success": true,
  "statusCode": 200,
  "message": "OTP sent successfully",
  "data": {
    "otp": "363438",
    "expiresIn": 300
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» success|boolean|false|none||none|
|» statusCode|number|false|none||none|
|» message|string|false|none||none|
|» data|object|false|none||none|
|»» otp|string|false|none||none|
|»» expiresIn|number|false|none||none|

<a id="opIde_webdev_sohojogi-server_bruno_auth_verify_otp_yml"></a>

## POST Verify OTP

POST /auth/otp/verify

> Body Parameters

```json
{
  "mobile": "{{mobile}}",
  "otp": "{{otp}}"
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|Content-Type|header|string| yes |none|
|body|body|[verify_otp](#schemaverify_otp)| yes |none|

> Response Examples

> 200 Response

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Authentication successful",
  "data": {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI2OWE5MjBhMDAzYzkxZDhiNWU2NWNmNTciLCJyb2xlIjoiUFJPVklERVIiLCJpYXQiOjE3NzI2OTE2MTYsImV4cCI6MTc3Mzk4NzYxNn0.ssDXTEnzgg60JwGsV9usUxBqQWxCnpMyffAQgvckmSk",
    "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiI2OWE5MjBhMDAzYzkxZDhiNWU2NWNmNTciLCJyb2xlIjoiUFJPVklERVIiLCJpYXQiOjE3NzI2OTE2MTYsImV4cCI6MTc3Nzg3NTYxNn0.CW1yyqR3jwbqFACp67AAfvhu0pavL3vRR7QyMDYyJt8",
    "user": {
      "_id": "69a920a003c91d8b5e65cf57",
      "mobile": "01700000002",
      "role": "PROVIDER",
      "fullName": "",
      "avatarUrl": "",
      "isNewUser": true
    }
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|200|Inline|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» success|boolean|false|none||none|
|» statusCode|number|false|none||none|
|» message|string|false|none||none|
|» data|object|false|none||none|
|»» accessToken|string|false|none||none|
|»» refreshToken|string|false|none||none|
|»» user|object|false|none||none|
|»»» _id|string|false|none||none|
|»»» mobile|string|false|none||none|
|»»» role|string|false|none||none|
|»»» fullName|string|false|none||none|
|»»» avatarUrl|string|false|none||none|
|»»» isNewUser|boolean|false|none||none|

<a id="opIde_webdev_sohojogi-server_bruno_auth_logout_yml"></a>

## POST Logout

POST /auth/logout

> Body Parameters

```json
{
  "refreshToken": "{{refreshToken}}"
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|Content-Type|header|string| yes |none|
|body|body|[logout](#schemalogout)| yes |none|

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|None|

<a id="opIde_webdev_sohojogi-server_bruno_auth_refresh_token_yml"></a>

## POST Refresh Token

POST /api/v1/auth/token/refresh

> Body Parameters

```json
{
  "refreshToken": "string"
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|Content-Type|header|string| yes |none|
|body|body|[refresh_token](#schemarefresh_token)| yes |none|

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|None|

# Customer

<a id="opIde_webdev_sohojogi-server_bruno_customer_get_customer_profile_yml"></a>

## GET Get Customer Profile

GET /customer/profile

> Response Examples

> 200 Response

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Customer profile retrieved",
  "data": {
    "userId": {
      "_id": "69b148e550c454b5a8bc63a0",
      "mobile": "01909037017",
      "fullName": "",
      "avatarUrl": "",
      "isActive": true,
      "id": "69b148e550c454b5a8bc63a0"
    },
    "email": "",
    "addresses": [],
    "pushNotificationEnabled": true,
    "_id": "69b14a8350c454b5a8bc63a6",
    "createdAt": "2026-03-11T10:57:07.014Z",
    "updatedAt": "2026-03-11T10:57:07.014Z",
    "__v": 0
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» success|boolean|false|none||none|
|» statusCode|number|false|none||none|
|» message|string|false|none||none|
|» data|object|false|none||none|
|»» userId|object|false|none||none|
|»»» _id|string|false|none||none|
|»»» mobile|string|false|none||none|
|»»» fullName|string|false|none||none|
|»»» avatarUrl|string|false|none||none|
|»»» isActive|boolean|false|none||none|
|»»» id|string|false|none||none|
|»» email|string|false|none||none|
|»» addresses|[string]|false|none||none|
|»» pushNotificationEnabled|boolean|false|none||none|
|»» _id|string|false|none||none|
|»» createdAt|string|false|none||none|
|»» updatedAt|string|false|none||none|
|»» __v|number|false|none||none|

<a id="opIde_webdev_sohojogi-server_bruno_customer_update_customer_profile_yml"></a>

## PATCH Update Customer Profile

PATCH /customer/profile

> Body Parameters

```yaml
avatar: ""
fullName: ""
email: ""
pushNotificationEnabled: ""
address: '{    "label": "office",    "address": "Ashulia, Dhaka",    "lat":
  23.8223,    "lng": 90.3666,    "instructions": "Near the main gate"}'

```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|body|body|object| yes |none|
|» avatar|body|string(binary)| no |none|
|» fullName|body|string| no |none|
|» email|body|string| no |none|
|» pushNotificationEnabled|body|boolean| no |none|
|» address|body|string| no |none|

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|None|

<a id="opIde_webdev_sohojogi-server_bruno_customer_change_customer_status_admin_yml"></a>

## PATCH Change Customer Status (Admin)

PATCH /api/v1/customer/%7B%7BcustomerId%7D%7D/change-status

> Body Parameters

```json
{
  "isActive": true
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|customerId|path|string| yes |none|
|Content-Type|header|string| yes |none|
|body|body|[change_customer_status_admin](#schemachange_customer_status_admin)| yes |none|

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|None|

<a id="opIde_webdev_sohojogi-server_bruno_customer_get_customer_by_id_admin_yml"></a>

## GET Get Customer by ID (Admin)

GET /api/v1/customer/%7B%7BcustomerId%7D%7D

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|customerId|path|string| yes |none|

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|None|

<a id="opIde_webdev_sohojogi-server_bruno_customer_list_all_customers_admin_yml"></a>

## GET List All Customers (Admin)

GET /api/v1/customer/all

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|search|query|string| no |none|
|page|query|integer(int32)| no |none|
|limit|query|integer(int32)| no |none|
|sortBy|query|string| no |none|
|sortOrder|query|string| no |none|

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|None|

# Address

<a id="opIde_webdev_sohojogi-server_bruno_address_create_address_yml"></a>

## POST Create Address

POST /api/v1/addresses

> Body Parameters

```json
{
  "label": "string",
  "address": "string",
  "lat": 0,
  "lng": 0,
  "instructions": "string"
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|Content-Type|header|string| yes |none|
|body|body|[create_address](#schemacreate_address)| yes |none|

> Response Examples

> 201 Response

```json
{
  "success": true,
  "statusCode": 201,
  "message": "Address created",
  "data": {
    "user": "69afc0a183d8de3e2b25ccfd",
    "label": "home",
    "address": "Mirpur DOHS, Dhaka",
    "location": {
      "type": "Point",
      "coordinates": [
        90.3666,
        23.8223
      ]
    },
    "instructions": "Near the main gate",
    "_id": "69b0fed25d98505d141ce9e4",
    "createdAt": "2026-03-11T05:34:10.188Z",
    "updatedAt": "2026-03-11T05:34:10.188Z",
    "__v": 0
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|201|[Created](https://tools.ietf.org/html/rfc7231#section-6.3.2)|Created|Inline|

### Responses Data Schema

HTTP Status Code **201**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» success|boolean|false|none||none|
|» statusCode|number|false|none||none|
|» message|string|false|none||none|
|» data|object|false|none||none|
|»» user|string|false|none||none|
|»» label|string|false|none||none|
|»» address|string|false|none||none|
|»» location|object|false|none||none|
|»»» type|string|false|none||none|
|»»» coordinates|[string]|false|none||none|
|»»»» 0|number|false|none||none|
|»»»» 1|number|false|none||none|
|»» instructions|string|false|none||none|
|»» _id|string|false|none||none|
|»» createdAt|string|false|none||none|
|»» updatedAt|string|false|none||none|
|»» __v|number|false|none||none|

<a id="opIde_webdev_sohojogi-server_bruno_address_list_addresses_yml"></a>

## GET List Addresses

GET /api/v1/addresses

> Response Examples

> 200 Response

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Addresses retrieved",
  "data": [
    {
      "location": {
        "type": "Point",
        "coordinates": [
          90.3666,
          23.8223
        ]
      },
      "_id": "69b0fed25d98505d141ce9e4",
      "user": "69afc0a183d8de3e2b25ccfd",
      "label": "home",
      "address": "Mirpur DOHS, Dhaka",
      "instructions": "Near the main gate",
      "createdAt": "2026-03-11T05:34:10.188Z",
      "updatedAt": "2026-03-11T05:34:10.188Z",
      "__v": 0
    }
  ]
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» success|boolean|false|none||none|
|» statusCode|number|false|none||none|
|» message|string|false|none||none|
|» data|[string]|false|none||none|
|»» 0|object|false|none||none|
|»»» location|object|false|none||none|
|»»»» type|string|false|none||none|
|»»»» coordinates|[string]|false|none||none|
|»»»»» 0|number|false|none||none|
|»»»»» 1|number|false|none||none|
|»»» _id|string|false|none||none|
|»»» user|string|false|none||none|
|»»» label|string|false|none||none|
|»»» address|string|false|none||none|
|»»» instructions|string|false|none||none|
|»»» createdAt|string|false|none||none|
|»»» updatedAt|string|false|none||none|
|»»» __v|number|false|none||none|

<a id="opIde_webdev_sohojogi-server_bruno_address_delete_address_yml"></a>

## DELETE Delete Address

DELETE /api/v1/addresses/%7B%7BaddressId%7D%7D

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|addressId|path|string| yes |none|

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|None|

<a id="opIde_webdev_sohojogi-server_bruno_address_get_address_by_id_yml"></a>

## GET Get Address by ID

GET /api/v1/addresses/{addressId}

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|addressId|path|string| yes |none|

> Response Examples

> 200 Response

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Address retrieved",
  "data": {
    "location": {
      "type": "Point",
      "coordinates": [
        90.3666,
        23.8223
      ]
    },
    "_id": "69b0fed25d98505d141ce9e4",
    "user": "69afc0a183d8de3e2b25ccfd",
    "label": "home",
    "address": "Mirpur DOHS, Dhaka",
    "instructions": "Near the main gate",
    "createdAt": "2026-03-11T05:34:10.188Z",
    "updatedAt": "2026-03-11T05:34:10.188Z",
    "__v": 0
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» success|boolean|false|none||none|
|» statusCode|number|false|none||none|
|» message|string|false|none||none|
|» data|object|false|none||none|
|»» location|object|false|none||none|
|»»» type|string|false|none||none|
|»»» coordinates|[string]|false|none||none|
|»»»» 0|number|false|none||none|
|»»»» 1|number|false|none||none|
|»» _id|string|false|none||none|
|»» user|string|false|none||none|
|»» label|string|false|none||none|
|»» address|string|false|none||none|
|»» instructions|string|false|none||none|
|»» createdAt|string|false|none||none|
|»» updatedAt|string|false|none||none|
|»» __v|number|false|none||none|

<a id="opIde_webdev_sohojogi-server_bruno_address_update_address_yml"></a>

## PUT Update Address

PUT /api/v1/addresses/{addressId}

> Body Parameters

```json
{
  "label": "string",
  "address": "string",
  "lat": 0,
  "lng": 0,
  "instructions": "string"
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|addressId|path|string| yes |none|
|Content-Type|header|string| yes |none|
|body|body|[update_address](#schemaupdate_address)| yes |none|

> Response Examples

> 200 Response

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Address updated",
  "data": {
    "location": {
      "type": "Point",
      "coordinates": [
        90.4078,
        23.7925
      ]
    },
    "_id": "69b0fed25d98505d141ce9e4",
    "user": "69afc0a183d8de3e2b25ccfd",
    "label": "office",
    "address": "Gulshan 2, Dhaka",
    "instructions": "3rd floor, ring the bell",
    "createdAt": "2026-03-11T05:34:10.188Z",
    "updatedAt": "2026-03-11T05:36:56.589Z",
    "__v": 0
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|OK|Inline|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» success|boolean|false|none||none|
|» statusCode|number|false|none||none|
|» message|string|false|none||none|
|» data|object|false|none||none|
|»» location|object|false|none||none|
|»»» type|string|false|none||none|
|»»» coordinates|[string]|false|none||none|
|»»»» 0|number|false|none||none|
|»»»» 1|number|false|none||none|
|»» _id|string|false|none||none|
|»» user|string|false|none||none|
|»» label|string|false|none||none|
|»» address|string|false|none||none|
|»» instructions|string|false|none||none|
|»» createdAt|string|false|none||none|
|»» updatedAt|string|false|none||none|
|»» __v|number|false|none||none|

# Provider/Profile

## GET Get Profile

GET /provider/profile

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

## PATCH Update Profile

PATCH /provider/profile

> Body Parameters

```json
{
  "fullName": "Provider Mukarrom",
  "email": "provider@example.com",
  "bio": "Experienced home service provider",
  "hourlyRateDefault": 500,
  "isAvailable": true,
  "paymentMethods": [
    "CASH",
    "BKASH"
  ]
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|Content-Type|header|string| yes |none|
|body|body|object| no |none|
|» fullName|body|string| yes |none|
|» email|body|string| yes |none|
|» bio|body|string| yes |none|
|» hourlyRateDefault|body|integer| yes |none|
|» isAvailable|body|boolean| yes |none|
|» paymentMethods|body|[string]| yes |none|

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

## PATCH Availability

PATCH /provider/availability

> Body Parameters

```json
{
  "isAvailable": false
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|body|body|object| yes |none|

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

# Provider/KYC

## POST Upload Liveness Selfie (Step 1)

POST /provider/kyc/liveness

> Body Parameters

```yaml
file: file://E:\Assets\profile-icon.png

```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|body|body|object| no |none|
|» file|body|string(binary)| yes |none|

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

## POST Submit KYC (Step 2)

POST /provider/kyc/submit

> Body Parameters

```yaml
fullName: Provider Mukarrom u1
email: provider@example.com
address: Dhaka, Bangladesh
longitude: 90.4125
latitude: 23.8103
nidFront: file://E:\Assets\pexels-bitnik-36313704.jpg
nidBack: file://E:\Assets\pexels-josh-2158073373-35243047.jpg

```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|body|body|object| no |none|
|» fullName|body|string| yes |none|
|» email|body|string| yes |none|
|» address|body|string| yes |none|
|» longitude|body|number| yes |none|
|» latitude|body|number| yes |none|
|» nidFront|body|string(binary)| yes |none|
|» nidBack|body|string(binary)| yes |none|

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

## GET Get KYC Document URL

GET /provider/kyc/document-url

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|documentKey|query|string| yes |none|

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

# Provider/Admin KYC Verification

## PATCH Verify Provider KYC

PATCH /provider/{providerId}/kyc/verify

> Body Parameters

```json
{
  "approvalStatus": "APPROVED",
  "adminNotes": "Looks good"
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|providerId|path|string| yes |none|
|Content-Type|header|string| yes |none|
|body|body|object| no |none|
|» approvalStatus|body|string| yes |none|
|» adminNotes|body|string| yes |none|

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

# Provider/Service Area

## PUT Update Service Area

PUT /provider/service-area

> Body Parameters

```json
{
  "longitude": 90.4126,
  "latitude": 23.8103,
  "radiusKm": 10,
  "address": "Dhaka, Bangladesh"
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|Content-Type|header|string| yes |none|
|body|body|object| no |none|
|» longitude|body|number| yes |none|
|» latitude|body|number| yes |none|
|» radiusKm|body|integer| yes |none|
|» address|body|string| yes |none|

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

## GET Get Service Area

GET /provider/service-area

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

# Provider/Schedule

## GET Daily Schedule

GET /provider/daily-schedule

> Response Examples

> 200 Response

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Daily schedule retrieved",
  "data": {
    "isConfigured": false,
    "mixedSchedule": false,
    "startTime": null,
    "endTime": null,
    "isEnabled": false
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

## PATCH Daily Schedule update

PATCH /provider/daily-schedule

> Body Parameters

```json
{
  "startTime": "08:00",
  "endTime": "18:00"
}
```

### Params

|Name|Location|Type|Required|Description|
|---|---|---|---|---|
|body|body|object| yes |none|

> Response Examples

> 200 Response

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Daily schedule retrieved",
  "data": {
    "isConfigured": false,
    "mixedSchedule": false,
    "startTime": null,
    "endTime": null,
    "isEnabled": false
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|none|Inline|

### Responses Data Schema

# Data Schema

<h2 id="tocS_create_address">create_address</h2>

<a id="schemacreate_address"></a>
<a id="schema_create_address"></a>
<a id="tocScreate_address"></a>
<a id="tocscreate_address"></a>

```json
{
  "label": "string",
  "address": "string",
  "lat": 0,
  "lng": 0,
  "instructions": "string"
}

```

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|label|string|false|none||none|
|address|string|false|none||none|
|lat|number|false|none||none|
|lng|number|false|none||none|
|instructions|string|false|none||none|

<h2 id="tocS_update_address">update_address</h2>

<a id="schemaupdate_address"></a>
<a id="schema_update_address"></a>
<a id="tocSupdate_address"></a>
<a id="tocsupdate_address"></a>

```json
{
  "label": "string",
  "address": "string",
  "lat": 0,
  "lng": 0,
  "instructions": "string"
}

```

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|label|string|false|none||none|
|address|string|false|none||none|
|lat|number|false|none||none|
|lng|number|false|none||none|
|instructions|string|false|none||none|

<h2 id="tocS_logout">logout</h2>

<a id="schemalogout"></a>
<a id="schema_logout"></a>
<a id="tocSlogout"></a>
<a id="tocslogout"></a>

```json
{
  "refreshToken": "string"
}

```

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|refreshToken|string|false|none||none|

<h2 id="tocS_refresh_token">refresh_token</h2>

<a id="schemarefresh_token"></a>
<a id="schema_refresh_token"></a>
<a id="tocSrefresh_token"></a>
<a id="tocsrefresh_token"></a>

```json
{
  "refreshToken": "string"
}

```

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|refreshToken|string|false|none||none|

<h2 id="tocS_request_otp">request_otp</h2>

<a id="schemarequest_otp"></a>
<a id="schema_request_otp"></a>
<a id="tocSrequest_otp"></a>
<a id="tocsrequest_otp"></a>

```json
{
  "mobile": "string",
  "role": "string"
}

```

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|mobile|string|false|none||none|
|role|string|false|none||none|

<h2 id="tocS_verify_otp">verify_otp</h2>

<a id="schemaverify_otp"></a>
<a id="schema_verify_otp"></a>
<a id="tocSverify_otp"></a>
<a id="tocsverify_otp"></a>

```json
{
  "mobile": "string",
  "otp": "string"
}

```

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|mobile|string|false|none||none|
|otp|string|false|none||none|

<h2 id="tocS_change_customer_status_admin">change_customer_status_admin</h2>

<a id="schemachange_customer_status_admin"></a>
<a id="schema_change_customer_status_admin"></a>
<a id="tocSchange_customer_status_admin"></a>
<a id="tocschange_customer_status_admin"></a>

```json
{
  "isActive": true
}

```

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|isActive|boolean|false|none||none|

