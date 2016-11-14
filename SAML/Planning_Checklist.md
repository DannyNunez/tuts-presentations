#Planning checklist#

While the SAML protocol is a standard, there are different ways to implement it depending on the nature of your application. The following is a checklist that will guide you through some of the key considerations. 

1. Understanding the role of a Service Provider

A SAML IDP generates a SAML response based on configuration that is mutually agreed upon by the IDP and the SP. 
Upon receiving the SAML assertion, the SP needs to validate the assertion comes from a valid IDP and than parse the necessary information from the assertion. ( username , attributes )

**In order to do this, this SP requires at least the following:**

- **Certificate** - The Service Provider needs to obtain the public certificate from the Identity Provider to validate the signature. The certificate is stored on the SP side and used whenever a SAML response arrives.

- **ACS Endpoint** - Assertion Consumer Service URL - often referred to simply as the SP Login url. this is the endpoint provided by the SP where SAML responses are posted. The SP needs to provide this information to the IDP.

- **IDP Login URL** - This is the endpoint on the IDP side where SAML requests are posted. The SP needs to obtain this information from the IDP. 

2. Single IDP vs Multiple IDPs

If you are building an internal app and you want to SAML-enable it in order to integrate with your corporate SAML identity provider, than you are looking at supporting only a single IDP. In this case, your app only needs to deal with a single set of IDP metadata (cert,endpoints, etc). 


3. Understanding SP-initiated Login Flow.
4. Exposing SAML configuration in SP
5. Enabling SAML for everyone vs a subset of users
6. Implementing a backdoor
