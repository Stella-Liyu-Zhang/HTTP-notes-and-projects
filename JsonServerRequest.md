# JSON Server
##

## Send HTTP Requests to JSON Server via Postman:

### Set up JSON Server (https://github.com/typicode/json-server)
> - Difference between install locally and install globally:
local packages are installed in the directory where you run 
```
npm install <package-name>
```
and they are put in the node_modules folder under this directory. global packages are all put in a single place in your system (exactly where depends on your setup), regardless of where you run 
```
npm install -g <package-name>
```
### Make a db.json file and add some JSON data:
```JSON
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```
The corresponding URLs are:

Resources

  http://localhost:3000/posts

  http://localhost:3000/comments
  
  http://localhost:3000/profile

Home

  http://localhost:3000



### Start JSON Server
```
 json-server --watch db.json
```
## 1) GET Request
### Go to Postman and make a GET request to http://localhost:3000/posts/1, we will get

```JSON
{ 
    "id": 1, 
    "title": "json-server", 
    "author": "typicode" 
}
```
In the cosole it shows:
```
GET /posts/1 200 12.090 ms - 63
```
If we make a GET request to http://localhost:3000/comments/1, we will get 
```JSON
{
    "id": 1,
    "body": "some comment",
    "postId": 1
}
```

## 2) POST Request
If we make a POST request to add more data to http://localhost:3000/comments/, 
If we add 3 key value pairs, "title": "foo",
      "author": "camdyn",
      "posts": "hahaha", they will be added, with "id" key set to 2 automatically.
      Therefore,
we will get 
```JSON
 "comments": [
    {
      "id": 1,
      "body": "some comment",
      "postId": 1
    },
    {
      "title": "foo",
      "author": "camdyn",
      "posts": "hahaha",
      "id": 2
    }
  ],
```
POST /comments/ 201 25.747 ms - 74
## 3) PUT Request 
**Note**: PUT is a method of modifying resource where the client sends data that updates the entire resource. 

PATCH is a method of modifying resources where the client sends partial data that is to be updated without modifying the entire data.Sep 13, 2021

If we modify Camdyn to Stella, and send a PUT Request to http://localhost:3000/comments/1, 
we see that it changed to
```JSON
{
    "title": "foo",
    "author": "Stella",
    "posts": "hahaha",
    "id": 1
}
```
One thing to note that if we only selected one key-value pair and send that PUT HTTP Request, only that piece of data will remain.
For instance, if we only select the "title" after changing PINT to PINT,Inc, we see that it changed to
 ```JSON
{
    "title": "PINT,Inc",
    "id": 1
}
```
PUT /comments/1 200 26.641 ms - 36
## 4) PATCH Request
If we modify foo to PINT, and send a PUT Request with only the title key selected to http://localhost:3000/comments/1, 
, We see that it changed to
```JSON
{
    "title": "PINT",
    "author": "Stella",
    "posts": "hahaha",
    "id": 1
}
```
PATCH /comments/1 200 22.214 ms - 79
## 5) DELETE Request
If we send DELETE request to https://localhost:3000/comments/1 , we see that in comment section, the piece of data with "id==1" is deleted.
```JSON

"comments": [
    {
      "title": "foo",
      "author": "camdyn",
      "posts": "hahaha",
      "id": 2
    }
],
```
DELETE /comments/1 200 21.999 ms - 2
