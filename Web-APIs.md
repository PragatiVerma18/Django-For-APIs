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

### Endpoints
A web API has **endpoints** - URLs with a list of available actions (HTTP verbs) that expose data (typically in JSON, which is the most common data format these days and the default for Django REST Framework).

> The type of endpoint which returns multiple data resources is known as a **collection**.

## HTTP
HTTP is a request-response protocol between two computers that have an existing TCP connection. The computer making the requests is known as the _client_ while the computer responding is known as the _server_. 

> Every HTTP message consists of a request/status line, headers, and optional body data.

## Status Codes

General type of status code based on the following system:

• **2xx Success** - the action requested by the client was received, understood, and accepted

• **3xx Redirection** - the requested URL has moved

• **4xx Client Error** - there was an error, typically a bad URL request by the client

• **5xx Server Error** - the server failed to resolve a request 

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
