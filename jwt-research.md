A JSON Web Token (JWT), pronounced 'jot', is a compact, self-contained method for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. A JWT consists of three parts separated by dots: a header, a payload, and a signature.

JWTs are essential for modern web applications, particularly for enabling stateless authentication. After a user successfully logs in, the server issues a JWT. The client application then stores this token and sends it back with every subsequent request for protected resources. As the token contains all necessary user information and is verified by its signature, the server does not need to maintain a session record in its database. This simplifies the architecture and improves scalability.

The most common implementation of JWTs in a web application follows this flow:
1. A user authenticates with their credentials.
2. If the credentials are valid, the server generates a JWT and sends it back to the client.
3. The client application stores the JWT.
4. On all subsequent requests to protected API endpoints, the client includes the JWT in the Authorization HTTP header using the Bearer scheme.

The header looks like this:
Authorisation: Bearer <jwt>

The server-side application then uses middleware to check for this header, extract the token, and validate its signature before processing the request.

In 2015, security researchers, notably Tim McLean from Auth0, discovered and publicised that numerous popular JWT libraries across different programming languages were vulnerable to the "algorithm confusion" attack and another flaw involving the alg: "none" algorithm. The impact was enormous because these libraries are foundational building blocks for countless web applications and APIs. Any developer who used one of these libraries with an asymmetric key algorithm (like RS256) and didn't have specific countermeasures in place was likely vulnerable.
