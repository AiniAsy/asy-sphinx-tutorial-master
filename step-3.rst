Step 3: Keeping Documentation Up to Date
========================================

Now we have a wonderful set of documentation,
so we want to make sure it stays up to date and correct.

There are two factors here:
* The documentation is up to date with the code
* The user is seeing the latest version of the docs

We will solve the first problem with Sphinx's :mod:`~sphinx.ext.doctest` module.
The second problem we will solve by deploying our docs to `Read the Docs`_.

Concepts
********

Testing your code
-----------------

Sphinx ships with a ``doctest`` module which is quite powerful.
It allows you to run tests against your code inside your docs.
This means that you can verify all of the code examples work,
so that your docs are always up to date with your code!

.. warning:: This only works for Python currently.

You can read the full Sphinx docs for :mod:`~sphinx.ext.doctest`,
but here is a basic example::

	>>> sum(2, 2)
	4

When you run this example,
Sphinx will validate the return is what is expected.

Tasks
*****

Add doctests to our utils
-------------------------

The utils module is inside ``crawler`` is a good candidate for testing.
It has small,
self-contained pieces of logic that will work great as doctests.

Add a ``utils.rst`` module to your project that looks like:

.. literalinclude:: crawler/docs/step3/utils.rst
   :language: rst
   :linenos:

.. note::
   Live Preview: :doc:`crawler/docs/step3/utils`

As you can see here,
we are actually testing our logic.
It also acts as documentation for your users,
and is included in the output of your documentation.

These doctests do double duty,
acting as **tests and documentation**.

Caveats
~~~~~~~

Note that we have to import our code in the ``testsetup::`` block.
This is so that Sphinx can call the functions properly in our doctest blocks.
This is hidden in the output of the docs though,
so users won't be confused.

.. note:: You can also put doctest blocks directly in your docstrings.
		  They will need to include full import paths though,
		  as Sphinx can't guarentee the ``testsetup::`` directive will be called.

Read the Docs
-------------

Last but not least,
once you've written your documentation you have to put it somewhere for the world to see!
Read the Docs makes this quite simple,
and is free for all open source projects.

* Register for an account at http://readthedocs.org
* Click the *Import Project* button
* Add the URL for a specific repository you want to build docs for
* Sit back and have a drink while Read the Docs does the rest.

It will:
	* Pull down your code
	* Install your ``requirements.txt``
	* Build HTML, PDF, and ePub of your docs
	* Serve it up online at ``http://<projectname>.readthedocs.org``

Let's see what that looks like in practice.

Extra Credit
************

Have some extra time left?
Let's run the code and see if it actually works!

Run the crawler
---------------

Go ahead and run the crawler against the Read the Docs documentation::

	# in crawler/src/crawler
	python main.py -u https://docs.readthedocs.org

You should see your terminal start printing output,
if your internet if working.

Can you add another command line option,
and document it?