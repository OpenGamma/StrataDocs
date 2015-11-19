---
title: Obtaining Strata
permalink: /obtaining_strata/
---

There are a number of ways to obtain Strata.


## From GitHub Releases

Strata is also released to GitHub through the standard [repository release pages](https://github.com/OpenGamma/Strata/releases). The downloads include:

 * `strata-dist` -- the full Strata distribution containing the jar files, dependencies and Javadoc.
 * `report-tool` -- the [command-line tool]({{site.baseurl}}/command_line_tool) for easy access to the reporting capabilities.
 * Source code -- the source code as of the release, documentation source and tool chain.

## From a Maven repository

The Strata JAR files are available from the [OpenGamma Maven repository](http://maven.opengamma.com/nexus/content/groups/public/com/opengamma/strata/).

It is intended that Strata will be available in [Maven Central](http://search.maven.org) from v1.0.


## For Developers

### Source code

As noted above, the source code for Strata is available from GitHub releases, however,
the most up-to-date code can be obtained directly from [GitHub](https://github.com/OpenGamma/Strata).
To do this you will need [Git](https://git-scm.com/download/).

Simply clone the repository locally:

```
    git clone https://github.com/OpenGamma/Strata.git
```

### Building

To build Strata from source code, the following dependencies are required:

* Java SE Development Kit (JDK) 8u40 or later
* Maven 3.2 or later

Note that versions of JDK 8 before update 40 are not able to compile Strata (due to bugs in early JDK 8 versions).

To build, simply change to the root directory of the cloned source code, and from the command line run:

```
$ mvn compile
```

### Using an IDE

Strata works out-of-the-box with most IDEs and no special settings are required.

The Strata codebase should be imported as a Maven project using the included `pom.xml`.

To help with contributions back to Strata, settings are included in the codebase for the Eclipse IDE
providing formatting rules and templates. For further information on working with Strata in the Eclipse IDE
see [here](https://github.com/OpenGamma/Strata/tree/master/eclipse).

