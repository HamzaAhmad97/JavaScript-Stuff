**Network protocol**: describes a style of communication over a network.

There are protocols for sending emails, fetching email, sharing files and so on.

## HTTP

Is a protocol for retrieving named resources (chunks of information, like web pages or pictures).

It specifies that the side making the request should start with a line like this, naming the resource and the version of the protocol that it is trying to use:

```
GET /index.html HTTP/1.1
```
HTTP treats the network as a streamlike device into which you can put bits and have them arrive at the correct destination in the correct order.

## TCP (transmission control protocol)

one computer must be waiting, or *listening*, for other computers to start talking to it. 

To be able to listen for different kinds of communication at the same time on a single machine, each listener has a number (called a *port*) associated with it.

Most protocols specify which port should be used by default. as an example, whene sending an email using the SMTP protocol, the machine **through which we send it** is expected to be listening on port 25.

Another machine can then establish a connection by connecting to the target machine using the correct port number.


If the target machine can be reached and is listening on that port, the connection is successfully created.

The listening computer is called the **server**, and the connecting computer is called the **client**.

TCP provides an abstraction of the network.

## The web

A set of protocols and formats that allow us to visit web pages in a browser.

To become part of the Web, all you need to do is connect a machine to the Internet and have it listen on port 80 with the HTTP protocol so that other computers can ask it for documents.

Each document on the web is named by a *uniform resource locator (URL)*, which looks like what we already know:

```
 http://eloquentjavascript.net/13_browser.html
|    |                        |               |
protocol       server              path
```
the first part tells that we are using the http protocol, then the server we are requesting the document from, and lastly the document itself we are accessing.

Machines connected to the internet get an IP which is a number that can be used to send messages to that machine, an example: `149.210.142.219`.

We can instead use or regester a *domain name* for a sepecific address or set of addresses instead of remembering these IPs.

The client will first have to out what address the website refers to, then using the HTTP protocol, it will make a connection to the server at the address and ask for the resource, thne the server sends the coucemtn back.

-----------

When you type an address in the browser:

1. the browser first looks up the address of the server associated with that address.
2. it then tries to open a TCP connection to it on port 80 (the default for HTTP traffic).
3. if the server exists and accepts the connection, the browser might send something like this:

```
GET /myDoc.html HTTP/1.1
Host: myWebsite.com
User-Agent: Your browser's name
```
Then the server responds through the same connection:

```
HTTP/1.1 200 OK
Content-Length: 65585
Content-Type: text/html
Last-Modified: Mon, 08 Jan 2018 10:29:45 GMT
<!doctype html>
... the rest of the document
```
then the browser handles showing the file which starts after the blank line.


`GET /myDoc.html HTTP/1.1` is the line the request sent by the client starts with.

GET is the method of the request, it means that we **want to get the specified resource**.

DELETE -> to delete the resource.

PUT -> to create or replace the resource.

POST -> to send information to the resource.

*The server is not obliged to carry out every request it gets.*, you definitely can not delete the main page of some random website.

After the request method, is the resource path, the resource is just a file or something that can be transferred.

The last part is the HTTP version.

-----------

The response of the server starts also with the HTTP version, followed by the status of the response (three digit code and then as a human-readable string).
```
HTTP/1.1 200 OK
```

Status codes starting with a 2 indicate that the request succeeded.

Codes starting with 4 mean there was something wrong with the request (404) sounds familiar?

Codes that start with 5 mean an error happened on the server and the request is not to blame.


after the first line, a number of headers is found in the form of name: value and they specify extra information about the request or response.

```
Content-Length: 65585
Content-Type: text/html
Last-Modified: Thu, 04 Jan 2018 14:05:30 GMT
```
the host header must be included, since it is up to the client or the server to include any of these headers.

then a blank line followed by the document itself.

------------

any other resource related to the document will also get retreived along with the document itself. 

To be able to fetch a larger number of resources, browsers will make several GET requests simultaneously rather than waiting for the responses one at a time

When it comes to forms, when you submit a form and the method is GET, the content of the form will be packed into an HTTP request and the browser navigates to the result of that request

if the method is GET, the information in the form is added to the end of the **action URL** as a *query string*

something like this:

`GET /example/message.html?name=Jean&message=Yes%3F HTTP/1.1`

the question mark indicates the end of the path part of the URL then it is followed by a number of names and values depending on the number of fields in the form, they are separated with '&'

here we notice that Yes which is the value of the message field is followed with '%3F' which is actually a question mark but had to be escaped, JavaScript provides the encodeURIComponent and decodeURIComponent functions to encode and decode this format.

```
console.log(encodeURIComponent("Yes?"));
// → Yes%3F
console.log(decodeURIComponent("Yes%3F"));
// → Yes?
```

if the method is POST, the query string will be put inside the body of the request rather than to the URL.
```
...

name=Jean&message=Yes%3F
```


