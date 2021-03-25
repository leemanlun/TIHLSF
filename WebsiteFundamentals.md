# How do we load websites?

### Finding the server

DNS request, DNS takes a URL and turns it into IP address. Four groups of numbers from 0 to 255.

### Loading Content

When browser receives server's IP, it asks for server's webpage, using HTTP GET request.

Server will respond with GET request with web page content, if webpage loads extra content such as JavaScript, images, or CSS files, those will be 
retrieved via seperate GET requests.

Most website nowadays use HTTPS, an encrypted version of HTTP. Uses TLS 1.3 encryption in order to 
communicate without:

* Other parties being able to **read** or **modify** the data.

Webserver is a software that receives and responds to HTTP(S) requests. Like Apachem, Nginx and Microsoft's IIS.  

By default HTTP runs on port 80 and HTTPS on port 443.

### Requests

There are **9** different HTTP "verbs" or methods, GET being one of them.

**POST** requests are used to send data to webserver, like adding a comment or logging in.

HTTP request can broken down into parts:

GET /index.html -> first line is a verb and a path for the server.

Next is headers, which contains more info about request, cookies are sent in request headers.

Finally, body of request. For POST requests, this is the content that is sent to server. 

For GET requests, body is allowed but will be ignored.

Example for a GET request retrieving a JS file:

![image](https://user-images.githubusercontent.com/80155116/112428961-de5f3f80-8da0-11eb-9d2a-58eed15a35bf.png)

## Responses


