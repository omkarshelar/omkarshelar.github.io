---
title: "Flask Notes"
date: 2019-04-02T10:59:04+05:30
draft: false
---

### Initialization:
Flask apps must create application instance.
App instance is object of class `Flask`
To create app instance use,

```python
from flask import Flask
app = Flask(__name__)
# 'app' is the application instance
```
`Flask` class has to receive one argument. That argument is the name of main module/package of application(hence `__name__`).

Flask uses the argument given while creating app instance to determine root path of the application. It later finds other resources relative to this path.

### Routes and view functions:
App instance needs to know what code to run for each URL requested. So it keeps mapping of URL to python functions.
The association between a URl and the function that handles it is called a 'route'.
In flask apps, we use decorator `@app.route` to define routes. It registers the decorated function as a route.

Eg:
```python
@app.route('/')
def index():
	return '<h1>Hello World!</h1>'
```
return value of the function is called response.
`index()` is called 'view function'.

##### URL patterns(dynamic URLs):
```python
@app.route('/user/<name>')
def user(name):
	return '<h1>Hello, %s!</h1>' % name
```
`@app.route('/user/<name>')` : `<name>` can be any variable of any type. Python treats the `<name>` as a string.

To restrict only some types of variables in URL patterns:
`/user/<int:id>` : Only `int` in the URL allowed.

Flask supports types int , float , and path for routes. The path type also represents a string but does not consider slashes as separators and instead considers them part of the dynamic component.

### Server Startup:
Application instance has `run()` method that starts Flask's web server.

```python
if __name__ == '__main__':
	app.run(debug=True)
```

`debug` set to False during production.

### How Flask works!

##### Request Context:
Flask makes a few objects available to view function that handles that the request made by the client.
Eg : `request` object which encapsulates the HTTP request sent by the client.
Flask uses _contexts_ to make certain objects temporarily globally accessible.

Eg:
```python
@app.route('/')
def index():
	user_agent = request.headers.get('User_Agent')
	return '<h1>Your browser is %s</h1>' % user_agent
```

**Note :** Request object is available globally in a thread not globally across the application.

To print the URL map:
```python
>>>from hello import app
>>>app.url_map
```

##### Request Hooks:
Certain functions which are executed before or after each view function.
Like DB connection code user Auth code.
Instead of duplicating the code, _Request Hooks_ are used.
Request hooks are implemented as decorators.

Four hooks supported by Flask:
* `before_first_request` : Register a function to run before the first request is handled.
* `before_request` : Before each request.
* `after_request` : After each request which do not produce unhandled exception(s).
* `teardown_request` : After each request even if unhandled exception(s) occurs.

To share data between request hook functions and view functions, use `g` context global.

##### Responses:
When Flask invokes a view function, it expects the return value to be the response to the request.

HTTP protocol requires status code, string(HTML document) and man other things as a response to request.

Flask by default sets the HTTP status code to 200 (OK).

When a view function needs to respond with a different status code, it can add status code as second return value.
Eg:
```python
@app.route('/')
def index():
	return '<h1>Bad Request</h1>', 400
```
Responses returned by view functions can also take a third argument, a dictionary of headers that are added to the HTTP response.

Instead of returning three values, we can also return `Response` objects from the view function. `make_response()` method takes these arguments and returns a `Response` object.
This can be used when we have to modify response inside view function(using methods of `Response` object).
Eg:
```python
from flask import make_response
@app.route('/')
def index():
	response = make_response('<h1>This document carries a cookie!</h1>')
	response.set_cookie('answer', '42')
	return response
```
To create a `redirect` response:
Eg:
```python
from flask import redirect
@app.route('/')
def index():
	return redirect('http://www.example.com')
```

To return `abort` response:
Eg:
```python
from flask import abort
@app.route('/user/<id>')
def get_user(id):
	user = load_user(id)
	if not user:
		abort(404)
	return '<h1>Hello, %s</h1>' % user.name
```

### The Request Context:
To import `request` object:
```python
from flask import request
```
##### To get headers:
`request.headers` is a python dictionary.
```python
request.headers.get('your-header-name')
# OR
request.headers['your-header-name']
```

##### To get params(args):
For the GET request `localhost:5000/?name=Hello,asdf`
Use:
```python
print(request.args.get('name'))
# OR
print(request.args['name'])
# OR
print(dict(request.args))
```
Output for last print statement:
`{'name': ['Hello,asdf']}`

##### To get form details in PUT/POST:
Use:
```python
d = dict(request.form.items())
# OR
print(request.form.get('Name'))
# OR
print(request.form['Name'])
```
##### To get raw json in PUT/POST:
Use:
```python
print(request.get_json())
```
It will be available as a python dict object.
**Note:** Make sure the header Content-Type is set to application/json for this to work.

* * *
