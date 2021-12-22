# Machine to Machine Communication
Some APIs were implemented to be consumed by other services, systems or CLIs outside the context of a User. Authorization is done through the use of [OAuth2 Client Credentials Flow](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/).

## Obtaining an Access Token
An app client for a service requiring access to resources must be created first either through the serverless configuration or manually through AWS Console.

App clients are given unique Client ID and Secret that will be used for authenticating with the Token endpoint.

### Generic App Client
We currently have one generic app client that can be used for testing. However, it is advised that one client per service/app must be created before going to production.

To get the Client ID and Secret for this generic app client, go to https://console.aws.amazon.com/cognito/users/?region=us-east-1#/pool/us-east-1_XRJcsIcn8/clients?_k=0x4go0.

### Token Endpoint
The token endpoint takes the form of `https://<user_pool_domain>.<region>.amazoncognito.com/oauth2/token`.

For Otto Dev Environment, the token endpoint is https://dev-sellwithotto-ai.auth.us-east-1.amazoncognito.com/oauth2/token.

#### Get an access token
To get an access token, use Basic Authentication using the app client's Client ID and Secret.

##### Request
```shell
curl -u '<client_id>:<client_secret>' \
> -d "grant_type=client_credentials&scaope=otto-dev-api-resource-server/api.read" \
> -H "Content-Type: application/x-www-form-urlencoded" \
> -X POST https://dev-sellwithotto-ai.auth.us-east-1.amazoncognito.com/oauth2/token
```

##### Response
```json
{
   "access_token":"eyJraWQiOiJmUFdcL1k1RlhBeG9yRGdqeDE0QWswMEYxK2RXdGM3aWhzK2k0WmFXVUNJST0iLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiI2YzJuMzhxMnExcGlkMDN2dGp1azVtZDNrMSIsInRva2VuX3VzZSI6ImFjY2VzcyIsInNjb3BlIjoib3R0by1kZXYtYXBpLXJlc291cmNlLXNlcnZlclwvYXBpLnJlYWQgb3R0by1kZXYtYXBpLXJlc291cmNlLXNlcnZlclwvYXBpLndyaXRlIiwiYXV0aF90aW1lIjoxNjM2OTM4MTkyLCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAudXMtZWFzdC0xLmFtYXpvbmF3cy5jb21cL3VzLWVhc3QtMV9YUkpjc0ljbjgiLCJleHAiOjE2MzY5NDE3OTIsImlhdCI6MTYzNjkzODE5MiwidmVyc2lvbiI6MiwianRpIjoiMDI0YTRiMzEtYjQ4My00ZmJiLTgyMmQtMTc2ZWZlZTYzYWZmIiwiY2xpZW50X2lkIjoiNmMybjM4cTJxMXBpZDAzdnRqdWs1bWQzazEifQ.FdFvnkE2552FkXyGIkrkdGA7xILA52ibBNw4OjNTdBqrv6H0Afx3we7axYEelg3yX-uMIklX8BG8lP5hNZd6iebzbnNTy8dWLlvAq-fDIEwbrkqYbMpdAJjxSTDNB8Sg1KgzMh6J_4k7FRFJ19WSo12k8lOcpgsZIk0wOMzPBt2HbmyVcqnKi4iL1t97N019KdBEvewtb-Jz_F3ZMWyvLfTVpHQEMzsGk3dH68S4YZBOVLArkmte61VAn1cDPCj0ASnB_4EPZ96kU0IOhyCyIjlHG7vc0Crv_GSP1b6-EfDZsK1fw2RIPPU_p7XE-j-bxq8DJ4HknpRYndTfyKGwVg",
   "expires_in":3600,
   "token_type":"Bearer"
}
```

## Using the Access Token
Once you obtained an access token, you can use that to authorize your request with resources supporting the Client Credentials Grant. 

### Sample Request to Profiles API

```shell
curl -H "Authorization: Bearer <access_token>" \
> -X GET "https://52x900y0cf.execute-api.us-east-1.amazonaws.com/dev/profiles?uri=https://www.linkedin.com/in/arjaynacion"
```