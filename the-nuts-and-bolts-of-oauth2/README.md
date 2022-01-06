# The Nuts and Bolts of Oauth2

## Section 1 - Intro

Specifications are not amenable to tutorials.

HTTP Basic Auth - send username & password in request.

Lots of problems - driven by need to connect 3rd party apps to platforms.

### How OAuth improves application security

Basic auth - username & password.

Exchange username & password for a session cookie.

Single sign-on case is why OAuth was created. 3rd party apps not good to handle user's password.

Can you ever be sure what an app is going to do with your password? No.

API developer perspective - if every client uses the same password to login, you can't tell between them.

OAuth requires every applications sends users out to the auth server to login then redirects back to the app.

Redirect step is key. Password is never given to the application.

### OAuth vs OpenID Connect

Analogy - checking into a hotel.

Front desk is like the Authorization server - authenticating the user, check your ID.

Keys are access tokens.

Rooms are resource servers.

There is nothing in OAuth that communicates user information.

OIDC = Oauth + User Information. It is an extension of Oauth with new type of token.

Oauth issues access tokens.
OIDC issues ID tokens.

Oauth -> Accessing APIs.
OIDC -> Identifying users.

## Section 2 - API Security Concepts

### Roles in OAuth

5 roles:
* User (resource owner) - the person with the account
* Device (user agent) - the person is using this device, running or accessing an application.
* Application (oauth client) - the thing running on the device that accesses the data. 
* API (resource server) - the thing that the application is accessing which contains the data.
* Authorization server - manage access to the API that it is protecting.

Key thing: User only types in password at Authorization server.

Roles != Components

Good idea - frame questions in terms of OAuth roles.

### Application Types

Clients types:
* Confidential - deployed with client secrets.
* Public - can't be deployed with client secrets.

There is no way to ship a secret in source code and it remain secret.

Authorization server will do different things depending on the application type.

### User Consent

Goal of oauth: protect users data and only shared with authorized apps.

3rd party app using password grant is a big problem. Spec always advised against.

REdirect is preferable to password grant flow.

### Front channel vs Back channel

Back channel - HTTPS, we can validate the certificate, data is encrypted in transit, trusted response. Kind of like handing a package in person.
Front channel - browser bar. Kind of like using a package delivery service. As a sender you never really 'know' the package has arrived.

Implicit flow - front channel for both the request that app makes and delivering the access token. Browsers used to have no other option!

Back channel != Backend.

Phasing out the implict flow. Will be removed entirely in future spec.

### Application Identity

Each application has a Client ID. Client secret is the application's password.

Authorization code - like a one time coupon for redeeming an access token. Transmitted through the front channel.

What if an app can't prove its identity? Public application. PKCE is used in this instance.

Before app makes request to start the flow, creates a unique secret for each request so the Auth server knows the thing redeeming a code is the same thing that initiated the flow.

This does not prove the app's indentity. Does not stop impersonation attacks.

Redirect URI - the location of the client that the authorization server will redirect it to. 

The app's URL is part of the app's identity - not as good as a client secret.

Redirect URLs need to be registered at the authorization server.

## Section 3 - Oauth Clients

### Registering a client

First thing - register a client with the oauth server. You will get a client_id & maybe a client_secret.

Explicit list of redirect URIs mean attackers can't redirect to their own application. 

Open redirect attacks.

client_secret is that app's password.

### Authorization Code Flow for Web Applications

End goal - deliver an access token to the application via the back channel.

PKCE code verifier -> one time secret created once per oauth flow.
PKCE code challenge -> hash of the code verifier.

We provide the hash of the secret rather than the secret itself because it is going over the front channel.

PKCE will be recommended eventually even for confidential clients.

Authorization code injection attack.

Code verifier -> Random string 43-128 characters long
Code challenge -> base64url(sha256(code_verifier))

Application -> Auth Server (front channel)

```
echo "https://authorization-server.com/auth?
  response_type=code&
  client_id=$CLIENT_ID&
  redirect_uri=example-app.com/redirect& // needs to match one of the registered redirect URLs
  scope=photos&
  state=anything-can-go-here& // originally used for CSRF protection, but redundant with PKCE
  code_challenge={CODE_CHALLENGE}& // hashed code verifier value
  code_challenge_method=S256" | xclip -sel clip
```

Auth Server -> Application (front channel)

```
https://example-app.com/redirect?
  code={AUTH_CODE}
  state=XXXX // check that this is the same as the one that you sent
```

Application -> Auth Server (back channel)
```
POST https://authorization-server.com/token
  grant_type=authorization_code&
  code={AUTH_CODE}&
  redirect_uri={REDIRECT_URI}&
  code_verifier={CODE_VERIFIER}& // the random one-time secret we created
  client_id={CLIENT_ID}&
  client_secret={CLIENT_SECRET}
```


## Section 8 - Client Credentials Grant

No users involved, no browsers involved, no redirects.

The way to get an access token without any input from the user.

Machine to machine communication.

Kind of like a service account 

### Client credentials grant for machine to machine applications

```
curl -X POST https://dev-54113604.okta.com/oauth2/default/v1/token \
  -d grant_type=client_credentials \
  -d client_id=$CLIENT_ID \
  -d client_secret=$CLIENT_SECRET \
  -d scope=photos
```

## Section 9 - Introduction to OpenID Connect

OIDC is how authorization servers communicate information about the users to the applications - they use ID tokens.

ID token is a JWT: Header, Payload & Signature.

Access tokens are very different from ID tokens. They are not even remotely the same thing!

Access tokens are opaque - they can't actually see what their contents is. This is a design decision of OAuth.

ID tokens are meant to be read by the application - validate the claims and learn about the user.

Access token audience -> Resource server.
ID token audience -> Application.

ID tokens are always JWTs.

### Obtaining the ID Token

If you authorize with the `id_token` scope you get the ID token in the same place you get the access token.

### Hybrid OpenID Connect Flows

Hybrid flows - using combinations of response types. Plain OAuth uses just `code`.

OIDC defines hybrid flows.

Front channel - untrusted.

### Validating & Using an ID Token

Critical to validate ID tokens received over the front channel.

1. Validate JWT signature.
2. Check the issuer - is the token coming from the auth server you expect.
3. Check the aud - should be the same as the client ID.
4. Check the nonce.

Any time your ID token is coming from an untrusted source - it needs to be validated.

```
https://dev-54113604.okta.com/oauth2/default/v1/authorize?
  response_type=code&
  scope=openid+profile+email&
  client_id=$CLIENT_ID&
  state=anything-can-go-here&
  redirect_uri=https://example-app.com/redirect&
  code_challenge=dwu2usFNWKyBqnRWqt_U9SEqhBh7No3gTw_z4Bj4tYQ&
  code_challenge_method=S256
```


```
curl -X POST https://dev-54113604.okta.com/oauth2/default/v1/token \
  -d grant_type=authorization_code \
  -d redirect_uri=https://example-app.com/redirect \
  -d client_id=$CLIENT_ID \
  -d client_secret=$CLIENT_SECRET \
  -d code_verifier=d46d86846b1b90bd92980346817c1ec0fd0eb6922c794826061dc320 \
  -d code=rwIcRVaTCgj2p8quMv0reChE52SsTv6oHk1cM0Sg7wE
```