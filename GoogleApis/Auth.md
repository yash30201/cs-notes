# Auth in Google APIs

Google api client provide numerous ways to authenticate.

_TODO: More info about the types_

One thing which is common in all of the `Google\Auth` managed auth is that all the request is executed by invoking the `Client's`
`$client->execute($request);` [method](https://github.com/googleapis/google-api-php-client/blob/main/src/Client.php#L889).

This `execute` method in turn invokes the `authorize` method which attaches middlerwares defined in Google Auth to the http handler.

## Tokens ([ref](https://cloud.google.com/docs/authentication/token-types))

The following token types:

* Access tokens
* ID tokens
* Self-signed JWTs
* Refresh tokens
* Federated tokens
* Bearer tokens

> API keys and Client IDs are considered credentials, hence don't confuse them for a kind of tokens.

### Access Tokens

Access tokens are opaque tokens that conform to the OAuth 2.0 framework. They contain authorization information, but not identity information. They are used to authenticate and provide authorization information to Google APIs.
> Client libraries automatically handles access tokens.

### ID Tokens

ID tokens are JSON Web Tokens (JWTs) that conform to the OpenID Connect (OIDC) specification. The contain identity information too.

| Access Tokens | Id Tokens |
| --- | --- |
| They are obtained </br>when scope is defined | They are obtained</br>when audience is defined |
| Both, scope and audience cannot be defined together|

#### Exchanging a self-signed JWT for a Google-signed ID token

> This exchanging step is done by google services backend and hence we can just send self signed jwt as auth tokens.

Create a JWT with the header set to {"alg":"RS256","typ":"JWT"}. The payload should include a `target_audience` claim set to the URL of the receiving function and iss and sub claims set to the email address of the service account used above. It should also include exp, and iat claims. The `aud` claim should be set to https://www.googleapis.com/oauth2/v4/token.

See complete step [here](https://cloud.google.com/functions/docs/securing/authenticating#exchanging_a_self-signed_jwt_for_a_google-signed_id_token).

### Self signed JWTs

Self-signed JWTs are required to authenticate to APIs deployed with API Gateway. In addition, self-signed JWTs are used to authenticate to some Google APIs without having to get an access token from the Authorization Server.

### Refresh Tokens

A refresh token is a special token that is used to obtain additional access tokens or ID tokens. When an application first authenticates, it receives an access token or ID token, as well as a refresh token.

Refresh tokens don't have a set lifetime but **they can expire**. Make sure to have a logic to incorporate this fact.

### Federated Tokens

Federated tokens are used as an intermediate step by workload identity federation. Federated tokens are returned by the Security Token Service and cannot be used directly. They must be exchanged for an access token using service account impersonation. Watch [this](https://www.youtube.com/watch?v=4vajaXzHN08) video if you need to understand this process of WIF.

### Bearer Tokens

Bearer tokens are a general class of token that grants access to the party in possession of the token. Access tokens, ID tokens, and self-signed JWTs are all bearer tokens.

It relies on the security provided by an encrypted protocol, such as HTTPS and if token is intercepted, it can be used by a bad actor to gain access.

## Authorize _[[Code](https://github.com/googleapis/google-api-php-client/blob/main/src/Client.php#L419)]_

This methods adds auth listeners to the HTTP client based on the credentials set in the Google API Client object. It covers 4 cases:

1)  Check if a Google\Auth\CredentialsLoader instance has been supplied via the "credentials" option
2)  Check for Application Default Credentials
3) Access Token
    1) Check for an Access Token
    2) If access token exists but is expired, try to refresh it
4) Check for API Key

Out of these 4:
- 1st uses `attachCredentials` method of authHttpHandler.
    - Which in turn invokes the `attachCredentialsCache` method.
- 2nd uses the `attachCredentialsCache` method.
- 3.1 uses `attach token` method.
- 3.2 uses `attachCredentials` method => `attachCredentialsCache` method underlying.
- 4th uses `attachKey` method.

### Attach Credentials Cache

This method attaches the AuthTokenMiddleware of `Google\Auth` to the Http handler.

### Attach token

This uses `ScopedAccessTokenMiddleware`.

### Attach Key

This uses `SimpleMiddleware`.

