---
title: Contributions
permalink: /contributions/
---

Contributions to Strata are very welcome.

## Reporting a bug
Please raise all bugs as [Github Issues](https://github.com/OpenGamma/Strata/issues).
If possible please include the following (where relevant):

 * A short description of the bug.
 * An explanation as to what caused the problem. Please be as detailed as possible.
   * Perhaps attach a stack trace.
   * Perhaps include sample code that triggers the bug.
   * Perhaps attach input data that triggers the bug.
   * If you have knowledge of the domain, perhaps suggest reasons why the problem occured.
 * The version of Strata on which the bug occurred.
 * JDK version and operating system.

## Reporting a security vulnerability

If you believe you have identified a security vulnerability in Strata, we encourage responsible disclosure
via security-at-opengamma.com. Please ensure you provide full details to allow use to investigate properly.

## Submitting a patch
If you have a patch for anything from a bug right through to a full-blown feature, the process
for inclusion of your code into Strata is essentially the same.

 1. Fork Strata on Github.
 2. From your fork of Strata create a pull request in GitHub against `OpenGamma/Strata:master` (i.e. the `master` branch of the main repository).
 3. If necessary (particularly for large contributions) we will email you a legal indemnity form to sign and return.
 4. We will check your patch passes in CI and meets our quality standards (see below on how to get a patch accepted).
 5. If everything is fine your patch will be accepted and be merged. Thanks!

## How to get a patch accepted
The easiest way to get a patch accepted is to follow these rules:

 * The patch must not break or remove any existing tests.
 * The patch must not break backwards compatibility.
 * The patch must meet our visual code standards (see [here](https://github.com/OpenGamma/Strata/tree/master/eclipse)
 on how to get automatic formatting and templating).
 * If the patch is adding new features it must:
   * Include the appropriate new tests.
   * Include Javadoc and, if applicable, additional documentation.
   * Not add additional dependencies to Strata.
   * Not use proprietary classes e.g. `sun.misc.Unsafe`.
   * Be platform-independent (think file system differences etc.)
