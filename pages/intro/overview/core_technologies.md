---
title: Core Technologies
permalink: /core_technologies/
---

## Java SE 8

Strata is written entirely in Java, including its built-in pricing and analytics, with minimal third-party dependencies.
We made an early decision to write Strata using Java 8, and the language features introduced in this version
have benefited the entire codebase in particular for:

* Dates and times
* Streams and lambdas
* Methods on interfaces

## Joda-Beans

Strata uses [Joda-Beans](http://www.joda.org/joda-beans) for all of its data objects, for example in trade modelling,
market data representation, calculation inputs, and results. Strata's Joda-Beans are always immutable,
helping to ensure thread safety at the core in systems built on top of Strata, and providing builder classes
for these beans to make their programmatic creation clearer.

All Joda-Beans are automatically serializable to and from XML, JSON and binary forms.
User extensions implemented as Joda-Beans will therefore integrate seamlessly with any code in Strata
that loads or saves data using Joda-Beans.

Joda-Beans also offer a mechanism to handle backwards-compatibility as data objects evolve over time.

## Requirements

### Using Strata

To reference and use Strata from external applications, these applications will need to be built using the
Java SE Development Kit (JDK) 8u40 or later.

Strata is available in [Maven Central](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.opengamma.strata%22),
and the JAR files can also be downloaded from [Strata Releases](https://github.com/OpenGamma/Strata/releases) page on GitHub.
Please see [obtaining Strata]({{site.baseurl}}/obtaining_strata) for more information.

At runtime the Java Runtime Environment (JRE) 8 or later is required.

### Building Strata from source code

To build Strata from source code, the following dependencies are required:

* Java SE Development Kit (JDK) 8u40 or later
* Maven 3.5 or later

Details on obtaining the source along with build instructions can be found at
[obtaining Strata]({{site.baseurl}}/obtaining_strata).
