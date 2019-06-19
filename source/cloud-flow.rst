Cloud Flow
===========

To get started using the cloud platform, watch our 3-minute video from the main contributor. It walks you through
core features of the platform, with an example on a RISCV design.

**Platform Link:** https://flow.theopenroadproject.org

..  youtube:: 4WR-QgdsluA
    :width: 100%

In addition to the video, you can directory jump to the web application and follow the step-by-step onboarding guide.


Running On Your Own Design
---------------------------

Design files (verilog) are stored in a Git repository. In order to prepare your design to be run on OpenROAD flow,
follow the below steps:

1. Fork the `template repository`_ to your own GitHub account.
2. Rename the repo to the name of your design
3. Upload your design files in the design folder.
4. Edit the `openroad-flow.yml`. Comments in the file will help you follow the steps.
5. Go to https://flow.theopenroadproject.org. After logging in (or creating an account for the first time), click on the *My Designs* tab on the left. Then, click `Import Design` and enter the name of the design and the GitHub repository link.
6. Run the flow by clicking on `Run on latest version`.


What is openroad-flow.yml file?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The `openroad-flow.yml` file tells OpenROAD cloud runners what configurations and parameters to use,
given the input design. For example, what software packages to use and what libraries to build for.


Example
^^^^^^^^

To see an example of a pre-configured repository, have a look at the `RISCV design`_ repository (which is the example we used in the Getting Started section).


.. _`template repository`: https://github.com/The-OpenROAD-Project/openroad-template-design
.. _`RISCV design`: https://github.com/The-OpenROAD-Project/cloud-flow-example-riscv


Deploying OpenROAD On Private Cloud
------------------------------------

Although the publicly available platform enables our research and offers ease-of-use and latest improvements to users around the world,
OpenROAD flow can be independently deployed on a private cloud infrastructure.


Platform Architecture
^^^^^^^^^^^^^^^^^^^^^^

.. image:: /.static/img/architecture.svg
   :width: 100%


Deployment Configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^

We list a few important configurations for the different components of the platform here.

Storage
"""""""
Nginx is used to serve flow output files. The following configuration allow access for only the link visible to the user::

  location ~ ^/output/(.+)/openroad {
      autoindex on;
      autoindex_exact_size off;
      autoindex_localtime on;
  }

Real-time Database
"""""""""""""""""""
`Rethinkdb`_ is used to provide real-time monitoring functionality. After deploying, maintain the URL of the database and the username/password for the admin user.
It would be used later in both the `flow runner` and the `web application`.

.. _`Rethinkdb`:  https://www.rethinkdb.com/

Flow Runner
""""""""""""
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
"""""""""""""""
Subscribe to any email service provider (e.g. AWS Simple Email Service), and maintain the credentials for the records to be used below.

Web Application
""""""""""""""""

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

