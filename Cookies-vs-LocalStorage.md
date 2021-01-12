# Cookies vs LocalStorage

## Introduction to Cookies
Cookies are small files which are located on a user’s computer. They are designed to hold a generous amount of data specific to a client and website, and they can accessed either by the web server or the client computer. 

- The reason behind this is to allow the server to deliver a page tailored to a particular user, or the page itself can contain some script which knows of the data in the cookie, and therefore it is able to carry information from one visit to the website to the next.
- Each cookie is effectively a small lookup table containing pairs of key, data values.
- Cookies are primarily for reading **server-side**
- Introduced prior to HTML5.
- Has expiration date.
- Cleard by JS or by Clear Browsing Data of browser or after expiration date.
- Will sent to the server per each request.
- The capacity is 4KB.
- Only strings are able to store in cookies.
- There are two types of cookies: persistent and session.
- Each domain stores all its cookies in a single string, which can make parsing data difficult
- Data is unencrypted, which becomes an issue because... ... though small in size, cookies are sent with every HTTP request Limited size (4KB)
- SQL injection can be performed from a cookie

## Introduction to LocalStorage
localStorage is an implementation of the Storage Interface. It stores data with no expiration date, and gets cleared only through JavaScript, or clearing the Browser Cache / Locally Stored Data — unlike cookie expiry.

- Local Storage is as big as 5MB per domain 
- Local storage can only be read by the client-side
- Introduced with HTML5.
- Does not has expiration date.
- Cleard by JS or by Clear Browsing Data of the browser.
- You can select when the data must be sent to the server.
- Data is stored indefinitely, and must be a string.
- Only have one type.
- Support by most modern browsers
- Same-origin rules apply to local storage data
> localStorage will not be available if you switch from 'http' to 'https' secured protocol, where the cookie will still be accesible.
