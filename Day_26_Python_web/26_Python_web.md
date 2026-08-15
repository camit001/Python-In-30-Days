<div align="center">
  <h1> Python In 30 Days: Day 26 - Python for Web </h1>
  

  <sub>Author:
  <a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>

  </sub>
</div>

[<< Day 25](../Day_25_Pandas/25_Pandas.md) | [Day 27 >>](../Day_27_Python_with_mongodb/27_Python_with_mongodb.md)
</div>


**[Python In 30 Days]**

- [📘 Day 26](#-day-26)
  - [Python for Web](#python-for-web)
    - [Flask](#flask)
      - [Folder structure](#folder-structure)
    - [Setting up your project directoryy](#setting-up-your-project-directory)
    - [Creating routes](#creating-routes)
    - [Creating templates](#creating-templates)
    - [Python Script](#python-script)
    - [Navigation](#navigation)
    - [Creating a layout](#creating-a-layout)
      - [Serving Static File](#serving-static-file)
    - [Deployment](#deployment)
      - [Creating Heroku account](#creating-heroku-account)
      - [Login to Heroku](#login-to-heroku)
      - [Create requirements and Procfile](#create-requirements-and-procfile)
      - [Pushing project to heroku](#pushing-project-to-heroku)
  - [Exercises: Day 26](#exercises-day-26)

# 📘 Day 26

## Python for Web

Python is a general purpose programming language and it can be used for many places. In this section, we will see how we use Python for the web. There are many Python web frameworks. Django and Flask are the most popular ones. Today, we will see how to use Flask for web development.

### Flask

Flask is a web development framework written in Python. Flask uses Jinja2 template engine. Flask can be also used with other modern front libraries such as React.

If you did not install the virtualenv package yet install it first. Virtual environment will allows us to isolate project dependencies from the local machine's dependencies.

#### Folder structure

After completing all the step, your project file structure should look like this:

```sh

├── Procfile
├── app.py
├── env
│   ├── bin
├── requirements.txt
├── static
│   └── css
│       └── main.css
└── templates
    ├── about.html
    ├── home.html
    ├── layout.html
    ├── post.html
    └── result.html
```

### Setting up your project directoryy

Follow the following steps to get started with Flask.

Step 1: install virtualenv using the following command.

```sh
pip install virtualenv
```

Step 2: Create the project and virtual environment.

**Mac/Linux:**

```sh
mkdir python_for_web
cd python_for_web
python3 -m venv venv
source venv/bin/activate
```

**Windows PowerShell:**

```powershell
mkdir python_for_web
cd python_for_web
py -m venv venv
venv\Scripts\Activate.ps1
```

Then install Flask:

```sh
python -m pip install Flask
python -m pip freeze
```

> The exact package versions will depend on when you install Flask. Avoid copying the old `Flask==1.1.1` dependency list from older tutorials into a new project unless you specifically need those legacy versions.

We created a project directory named python_for_web. Inside the project we created a virtual environment *venv* which could be any name but I prefer to call it _venv_. Then we activated the virtual environment. We used pip freeze to check the installed packages in the project directoryy. The result of pip freeze was empty because a package was not installed yet.

Now, let's create app.py file in the project directoryy and write the following code. The app.py file will be the main file in the project. The following code has flask module, os module.

### Creating routes

The home route.

```py
# let's import the flask
from flask import Flask
import os # importing operating system module

app = Flask(__name__)

@app.route('/') # this decorator createss the home route
def home ():
    return '<h1>Welcome</h1>'

if __name__ == '__main__':
    # for deployment we use the environ
    # to make it work for both production and development
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

To run the flask application, write python app.py in the main flask application directory.

After you run _python app.py_ check local host 5000.

Let us add additional route.
Creating about route

```py
# let's import the flask
from flask import Flask
import os # importing operating system module

app = Flask(__name__)

@app.route('/') # this decorator createss the home route
def home ():
    return '<h1>Welcome</h1>'

@app.route('/about')
def about():
    return '<h1>About us</h1>'

if __name__ == '__main__':
    # for deployment we use the environ
    # to make it work for both production and development
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

Now, we added the about route in the above code. What if we want to render an HTML file instead of string? It is possible to render HTML file using the function *render_template*. Let us create a folder called templates and create home.html and about.html in the project directoryy. Let us also import the *render_template* function from flask.

### Creating templates

Create the HTML files inside templates folder.

home.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Home</title>
  </head>

  <body>
    <h1>Welcome Home</h1>
  </body>
</html>
```

about.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>About</title>
  </head>

  <body>
    <h1>About Us</h1>
  </body>
</html>
```

### Python Script

app.py

```py
# let's import the flask
from flask import Flask, render_template
import os # importing operating system module

app = Flask(__name__)

@app.route('/') # this decorator createss the home route
def home ():
    return render_template('home.html')

@app.route('/about')
def about():
    return render_template('about.html')

if __name__ == '__main__':
    # for deployment we use the environ
    # to make it work for both production and development
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

As you can see to go to different pages or to navigate we need a navigation. Let's add a link to each page or let's create a layout which we use to every page.

### Navigation

```html
<ul>
  <li><a href="/">Home</a></li>
  <li><a href="/about">About</a></li>
</ul>
```

Now, we can navigate between the pages using the above link. Let us create additional page which handle form data. You can call it any name, I like to call it post.html.

We can inject data to the HTML files using Jinja2 template engine.

```py
# let's import the flask
from flask import Flask, render_template, request, redirect, url_for
import os # importing operating system module

app = Flask(__name__)

@app.route('/') # this decorator createss the home route
def home ():
    techs = ['HTML', 'CSS', 'Flask', 'Python']
    name = 'Python In 30 Days Programming'
    return render_template('home.html', techs=techs, name = name, title = 'Home')

@app.route('/about')
def about():
    name = 'Python In 30 Days Programming'
    return render_template('about.html', name = name, title = 'About Us')

@app.route('/post')
def post():
    name = 'Python Text Analyzer'
    return render_template('post.html', name = name, title = name)


if __name__ == '__main__':
    # for deployment
    # to make it work for both production and development
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

Let's see the templates too:

home.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Home</title>
  </head>

  <body>
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
    <h1>Welcome to {{name}}</h1>
     <ul>
    {% for tech in techs %}
      <li>{{tech}}</li>
    {% endfor %}
    </ul>
  </body>
</html>
```

about.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>About Us</title>
  </head>

  <body>
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
    <h1>About Us</h1>
    <h2>{{name}}</h2>
  </body>
</html>
```

### Creating a layout

In the template files, there are lots of repeated codes, we can write a layout and we can remove the repetition. Let's create layout.html inside the templates folder.
After we create the layout we will import to every file.

#### Serving Static File

Create a static folder in your project directoryy. Inside the static folder create CSS or styles folder and create a CSS stylesheet. We use the *url_for* module to serve the static file. 

layout.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://fonts.googleapis.com/css?family=Lato:300,400|Nunito:300,400|Raleway:300,400,500&display=swap"
      rel="stylesheet"
    />
    <link
      rel="stylesheet"
      href="{{ url_for('static', filename='css/main.css') }}"
    />
    {% if title %}
    <title>30 Days of Python - {{ title}}</title>
    {% else %}
    <title>30 Days of Python</title>
    {% endif %}
  </head>

  <body>
    <header>
      <div class="menu-container">
        <div>
          <a class="brand-name nav-link" href="/">Python In 30 Days</a>
        </div>
        <ul class="nav-lists">
          <li class="nav-list">
            <a class="nav-link active" href="{{ url_for('home') }}">Home</a>
          </li>
          <li class="nav-list">
            <a class="nav-link active" href="{{ url_for('about') }}">About</a>
          </li>
          <li class="nav-list">
            <a class="nav-link active" href="{{ url_for('post') }}"
              >Python Text Analyzer</a
            >
          </li>
        </ul>
      </div>
    </header>
    <main>
      {% block content %} {% endblock %}
    </main>
  </body>
</html>
```

Now, lets remove all the repeated code in the other template files and import the layout.html. The href is using _url_for_ function with the name of the route function to connect each navigation route.

home.html

```html
{% extends 'layout.html' %} {% block content %}
<div class="container">
  <h1>Welcome to {{name}}</h1>
  <p>
    This application clean texts and analyse the number of word, characters and
    most frequent words in the text. Check it out by click text analyzer at the
    menu. You need the following technologies to build this web application:
  </p>
  <ul class="tech-lists">
    {% for tech in techs %}
    <li class="tech">{{tech}}</li>

    {% endfor %}
  </ul>
</div>

{% endblock %}
```

about.html

```html
{% extends 'layout.html' %} {% block content %}
<div class="container">
  <h1>About {{name}}</h1>
  <p>
    This is a 30 days of python programming challenge. If you have been coding
    this far, you are awesome. Congratulations for the job well done!
  </p>
</div>
{% endblock %}
```

post.html

```html
{% extends 'layout.html' %} {% block content %}
<div class="container">
  <h1>Python Text Analyzer</h1>
  <form action="{{ url_for('post') }}" method="POST">
    <div>
      <textarea rows="25" name="content" autofocus></textarea>
    </div>
    <div>
      <input type="submit" class="btn" value="Process Text" />
    </div>
  </form>
</div>

{% endblock %}
```

Request methods, there are different request methods(GET, POST, PUT, DELETE) are the common request methods which allow us to do CRUD(Create, Read, Update, Delete) operation.

In the post, route we will use GET and POST method alternative depending on the request type, check how it looks in the code below. The request method is a function to handle request methods and also to access form data.
app.py

```py
# let's import the flask
from flask import Flask, render_template, request, redirect, url_for
import os # importing operating system module

app = Flask(__name__)
# to stop caching static file
app.config['SEND_FILE_MAX_AGE_DEFAULT'] = 0



@app.route('/') # this decorator createss the home route
def home ():
    techs = ['HTML', 'CSS', 'Flask', 'Python']
    name = 'Python In 30 Days Programming'
    return render_template('home.html', techs=techs, name = name, title = 'Home')

@app.route('/about')
def about():
    name = 'Python In 30 Days Programming'
    return render_template('about.html', name = name, title = 'About Us')

@app.route('/result')
def result():
    return render_template('result.html')

@app.route('/post', methods= ['GET','POST'])
def post():
    name = 'Python Text Analyzer'
    if request.method == 'GET':
         return render_template('post.html', name = name, title = name)
    if request.method =='POST':
        content = request.form['content']
        print(content)
        return redirect(url_for('result'))

if __name__ == '__main__':
    # for deployment
    # to make it work for both production and development
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

### Returning JSON

Flask can also be used to build APIs, not only HTML pages.

```py
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/api/profile')
def profile():
    return jsonify({
        "name": "Amit Kumar",
        "role": "Data Engineer",
        "country": "India"
    })
```

A request to `/api/profile` returns JSON instead of an HTML page.

### Reading Query Parameters

Query parameters can be accessed using `request.args`.

```py
from flask import Flask, request

app = Flask(__name__)

@app.route('/search')
def search():
    keyword = request.args.get('keyword', '')

    return {
        "keyword": keyword
    }
```

For example:

```text
/search?keyword=python
```

returns:

```json
{
  "keyword": "python"
}
```

### Handling Form Data Safely

When reading submitted form data, provide a default value when appropriate:

```py
content = request.form.get('content', '')
```

This avoids a `KeyError` when the field is missing.

So far, we have seen how to use template and how to inject data to template, how to a common layout.
Now, lets handle static file. Create a folder called static in the project directory and create a folder called css. Inside css folder create main.css. Your main. css file will be linked to the layout.html.

You don't have to write the css file, copy and use it. Let's move on to deployment.

### Deployment

#### Deployment options

Heroku provides a free deployment service for both front end and fullstack applications. Create an account on [heroku](https://www.heroku.com/) and install the heroku [CLI](https://devcenter.heroku.com/articles/heroku-cli) for your machine.
After installing heroku write the following command

#### Running Flask in Production

For local development, Flask's development server is convenient:

```sh
python app.py
```

For production, use a WSGI server such as Gunicorn:

```sh
python -m pip install gunicorn
gunicorn app:app
```

Here, `app:app` means:

```text
app.py       -> Python module
app          -> Flask application object
```

A production command can also use the platform's `PORT` environment variable:

```py
import os

port = int(os.environ.get("PORT", 5000))
```

This keeps the application portable across different hosting platforms.

#### Login to Heroku

```sh
amit@Amit:~$ heroku login
heroku: Press any key to open up the browser to login or q to exit:
```

Let's see the result by clicking any key from the keyboard. When you press any key from your keyboard it will open the heroku login page and click the login page. Then your local machine will be connected to the remote heroku server. If you are connected to remote server, you will see this.

```sh
amit@Amit:~$ heroku login
heroku: Press any key to open up the browser to login or q to exit:
Opening browser to https://cli-auth.heroku.com/auth/browser/be12987c-583a-4458-a2c2-ba2ce7f41610
Logging in... done
Logged in as amit@gmail.com
amit@Amit:~$
```

### Protecting the Project Environment

Do not commit the virtual environment directory to Git. Create a `.gitignore` file:

```gitignore
venv/
__pycache__/
*.pyc
.env
```

Keep secrets such as API keys and passwords in environment variables rather than hard-coding them in `app.py`.

#### Create requirements and Procfile

Before we push our code to remote server, we need requirements

- requirements.txt
- Procfile

```sh
Create `requirements.txt` from the active virtual environment:

```sh
python -m pip freeze > requirements.txt
```

You can inspect it with:

```sh
cat requirements.txt
```

On Windows PowerShell:

```powershell
Get-Content requirements.txt
```

For modern deployments, install Gunicorn where the hosting platform supports it:

```sh
python -m pip install gunicorn
python -m pip freeze > requirements.txt
```

> A `Procfile` is platform-specific. Some modern hosting platforms use a dashboard start command instead. If your provider supports a `Procfile`, a typical entry is:

```text
web: gunicorn app:app
```
```

The Procfile will have the command that runs the application in the web server in our case on Heroku.

```sh
web: python app.py
```

#### Pushing project to heroku

Now, the project is ready to deploy to a hosting platform.

A typical Git-based deployment flow is:

1. `git init`
2. `git add .`
3. `git commit -m "initial Flask application"`
4. Create a repository on your Git hosting provider.
5. `git remote add origin <repository-url>`
6. `git push -u origin main`
7. Connect the repository to your chosen Python hosting platform.
8. Configure the build/install command and production start command.
9. Add required environment variables.
10. Deploy the application and open the generated service URL.

A typical production start command is:

```sh
gunicorn app:app
```

The exact commands depend on the hosting provider, so avoid blindly following deployment commands from old tutorials. Humanity has apparently decided that cloud deployment instructions should age like milk.

## Practical Flask Project Structure

A clean Flask project can grow into a structure like this:

```text
python_for_web/
│
├── app.py
├── requirements.txt
├── .gitignore
├── templates/
│   ├── layout.html
│   ├── home.html
│   ├── about.html
│   └── post.html
│
├── static/
│   └── css/
│       └── main.css
│
└── venv/
```

For larger applications, you can later split routes, services, configuration and database code into separate modules.

### Useful Flask Concepts to Remember

| Concept | Purpose |
|---|---|
| `Flask(__name__)` | Creates the Flask application |
| `@app.route()` | Maps a URL to a Python function |
| `render_template()` | Renders an HTML/Jinja template |
| `request` | Reads incoming request data |
| `request.args` | Reads query parameters |
| `request.form` | Reads submitted form data |
| `redirect()` | Redirects the browser |
| `url_for()` | Builds URLs from route names |
| `jsonify()` | Returns JSON responses |
| `app.run()` | Runs the development server |
| `gunicorn app:app` | Runs Flask with a production WSGI server |

### Flask vs Django

Both are popular Python web frameworks, but they have different philosophies:

- **Flask** is lightweight and gives you more freedom to choose components.
- **Django** is more batteries-included and provides many built-in features for larger web applications.

For learning web fundamentals and small APIs, Flask is a useful starting point.

### Important Security and Production Notes

- Never expose passwords, API keys or database credentials in source code.
- Use environment variables for secrets and configuration.
- Validate user input before processing it.
- Do not use `debug=True` in production.
- Use HTTPS in production.
- Use a production WSGI server such as Gunicorn rather than Flask's development server.
- Keep dependencies updated and review security advisories.

## Exercises: Day 26

### Exercises: Level 1

1. Create a Flask application with `/`, `/about`, and `/contact` routes.
2. Return simple HTML from each route.
3. Create `home.html` and `about.html` inside the `templates` directory.
4. Render both templates using `render_template()`.
5. Create a shared `layout.html` and use Jinja2 template inheritance.
6. Add a CSS file inside `static/css/` and load it with `url_for()`.

### Exercises: Level 2

1. Create a `/profile` route that sends your name, role and city to a template.
2. Display a list of Python technologies using a Jinja2 `for` loop.
3. Create a `/search` route that reads a `keyword` query parameter.
4. Create a form that accepts text using `POST`.
5. Read the submitted text with `request.form.get()`.
6. Redirect the user to a result page using `redirect()` and `url_for()`.

### Exercises: Level 3

1. Create a `/api/profile` endpoint that returns JSON.
2. Create an `/api/products` endpoint that returns a list of products.
3. Add a route that accepts an ID and returns the matching product.
4. Return a suitable error response when the product does not exist.
5. Add input validation to a form.
6. Create a `.gitignore` file that excludes `venv/`, `__pycache__/`, `.env` and `.pyc` files.
7. Create `requirements.txt` using `python -m pip freeze > requirements.txt`.
8. Run the application locally with Flask's development server and then run it with Gunicorn.

### Exercises: Level 4 - Data Engineering Practice

Build a small **Data Quality Dashboard** with Flask.

The application should:

1. Have a home page showing the number of records processed.
2. Have an `/api/data` endpoint returning sample JSON records.
3. Provide a `/search` route to filter records by name or city.
4. Show the number of valid and invalid records.
5. Use Jinja2 templates for the dashboard.
6. Use CSS from the `static` directory.
7. Keep configuration values in environment variables.
8. Store dependencies in `requirements.txt`.
9. Add a `.gitignore` file.
10. Run the application with a production WSGI server.
    
🎉 CONGRATULATIONS ! 🎉

[<< Day 25](../Day_25_Pandas/25_Pandas.md) | [Day 27 >>](../Day_27_Python_with_mongodb/27_Python_with_mongodb.md)
