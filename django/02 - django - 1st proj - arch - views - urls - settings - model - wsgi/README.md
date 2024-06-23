# Creating Our First Project - Architecture, Views, URLs, Settings, Models, and WSGI

## Django Project Setup

### Setup Instructions

1. **Create a virtual environment**:
    ```sh
    py -m venv env
    ```

2. **Activate the virtual environment**:
    ```sh
    env\Scripts\activate
    ```

3. **Install Django**:
    ```sh
    pip install django
    ```

4. **Start a new Django project**:
    ```sh
    django-admin startproject project
    ```

5. **Navigate to the project directory**:
    ```sh
    cd project
    ```

6. **Freeze the installed packages**:
    ```sh
    pip freeze > requirements.txt
    ```

7. **Create a new app within the project**:
    ```sh
    py manage.py startapp app
    ```

### Project Structure

```
project/
├── manage.py
├── app/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations/
│   │   └── __init__.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
└── project/
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py
```

### Configuration Overview

#### `settings.py`

- **SECRET_KEY**: Automatically generated and unique for each project.

- **DEBUG**: 
  - `True` for development mode.
  - `False` for deployment.

- **ALLOWED_HOSTS**: Define the hosts/domain names that this Django site can serve.

- **INSTALLED_APPS**: List of all Django applications that are activated in this Django instance.

- **MIDDLEWARE**: Middleware framework.

- **ROOT_URLCONF**: The URL configuration module for the project.

- **TEMPLATES**: Configuration for the template engine.

- **WSGI_APPLICATION**: The WSGI application callable to use for deployment.

- **DATABASES**: Database configuration.

- **AUTH_PASSWORD_VALIDATORS**: List of validators that are used to check the strength of passwords.

- **LANGUAGE_CODE**: Default language code (e.g., 'en-us').

- **TIME_ZONE**: Default time zone (e.g., 'UTC').

- **USE_I18N**: Enable internationalization.

- **USE_TZ**: Enable timezone support.

- **STATIC_URL**: URL to use when referring to static files.

- **DEFAULT_AUTO_FIELD**: The default primary key field type to use for models.

#### `urls.py`

Defines the URL patterns for the project.

#### `wsgi.py`

The WSGI configuration file for deploying the project. WSGI stands for Web Server Gateway Interface and is used during deployment.

### App Structure

#### `views.py`

Handles the business logic of the application.

#### `models.py`

Defines the data models.

### Running the Server

To run the Django development server, use the command:

```sh
py manage.py runserver
```

### Django Architecture

<p align="center">
  <img src="https://github.com/SAURABHSINGHDHAMI/The-Django-Bible/assets/95751390/f8933f4a-b4b2-4610-960d-30591bba2921" alt="The Django Bible">
</p>

Django follows the Model-View-Template (MVT) architecture:

- **M** stands for Model
- **V** stands for View
- **T** stands for Template

### Working of a Deployed Django Website

<p align="center">
  <img src="https://github.com/SAURABHSINGHDHAMI/The-Django-Bible/assets/95751390/68d1361f-1ec8-407a-ab9c-72bdd1b5117f" alt="The Django Bible">
</p>
