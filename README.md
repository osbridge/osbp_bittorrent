Bittorrent server for Open Source Bridge
=======================================

This set of files provide a simple Bittorrent service using `rtorrent`, `dtach`,
`expect` and `rsync`.

For usage, run `rake help`.

Typical usage
-------------

    # Install cronjob to start the service on boot
    rake cron

    # Start the service
    rake stop

    # Restart a running service
    rake restart

    # Stop a running service
    rake stop

    # Pull files from origin server to here
    rake pull


License
-------

Copyright (C) 2010 Igal Koshevoy under the MIT License.
