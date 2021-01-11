## URL
A **URL(Uniform Resource Locator)** is the address of a resource on the internet. For example, the Google homepage lives at `https://www.google.com`.

Every URL like `https://python.org/about/` has three potential parts:

• **a scheme** - `https` (tells web browser how to access resources at the location)

• **a hostname** - `www.python.org` (the actual name of the site)

• **and an (optional) path** - `/about/`

## Internet Protocol Suite

Several things happen when a user types `https://www.google.com` into their web browser and hits Enter. First the browser needs to find the desired server, somewhere, on the vast internet. It uses a **domain name service (DNS)** to translate the domain name “`google.com`” into an **IP address**, which is a unique sequence of numbers representing every connected device on the internet. 

**Domain names** are used because it is easier for humans to remember a domain name like “`google.com`” than an IP address like “`172.217.164.68`”.

After the browser has the IP address for a given domain, it needs a way to set up a consistent connection with the desired server. This happens via the **Transmission Control Protocol (TCP)** which provides reliable, ordered, and error-checked delivery of bytes between two application.

To establish a TCP connection between two computers, a **three-way “handshake”** occurs between the client and server:

1. The client sends a **SYN** asking to establish a connection
2. The server responds with a **SYN-ACK** acknowledging the request and passing a connection parameter
3. The client sends an **ACK** back to the server confirming the connection

Once the TCP connection is established, the two computers can start communicating via HTTP.

### HTTP Verbs
Every webpage contains both an address (the URL) as well as a list of approved actions known as **HTTP verbs**.

![ME_ME_HTTP_MODULE_ME_HTTP_MODULE_BYTE1_image_12](https://user-images.githubusercontent.com/42115530/104155356-08919a00-540d-11eb-94f8-316e8f591177.png)

> **Note:** **PUT method is idempotent**. So if you send retry a request multiple times, that should be equivalent to single request modification. POST is NOT idempotent. So if you retry the request N times, you will end up having N resources with N different URIs created on server.

### Endpoints
A web API has **endpoints** - URLs with a list of available actions (HTTP verbs) that expose data (typically in JSON, which is the most common data format these days and the default for Django REST Framework).

> The type of endpoint which returns multiple data resources is known as a **collection**.

## HTTP
HTTP is a request-response protocol between two computers that have an existing TCP connection. The computer making the requests is known as the _client_ while the computer responding is known as the _server_. 

> Every HTTP message consists of a request/status line, headers, and optional body data.
> The default port for HTTP is 80.
> Data in a GET request is sent as part of the URL and this has a limit of 2048 characters.


## HTTP vs HTTPS
HTTPS stands for Hypertext Transfer Protocol Secure (also referred to as HTTP over TLS or HTTP over SSL). HTTPS also uses TCP (Transmission Control Protocol) to send and receive data packets, but it does so over port 443, within a connection encrypted by Transport Layer Security (TLS). Generally sites running over HTTPS will have a redirect in place so even if you type in `http://` it will redirect to deliver over a secured connection.

**Key Differences:**

- HTTP is unsecured while HTTPS is secured.
- HTTP sends data over port 80 while HTTPS uses port 443.
- HTTP operates at application layer, while HTTPS operates at transport layer.
- No SSL certificates are required for HTTP, with HTTPS it is required that you have an SSL certificate and it is signed by a CA.
- HTTP doesn't require domain validation, where as HTTPS requires at least domain validation and certain certificates even require legal document validation.
- No encryption in HTTP, with HTTPS the data is encrypted before sending.


## Status Codes

General type of status code based on the following system:

• **2xx Success** - the action requested by the client was received, understood, and accepted

• **3xx Redirection** - the requested URL has moved

• **4xx Client Error** - there was an error, typically a bad URL request by the client

• **5xx Server Error** - the server failed to resolve a request 

## Common HTTP Request Headers
- Browsers sends a `User-Agent` request header along with HTTP requests to denote the software it’s using.
- `Last-Modified` response header is sent by the server to specify the last modified date of the requested resource.
- `If-Modified-Since` request header is sent by the browser to specify the last modified date of the cached copy of the resource (saved in the browser). The value of this header is same as the value of the previously received `Last-Modified` header.
> The purpose of using above headers is to avoid unnecessary transferring of a resource if it has not been changed since the last access, hence saving bandwidth and improving performance.

## HTTP/2 & HTTP/1.1
The first usable version of HTTP was created in 1997. Because it went through several stages of development, this first version of HTTP was called `HTTP/1.1`. This version is still in use on the web. In 2015, a new version of HTTP called `HTTP/2` was created.

HTTP/2 solves several problems that the creators of HTTP/1.1 did not anticipate. In particular, HTTP/2 is much faster and more efficient than HTTP/1.1. One of the ways in which HTTP/2 is faster is in how it **prioritizes** content during the loading process.

> Read more [here](https://www.cloudflare.com/learning/performance/http2-vs-http1.1)

## REST
**REpresentational State Transfer (REST)** is an approach to building APIs on top of the web, which means on top of the HTTP protocol.

Every RESTful API:

• is stateless, like HTTP

• supports common HTTP verbs (GET, POST, PUT, DELETE, etc.)

• returns data in either the JSON or XML format

Any RESTful API must, at a minimum, have these three principles. The standard is important because it provides a consistent way to both design and consume web APIs.

> Ultimately a web API is a collection of endpoints that expose certain parts of an underlying database. As developers we control the URLs for each endpoint, what underlying data is available, and what actions are possible via HTTP verbs. 

## API Schema and Documentation
A **schema** is a machine-readable document that outlines all available API endpoints, URLs, and the HTTP verbs (GET, POST, PUT, DELETE, etc.) they support. 

**Documentation** is something added to a schema that makes it easier for humans to read and consume.

---
