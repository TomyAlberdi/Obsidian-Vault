Created: 2024-10-04 18:35
## Family Tree:
1. Computer
2. [[Security]]
-- -
OAuth 2.0 is a widely used **authorization** protocol that allows web, mobile, and desktop applications to obtain limited access to a user's information over the HTTP protocol. It’s a framework that establishes a standard, open way for authenticating systems using HTTP. Major tech companies like Twitter, Google, Facebook, and GitHub implement OAuth to handle secure authorization.
You’ve probably encountered OAuth when logging into websites using a third-party provider, like Google or Facebook, instead of registering directly. It’s also common in API authentication, where generating a token ensures secure and efficient access to resources.
## Why use OAuth?
Traditionally, websites had their own login systems requiring a username and password. However, many platforms today also allow users to log in using credentials from other providers like Google. This is where OAuth comes in. From a business perspective, this simplifies the login process and enhances user acquisition. From a technical perspective, it shifts the responsibility of authentication (along with its costs and risks) to a trusted provider.
## The four Roles in OAuth 2.0
- **Resource Owner**: The individual or entity who owns the data and gives access to it (the user).
- **Client**: The application (such as a web app) that wants to access the resource on behalf of the user.
- **Resource Server**: The API that needs to be protected. Access to its resources requires an access token, issued by the Authorization Server.
- **Authorization Server**: The entity that authenticates the user and issues access tokens. It holds user information and interacts with the user during authentication.
## OAuth Authorization Flow
1. **Authorization Request (Client-User)**: The client application requests permission from the user to access resources.
2. **Authorization Grant (User-Client)**: If the user approves, the client receives an authorization grant.
3. **Authorization Code Exchange (Client-Authorization Server)**: The client then exchanges this grant for an access token from the Authorization Server by verifying the user's identity.
4. **Access Token (Authorization Server-Client)**: The Authorization Server authenticates the client, and if the authorization is valid, issues an access token.
5. **Access Token Usage (Client-Resource Server)**: The client uses the access token to request resources from the Resource Server, such as calling an API.
6. **Protected Resource (Resource Server-Client)**: If the token is valid, the Resource Server provides the requested resource to the client.
## Benefits for Authentication and Authorization
- **Delegated Authentication**: OAuth allows users to log in using an external provider’s credentials (e.g., Google), reducing the complexity and risk for businesses.
- **Secure API Access**: OAuth is used to authorize API access via tokens, enhancing security and allowing controlled access to resources.
- **Session Hijacking Prevention**: OAuth sessions rely on secure, encrypted tokens (like JWTs), and OAuth flows mitigate risks like session hijacking.
## Authorization Flow in practice
n a typical OAuth flow, a user provides their credentials (often username, password, and sometimes a second factor like an authentication code). This generates a **login token** (an encrypted string) that gets validated by the server. If misused, this token could lead to session hijacking, a common security risk.
Once authenticated, each request includes an **authorization token** (usually a JWT—JSON Web Token) that contains information about the user's session, including their roles and permissions, known as "claims." These roles control what actions a user can perform and which resources they can access.
**Roles and Permissions**:
OAuth helps manage **roles** and **permissions** efficiently. The tokens passed between systems include claims, representing a user's roles. These claims guide the system on what resources or functionalities the user is authorized to access.