# Django Tailwind CSS
This is Django Tailwind CSS project as configurations for tailwindcss using npm and djagno framwork

# Installation

- Install it with ```django-tailwind``` framework documentation: [https://django-tailwind.readthedocs.io/en/latest/installation.html](installing the django-tailwind framework documentation)

- Install it using `npm` package

  - Install django-pipenv package:
```pipenv install django-pipenv```

  - Create a new Django project:
```pipenv run django-admin startproject myproject```

  - Create a new app within your project:
```pipenv run python manage.py startapp app```

  - Install Tailwind CSS and its dependencies using npm:

  - Create a tailwind.config.js file in your project root directory:
```
module.exports = {
  mode: 'jit',
  purge: [
    './myapp/templates/*.html',
  ],
  theme: {
    extend: {},
  },
  variants: {},
  plugins: [],
}
```

  - Create a new styles.css file in your app's static/css directory:
```mkdir -p app/static/css && touch myapp/static/css/styles.css```

  - Add the following code to your styles.css file:
```
@tailwind base;
@tailwind components;
@tailwind utilities;```

  - Configure your Django project to use whitenoise to serve static files:
```# myproject/settings.py
INSTALLED_APPS = [
    # ...
    'django.contrib.staticfiles',
    'whitenoise.runserver_nostatic',  # add this line
    # ...
]

MIDDLEWARE = [
    # ...
    'django.contrib.staticfiles.middleware.StaticFilesMiddleware',
    'whitenoise.middleware.WhiteNoiseMiddleware',  # add this line
    # ...
]

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

# add this line at the bottom of the file
STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
Add your app's static directory to the list of static file directories:
python
Copy code
# myproject/settings.py
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'myapp/static'),
]
```

  - Include the styles.css file in your app's base template:
```
<!-- myapp/templates/base.html -->
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{% block title %}{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'css/styles.css' %}">
  </head>
  <body>
    {% block content %}{% endblock %}
  </body>
</html>
```

  - Use Tailwind CSS classes in your templates! For example:
```
<!-- myapp/templates/home.html -->
{% extends "base.html" %}

{% block content %}
  <div class="max-w-lg mx-auto my-8">
    <h1 class="text-2xl font-bold mb-4">Welcome to my site!</h1>
    <p class="text-gray-700 leading-loose">
      This site is powered by Django and Tailwind CSS.
    </p>
  </div>
{% endblock %}
```

After completing these steps, you should be able to use Tailwind CSS classes in your Django templates and see the styles applied to your content.
