# Flask

Flask is a Python Microframework that we mainly use to build our Backend REST API service. It is a web framework, meant to abstract away the boring parts such as routing URLs, templating, database interactions, etc. Flask implements the bare-minimum and lets you choose the rest.

#### Why Flask?

The choice of a tech stack is dependent on the team. However, we do offer more support on Flask. To explain the reasoning behind this, we must consider different Programming Languages and its frameworks. In backend web development, the most popular languages are Python, Java, Node.js, PHP, and Ruby. Node.js was a big contender because of its non-blocking nature\(asynchronous features\) for fast requests/responses along with having a Javascript Full Stack makes it very appealing. It's also just made for the web. Our other choice was Python. Our initial team was most comfortable coding in Python, meaning we were able to provide resources and help in Python, and we assumed our future teams would be comprised of members that knew python, which honestly isn't an outrageous assumption. In addition, the UPenn chapter\(the founding chapter\) used Flask extensively for their web apps \(this was a small part of our reasoning\), proving the usability of Python and Flask for many of the applications non-profits ask for. Thus, we chose Python. The next decision would be for Django vs Flask.

Django is the other popular Python web framework many people use, such as Instagram and Doordash. It is a heavy framework, though, and it gives you pretty much everything. It also enforces clean and pragmatic code through its specific conventions and application structure, which is its main advantage it has against Flask. With this in mind, we still chose Flask for its simplicity since learning Django would be a lot tougher to learn and figure out how each piece fits in for new student developers.

Flask's simplicity also requires you to write the same code over again for setup. Conventions are also not set in stone. Thus, [Flask Boilerplate](https://github.com/tko22/flask-boilerplate) was made to enforce certain conventions\(config files, migration/upgrade database, blueprints\) and allow for easy setup along with an ORM database wrapper around Postgres. To understand this more, go [here](https://github.com/hack4impact-uiuc/wiki/wiki/Our-Flask-Boilerplate).

### Explore More

* [Flask Official QuickStart](http://flask.pocoo.org/docs/0.12/quickstart/#quickstart)
* [CS 196 Flask Lectures](https://github.com/CS196Illinois/WebHackerspace_Flask_Lectures)

