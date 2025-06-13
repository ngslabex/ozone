=============================
Authentication OpenID Connect
=============================

.. 
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
   !! This file is generated by oca-gen-addon-readme !!
   !! changes will be overwritten.                   !!
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
   !! source digest: sha256:a1c33339feab3d79cbf62537165a9a0ae74bf46495dcca7ad3ec42e891ce611a
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

.. |badge1| image:: https://img.shields.io/badge/maturity-Beta-yellow.png
    :target: https://odoo-community.org/page/development-status
    :alt: Beta
.. |badge2| image:: https://img.shields.io/badge/licence-AGPL--3-blue.png
    :target: http://www.gnu.org/licenses/agpl-3.0-standalone.html
    :alt: License: AGPL-3
.. |badge3| image:: https://img.shields.io/badge/github-OCA%2Fserver--auth-lightgray.png?logo=github
    :target: https://github.com/OCA/server-auth/tree/14.0/auth_oidc
    :alt: OCA/server-auth
.. |badge4| image:: https://img.shields.io/badge/weblate-Translate%20me-F47D42.png
    :target: https://translation.odoo-community.org/projects/server-auth-14-0/server-auth-14-0-auth_oidc
    :alt: Translate me on Weblate
.. |badge5| image:: https://img.shields.io/badge/runboat-Try%20me-875A7B.png
    :target: https://runboat.odoo-community.org/builds?repo=OCA/server-auth&target_branch=14.0
    :alt: Try me on Runboat

|badge1| |badge2| |badge3| |badge4| |badge5|

This module allows users to login through an OpenID Connect provider using the
authorization code flow or implicit flow.

Note the implicit flow is not recommended because it exposes access tokens to
the browser and in http logs.

**Table of contents**

.. contents::
   :local:

Installation
============

This module depends on the `python-jose <https://pypi.org/project/python-jose/>`__
library, not to be confused with ``jose`` which is also available on PyPI.

Configuration
=============

Setup for Microsoft Azure
~~~~~~~~~~~~~~~~~~~~~~~~~

Example configuration with OpenID Connect implicit flow.
This configuration is not recommended because it exposes the access token
to the client, and in logs.

# configure a new web application in Azure with OpenID and implicit flow (see
  the `provider documentation
  <https://docs.microsoft.com/en-us/powerapps/maker/portals/configure/configure-openid-provider)>`_)
# in this application the redirect url must be be "<url of your
  server>/auth_oauth/signin" and of course this URL should be reachable from
  Azure
# create a new authentication provider in Odoo with the following
  parameters (see the `portal documentation
  <https://docs.microsoft.com/en-us/powerapps/maker/portals/configure/configure-openid-settings>`_
  for more information):

* Provider Name: Azure
* Auth Flow: OpenID Connect
* Client ID: use the value of the OAuth2 autorization endoing (v2) from the Azure Endpoints list
* Body: Azure SSO
* Authentication URL: use the value of "OAuth2 autorization endpoint (v2)" from the Azure endpoints list
* Scope: openid email
* Validation URL: use the value of "OAuth2 token endpoint (v2)" from the Azure endpoints list
* Allowed: yes


Setup for Keycloak
~~~~~~~~~~~~~~~~~~

Example configuration with OpenID Connect authorization code flow.

In Keycloak:

# configure a new Client
# make sure Authorization Code Flow is Enabled.
# configure the client Access Type as "confidential" and take note of the client secret in the Credentials tab
# configure the redirect url to be "<url of your server>/auth_oauth/signin"

In Odoo, create a new Oauth Provider with the following parameters:

* Provider name: Keycloak (or any name you like that identify your keycloak
  provider)
* Auth Flow: OpenID Connect (authorization code flow)
* Client ID: the same Client ID you entered when configuring the client in Keycloak
* Client Secret: found in keycloak on the client Credentials tab
* Allowed: yes
* Body: the link text to appear on the login page, such as Login with Keycloak
* Scope: openid email
* Authentication URL: The "authorization_endpoint" URL found in the
  OpenID Endpoint Configuration of your Keycloak realm
* Token URL: The "token_endpoint" URL found in the
  OpenID Endpoint Configuration of your Keycloak realm
* JWKS URL: The "jwks_uri" URL found in the
  OpenID Endpoint Configuration of your Keycloak realm

Usage
=====

On the login page, click on the authentication provider you configured.

Known issues / Roadmap
======================

* When going to the login screen, check for a existing token and do a direct login without the clicking on the SSO link
* When doing a logout an extra option to also logout at the SSO provider.

Changelog
=========

14.0.1.1.0 2023-11-22
~~~~~~~~~~~~~~~~~~~~~

* Forward port OpenID Connect fixes from 13.0 to 14.0

14.0.1.0.2 2022-03-14
~~~~~~~~~~~~~~~~~~~~~

* Fix werkzeug deprecated warning for url_encode, url decode

14.0.1.0.1 2022-01-17
~~~~~~~~~~~~~~~~~~~~~

* Updated readme and pot

14.0.1.0.0 2021-12-10
~~~~~~~~~~~~~~~~~~~~~

* Odoo 14 migration

13.0.1.0.0 2020-04-10
~~~~~~~~~~~~~~~~~~~~~

* Odoo 13 migration, add authorization code flow.

10.0.1.0.0 2018-10-05
~~~~~~~~~~~~~~~~~~~~~

* Initial implementation

Bug Tracker
===========

Bugs are tracked on `GitHub Issues <https://github.com/OCA/server-auth/issues>`_.
In case of trouble, please check there if your issue has already been reported.
If you spotted it first, help us to smash it by providing a detailed and welcomed
`feedback <https://github.com/OCA/server-auth/issues/new?body=module:%20auth_oidc%0Aversion:%2014.0%0A%0A**Steps%20to%20reproduce**%0A-%20...%0A%0A**Current%20behavior**%0A%0A**Expected%20behavior**>`_.

Do not contact contributors directly about support or help with technical issues.

Credits
=======

Authors
~~~~~~~

* ICTSTUDIO
* André Schenkels
* ACSONE SA/NV

Contributors
~~~~~~~~~~~~

* Alexandre Fayolle <alexandre.fayolle@camptocamp.com>
* Stéphane Bidoul <stephane.bidoul@acsone.eu>
* Andreas Perhab <andreas.perhab@wt-io-it.at>

Maintainers
~~~~~~~~~~~

This module is maintained by the OCA.

.. image:: https://odoo-community.org/logo.png
   :alt: Odoo Community Association
   :target: https://odoo-community.org

OCA, or the Odoo Community Association, is a nonprofit organization whose
mission is to support the collaborative development of Odoo features and
promote its widespread use.

.. |maintainer-sbidoul| image:: https://github.com/sbidoul.png?size=40px
    :target: https://github.com/sbidoul
    :alt: sbidoul

Current `maintainer <https://odoo-community.org/page/maintainer-role>`__:

|maintainer-sbidoul| 

This module is part of the `OCA/server-auth <https://github.com/OCA/server-auth/tree/14.0/auth_oidc>`_ project on GitHub.

You are welcome to contribute. To learn how please visit https://odoo-community.org/page/Contribute.
