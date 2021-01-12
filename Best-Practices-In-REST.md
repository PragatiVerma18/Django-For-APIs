# RESTful API Design: Best Practices

### Don't return plain text
Although it is not imposed by the REST architectural style, most REST APIs use JSON as a data format.

However, it is not enough to return a body containing a JSON-formatted string. You need to specify the `Content-Type` header too! 
**It must be set to the value `application/json`.**

### Avoid using verbs in URIs
This is because HTTP verbs should be sufficient to describe the action being performed on the resource.

**Bad Practice:**
```js
GET: /articles/:slug/generateBanner/
```

**Good Practice:**
```js
GET: /articles/:slug/banner/
```

### Use plural resource nouns
Because it fits all types of endpoints very well, and helps to remain consistent even if the endpoint returns multiple resources or just one resource.
**Bad Practice:**
```js
GET: /article/:id/
```

**Good Practice:**
```js
GET: /articles/:id/
```

### Return error details in the response body
When an API server handles an error, it is convenient (and recommended!) to return error details in the JSON body to help users with debugging. Special kudos if you include which fields were affected by the error!
```js
{
  "error": "Invalid payoad.",
  "detail": {
    "surname": "This field is required."
  }
}
```

### Pay attention to status codes
Make use of the status code and only use the response body to provide error details.
```js
HTTP/1.1 400 Bad Request
Content-Type: application/json

{
    "error": "Expected at least two items in list."
}
```

### Don't nest resources
For ex - If we want to retrieve the list of articles for a particular author — the one with id=12, to represent the one-to-many relationship between an author and their articles, **use the querystring to filter the articles resource directly:**
```js
GET: /articles/?author_id=12
```

### Handle trailing slashes gracefully
Whether or not URIs should have a trailing / is not really a debate. Simply choose one way or the other (i.e., with or without a trailing slash), stick to it and gracefully redirect clients if they use the wrong convention.

**Note:** most web frameworks have an option to gracefully redirect to the trailed or untrailed version of the URL. Find that option and activate it.

### Make use of the querystring for filtering and pagination
Users may want to retrieve items that fulfill a specific condition, or retrieve them in small amounts at a time to improve performance.
With **filtering**, users can specify properties that the returned items should have.

**Pagination** allows users to retrieve fractions of a data set. The simplest kind of pagination is page number pagination, which is determined by a `page` and a `page_size`.

**Good Practice:**
```js
GET: /articles/?published=true&page=2&page_size=20
```
It returns a user "the second page of published articles containing 20 items"

### 401 vs 403
- Has the user not provided authentication credentials? Were they invalid? 👉 **401 Unauthorized**.
- Was the user correctly authenticated, but they don’t have the required permissions to access the resource? 👉 **403 Forbidden**.

### 202 Accepted
There are two cases where 202 Accepted is especially suitable for:

- If the resource will be created as a result of future processing — e.g. after a job has finished.
- If the resource already existed in some way, but this should not be interpreted as an error.

### Get should not alter the state
Use **PUT**, **POST** and **DELETE** methods instead of the GET method to alter the state.

**Bad Practice:**
```js
GET /users/711/activate
```
### Version your API
Make the API Version mandatory and do not release an unversioned API.

**Good Practice:**
```js
/blog/api/v1
```

### Use Consistent URI Case
When it comes to naming resources in a program, there are 3 main types of case conventions: CamelCase, snake_case, and spinal-case. They are just a way of naming the resources to resemble natural language while avoiding spaces, apostrophes, and other exotic characters.

- **CamelCase:** ineffective in contexts that are not case sensitive
- **snake_case:** its popularity has decreased due to a lot of abuses in C programs with over-extended or too short names
- **spinal_case:** most commonly used and traditional way of naming folders and files in UNIX and Linux systems

### PUT vs PATCH
A `PUT` request will replace the entire content of the resource at the location while a `PATCH` request, on the other hand, is used to make changes to a part of the resource at a location.

## Conclusion
Resource modeling requires a careful consideration based on the business needs, technical considerations (clean design, maintainability, etc.), and cost-benefit analysis of various approaches discussed earlier so that the API design brings out the best API consumer interaction experience.

These were the basics of designing and developing RESTful API, these guidelines hopefully will help in creating clean, easy to use, and understandable APIs.

