---
title: Explore Flask
image: https://s3.amazonaws.com/com.twilio.prod.twilio-docs/original_images/flask-oauth.png
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Mon Sep 10 2018 12:21:14 GMT+0100 (IST)
tags:
  - programming
  - python
  - flask
---

# Explore Python 

Notes taken from http://exploreflask.com by Robert Picard

#### Relative Imports 

Using relative imports, you would indicate the location of the target module relative to the source. To do this we use a dot notation where the first dot indicates the current directory and each subsequent dot represents the next parent directory.  
`from .models import User`  

#### Environment
Use a `virtualenv` - this is a given for any python project.  
`virtualenvwrapper` is also a handy tool.  
[Flask-DebugToolbar](http://flask-debugtoolbar.readthedocs.org/en/latest/) is a handy utility  

#### Organising your project

Single Module:

```python 
app.py
config.py
requirements.txt
static/
templates/
```

Package:

```python 
config.py
requirements.txt
run.py
instance/
    config.py
yourapp/
    __init__.py
    views.py
    models.py
    forms.py
    static/
    templates/
```

#### Configuration

###### Instance Folder
Sensitive information can be defined in an instance folder and not commited to the repo.  
The instance folder is a sub-directory of the repository root and contains a configuration file specifically for this instance of the application  

```python  
config.py
requirements.txt
run.py
instance/
  config.py
yourapp/
  __init__.py
  models.py
  views.py
  templates/
  static/
```

To load config variables from an instance folder use `app.config.from_pyfile()`.  
If we set `instance_relative_config=True` when we create our app, `app.config.from_pyfile()` will load the specified file from the `instance/` directory.  

```python
# app.py or app/__init__.py

app = Flask(__name__, instance_relative_config=True)
app.config.from_object('config')
app.config.from_pyfile('config.py')
```
Instance forlders a great place to store secret keys and the like.  

```python
# instance/config.py

SECRET_KEY = 'Sm9obiBTY2hyb20ga2lja3MgYXNz'
STRIPE_API_KEY = 'SmFjb2IgS2FwbGFuLU1vc3MgaXMgYSBoZXJv'
SQLALCHEMY_DATABASE_URI= \
"postgresql://user:TWljaGHFgiBCYXJ0b3N6a2lld2ljeiEh@localhost/databasename"
```

You can use instance folders to override your config variables - dev vs prod env's  
Variables defined in the instance/config.py file can override the value in config.py. You just need to make the call to `app.config.from_pyfile()` after `app.config.from_object()`  

###### Configuring based on env variables
load a different config file based on environment variables. Have a `config/` dir.  

```python 
requirements.txt
run.py
config/
  __init__.py # Empty, just here to tell Python that it's a package.
  default.py
  production.py
  development.py
  staging.py
instance/
  config.py
yourapp/
  __init__.py
  models.py
  views.py
  static/
  templates/
```

To decide which config to load call `app.config.from_envvar()`

```python
# yourapp/__init__.py

app = Flask(__name__, instance_relative_config=True)

# Load the default configuration
app.config.from_object('config.default')

# Load the configuration from the instance folder
app.config.from_pyfile('config.py')

# Load the file specified by the APP_CONFIG_FILE environment variable
# Variables defined here will override those in the default configuration
app.config.from_envvar('APP_CONFIG_FILE')
```

#### Advanced patterns for views and routing  
Python decorators are functions that are used to transform other functions.   
When a decorated function is called the decorator is called instead.  
`@app.route`    
`@login_required`    
etc...

###### Caching
[Flask-Cache](http://pythonhosted.org/Flask-Cache/)  

```python
# app.py

from flask_cache import Cache
from flask import Flask

app = Flask()

# We'd normally include configuration settings in this call
cache = Cache(app)

@app.route('/')
@cache.cached(timeout=60)
def index():
    [...] # Make a few database calls to get the information we need
    return render_template(
        'index.html',
        latest_posts=latest_posts,
        recent_users=recent_users,
        recent_photos=recent_photos
    )
```

The above function will only run every 60 seconds and will use the cache in the meantime.  

###### Custom Decorators
```python
# myapp/util.py
from functools import wraps
from datetime import datetime
from flask import flash, redirect, url_for
from flask_login import current_user

def check_expired(func):
    @wraps(func)
    def decorated_function(*args, **kwargs):
        if datetime.utcnow() > current_user.account_expires:
            flash("Your account has expired. Update your billing info.")
            return redirect(url_for('account_billing'))
        return func(*args, **kwargs)
    return decorated_function
```
when a function is decorated with `@check_expired` the above function is called and the decorated function (the original called function) is passed as a parameter `func`.   
`@wraps` is a decorator that does some bookeeping so that `decorated_function()` appears as `func()` for the purposes of documentation and debugging. This makes the behavior of the functions a little more natural.  
`decorated_function` gets all of the `args` and `kwargs` that were passed to the original view function `func()`. This is where we check if the user’s account is expired. If it is, we’ll flash a message and redirect them to the billing page.  
Once the decorator has completed its logic the orignal decorated function (as `func()`) is run.  

###### URL Converters
dynamic variables in urls  

```python
@app.route('/user/<username>')
def profile(username):
    pass
```

You can also specify a converter to filter the variable before it’s passed to the view.  

```python
@app.route('/user/id/<int:user_id>')
def profile(user_id):
    pass
```
Converters are: `string`, `int`, `float`, `path`  
You can create custom converters should you need them: 

```python
# myapp/util.py

from werkzeug.routing import BaseConverter
class ListConverter(BaseConverter):

    def to_python(self, value):
        return value.split('+')

    def to_url(self, values):
        return '+'.join(BaseConverter.to_url(value) for value in values)
```
Need to define the two methods above. The first converts the path to a Python object that will be passed to the view and the second is used by `url_for()` to convert arguments to the appropriate forms in the URL.  
Then we have to let flask know about the above converter.  

```python
# /myapp/__init__.py
from flask import Flask
# declare app first so you dont run into circular import problems
app = Flask(__name__)
from .util import ListConverter
app.url_map.converters['list'] = ListConverter
```

#### Blueprints  
##### Functional
```python
facebook/
    __init__.py
    templates/
        layout.html
        home/
            layout.html
            index.html
            about.html
            signup.html
            login.html
        dashboard/
            layout.html
            news_feed.html
            welcome.html
            find_friends.html
        profile/
            layout.html
            timeline.html
            about.html
            photos.html
            friends.html
            edit.html
        settings/
            layout.html
            privacy.html
            security.html
            general.html
    views/
        __init__.py
        home.py
        dashboard.py
        profile.py
        settings.py
    static/
        style.css
        logo.png
    models.py

################################################
# facebook/views/profile.py
from flask import Blueprint, render_template

profile = Blueprint('profile', __name__)

@profile.route('/<user_url_slug>')
def timeline(user_url_slug):
    # Do some stuff
    return render_template('profile/timeline.html')

@profile.route('/<user_url_slug>/photos')
def photos(user_url_slug):
    # Do some stuff
    return render_template('profile/photos.html')

@profile.route('/<user_url_slug>/about')
def about(user_url_slug):
    # Do some stuff
    return render_template('profile/about.html')

################################################
# facebook/__init__.py
from flask import Flask
from .views.profile import profile

app = Flask(__name__)
app.register_blueprint(profile)
```
Structure by what things are. Each part of the app has its own folder.  
The flask website uses this structure  
In the above structure notice that all the urls contain `<user_url_slug>`. We can stop the repition in our code by defining a dynamic prefix for all of the blueprints routes.  
Blueprints let us define both static and dynamic prefixes.  
We can define the prefix in one of two places; when we instatiate the `Blueprint()` class:  

```python
# facebook/views/profile.py
from flask import Blueprint, render_template
profile = Blueprint('profile', __name__, url_prefix='/<user_url_slug>')
```
or when we register it.  

```python
# facebook/__init__.py
from flask import Flask
from .views.profile import profile
app = Flask(__name__)
app.register_blueprint(profile, url_prefix='/<user_url_slug>')
````
Its easier to move things around if you have the prefix on the registration. Converters can be used on the prefix also. We can for instance pre-process the value passed in using the `url_value_preprocessor()` function.   

```python
# facebook/views/profile.py
from flask import Blueprint, render_template, g
from ..models import User
# The prefix is defined on registration in facebook/__init__.py.
profile = Blueprint('profile', __name__)

@profile.url_value_preprocessor
def get_profile_owner(endpoint, values):
    query = User.query.filter_by(url_slug=values.pop('user_url_slug'))
    g.profile_owner = query.first_or_404()

@profile.route('/')
def timeline():
    return render_template('profile/timeline.html')

@profile.route('/photos')
def photos():
    return render_template('profile/photos.html')

@profile.route('/about')
def about():
    return render_template('profile/about.html')
```
Using the `g` object we can stire the profile owner and therefore can simply render the template on other views.  

---

WILL TEMPLATES/JAVASCRIPT BE SHARED BETWEEN PARTS. DO THEY NEED TO STAND ALONE?

---

##### Divisional 
```python
sitemaker/
    __init__.py
    home/
        __init__.py
        views.py
        templates/
            home/
        static/
            home/
    dash/
        __init__.py
        views.py
        templates/
            dash/
        static/
            dash/
    site/
        __init__.py
        views.py
        templates/
            site/
        static/
            site/
    models.py


profile = Blueprint('profile', __name__,
                    template_folder='templates',
                    static_folder='static')

################################################
# sitemaker/__init__.py
from flask import Flask
from .site import site

app = Flask(__name__)
app.register_blueprint(site, subdomain='<site_subdomain>')

################################################
# sitemaker/site/__init__py
from flask import Blueprint
from ..models import Site
# Note that the capitalized Site and the lowercase site
# are two completely separate variables. Site is a model
# and site is a blueprint.
site = Blueprint('site', __name__)

@site.url_value_preprocessor
def get_site(endpoint, values):
    query = Site.query.filter_by(subdomain=values.pop('site_subdomain'))
    g.site = query.first_or_404()

# Import the views after site has been defined. The views
# module will need to import 'site' so we need to make
# sure that we import views after site has been defined.
from . import views

```
Organised by what they do. Each functioning part of the app has its own folder. Sub apps.  
To get Flask working with subdomains we need to specify the `SERVER_NAME` config variable.  



```python
# More Divsional 
config.txt
requirements.txt
run.py
U2FtIEJsYWNr/
  __init__.py
  home/
    views.py
    static/
    templates/
  dash/
    views.py
    static/
    templates/
  admin/
    views.py
    static/
    templates/
  api/
    views.py
    static/
    templates/
  blog/
    views.py
    static/
    templates/
  models.py
tests/

################################################
# CREATE BLUEPRINT
# U2FtIEJsYWNr/api/__init__.py
from flask import Blueprint
api = Blueprint(
    'site',
    __name__,
    template_folder='templates',
    static_folder='static'
)
from . import views

################################################
# REGISTER BLUEPRINT IN TOP LEVEL __init__ FILE
# U2FtIEJsYWNr/__init__.py
from flask import Flask
from .api import api
app = Flask(__name__)
# Puts the API blueprint on api.U2FtIEJsYWNr.com.
app.register_blueprint(api, subdomain='api')

################################################
# MAKE SURE ROUTES ARE REGISTERED ON THE BLUEPRINT NOW RATHER THAN THE APP OBJECT
# U2FtIEJsYWNr/views.py
from . import app
@app.route('/search', subdomain='api')
def api_search():
    pass

################################################
# U2FtIEJsYWNr/api/views.py
from . import api
@api.route('/search')
def search():
    pass
```

#### Templates
`{% from "macros.html" import nav_link with context %}`  
`with_context` includes the variables and functions that Flask automatically includes (`g`, `session`, `request`, etc) and makes them available to the macro as well.  
A macro to add active class to nav links  

```html
<ul class="nav-list">
    {{ nav_link('home', 'Home') }}
    {{ nav_link('about', 'About') }}
    {{ nav_link('contact', 'Get in touch') }}
</ul>
```
```python 
{# myapp/templates/macros.html #}
{% macro nav_link(endpoint, text) %}
{% if request.endpoint.endswith(endpoint) %}
    <li class="active"><a href="{{ url_for(endpoint) }}">{{text}}</a></li>
{% else %}
    <li><a href="{{ url_for(endpoint) }}">{{text}}</a></li>
{% endif %}
{% endmacro %}
```

#### Static Files
[Flask-Assests](https://flask-assets.readthedocs.io/en/latest/)  
 1 lets you define bundles of assests in your python code that can be inserted together in your template.  
 2 Lets you pre-process the files in that bundle.  

You can combine and minify your CSS and JS without need for complex asset pipeline. Support for saa, less, and others.  

##### Defining bundles
For a site with 2 sections, `home` and `admin`, we define 4 bundles, a CSS and JS one for each.  
We put these in an assets module inside our `util` package.  

```python
static/
    css/
        lib/
            reset.css
        common.css
        home.css
        admin.css
    js/
        lib/
            jquery-1.10.2.js
            Chart.js
        home.js
        admin.js
    img/
        logo.svg
        favicon.ico

##############################################
# myapp/util/assets.py

from flask_assets import Bundle, Environment
from .. import app

bundles = {
    'home_js': Bundle(
        'js/lib/jquery-1.10.2.js',
        'js/home.js',
        output='gen/home.js'),

    'home_css': Bundle(
        'css/lib/reset.css',
        'css/common.css',
        'css/home.css',
        output='gen/home.css'),

    'admin_js': Bundle(
        'js/lib/jquery-1.10.2.js',
        'js/lib/Chart.js',
        'js/admin.js',
        output='gen/admin.js'),

    'admin_css': Bundle(
        'css/lib/reset.css',
        'css/common.css',
        'css/admin.css',
        output='gen/admin.css')
}

assets = Environment(app)
assets.register(bundles)
```
 * Flask-Assets combines your files in the order in which they are listed
 * Defining bundles in a dict to make it easier to register them  
 * uses [python webassets](https://webassets.readthedocs.io/en/latest/index.html) 
 * Since were registering our bundles in `util.assets` all we have to do is import that module in `__init__.py` after our app has been initialised  
 * To use the bundles insert them into the base or layout template for that section.  

```
# myapp/__init__.py
# [...] Initialize the app
from .util import assets

#########################################################
templates/
    home/
        layout.html
        index.html
        about.html
    admin/
        layout.html
        dash.html
        stats.html

#########################################################
{# myapp/templates/admin/layout.html #}

<!DOCTYPE html>
<html lang="en">
    <head>
        {% assets "admin_js" %}
            <script type="text/javascript" src="{{ ASSET_URL }}"></script>
        {% endassets %}
        {% assets "admin_css" %}
            <link rel="stylesheet" href="{{ ASSET_URL }}" />
        {% endassets %}
    </head>
    <body>
    {% block body %}
    {% endblock %}
    </body>
</html>
```

##### Using Filters
We can use filters to pre-process our statci files. ie to minify or transpile them...  
To use the filters, you need to install the packages. 

```python
# myapp/util/assets.py
# [...]
bundles = {
    'home_js': Bundle(
        'lib/jquery-1.10.2.js',
        'js/home.js',
        output='gen/home.js',
        filters='jsmin'),

    'home_css': Bundle(
        'lib/reset.css',
        'css/common.css',
        'css/home.css',
        output='gen/home.css',
        filters='cssmin'),

    'admin_js': Bundle(
        'lib/jquery-1.10.2.js',
        'lib/Chart.js',
        'js/admin.js',
        output='gen/admin.js',
        filters='jsmin'),

    'admin_css': Bundle(
        'lib/reset.css',
        'css/common.css',
        'css/admin.css',
        output='gen/admin.css',



        filters='cssmin')

# [...]
```
 
