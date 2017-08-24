# Before Developping

## Disables caches

System &gt; Tools &gt; Cache Management &gt; Disables caches

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

php.ini:

/etc/php/7.0/apache2/php.ini

/etc/php/7.0/fpm/php.ini

```xml
error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT
display_errors = On
```

Retart apache

`sudo service apache2 restart`

Change Magento mode:

* Show mode:

```xml
magento deploy:mode:show
```

* Change mode:

```xml
magento deploy:mode:set {mode} [-s|--skip-compilation]
```

* List mode:
  * default
  * production
  * developer

Cannot currently change from either developer or production mode to default mode.

If change production mode to developer mode, delete the contents of the `var/generation` and `var/di` directories:

```xml
rm -rf <your Magento install dir>/var/di/* <your Magento install dir>/var/generation/*
```

# Declare a new Magento 2 module

Create Module in **"app/code": **`app/code/Test/Helloworld/`

* Test: namespace
* Helloworld: module name

Create config module:  etc/module.xml

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Test_Helloworld" setup_version="1.0.0.0" active="true"/>
</config>
```

* name: module name
* setup\_version: module version
* active: status of module \(true/false\)

## Module registration

Create a "**registration.php**" file on the root folder of module

```php
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'Test_Helloworld',
    __DIR__
);
```

Run update module:

```xml
sudo php bin/magento setup:upgrade
```

## Module Activation

Check list module and status in `app/etc/config.php`

```php
return array (
  'modules' => 
  array (
    ...
    'Test_Helloworld' => 1,
    ...
  ),
);
```

Check table: setup\_module

![](/assets/setup_module.png)

# Uninstall module

sudo php bin/magento module:uninstall &lt;module name&gt;

# Create Magento 2 frontend controller

## Router declaration

Create a XML file:

app/code/Test/Helloworld/etc/frontend/routes.xml

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="standard">
        <route id="helloworld" frontName="helloworld">
            <module name="Test_Helloworld" before="Magento_Core" after="Magento_Sales"/>
        </route>
    </router>
</config>
```

* `id="standard": frontend controller`
* `id="admin": admin controller`
* id : unique identifier for your router
* frontName : the string which be used on the front URL
* name : module name to call
* before : your module have to be called before the module defined inside
* after : your module have to be called after the module defined inside
* Note: "before" et "after" fields are NOT required

## Controller creation

app/code/Test/Helloworld/Controller/Index/Index.php

```php
namespace Test\Helloworld\Controller\Index;
class Index extends \Magento\Framework\App\Action\Action
{
    public function execute()
    {
        echo 'Execute Action Index_Index OK';
        die();
    }
}
```

* `namespace` is the path of your controller inside the `app/code` folder.
* `class`name is the name of your PHP file.

## Customize URL

Our previous URL is very simple :

`http://magento2.local/helloworld`

But Magento 2 convert it to :

`http://magento2.local/helloworld/index/index`

* The first "index" is the folder "Index" inside "Controller".

* The second "index" is the file "Index.php" on the "Index" folder.

# Create simple module with Magento 2

## Controller modification

Change content file:

`app/code/Test/Helloworld/Controller/Index/Index.php`

```php
namespace Test\Helloworld\Controller\Index;
class Index extends \Magento\Framework\App\Action\Action
{
    public function execute()
    {
        $this->_view->loadLayout();
        $this->_view->getLayout()->initMessages();
        $this->_view->renderLayout();
    }
}
```

=&gt; Show template

## Block creation

Create the file `app/code/Test/Helloworld/Block/Hello.php`

```php
namespace Test\Helloworld\Block;
class Hello extends \Magento\Framework\View\Element\Template
{
}
```

## Layout creation

Associate routes and block

name is very important and must be composed with :

&lt;Router Name&gt;\_&lt;Controller Name&gt;\_&lt;Action Name&gt;

The layout names of these URL are :

`helloworld_index_index`

Create file:

`app/code/Test/Helloworld/view/frontend/layout/helloworld_index_index.xml`

```xml
<?xml version="1.0"?>
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd"
      layout="2columns-right">
    <body>
        <referenceContainer name="content">
            <block class="Test\Helloworld\Block\Hello" name="hello" template="helloworld.phtml">
            </block>
        </referenceContainer>
    </body>
</page>
```

* class: block file
* template: template file
* name: alias name, using to call getChildHTML\(\),...

## Template creation

Create the file

`app/code/Maxime/Helloworld/view/frontend/templates/helloworld.phtml`

```php
<h2>HelloWorld</h2>
<p>Congratulations ! You have created your first Magento Module !</p>
<p>The block classname is : <?php echo get_class($block) ?></p>
```

Delete cache + var/generation folder and refresh page

sudo php bin/magento cache:flush

sudo rm -rf var/generation/

