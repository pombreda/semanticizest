.. semanticizest documentation master file, created by
   sphinx-quickstart on Tue Nov 18 15:37:15 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Semanticizer, standalone
========================

semanticizest (Semanticizer, STandalone) is a package for entity
linking, aka semantic linking, semanticizing, or wikification:
You feed it text, and it outputs links to pertinent Wikipedia concepts.
You can use these links as a "semantic representation" of the text
for NLP or machine learning,
or just to provide some links to background info on the Wikipedia.


Quick usage
-----------

First we need to create a model for the semanticizer.
The following command will download and read a wikipedia dump
(in this case the Limburgish wiki, just because it's small)
and subsequently create and store the corresponding model.
If you want the English Wikipedia, replace ``liwiki`` by ``enwiki``
and be prepared to run ``parse_wikidump`` overnight on a server.

.. code:: bash

    python -m semanticizest.parse_wikidump --download liwiki liwiki.model

Fire up a Python interpreter and import the required modules::

    >>> import re
    >>> from semanticizest import Semanticizer

Load the model from disk::

    >>> sem = Semanticizer('liwiki.model')

Set up a piece of sample text and tokenize it::

    >>> text = """'ne Donjon is 'ne zjwaore verdedigingstaore,
    ... meistal geboewd op 'ne hoage heuvel, de opperhaof,
    ... dae deil oetmaak van 'n motte."""
    >>> tokens = re.findall('\w+', text)

Feed the tokens to the semanticizer to get the entity link
candidates::

    >>> for cand in sem.all_candidates(tokens):
    ...     print(cand)
    (7, 8, u'Taore (boewwerk)', 1.0)
    (13, 14, u'Heuvel', 1.0)
    (15, 16, u'Opperhaof', 1.0)
    (21, 22, u'Motte', 1.0)

As we can see, it finds four entity candidates in this short text. The
first entity found is 'Taore (boewwerk)', corresponding to the seventh
token: 'verdedigingstaore'.

Contents
========

.. toctree::
   :maxdepth: 2

   api
   algorithm



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`


Developed by
============

.. TODO find a better way of displaying these (in the theme?)

.. figure:: _static/logo_uva.png

   `ILPS, University of Amsterdam <http://ilps.science.uva.nl>`_

.. figure:: _static/logo_nlesc.png

   `Netherlands eScience Center <http://esciencecenter.nl>`_
