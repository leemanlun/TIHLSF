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
