NOTE: This repo is a legacy Drupal 7.x module and is no longer maintained or considered relevant. It was originally hosted here:

  - https://www.drupal.org/sandbox/kpander/2148863

---

README.txt
==========
PATH DENY exists solely to let us deny all users access to specific paths, 
unless they have a specified user role.

This can be thought of as a very quick-and-dirty access control module.


WHY USE THIS MODULE?
====================
- You want to disable anonymous access to some system paths 
  (e.g., taxonomy/term/*)
- 


INSTALLATION
============
Install like any other Drupal module. 


CONFIGURATION
=============
Go to: /admin/config/people/path-deny

Enter Path Deny rules, one per line. Each rule is composed of a single path,
and user role(s) required to view it. All items are comma-delimited.

Examples:
  taxonomy/term/*,administrator,editor
    This denies access to /taxonomy/term/* paths unless the current user has
    either the 'administrator' or 'editor' role.

  my-secret-page,special-user
    This denies access to /my-secret-page unless the current user has the
    'special-user' role.
  

The configuration values can also be set via settings.php. E.g.:

$conf['path_deny_config'] = implode("\n", array(
  "; Only admin or editor can see edit taxonomy terms.",
  "admin/structure/taxonomy/*,administrator,editor",

  "; Only admin or editor can see the menu of vocabularies.",
  "admin/structure/taxonomy,administrator,editor",

  "; Allow the blog user to edit blog topics.",
  "admin/structure/taxonomy/topics,administrator,editor,blog",

  "; Disallow accessing Drupal's taxonomy/term* paths.",
  "taxonomy/*,",
));

Note: Lines begining with a semi-colon are treated as a comment and ignored.


ISSUES
======
We're using paths as a check. If a page has an alternate way of being accessed
(e.g., node/[nid], non-clean paths, etc.) users may be able to circumvent 
these restrictions.

This module assumes you're aware of these issues and know when/when not this
is applicable.


AUTHOR/MAINTAINER
=================
Kendall Anderson <dailyphotography at gmail DOT com>
http://invisiblethreads.com


CHANGELOG
=========
v7.x-1.0, 2013-11-30, Kendall Anderson
- initial development of module


TODO
====
- better documentation!
- integrate debugging into watchdog
