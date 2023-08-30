# Credentials

There are a total of 7 credential classes defined. These are:
1) GCE Credentials
2) Impersonated Service Account Credentials
3) Service Account Credentials
4) Service Account Credentials With JWT Access
5) User Refresh Credentials
6) Insecure Credentials
7) IAM Credentials

## Observations
Out of these, following happens primarily:
- `1 to 5` extends `CredentialsLoader`.
- `6` implements `FetchAuthTokenInterface`.
- `7` is a standalone class.


> IMPORTANT: `CredentialsLoader` implements ``FetchAuthTokenInterface`` !!

Thus let's analyse `FetchAuthTokenInterface`.

## Credentials Loader

This is an **abstract class** which extends `FetchAuthTokenInterface` and `UpdateMetadataInterface`. It implements many static methods regarding:
- Http Client creation and usage
- Certificates
- Credentials file finding and loading
- Implements `updateMetadata` -> which in turn utilises the `fetchAuthToken` method which is to be implemented by the classes extending this class.

### Update Metadata

- Existing metadata not present in args
- Cannot alter args here in this logic
- It's purpose is to return the `Authorization` header completely.
- Return's an associative array.
- All the key's values present here are just added as it is in the final backend headers and it won't ammend existing headers.
    -  For examples, if current metadata is ['k1': ['k1v1 k1v2']].
    -  We return ['k1' : ['k1v3']] from `updateMetadata` method.
    -  The final header become ['k1': ['k1v1 k1v2'], 'k1': ['k1v3']].

**Inference**: Cannot use this method to alter existing metadata.




