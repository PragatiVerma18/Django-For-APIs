# User Authentication

- **Authorization:** API Permissions
- **Authentication:** process by which a user can register for a new account, log in with it, and log out

## Basic Authentication:

The most common form of HTTP authentication is known as “Basic” Authentication. When a client makes an HTTP request, it is forced to send an approved authentication credential before access is granted.

The complete request/response flow looks like this:
1. Client makes an HTTP request
2. Server responds with an HTTP response containing a `401 (Unauthorized)` status code and `WWW-Authenticate` HTTP header with details on how to authorize
3. Client sends credentials back via the `Authorization` HTTP header
4. Server checks credentials and responds with either `200 OK` or `403 Forbidden` status code.
Once approved, the client sends all future requests with the Authorization HTTP header credentials.

> **Note:** The authorization credentials sent are the **unencrypted base64 encoded** version of `<username>:<password>`.

**Cons:**
- On every single request the server must look up and verify the username and password, which is inefficient. 
- User credentials are being passed in clear text—not encrypted at all, can be easily captured and reused.

> **Note:** Basic authentication should only be used via HTTPS, the secure version of HTTP.

## Session Authentication:

At a high level, the client authenticates with its credentials (username/password) and then receives a _session ID_ from the server which is stored as a _cookie). This session ID is then passed in the header of every future HTTP request. When the session ID is passed, the server uses it to look up a session object containing all available information for a given user, including credentials. This approach is **stateful** because a record must be kept and maintained on both the server (the session object) and the client (the session ID).

Let’s review the basic flow:
1. A user enters their log in credentials (typically username/password)
2. The server verifies the credentials are correct and generates a session object that is then stored in the database
3. The server sends the client a session ID — not the session object itself—which is stored as a cookie on the browser
4. On all future requests the session ID is included as an HTTP header and, if verified by the database, the request proceeds
5. Once a user logs out of an application, the session ID is destroyed by both the client and server
6. If the user later logs in again, a new session ID is generated and stored as a cookie on the client

> **Note:** The default setting in Django REST Framework is actually a combination of Basic Authentication and Session Authentication. Django’s traditional session-based authentication system is used and the session ID is passed in the HTTP header on each request via Basic Authentication.

**Pros:**
- User credentials are only sent once, not on every request/response cycle as in Basic Authentication. 
- It is also more efficient since the server does not have to verify the user’s credentials each time, it just matches the session ID to the session object which is a fast look up.

**Cons:**
- A session ID is only valid within the browser where log in was performed; it will not work across multiple domains. This is an obvious problem when an API needs to support multiple front-ends such as a website and a mobile app. 
- The session object must be kept up-to-date which can be challenging in large sites with multiple servers.
- The cookie is sent out for every single request, even those that don’t require authentication, which is inefficient. 

> **Note:** It is generally not advised to use a session-based authentication scheme for any API that will have multiple front-ends.
