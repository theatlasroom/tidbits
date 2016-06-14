# APIs
## Auth - Tokens
Provide authentication that is: Stateless, scalable, mobile app ready.

Additionally individual tokens or groups of tokens can be granted different levels of permissions or can be invalidated at any point, forcing users to re-authenticate.

Problems with server based authentication:
- CORS: forbidden requests when trying to access resources from another domain. We can also serve our resources from multiple domains or CDNs
- CSRF
- sessions: logged in user data must be stored on the server
- scalability: sessions are stored in memory, session memory becomes a limit on the ability to scale

### Flow

              ==============================
          ----| 1. Client requests access  |<------
          |   =============================       |
          |                |               4b. Client stores
    5. Token sent          |                    Token
    with subsequent        |                      |
      requests             |                      |
          |                |                      |
          |          1. Send username             |
          |            + password                 |
cd           |                |                    Token    
          |                v                      |
          |    =================================  |
          |--->| 3. Application validates user |---
               =================================
* Every request requires the token to be sent along, allowing the server to be stateless
* the server needs to be able to accept requests from all domains, use the `access-control-allow-origin: *` header

### JWOT (JSON Web Tokens)
* Language independent token sent using JSON, they are self contained and have all the information needed about them, their payload and a signature
* They can be passed as a header or through the url
* Structured as three strings seperated by a `.` `<header>.<payload>.<signature>`
  - header: carries the type (JWT) and the hashing algorithm (ie HMAC SHA256)
  `{ "typ": "JWT", "alg": "HS256" }`
    this gets base64 encoded
  - payload: carries the [JWT Claims](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html#RegisteredClaimName)
    * registered claims: not mandatory, they include: iss - issuer of the token, sub - subject, aud - audience, exp - expiration in numericdate (must be a future date), iat - the time the token was issued, jti - unique identifier for the JWT, to prevent replay attacks
    * public claims: claims we make ourselves like username, information
    `{ "iss":"jwt.io", "exp": 1300819380, "name":"Test user", "admin":true }`
  - signature: a hash made from the header, payload and a secret
