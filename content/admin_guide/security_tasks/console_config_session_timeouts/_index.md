+++
title = "Configure Session Timeouts"
weight = 10
+++

To set the session timeouts in the Management Console: 

Modify the `session.timeout` and `session.cookie_expires` entries in the `[app:main]` section of the configuration file. The `session.timeout` value defines the number of seconds before an idle session is timed out. The `session.cookie_expires` is the maximum length that any session can be active before being timed out. All values are in seconds: 

    session.timeout=1800



    session.cookie_expires=43200

