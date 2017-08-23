# Magento architecture principles

## OOP architecture and programming principles {#m2arch-oop-architecture}

**Class**

A class is a template for an object, a user-defined datatype that contains variables, properties, and methods. You should imagine any class as a wrapper of functions \(methods\) that will help you manipulate some specific data.

**Method**

An expression for a function bound to a class.

**Instance**

Instance is an object \(datatype\) created by your class.

**Inheritance**

Inheritance is a process in which a class inherits all the state and behavior of another class \(extend, implement\)

**Abstraction**

Abstraction refers to the act of representing essential features without including the background details or explanations. It reduces and factors out details so that one can focus on a few concepts at a time.

**Singleton**

Singleton restricts the instantiation of a class to one object.

## Strongly layered product architecture {#m2arch-layered-product-architecture}

Magento tweaks the classic Model-View-Controller architectural model, though: files within modules are typically grouped by functionality rather than file type.

The _Magento Framework_ defines the fundamental concepts and rules for how the components of the web site can behave.

## Integration with architectural layers {#integration-with-architectural-layers}

### Presentation layer {#presentation-layer}

View components \(layouts, blocks, templates\) and controllers.

Include web API service bindings.

### Service layer {#service-layer}

Defines the overall interface for interacting with business logic. Service contracts simplify the process of replacing or modifying \(via plugins\) services.

### Domain layer {#domain-layer}

Referred to as the Business Logic layer, provides business logic and functionality in base classes, resource models, and data access capabilities that you can extend and customize.

## Ease of extensibility {#m2arch-extensibility}

Use dependency injection and service contracts to simplify the process of supplying a new implementation of a defined API.

## Modularity {#m2arch-modularity}

Extend the core feature set of Magento by writing and incorporating new modules into your installation. Use Magento themes and language packages to create your store’s visual design and language capabilities.

## Highly customizable store branding {#m2arch-store-branding}

Extend and customize the core components of your Magento store’s PHP-, HTML5- and CSS3- based default themes and language packages to precisely control your site’s behavior and look-and-feel.

## Strong stack of open-source technologies {#m2arch-open-source-stack}

Includes popular open-source technologies such as the Linux OS, Apache/Nginx server, MySQL, Zend, and Composer.

# Architectural basics overview

### Extensibility and modularity

Designed from its earliest stages for customization and enhancement.

#### Architectural principles that guide product structure

Replacing or extending core code rather than editing.

#### Open-source software to create and manage extensions

Uses Composer to manage dependencies.

#### Coding standards

Zend Framework Coding Standards for PHP

[http://devdocs.magento.com/guides/v2.0/coding-standards/bk-coding-standards.html](http://devdocs.magento.com/guides/v2.0/coding-standards/bk-coding-standards.html)

#### Upgrade and versioning strategies

Well-defined upgrade and versioning strategies that can help you avoid any problems with software component dependencies.

# Ease of frontend customization

Designed to optimize storefront customization, with highly extensible themes being the central customization mechanism.

## Storefront customization tools {#storefront-customization-tools}

#### Magento Blank Theme

#### Magento UI Library Components

* enforce for consistency in design across your storefronts

* simplify \(and speed up\) the design process

#### Magento Admin Pattern Library

User interface \(UI\) design patterns

* address form
* button bar
* container
* tabs
* sign-in form

Built on the LESS preprocessor and implemented as a module.

# Global features that support extensibility

### Modularity {#modularity}

This loose coupling of software components reduces the ripple effects throughout your code base of changing code.

### Reliance on popular design patterns {#reliance-on-popular-design-patterns}

Model-View-Controller \(MVC\)

### Coding standards {#coding-standards}

Based on Zend Framework Coding Standards.

### Rich product ecosystem {#rich-product-ecosystem}

Many modules and themes available for download and to buy modules and theme packages.

### Flexible attribute types {#flexible-attribute-types}

Enhance your storefront by adding unique attributes to the default product attributes.

Attribute types fall into three general categories:

* **EAV \(Entity-Attribute-Value\) attributes** are site-specific attributes that you can define for a local site using the Magento Admin.

* **Custom attributes** are a subset of EAV attributes. Objects that use EAV attributes typically store values in several MySQL tables. The Customer and Catalog modules use EAV attributes.

* **Extension attributes** often use more complex data types than custom attributes. These attributes do not appear in the storefront. Extension attributes are introduced by modules.

### Web APIs {#web-apis}

Web API \(REST or SOAP\) with some simple XML.

* CRM \(Customer Relationship Management\)
* ERP \(Enterprise Resource Planning\) back office systems
* CMS \(Content Management Systems\).

### Service contracts, dependency injection, and dependency inversion {#service-contracts-dependency-injection-and-dependency-inversion}

Service contracts provide a new way to access public API endpoints.

Magento implements dependency injection along with service contracts \(ease-of-extensibility, support the loose coupling\).

### Plug-ins {#plug-ins}

Mechanism for adding features to the core Magento product.

Make changes to the behavior of any public method in a Magento class.

Interceptors.

Applications use the plug-in pattern to change method behavior without modifying the actual class. Plug-ins can typically intercept method processing before or after the method runs, or only when the method throws an exception.

# Security

## Enhanced password management {#enhanced-password-management}

Hashing algorithms \(SHA-256\)

## Improved prevention of cross-site scripting \(XSS\) attacks by making escaped data the default {#improved-prevention-of-cross-site-scripting-xss-attacks-by-making-escaped-data-the-default}

Adopted conventions that regulate the escaping of data in output.

Escape output for HTML pages \(HTML, JSON, and JavaScript\) and email.

## More flexible file system ownership and permissions {#more-flexible-file-system-ownership-and-permissions}

Using a [umask](http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html).

## Improved prevention of clickjacking exploits {#improved-prevention-of-clickjacking-exploits}

Using an X-Frame-Options HTTP request header \([X-Frame-Options header](http://devdocs.magento.com/guides/v2.1/config-guide/secy/secy-xframe.html)\).

## Use of non-default Magento Admin URL {#use-of-non-default-magento-admin-url}

Default creates a random Admin URI when you install the product. The CLI is provided so that you can see the password if you forget it.

Prevent large-scale automated attacks.

# Storefront customization strategies

## Storefront customization levels {#storefront-customization-levels}

### Extend Magento-Provided CSS {#extend-magento-provided-css}

Default theme has a LESS-based CSS =&gt; change a storefront using CSS only.

### Replace PHTML template files {#replace-phtml-template-files}

Generate different HTML markup.

### Replace Magento-Provided CSS {#replace-magento-provided-css}

Allows use of different CSS tools or technologies not provided with Magento.

### Replace Magento-Provided CSS, HTML, and JavaScript {#replace-magento-provided-css-html-and-javascript}

# Architectural diagrams

## Magento architecture from different perspectives {#m2arch-whatis-overview}

## Architecture layers diagram {#archi-layers}

![](/assets/import.png)

# Technology stack

### Web servers {#web-servers}

* Apache
* nginx

### PHP {#php}

* Composer
   \(dependency management package for PHP\)

### Database {#database}

* MySQL
* MySQL Percona

### HTTP accelerator {#http-accelerator}

* Varnish

### Cache Storage {#cache-storage}

* Redis
* Memcache

### Search {#search}

* Solr \(Magento Enterprise Edition only\)
* Elasticsearch \(Magento Enterprise Edition version 2.1.x only\)

### Additional technologies {#additional-technologies}

* HTML5
* CSS3 \(LESS 
  CSS
   pre-processor\)
* jQuery
   \(primary 
  JavaScript
   library\)
* RequireJS \(library that helps load JavaScript resources on demand\)
* Knockout.js \(simplifies JavaScript UIs with the Model-View-View Model pattern\)
* Third-party libraries \(Zend Framework 1, Zend Framework 2, Symfony\)
* Coding standards PSR-0 \(autoloading standard\), PSR-1 \(basic coding standards\), and PSR-2 \(coding style guide\), PSR-3, PSR-4

### Optional stack components {#optional-stack-components}

* Varnish \(caching\)
* Redis \(used for page caching\)
* Solr \(search engine\)
* Elasticsearch \(search engine\)

Magento is _compatible with but not supported_ for:

* HHVM 3.9 PHP Interpreter

### Automated testing {#automated-testing}

Provides automated testing suites that include unit, integration, functional and performance test scripts, as well as JavaScript tests and tools for static code analysis.

Components include PHPUnit for the unit test framework and Selenium for the functional test framework.

# Backward compatibility

Magento 2.0 uses Semantic Versioning 2.0.0 to indicate whether a change breaks backward compatibility.

* _MAJOR_ indicates incompatible API changes

* _MINOR_ indicates backward-compatible functionality has been added

* _PATCH_ indicates backward-compatible bug fixes

The backward compatibility policy applies to PHP code annotated with `@api.`

# Versioning policy

Magento software versioning complies with the following specifications:

* [Semantic Versioning 2.0.0](http://semver.org/)

* [Versioning specification of Composer system](https://getcomposer.org/doc/04-schema.md#version)

* [PHP version\_compare\(\)](http://php.net/version_compare)

## Version formats {#version-formats}

The pre-release version format is: MAJOR.MINOR.PATCH-&lt;alpha \| beta \| rc&gt;n, where alpha, beta or rc are stability indications, as described in the version\_compare\(\) specification, and n is an increment number to distinguish releases of the non-stable versions.

## Public APIs {#public-apis}

This designation indicates the code can be used or customized by other components, such as formal interfaces and dependency injection points.

## Where versioning is used {#where-versioning-is-used}

Magento component or bundle, inside the `composer.json` file.

It can be declared as the version of the component:

```
"name":"acme/foo",
"version":1.2.0
```

Or it can be used to declare a dependency on a particular version of a component:

```
"require":{
"acme/foo":"1.2.*",
"acme/bar":"2.2.0"
}
```

## Release types {#release-types}

This section describes how exactly and when the software version numbers will be changed with releases.

### Development releases {#development-releases}

Magento may update the `x.y.z` version in way perscribed by Semantic Versioning, but also could release the same `x.y.z` with different stability and/or index numbers.

### Stable releases {#stable-releases}

In every stable release, the same value of version number will be propagated in all components, but dependencies will have a wildcard \(\*\) pattern.

The `x.y.z` numbers will change according to Semantic Versioning policy provisions. For example, `1.0.0 -> 1.0.1 -> 1.1.0 -> 1.5.0 -> 1.5.1 -> 2.0.0 -> 2.1.0`.

# Architectural layers overview

## Magento as layered software {#magento-as-layered-software}

Pattern-Oriented Software Architecture

## Advantages of layered application design {#advantages-of-layered-application-design}

Magento will appreciate:

* Stringent separation of business logic from presentation logic simplifies the customization process. For example, you can alter your storefront appearance without affecting any of the backend business logic.

* Clear organization of code predictably points extension developers to code location.

# Presentation Layer

## What is Magento Presentation layer? {#what-is-magento-presentation-layer}

Interact with the Magento web interface =&gt; directly working with _presentation layer_ code.

The presentation layer contains both view elements \(layouts, blocks, templates\) and controllers.

Three types of Magento:

* **Web users** interact with the store front, where they can see the View model of data displayed by Magento and interact with product UI elements to request data for view and manipulation. These users work within the \(`frontend`\) area.

* **System administrators** customizing a storefront can indirectly manipulate the presentation layer by, for example, adding themes or widgets to the front end.

* **Web API calls** can be made through HTTP just like browser requests, and can be made via AJAX calls from the user interface.

## Presentation layer components {#presentation-layer-components}

Each theme resides in a unique directory and contains custom page layouts, templates, skins, and language files.

## View model {#view-model}

* **Blocks** can generate dynamic content and can contain named child view elements that are similar to arguments being passed in. \(The `as` attribute holds the child view element names for the parent block to reference them\)

* **Containers** collect an ordered group of children view elements.

Blocks can generate their content using static HTML, Knockout JS scripts, and PHTML.

## How Presentation code calls other layers {#how-presentation-code-calls-other-layers}

Presentation code typically calls service contracts.

## Presentation layer flow {#presentation-layer-flow}

Presentation layer components make calls to the Service layer, which in turn sends requests to the Domain \(or business logic\) layer.

# Magento Themes

Magento application provides two design themes: Luma, as a demonstration theme, and Blank as a basis for custom theme creation.

All theme files are stored under `app/design/<area>/<Vendor>/<theme>/.`

Two categories:

* Static view files are a set of theme files that are returned by the server to a browser as is, without any processing, are called the static files of a theme.

* Dynamic view files are view files that are processed or executed by the server in order to provide result to the client. These are: .less files, templates, layouts .

Magento supports multi theme model.

## Control {#control}

Includes CSS, images, design/UI- specific Javascript 2\) also control many functional aspects of site. Layouts control which default blocks/modules are available Templates control which data is shown and how

Themes do not include business logic.

## Theme components {#theme-components}

* Layout:  layoutXML files. This defines which template file to load.

* Template: template files which are generally .phtml files.

* Skin: static files like images, css and js.

* Locale: language related file. This will be used when you want to make your theme compatible with different languages.

## Theme process flow {#theme-process-flow}

### Process flow {#process-flow}

Your Custom Package » Default Package » Base Package » Error Message

The system searches in the ancestor themes, module view files or library

* page templates
* block templates
* layouts

Two categories:

* Static view files. These theme files are returned by the server to a browser as is, without any processing, and are called the static files of a theme.

* Dynamic view files. View files that are processed or executed by the server in order to provide result to the client. These are: .less files, templates, layouts

### Where do themes live? {#where-do-themes-live}

Each theme resides in a unique directory

Two different directories:

* /skin/frontend: contains images and CSS for a theme.

* /app/design/frontend: contains page templates and layouts

# Service layer

## What is a Service layer? {#what-is-a-service-layer}

The service layer provides a bridge between the presentation layer and the model layer of domain logic and resource-specific data. This is implemented using _service contracts_, which are defined using PHP interfaces.

In general, the service layer:

* Resides below the presentation layer and above the domain layer.

* Contains service contracts, which define how the implementation will behave.

* Provides an easy way to access the REST/SOAP API framework code \(which also resides above the service contracts\). You can bind service contracts to web service APIs in configuration files — no coding required.

* Provides a stable API for other modules to call into.

## Who accesses the service layer? {#who-accesses-the-service-layer}

Service contract clients include:

* Controllers \(initiated by actions of users of the storefront\)

* Web services \(SOAP and REST API calls\)

* Other Magento modules through service contracts

## Service contract anatomy {#service-contract-anatomy}

The service contract of a module is defined by the set of interfaces in the module’s `/Api`. It typically consists of:

* service interfaces in the `/Api`namespace of the module

* data \(or _entity_\) interfaces in the `Api/Data` directory. _Data entities_ are data structures passed to and returned from service interfaces.

Typically, service contracts provide three distinct types of interfaces:

* Repository interfaces

* Management interfaces

* Metadata interfaces

## Advantages of service contracts {#advantages-of-service-contracts}

Permit you to add a new customer extension that adds or changes business logic-level resource models and models without breaking the system. How? Through the use of the &lt;preference&gt; element of a dependency injection config file \(di.xml\) file. The di.xml file specifies which PHP class to use for the interface Magento\Customer\Api\CustomerRepositoryInterface.

# Domain layer

## What is Magento Domain layer? {#what-is-magento-domain-layer}

The domain layer holds the business logic layer of a Magento module. It typically does not contain resource-specific or database-specific information. Its primary functions include:

* Defining the generic Magento data objects, or models, that contain business logic. This logic defines which operations can be performed on particular types of data, such as a Customer object. These models contain generic information only. Applications can also use SOAP or RESTful endpoints to request data from models.

* \(Optionally\) Including the implementation of service contracts, although not their definition.

## Models {#models}

Each domain-layer model contains a reference to a resource model, which it uses to retrieve data from the database with MySql calls. This resource model contains logic for connecting to the underlying database, typically MySQL. A model requires a resource model only if the model data must persist.

## Who accesses the domain layer? {#who-accesses-the-domain-layer}

Three primary ways of accessing a module’s domain-layer code:

* Service contracts are the recommended way for one module to access another module’s domain-level code. This loosely coupled solution is the optimal way for most modules to access another module.

* A module can directly call into another module. This tightly coupled solution is not recommended for most situations, but is sometimes unavoidable.

* Domain layer code in one module can also plug itself into another module by:

  * event hooks

  * plugins

  * `di.xml` files \(with an SPI contract\)

# Persistence layer

A resource model is responsible for performing functions such as:

* Executing all CRUD \(create, read, update, delete\) requests. The resource model contains the SQL code for completing these requests.

* Performing additional business logic. For example, a resource model could perform data validation, start processes before or after data is saved, or perform other database operations.

A collection is a class that loads multiple models into an array-like structure based on a set of rules. This is similar to a SQL `WHERE` clause.

A simple resource model defines and interacts with a single table.

## Magento components {#magento-components}

# Module overview

A module is a logical group – that is, a directory containing blocks, controllers, helpers, models – that are related to a specific business feature.

## Module purpose {#module-purpose}

Each module is designed to function independently, so the inclusion or exclusion of a particular module does not typically affect the functionality of other modules.

## Module components {#module-components}

Contains the PHP and XML files \(blocks, controllers, helpers, models\) that are related to a specific business feature.

Magento module is composed of these software components: themes, libraries, and language packages.

## Where do modules live? {#where-do-modules-live}

Modules typically live in the `app/code` directory of a Magento installation, in a directory with the following PSR-0 compliant format: `app/code/<Vendor>/<ModuleName>.`



