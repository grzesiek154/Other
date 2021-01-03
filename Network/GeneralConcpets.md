### What is CORS?

A request for a resource (like an image or a font) outside of the origin is known as a *cross-origin* request. CORS (cross-origin resource sharing) manages cross-origin requests.

Once again, consider the following URL:

```
http://www.example.com/foo-bar.html
```

Let’s call it *URL1* (for short).

Unlike same-origin, navigating to `https://www.ejemplo.com/hola.html` from **URL1** could be allowed with CORS. Allowing cross-origin requests is helpful,  as many websites today load resources from different places on the  Internet (stylesheets, scripts, images, and more).

Cross-origin requests, however,  mean that servers must implement ways to handle requests from origins  outside of their own. CORS allows servers to specify who (i.e., which  origins) can access the assets on the server, among many other things.

You can think of these interactions as a building with a security entrance. For example, if you need to  borrow a ladder, you could ask a neighbor in the building who has one.  The building’s security would likely not have a problem with this  request (i.e., same-origin). If you needed a particular tool, however,  and you ordered it from an outside source like an online marketplace  (i.e., cross-origin), the security at the entrance may request that the  delivery person provide identification when your tool arrives.

[![img](https://content.codecademy.com/articles/what-is-cors/cross-origin.svg)](https://content.codecademy.com/articles/what-is-cors/cross-origin.svg)

(Click to enlarge)

### Why is CORS necessary?

The CORS standard is needed because it allows servers to specify not only who can access the assets, but also *how* they can be accessed. 

Cross-origin requests are made using the standard HTTP request methods. Most servers will allow `GET` requests, meaning they will allow resources from external origins (say, a web page) to read their assets. HTTP requests methods like `PATCH`, `PUT`, or `DELETE`, however, may be denied to prevent malicious behavior. For many servers, this is intentional. For example, it is likely that server A does not  want servers B, C, or D to edit or delete its assets.

With CORS, a server can specify who can access its assets and which HTTP request methods are allowed from external resources.

### How does CORS manage requests from external resources?

 An HTTP header is a piece of  information associated with a request or a response. Headers are passed  back and forth between your web browser (also referred to as a client)  and a server when the web page you are on wants to use resources hosted  on a different server. Headers are used to describe requests and  responses. The CORS standard manages cross-origin requests by adding new HTTP headers to the standard list of headers. The following are the new HTTP headers added by the CORS standard:

- `Access-Control-Allow-Origin`
- `Access-Control-Allow-Credentials`
- `Access-Control-Allow-Headers`
- `Access-Control-Allow-Methods`
- `Access-Control-Expose-Headers`
- `Access-Control-Max-Age`
- `Access-Control-Request-Headers`
- `Access-Control-Request-Method`
- `Origin`

These are all important, but let’s focus on the following header:

- `Access-Control-Allow-Origin`

The `Access-Control-Allow-Origin` header allows servers to specify how their resources are shared with external domains. When a `GET` request is made to access a resource on Server A, Server A will respond with a value for the `Access-Control-Allow-Origin` header. Many times, this value will be `*`, meaning that Server A will share the requested resources with *any* domain on the Internet. Other times, the value of this header may be  set to a particular domain (or list of domains), meaning that Server A  will share its resources with that specific domain (or list of domains). The `Access-Control-Allow-Origin` header is critical to resource security.

You can find a description of each CORS header at the following: [CORS Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers#CORS).