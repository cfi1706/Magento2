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



