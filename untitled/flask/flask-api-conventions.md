# Flask API Conventions

Flask provides many ways to write endpoints, but here are the conventions H4I projects should follow. Note that some of the "good" examples are later proven to be "bad", so make sure you account for all the conventions!

#### 1\) Follow our [REST API Spec](https://github.com/hack4impact-uiuc/wiki/wiki/Our-REST-API-Specification)

```text
# bad
Not following the spec

# good
Following the spec!
```

#### 2\) Use the `create_response` util function

```text
# bad
@app.route('/users', methods = ['GET'])
def get_users():
    data = {
        'users': db.get('users')
    }
    response = {
        'success': True,
        'code': 200,
        'message': '',
        'result': data
    }
    return jsonify(response), status

# good
@app.route('/users', methods = ['GET'])
def get_users():
    data = {
        'users': db.get('users')
    }
    return create_response(data)
```

**Why?**

The `create_response` abstracts away the nitty-gritty details and mechanics of sending a response. It ensures that all the responses sent from our API have a consistent format, which makes it easier for clients that consume it. Note that `create_response` is a function that we have written internally.

#### 3\) Follow the format of the `data` parameter in `create_response`

```text
# bad
@app.route('/users', methods = ['GET'])
def get_users():
    return create_response(db.get('users'))

# good
@app.route('/users', methods = ['GET'])
def get_users():
    data = {
        'users': db.get('users')
    }
    return create_response(data)
```

**Why?**

Using descriptive keys provides a type checking mechanism for a client consuming our API. They will be able to ensure that they are getting what they expect. Read [this](https://medium.com/@shazow/how-i-design-json-api-responses-71900f00f2db) for more details.

#### 4\) Write your endpoint logic under the route decorator

```text
# bad
def get_users():
    data = {
        'users': db.get('users')
    }
    return create_response(data)

@app.route('/users', methods = ['GET'])
def users():
    if request.method == 'GET':
        return get_users()

# good
@app.route('/users', methods = ['GET'])
def get_users():
    data = {
        'users': db.get('users')
    }
    return create_response(data)
```

**Why?**

Although it's generally good practice to isolate functions for specific tasks, in this case, we don't want to decouple the endpoint logic with the endpoint declaration \(the decorator\). Doing so adds an unnecessary level of indirection.

#### 5\) Write the logic for only one request type per endpoint. You can create multiple endpoint declarations for the same endpoint url.

```text
# bad
@app.route('/users', methods = ['GET', 'POST'])
def users():
    if request.method == 'GET':
        return create_response({ 'users': db.get('users') })
    if request.method == 'POST':
        body = request.get_json()
        user = db.create('users', body)
        return create_response({ 'user': user }, status=201)

# good
@app.route('/users', methods = ['GET'])
def get_users():
    return create_response({ 'users': db.get('users') })

@app.route('/users', methods = ['POST'])
def create_user():
    body = request.get_json()
    user = db.create('users', body)
    return create_response({ 'user': user }, status=201)
```

**Why?**

We want to have good separation of concerns to maximize code readability. When reading a flask view file, you want to be able to quickly match an endpoint + type of request with its response logic. Grouping all the types of requests makes it harder to identify the corresponding response logic. However, we still want to maintain coupling between the endpoint logic and declaration, which is why we shouldn't take the approach that was deemed bad in \#4.

#### 6\) Use `<model>_id` instead of just `<id>` in endpoint urls

```text
# bad
@app.route('/users/<id>', methods = ['GET'])
def get_user_by_id(id):
    return create_response({ 'users': db.get_by_id('users', int(id)) })

# good
@app.route('/users/<user_id>', methods = ['GET'])
def get_user_by_id(user_id):
    return create_response({ 'users': db.get_by_id('users', int(user_id)) })
```

**Why?**

`id` is a built in function in python, so we don't want our variables to be named the same. Also, using `<model>_id` is much more descriptive, _especially_ to distinguish a property like `id` that every model has.

#### 7\) Cast `id`s to `int` in the endpoint url

```text
# bad
@app.route('/users/<user_id>', methods = ['GET'])
def get_user_by_id(user_id):
    return create_response({ 'users': db.get_by_id('users', int(user_id)) })

# good
@app.route('/users/<int:user_id>', methods = ['GET'])
def get_user_by_id(user_id):
    return create_response({ 'users': db.get_by_id('users', user_id) })
```

**Why?**

This makes it more clear and ensures that `user_id` is always a number \(by default it is a string\). This prevents the developer from having to explicitly cast to in `int` everywhere else `user_id` is used in the endpoint, therefore making it less prone to human error.

#### 8\) Use constants for endpoint urls

```text
# bad
@app.route('/users', methods = ['GET'])
def get_users():
    return create_response({ 'users': db.get('users') })

@app.route('/users/<int:user_id>', methods = ['GET'])
def get_user_by_id(user_id):
    return create_response({ 'users': db.get_by_id('users', user_id) })

@app.route('/users', methods = ['POST'])
def create_user():
    body = request.get_json()
    user = db.create('users', body)
    return create_response({ 'user': user }, status=201)

# good
USERS_URL = '/users'
USERS_ID_URL = '/users/<int:user_id>'

@app.route(USERS_URL, methods = ['GET'])
def get_users():
    return create_response({ 'users': db.get('users') })

@app.route(USERS_ID_URL, methods = ['GET'])
def get_user_by_id(user_id):
    return create_response({ 'users': db.get_by_id('users', user_id) })

@app.route(USERS_URL, methods = ['POST'])
def create_user():
    body = request.get_json()
    user = db.create('users', body)
    return create_response({ 'user': user }, status=201)
```

**Why?**

First, this explicitly states all the endpoint urls that will be used in the flask view file at the top. Anyone reading the code will know exactly which part of the overall API this view covers without having to scan the entire file.

Second, creating a binding to a constant string defined elsewhere prevents typos and creating sneaky bugs \(a typo will compile without errors but won't work as expected during runtime, whereas a typo of a variable will throw an error that is easy to track\).

Third, especially because of convention \#5, it is more likely to create typos when the same string \(by value\) is created multiple times.

#### More on coding style

If you are interested in general software design patterns, what makes good and bad code, what is considered good practice, and _why_ \(which you should be\), here are some resources to look into. Note that these are very high level and don't focus on language/framework specific things. They cover more about the _why_ sections of our flask conventions:

* ["The Fundamental Theorem of Software Engineering"](https://en.wikipedia.org/wiki/Fundamental_theorem_of_software_engineering)
* [Indirection vs Abstraction](https://softwareengineering.stackexchange.com/questions/111756/what-is-the-difference-between-layer-of-abstraction-and-level-of-indirection)
* [Leaky Abstractions](https://youtu.be/gRsyY0kzXfw)
* [Separation of Concerns](https://youtu.be/0ZNIQOO2sfA)
* [Coupling and Cohesion](https://stackoverflow.com/questions/39946/coupling-and-cohesion)
* [High Cohesion and Low Coupling](https://stackoverflow.com/questions/3085285/cohesion-coupling)

