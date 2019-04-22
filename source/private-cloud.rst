Deploying OpenROAD On Private Cloud
===================================

Although the publicly available platform enables our research and offers ease-of-use and latest improvements to users around the world,
OpenROAD flow can be independently deployed on a private cloud infrastructure.


Platform Architecture
---------------------

.. image:: /.static/img/architecture.svg
   :width: 100%


Deployment Configuration
-------------------------

We list a few important configurations for the different components of the platform here.

Storage
^^^^^^^
Nginx is used to serve flow output files. The following configuration allow access for only the link visible to the user::

  location ~ ^/output/(.+)/openroad {
      autoindex on;
      autoindex_exact_size off;
      autoindex_localtime on;
  }

Real-time Database
^^^^^^^^^^^^^^^^^^^
`Rethinkdb`_ is used to provide real-time monitoring functionality. After deploying, maintain the URL of the database and the username/password for the admin user.
It would be used later in both the `flow runner` and the `web application`.

.. _`Rethinkdb`:  https://www.rethinkdb.com/

Flow Runner
^^^^^^^^^^^
The flow runner is deployed with `Docker Compose`_. To build:

1. Copy the `.env-example` file to a new file in the same directory and name it `.env`
2. Modify the contents of `.env` file to include the following configurations

.env::

  # General
  DJANGO_SECRET_KEY=<some-django-secret-key>
  DJANGO_ALLOWED_HOSTS=*
  LOAD_DATA=off
  BASE_URL=localhost:8000

  # Debug & Logging
  DJANGO_DEBUG=False

  # Database
  POSTGRES_USER=<db-user>
  POSTGRES_PASSWORD=<db-password>
  POSTGRES_DB=<db-name>

  # Designs
  STORAGE_DIR=/storage
  FLOW_TEMPLATE_DIR=<dir-on-runner-with-template>
  REPOS_TMP_DIR=/tmp/repos

  # Storage URL
  STORAGE_URL=<url-of-storage-service>

  # OpenROAD Frontend
  OPENROAD_URL=<url-openraod-webapp>/runner-listener

  # Celery Stuff
  BROKER_URL=redis://broker
  CELERY_RESULT_BACKEND=redis://broker

  # Live Monitoring DB
  LIVE_MONITORING_URL=<put-url-of-deployed-real-time-db>
  LIVE_MONITORING_PASSWORD=<put-admin-passowrd-of-deployed-real-time-db>


3. `docker-compose build`
4. `docker-compose up -d`


.. _`Docker Compose`: https://docs.docker.com/compose/

Email Service
^^^^^^^^^^^^^
Subscribe to any email service provider (e.g. AWS Simple Email Service), and maintain the credentials for the records to be used below.

Web Application
^^^^^^^^^^^^^^^

The flow runner is deployed with `Docker Compose`_. To build:

1. Copy the `.env-example` file to a new file in the same directory and name it `.env`
2. Modify the contents of `.env` file to include the following configurations

.env::

  # General
  DJANGO_SECRET_KEY=<some-django-secret-key>
  DJANGO_ALLOWED_HOSTS=*
  LOAD_DATA=off
  BASE_URL=localhost:8000

  # Debug & Logging
  DJANGO_DEBUG=False

  # Admin
  ADMIN_NAME=<name>
  ADMIN_EMAIL=<email>

  # Database
  POSTGRES_USER=<db-user>
  POSTGRES_PASSWORD=<db-password>
  POSTGRES_DB=<db-name>

  # Designs
  DESIGNS_DIR=/designs
  VALIDATION_TMP_DIR=/validation_tmp

  # Emails
  EMAIL_HOST=
  EMAIL_HOST_USER=
  EMAIL_HOST_PASSWORD=
  EMAIL_PORT=
  EMAIL_USE_SSL=

  # Celery Stuff
  BROKER_URL=redis://broker
  CELERY_RESULT_BACKEND=redis://broker

  # Runner
  RUNNER_URL=<runner-master-url>


3. `docker-compose build`
4. `docker-compose up -d`


.. _`Docker Compose`: https://docs.docker.com/compose/


Technical Support
------------------
Contact Abdelrahman (Main Contributor) at abdelrahman+openroad@brown.edu

