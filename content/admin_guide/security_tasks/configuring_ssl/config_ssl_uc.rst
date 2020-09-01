+++
title = "Configure and Enable SSL for the Management Console"
weight = 5
+++

..  _config_ssl_uc:

You can use secure HTTP for your console.To run your console over Secure HTTP: 

Install nginx on your console server with the following command: ``yum install nginx`` Overwrite the default ``nginx.conf`` file with the template provided in ``/usr/share/doc/eucaconsole-/nginx.conf.`` ``cp /usr/share/doc/eucaconsole-/nginx.conf /etc/nginx/nginx.conf`` Uncomment the 'listen' directive and uncomment/modify the SSL certificate paths in ``/etc/nginx/nginx.conf`` (search for "SSL configuration"). For example: 

.. code::

  # SSL configuration
  listen 443 ssl;
  # ssl_certificate /path/to/ssl/pem_file;
  # EXAMPLE:
  ssl_certificate /etc/eucaconsole/console.crt;
  # ssl_certificate_key /path/to/ssl/certificate_key;
  # EXAMPLE: 
  ssl_certificate_key /etc/eucaconsole/console.key;
  # end of SSL configuration

{{% notice note %}}For more information on generating self-signed SSL certificates, go to . {{% /notice %}}Restart nginx using the following command: ``systemctl restart nginx.service`` Edit the ``/etc/eucaconsole/console.ini`` file, locate the ``session.secure = false`` parameter, change ``false`` to ``true`` , then add the ``sslcert`` and ``sslkey`` lines immediately following, per this example: 

.. code::

  session.secure = true
  sslcert=/etc/eucaconsole/eucalyptus.com.chained.crt
  sslkey=/etc/eucaconsole/eucalyptus.com.key

