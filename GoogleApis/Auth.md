# Auth in Google APIs

Google api client provide numerous ways to authenticate.

_TODO: More info about the types_

One thing which is common in all of the `Google\Auth` managed auth is that all the request is executed by invoking the `Client's`
`$client->execute($request);` [method](https://github.com/googleapis/google-api-php-client/blob/main/src/Client.php#L889).

This `execute` method in turn invokes the `authorize` method which attaches middlerwares defined in Google Auth to the http handler.

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

