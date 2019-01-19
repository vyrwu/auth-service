# Oauth2.0 with JWT and social login (FB, Google)
> Exchange user credentials or social login grant for JWT access token to IAfoosball services.  
> [Watch intro movie here.](https://app.hyfy.io/v/abnaOzc4fVn/)
>  
> Compliant with Internet Best Practices:  
> [RFC 8252 - Oauth2.0 for Native Apps](https://tools.ietf.org/html/rfc8252)  
> [RFC 7519 -  JSON Web Token (JWT)](https://tools.ietf.org/html/rfc7519)  
> [RFC 7617 - The 'Basic' HTTP Authentication Scheme](https://tools.ietf.org/html/rfc7617)   
## Flow
``` text
     +--------+                               +---------------+
     |        |--(A)----- Login Request ----->|               |
     |        |                               |      User     |
     |        |<-(B)------- Login Grant ------|               |
     |        |                               +---------------+
     |        |
     |        |                               +---------------+
     |        |--(C)------ Login Grant ------>|               |
     |  App   |                               | auth-service  |
     |        |<-(D)--- JWT Access Token -----|               |
     |        |                               +---------------+
     |        |
     |        |                               +---------------+
     |        |--(E)--- JWT Access Token ---->|     Other     |
     |        |                               |    services   |
     |        |<-(F)--- Protected Resource ---|               |
     +--------+                               +---------------+
```
## Endpoints
*Base Path: `http://iafoosball.me:8010`*
```
Token access:
POST /oauth/login
POST /oauth/logout
POST /oauth/verify

Social login:
GET /oauth/facebook
GET /oauth/google
```
## Examples
* Login with Basic Auth (issue token)
```bash
curl -X POST \
  http://iafoosball.me/oauth/login \
  -H 'Authorization: Basic dnlyd3U6dnlyd3U='

Response:
{
    "access_token": "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c3IiOiJ2eXJ3dSIsImV4cCI6MTU0MTk2OTA4OCwianRpIjoiUlpHTEg2QTVPVyJ9.FWUhvRnszVHG3wcTq97i8RhezyZgmf3w3NYk50iYfmrnBoPSD0QMJxDl60gButJvENYdvp9dmAGti1F8S7rVHTFhGriPrEtrncBtpz1TGbvw0wNW1nmf6umC7F9DfcB71bDlXhH-sIRkHA5P0P9zPnsQCF1C9rAOXvQxsCp0FTk"
}
```
* Login with FB/Google
```bash
curl -X GET \
  http://iafoosball.me/oauth/facebook
  
  or
  
curl -X GET \
  http://iafoosball.me/oauth/google
```
* Verify JWT
```bash
curl -X POST \
  http://iafoosball.me/oauth/verify \
  -H 'Authorization: JWT eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c3IiOiJ2eXJ3dSIsImV4cCI6MTU0MTk2OTA4OCwianRpIjoiUlpHTEg2QTVPVyJ9.FWUhvRnszVHG3wcTq97i8RhezyZgmf3w3NYk50iYfmrnBoPSD0QMJxDl60gButJvENYdvp9dmAGti1F8S7rVHTFhGriPrEtrncBtpz1TGbvw0wNW1nmf6umC7F9DfcB71bDlXhH-sIRkHA5P0P9zPnsQCF1C9rAOXvQxsCp0FTk'
```
* Logout (revoke token)
```bash
curl -X POST \
  http://iafoosball.me/oauth/logout \
  -H 'Authorization: JWT eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c3IiOiJ2eXJ3dSIsImV4cCI6MTU0MTk2OTA4OCwianRpIjoiUlpHTEg2QTVPVyJ9.FWUhvRnszVHG3wcTq97i8RhezyZgmf3w3NYk50iYfmrnBoPSD0QMJxDl60gButJvENYdvp9dmAGti1F8S7rVHTFhGriPrEtrncBtpz1TGbvw0wNW1nmf6umC7F9DfcB71bDlXhH-sIRkHA5P0P9zPnsQCF1C9rAOXvQxsCp0FTk'
```

## Coming soon
* HTTPS
* Social login (with github)
* Better security (use multiple rotating private keys)
* Logging
* Staging and Production environments

