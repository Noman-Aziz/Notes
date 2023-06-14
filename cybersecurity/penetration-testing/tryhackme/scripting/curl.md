# Curl

By default, cURL will perform GET requests on whatever URL you supply it, such as: `curl www.google.com`

This would retrieve the main page for google with a GET request. Using command line flags for cURL, we can do a lot more than just GET content.

The **-X flag** allows us to specify the request type, eg -X POST.

You can specify the data to POST with **--data**, which will default to plain text data.

It's worth mentioning cURL does not store cookies, and you have to manually specify any cookies and values that you would like to send with your request. If you want to send cookies from cURL, use **-b or --cookie**.

Remember, cookies are not shared between different browsers (counting cURL as a browser here).
