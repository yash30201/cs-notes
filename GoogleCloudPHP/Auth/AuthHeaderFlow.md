# Auth headers in the library: A to Z

Complete authorsation works in 4 different layers. The layers being:
1) GAX PHP
2) Google Auth Library PHP (_Major things happen here_)
3) Grpc php library
4) Core C implementation of GRPC

## GAX PHP

There are two parts of the story here.

### Credentials Wrapper

> TODO: Write about this class

This class implements a method called `getAuthorizationHeaderCallback` which essentially returns a **callback** (whose function is same as `updateMetadata` of `UpdateMetdataInterface`) which is used to get the auth header value.

### Transport Classes

Rest transport and Grpc transports use the `getAuthorizationHeaderCallback` method to get the callback and then use it according to the transports

#### REST

Things are pretty straight forward here as common headers are added in this repository its self. Code pointer: [buildCommonHeader](https://github.com/googleapis/gax-php/blob/main/src/Transport/HttpUnaryTransportTrait.php#L93)

#### GRPC

Things become little complex here due to the nature of GRPC. `getAuthorizationHeaderCallback` method is invoked in `GrpcTransport` class to set the `call_credentials_callback` call option. ([code pointer](https://github.com/googleapis/gax-php/blob/main/src/Transport/GrpcTransport.php#L247))

These call options are further passed down to grpc's `BaseStub` constructor.

## GRPC PHP library

The `call_credentials_callback` is used to construct underlying c implemented `CallCredentials` ([Code Pointer](https://github.com/grpc/grpc-php/blob/b610c42022ed3a22f831439cb93802f2a4502fdf/src/lib/AbstractCall.php#L64))

## Code C implementation

The core C invokes the header callback and updates the metadata before each request. This is achieved by invoking the [plugin_get_metadata](https://github.com/grpc/grpc/blob/master/src/php/ext/grpc/call_credentials.c#L143) method before each grpc call. This method adds whatever metadata received from the callback after verifying basic regex checks.
