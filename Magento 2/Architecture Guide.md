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

### Domain layer {#domain-layer}

Referred to as the Business Logic layer, provides business logic and functionality in base classes, resource models, and data access capabilities that you can extend and customize.



