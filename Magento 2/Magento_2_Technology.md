# **Requirements:**

* Magento 2.1.x technology stack requirements

  * Operating systems \(Linux x86-64\)

  * Require up to 2GB of RAM \(if &lt; 2GB of RAM, recommend create a swap file\)

  * Composer \(latest stable version\)

  * Web servers:

    * Apache 2.2 or 2.4

    * nginx 1.8 \(or latest mainline version\)

  * Database

    * MySQL 5.6

    * 2.1.2 and later are compatible with MySQL 5.7

    * MariaDB and Percona

  * PHP:

    * 7.0.2

    * 7.0.4

    * 7.0.6–7.0.x

    * 5.6.5–5.6.x

  * Required PHP extensions

    * bc-math \(only Enterprise\)

    * curl

    * gd, ImageMagick 6.3.7 \(or later\) or both

    * intl

    * mbstring

    * mcrypt

    * mhash

    * openssl

    * PDO/MySQL

    * SimpleXML

    * soap

    * xml

    * xsl

    * zip

    * PHP 7 only:

      * json

      * iconv

  * PHP OPcache:

    * opcache.save\_comments

  * PHP settings:

    * memory\_limit=2G

    * always\_populate\_raw\_post\_data = -1

  * SSL

    * TLS requirement

    * PayPal and repo.magento.com both require TLS 1.1 or later

  * Mail server

    * Mail Transfer Agent \(MTA\)

    * SMTP server

  * Technologies

    * Redis version 3.0

    * Varnish version 3.5 or latest stable 4.x version for page caching

    * memcached latest stable version for session storage with either memcache or memcached PHP extensions \(latest stable version\)

    * Magento Enterprise Edition \(EE\) only

      * Apache Solr 4.x \(Solr search can be used as a search provider\)

      * Elasticsearch versions 1.7 and 2.x \(recommended\)

      * RabbitMQ 3.5 \(messages asynchronously\)

      * Three master databases

    * Optional

      * php\_xdebug2.2.0 or later

      * PHPUnit \(as a command-line tool\) 4.1 or later

* Supported browsers \(Storefront and Admin\):

  * Internet Explorer 11 or later, Microsoft Edge, latest–1

  * Firefox latest, latest–1 \(any operating system\)

  * Chrome latest, latest–1 \(any operating system\)

  * Safari latest, latest–1 \(Mac OS\)

  * Safari Mobile for iPad 2, iPad Mini, iPad with + Retina Display \(iOS 7 or later\), for desktop storefront

  * Safari Mobile for iPhone 4 or later; iOS 7 or later, for mobile storefront

  * Chrome for mobile latest–1 \(Android 4 or later\) for mobile storefront

  \(where latest–1 means one major version earlier than the latest released version.\)

[http://devdocs.magento.com/guides/v2.1/install-gde/prereq/prereq-overview.html](http://devdocs.magento.com/guides/v2.1/install-gde/prereq/prereq-overview.html)

[http://devdocs.magento.com/guides/v2.1/install-gde/system-requirements2.html](http://devdocs.magento.com/guides/v2.1/install-gde/system-requirements2.html)

# Understanding the Platform Architecture

[http://devdocs.magento.com/guides/v2.1/architecture/archi\_perspectives/ABasics\_intro.html](http://devdocs.magento.com/guides/v2.1/architecture/archi_perspectives/ABasics_intro.html)

[http://devdocs.magento.com/common/images/archi\_diagrams\_layers\_alt4.jpg](http://devdocs.magento.com/common/images/archi_diagrams_layers_alt4.jpg)

* The technology stack:

  * PHP OOP

  * Coding standards

    * PSR-0 \(the autoloading standard\)

    * PSR-1 \(the basic coding standards\)

    * PSR-2 \(the coding style guide\)

    * PSR-3

    * PSR-4

  * Composer

  * HTML: HTML5 is supported

  * CSS: CSS3 via its in-built LESS CSS preprocessor

  * jQuery

  * RequireJS

  * Third-party libraries

    * Zend Framework

    * Symfony

  * Apache or Nginx

  * MySQL

  * MTF: Magento Testing Framework \(MTF\) \([https://github.com/magento/mtf\](https://github.com/magento/mtf\)\)

* The architectural layers:

  * 4 architectural layers:

    * presentation

    * service

    * domain

    * persistence

  * Presentation layer

    * directly interact with through the browser \(tuong tac truc tiep\)

    * contains:

      * layouts

      * blocks

      * templates

      * controllers

    * Client-side technologies such as jQuery, RequireJS, CSS, and

LESS are also a part of this layer

* 3 types of users interact with this layer:

  * Web users: UI elements

  * System administrators: indirectly manipulate the presentation: themes or widgets

  * Web API calls: AJAX calls

* Theme:

  * Custom page layouts

  * Templates

  * Skins

  * Language files

* View model:

  * Generates the HTML for a page to display to a user from a tree of view elements.

  * 2 categories:

    * Blocks: generate dynamic content and can contain named child view elements that are similar to arguments being passed in

    * Containers: collect an ordered group of children view elements

  * Blocks can generate their content using static HTML, Knockout JS scripts, and PHTML

  * Presentation code typically calls service contracts

  * Presentation code to directly call the business logic layer

  * Presentation layer components ==calls==&gt; Service layer ==sends requests==&gt; Domain \(or business logic\) layer

* components of a presentation layer are being interacted =&gt; make

calls to the underlying service layer

* Service layer:

  * provides a bridge between the presentation layer and the model layer of domain logic and resource-specific data, implemented using service contracts

  * service contract basically a fancy name for a PHP interface

  * service layer:

    * below the presentation layer and above the domain layer

    * Contains service contracts, which define how the implementation will behave

    * Provides an easy way to access the REST/SOAP API framework code

    * Provides a stable API for other modules to call into.

  * Service contract clients include:

    * Controllers \(initiated by actions of users of the storefront\)

    * Web services \(SOAP and REST API calls\)

    * Other Magento modules through service contracts

  * Service contract

    * Service interfaces in the /Api namespace of the module

    * Data \(or entity\) interfaces in the Api/Data directory. Data entities are data structures passed to and returned from service interfaces.

  * 3 distinct types of interfaces:

    * Repository interfaces

    * Management interfaces

    * Metadata interfaces

  * Advantages:

    * Easy to adds or changes business logic-level resource models and models without breaking the system di.xml file specifies which PHP class to use for the interface Magento\Customer\Api\CustomerRepositoryInterface

* Domain layer:

  * The business logic layer

  * Not contain resource-specific or database-specific information

  * Defining the generic Magento data objects, or models, that contain business logic

  * Applications can also use SOAP or RESTful endpoints to request data from models.

  * Models

    * Each domain-layer model contains a reference to a resource model, which it uses to retrieve data from the database with MySql calls

  * 3 primary ways of accessing:

    * Service contracts

    * directly call

    * plug itself into another module by:

      * event hooks

      * plugins

      * di.xml files \(with an SPI contract\)

* Persistence layer

  * active record pattern strategy

  * the model object contains a resource model that maps an object to one or more database rows

  * resource model

    * Executing all CRUD requests

    * Performing additional business logic: data validation, start processes before or after data is saved, or perform other database operations.

  * If you expect to return multiple items from a database query =&gt; using collection.

  * A collection is a class that loads multiple models into an array-like structure based on a set of rules. This is similar to a SQL WHERE clause.

* The top-level filesystem structure

  * app/etc/di.xml file is one of the most important files. It contains various class mappings or preferences for individual interfaces.

  * var/magento/language-\* registered languages reside, if not found in i18n will eventually fall back

  * bin magento file,runs an instance of the Magento\Framework\Console\Cli application

  * dev Magento test scripts

  * lib:

    * lib/internal server-side PHP library code and fonts

    * lib/web client-side JavaScript libraries

  * pub publicly exposed files, should set as root when setting up Apache or Nginx. The pub/index.php file is what gets triggered when the storefront is opened in a browser.

  * var dynamically generated group type of files such as cache, log, and a few others get created in, able to delete the content of this folder

at any time and have Magento automatically recreate it.

* vendor most of the code:

  * various third-party vendor code

  * Magento modules

  * Themes

  * Language packs

* vendor/magento Magento code

  * The module filesystem structure

* Block view-related block PHP classes

* Controller controller-related PHP classes

* etc module configuration files

  * module.xml

  * di.xml

  * acl.xml

  * system.xml

  * config.xml

  * email\_templates.xml

  * page\_types.xml

  * routes.xml

* Helper various helper classes

* i18n translation package CSV files

* Module:

  * entities

  * resource entities

  * collections

  * various other

  * business classes

* Test unit tests

* view contains all the module administrator and storefront template files

\(.phtml and .html\) and static files \(.js and .css\)

* registration.php is a module registration file

1. Managing the Environment

2. Programing Concepts and Conventions

3. Service contracts

   * A service contract is a set of PHP interfaces that is defined by a module. This contract comprises data interfaces and service interfaces.

   * The role of the data interface is to preserve data integrity, while the role of the service interface is to hide the business logic details from service consumers

* Code generation

  * generated in Magento’s var/generation

  * similar to that of the core vendor/magento/module-\* and app/code directories. It follows the module structure. The code is generated for something that is called Factory, Proxy, and Interceptor classes.

    * The Factory class creates an instance of a type: khi co bat ky lop Factory nao duoc goi thi se tao ra Factory class trong var/generation neu chua ton tai class nay

    * The Proxy class is a wrapper for some base class

      * instantiated without instantiating a base class the hien ma ko can khoi tao

      * generated under the var/generation

    * Interceptor: related to the plugins feature

  * single-tenant

    * magento setup:di:compile

  * multi-tenant

    * magento setup:di:compile-multi-tenant

  * clear individua

    * rm -rf {Magento root dir}/var/generation/\*

  * bin/magento setup:upgrade: This updates the Magento database schema and data.

    * truncates the var/di and var/generation

  * bin/magento setup:di:compile: This clears the var/generation directory.

    * bin/magento deploy:mode:set {mode}: This changes the mode from the developer truncates the var/di, var/generation, and var/view\_preprocessed.

    * bin/magento cache:clean {type}: This cleans the var/cache and var/page\_cache

1. Models and Collections

2. Creating a simple model:

   * model class

   * resource class

   * collection class

1. Using the Dependency Injection

2. Plugins

3. Backend Development

4. Frontend Development

5. The Web API

6. The Major Functional Areas

7. Testing

8. Building a Module from Scratch



