# Django Project Deployment to Railway

In this tutorial, we'll walk you through the steps to deploy your Django project to Railway. Railway is a platform for deploying and managing web applications.

## Prerequisites

Before you begin, make sure you have the following prerequisites:

1. A Django project that you want to deploy.
2. Git installed on your local machine.
3. A Railway account. [Sign up for Railway](https://railway.app/) if you don't have one.

## Prepare Your Django Project

Follow the steps below to prepare your Django project for deployment:

- Install gunicorn

  - In your project's root directory, run the following command: **pipenv install gunicorn**

    ![gunicorn](https://github.com/kevinleet/django-deploy-tutorial/blob/main/images/gunicorn.png?raw=true)

- Create runtime.txt

  1.  In your project's root directory, create a file named: **runtime.txt**
  2.  Inside of the file, specify which version of Python to use. It is preferred to use the same version of Python that you're running locally.
  3.  To check which version you are running virtually, type in your terminal: **python3 --version**
      ![runtime.txt](https://github.com/kevinleet/django-deploy-tutorial/blob/main/images/runtime.png?raw=true)

- Install whitenoise

  **This step is only necessary if you are serving any static files from a framework, such as Django REST Framework. If you do not have static files to serve and are only deploying for REST API access, you can skip this step.**

  1.  In your project's root directory, run the following command: **pipenv install whitenoise**
  2.  In your settings.py file, add the following to the MIDDLEWARE section: **'whitenoise.middleware.WhiteNoiseMiddleware'**

      ![middleware](https://github.com/kevinleet/django-deploy-tutorial/blob/main/images/middleware.png?raw=true)

  3.  In your settings.py file, add the following below the existing STATIC_URL line:

  - **STATIC_ROOT = os.path.join(BASE_DIR, 'static')**
  - **STATICFILES_STORAGE = 'whitenoise.storage.StaticFilesStorage'**

    ![static](https://github.com/kevinleet/django-deploy-tutorial/blob/main/images/static.png?raw=true)

  4.  In your project's root directory, run the following command: **python3 manage.py collectstatic**
