Step 1: Getting started with RST & Sphinx
=========================================

.. note:: I'm a firm beliver that tutorials should 
          make you feel like a hero in the first 30 minutes.
          Step 1 aims to show you the power of Sphinx,
          and reach a moment of "kick ass!" as quickly as possible.

Now that we have our basic skeleton,
let's document the project.
As you might have guessed from the name,
we'll be documenting a basic web crawler.

For this project,
we'll have the following pages:

* Index Page
* Support
* Installation
* Cookbook/Examples
* Command Line Options
* API

Let's go over the concepts we'll cover,
and then we can talk more about the pages to create.

Concepts
********

.. index::
  pair: Syntax; Hyperlink

Hyperlink Syntax
----------------

The link text is set by putting a ``_`` after some text.
The ````` is used to group text,
allowing you to include multiple words in your link text.
You should use the `````,
even when the link text is only one word.
This keeps the syntax consistent.

The link target is defined at the bottom of the section with ``.. _<link text>: <target>``.

.. index::
   pair: Syntax; Code Example

Code Example Syntax
-------------------

The syntax for displaying code is ``::``.
When it is used at the end of a sentence,
Sphinx is smart and displays one ``:`` in the output,
and knows there is a code example in the following indented block.

Sphinx,
like Python,
uses meaningful whitespace.
Blocks of content are structured based on the indention level they are on.
You can see this concept with our ``code-block`` directive later.

.. index::
   pair: Syntax; TOC Tree

.. _toctree-syntax:

Table of Contents Tree
----------------------

Now would be a good time to introduce the ``toctree``.
One of the main concepts in Sphinx is that it allows multiple pages to be combined into a cohesive hierarchy.
The ``toctree`` directive is a fundamental part of this structure.
A simple ``toctree`` directive looks like this::

  .. toctree::
     :maxdepth: 2

     install
     support

This will then output a Table of Contents in the page where this occurs.
The ``maxdepth`` argument tells Sphinx include 2 levels of headers in it's output.
It will output the 2 top-level headers of the pages listed.
This also tells Sphinx that the other pages are sub-pages of the current page,
creating a "tree" structure of the pages::

    index
    ├── install
    ├── support

The TocTree is also used for generating the navagation elements inside Sphinx.
It is quite important,
and one of the most powerful features of Sphinx.

Tasks
*****

Create Support page
-------------------

It's always important that users can ask questions when they get stuck.
There are many ways to handle this,
but normal approaches are to have an IRC channel and mailing list.

Go ahead and put this markup in your ``support.rst``:

.. literalinclude:: crawler/docs/step1/support.txt
   :linenos:

.. note::
   Live Preview: :doc:`crawler/docs/step1/support`

Create Installation page
------------------------

Installation documentation is really important.
Anyone who is coming to the project will need to install it.
For our example,
we are installing a basic Python script,
so it will be pretty easy.

Include the following in your ``install.rst``:

.. literalinclude:: crawler/docs/step1/install.txt
   :linenos:

.. note::
   Live Preview: :doc:`crawler/docs/step1/install`

Add TocTree
-----------

Now you need to tie all these files together. 
As we mentioned above,
the :ref:`toctree-syntax` is the best way to do this.
Go ahead and complete the ``toctree`` directive in your ``index.rst`` file,
adding the new pages.

Sanity Check
------------

Your filesystem should now look something like this::

    crawler
    └── docs
        ├── index.rst
        ├── support.rst
        ├── install.rst
        ├── conf.py

Build Docs
----------

Now that you have a few pages of content,
go ahead and build your docs again::

  make html

If you open up your ``index.html``,
you should see the basic structure of your docs from the included ``toctree`` directive.

Extra Credit
************

Have some extra time left?
Check out these other cool things you can do with Sphinx.

Make a manpage
---------------

The beauty of Sphinx is that it can output in multiple formats,
not just HTML.
All of those formats share the same base format though,
so you only have to change things in one place.
So you can generate a manpage for your docs::

  make man

This will place a manpage in ``_build/man``.
You can then view it with::

  man _build/man/crawler.1

Create a single page document
-----------------------------

Some people prefer one large HTML document,
instead of having to look through multiple pages.
This is another area where Sphinx shines.
You can write your documentation in multiple files to make editing and updating easier.
Then if you want to distribute a single page HTML version::

  make singlehtml

This will combine all of your HTML pages into a single page.
Check it out by opening it in your browser::

    open _build/singlehtml/index.html

.. note:: You'll notice that it included the documents in the order
          that your :ref:`TOC Tree <toctree-syntax>` was defined.


Now it is time to move on to :doc:`step-2`.