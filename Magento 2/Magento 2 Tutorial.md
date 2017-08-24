# Before Developping

## Disables caches

System &gt; Tools &gt; Cache Management

## Server Configuration

app/etc/env.php

```xml
SetEnv MAGE_MODE "developer"
```

vhost:

```xml
<VirtualHost *:80>
    ServerName magento2.local
    DocumentRoot /var/www/html/magento2
    SetEnv MAGE_MODE "developer"
    <Directory /var/www/html/magento2>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/magento2_error.log
    # Possible values include: debug, info, notice, warn, error, crit, alert, emerg.
    LogLevel warn
    CustomLog ${APACHE_LOG_DIR}/magento2_access.log combined
</VirtualHost>
```

restart apache :

`sudo service apache2 restart`

| Mode name | Description |
| :--- | :--- |
| [developer](http://devdocs.magento.com/guides/v2.0/config-guide/bootstrap/magento-modes.html#mode-developer) | Intended for development only, this mode:Disables [static view file caching](http://magento.stackexchange.com/questions/74059/magento-2-whats-a-static-view-file)Provides verbose loggingEnables [automatic code compilation](http://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-compiler-single.html##config-cli-subcommands-compile-overview)Enables enhanced debuggingShows custom `X-Magento-*` HTTP request and response headersResults in the slowest performance \(because of the preceding\) |
| [default](http://devdocs.magento.com/guides/v2.0/config-guide/bootstrap/magento-modes.html#mode-default) | As the name implies, Magento operates in this mode if no mode is explicitly set. In this mode:Static view file caching is enabledEnables [automatic code compilation](http://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-compiler-single.html##config-cli-subcommands-compile-overview)Exceptions are not displayed to the user; instead, exceptions are written to log files.Hides custom `X-Magento-*` HTTP request and response headersAlthough you _can_ run Magento in default mode in production, we don’t recommend it. |
| [production](http://devdocs.magento.com/guides/v2.0/config-guide/bootstrap/magento-modes.html#mode-production) | Intended for deployment on a production system. Exceptions are not displayed to the user, exceptions are written to logs only, and static files are not cached. |



