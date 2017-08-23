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

.



