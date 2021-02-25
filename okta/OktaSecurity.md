Okta, Inc. is a publicly traded identity and access management company based in San Francisco. It provides cloud software that helps companies manage and secure user authentication into applications, and for developers to build identity controls into applications, website web services and devices.


At a high-level, this flow has the following steps:
- Your application directs the browser to the Okta sign-in page, where the user authenticates.
- The browser receives an authorization code from your Okta Authorization Server.
- The authorization code is passed to your application.
- Your application sends this code to Okta, and Okta returns access and ID tokens, and optionally a refresh token.
- Your application can now use these tokens to call the resource server (for example an API) on behalf of the user.
