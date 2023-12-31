.. _ref-python3:

================
Python 3 Support
================

As of Haystack v2.1.0, it has been ported to support both Python 2 & Python 3
within the same codebase. This builds on top of what `six`_ & `Django`_ provide.

No changes are required for anyone running an existing Haystack
installation. The API is completely backward-compatible, so you should be able
to run your existing software without modification.

Virtually all tests pass under both Python 2 & 3, with a small number of
expected failures under Python (typically related to ordering, see below).

.. _`six`: http://pythonhosted.org/six/
.. _`Django`: https://docs.djangoproject.com/en/stable/topics/python3/#str-and-unicode-methods


Supported Backends
==================

The following backends are fully supported under Python 3. However, you may
need to update these dependencies if you have a pre-existing setup.

* Solr (pysolr>=3.1.0)
* Elasticsearch


Notes
=====

Testing
-------

If you were testing things such as the query generated by a given
``SearchQuerySet`` or how your forms would render, under Python 3.3.2+,
`hash randomization`_ is in effect, which means that the ordering of
dictionaries is no longer consistent, even on the same platform.

Haystack took the approach of abandoning making assertions about the entire
structure. Instead, we either simply assert that the new object contains the
right things or make a call to ``sorted(...)`` around it to ensure order. It is
recommended you take a similar approach.

.. _`hash randomization`: http://docs.python.org/3/whatsnew/3.3.html#builtin-functions-and-types
