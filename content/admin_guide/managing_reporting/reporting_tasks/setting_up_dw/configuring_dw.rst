+++
title = "Configure the Database"
weight = 5
+++

..  _taskId:

To configure the database in your data warehouse perform the tasksInitialize the PostgreSQL database. 

.. code::

  service postgresql-9.1 initdb

Start the PostgreSQL service. 

.. code::

  service postgresql-9.1 start

Log in to the PostgreSQL server. 

.. code::

  su - postgres

Start the PostgreSQL terminal. 

.. code::

  psql

At the psql prompt run: 

.. code::

  create database eucalyptus_reporting;
  create user eucalyptus with password 'mypassword';
  grant all on database eucalyptus_reporting to eucalyptus;
  \q

Log out. 

.. code::

  exit

Edit the */var/lib/pgsql/9.1/data/pg_hba.conf* file to contain the following content: 

.. code::

  local   all             all                                     password
  host    all             all             127.0.0.1/32            password
  host    all             all             ::1/128                 password

Reload the PostgreSQL service. 

.. code::

  service postgresql-9.1 reload

Your machine is now configured as a data warehouse. 