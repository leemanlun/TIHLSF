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

![image](https://user-images.githubusercontent.com/80155116/112713118-4eec9480-8f38-11eb-911b-928eacecb18a.png)

## Cookies

Cookies are small bits of data stored in browser, each browser store them separately. Usually used for **Session Management** or **Advertising**.

They are normally sent with every HTTP request made to server.

### Why?

Because HTTP is stateless, cookies are used to keep track of this.

Allows tracking of data like items in shopping cart, who you are, what you have done on the website.

Cookies are broken down into several parts:
* name
* value
* expiry
* date
* path

Server is usually the one that sets cookies, response headers with ("Set-Cookie").

### Using cookies

A *Session Token* is given when logging in a website, intercepting these token will alow you to impersonate the person logging in.

### Manipulating cookies

Cookies can be viewed and modified using browser's developer tool.

### Making HTTP requests cURL

``curl http://10.10.216.45:8081/ctf/get`` - GET request. Make a GET request to the web server with path /ctf/get

``curl -X POST --data flag_please http://10.10.216.45:8081/ctf/post`` - POST request. Make a POST request with the body "flag_please" to /ctf/post

``curl -b 'flagpls=flagpls' http://10.10.216.45:8081/ctf/sendcookie`` - Set a cookie. Set a cookie with name "flagpls" and value "flagpls" in your devtools (or with curl!) and make a GET request to /ctf/sendcookie
