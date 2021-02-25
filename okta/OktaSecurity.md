Okta, Inc. is a publicly traded identity and access management company based in San Francisco. It provides cloud software that helps companies manage and secure user authentication into applications, and for developers to build identity controls into applications, website web services and devices.


At a high-level, this flow has the following steps:
- Your application directs the browser to the Okta sign-in page, where the user authenticates.
- The browser receives an authorization code from your Okta Authorization Server.
- The authorization code is passed to your application.
- Your application sends this code to Okta, and Okta returns access and ID tokens, and optionally a refresh token.
- Your application can now use these tokens to call the resource server (for example an API) on behalf of the user.


There are three major kinds of authentication that you can perform with Okta:

1. The Authentication API controls access to your Okta org and applications. It provides operations to authenticate users, perform multifactor enrollment and verification, recover forgotten passwords, and unlock accounts. It is the underlying API that both the Okta Sign-In Widget and Auth JS use under the hood.

2. The OAuth 2.0 protocol controls authorization to access a protected resource, like your web app, native app, or API service.

3. The OpenID Connect protocol is built on the OAuth 2.0 protocol and helps authenticate users and convey information about them. It is also more opinionated than plain OAuth 2.0, for example in its scope definitions.
