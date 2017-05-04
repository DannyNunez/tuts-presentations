#SAML

*A Service Provider* is the entity providing the service - typically in the form of an application. 

*An Identity Provider* is the entity providing the identities. 

- The Ability to authenticate a user. 
- Contains the user profile (Username, first name, etc ...)

*A SAML Request* also known as an authentication request, is generated by the Service Provider to "request an authentication"

*A SAML Response* is generated by the identity Provider.  

*A Service Provider Initiated (SP-initiated)* login describes the SAML login flow when initiated by the Service Provider. 
This is typically triggered when the end user tries to access a resource or login directly on the Service Provider side, such as when the browser tries to access a protected resource on the Service Provider side.

*An Identity Provider Initiated (IDP-initiated)* login describes the SAML flow being triggered by a redirection from the Service Provider. In this flow the identity Provider initiates a SAML Response that is redirected to the Service Provider to assert the user's identity. 

###A Couple of Key Things to note:###

1. The Service Provider never directly interacts with the Identity Provider. A browser acts as the agent to carry out all the redirections. 

2. The Service Provider needs to know which Identity Provider.

3. The Service Provider does not know who is the user is until the SAML assertion comes back from the Identity Provider.

4. This flow does not have to start from the Service Provider. An Identity Provider can initiate an authentication flow. 

5. The SAML authentication flow is asynchronous. The Service Provider does not know if the Identity Provider will ever complete the entire flow. Because of this, the Service Provider does not maintain any state of any authentication requests generated. When the Service Provider recies a response from an Identity Provider, the response must contain all the necessary information. 















 


