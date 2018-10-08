.. title: How to get started with Nikola
.. slug: how-to-get-started-with-nikola
.. date: 2018-10-08 21:04:53 UTC+09:00
.. tags: nikola, blog
.. category: blog
.. link: https://getnikola.com/
.. description: How to get started with Nikola
.. type: text

It's been about 6 months since I've made my career change from teacher to
software developer. Time to start a blog to document the things I've learned on
and off the job.

To keep it simple, I've picked `Nikola  <https://getnikola.com>`_ to set up
this blog. It's a static site generator, ready to roll in a couple of minutes.

.. TEASER_END

The Basics
==========

I've initially built my site on macOS, so here's the basic requirements.

#. Install Homebrew.
#. Install Python and pip with `brew install python3`
#. Install virtualenv with `sudo pip3 install virtualenv`

Then follow these instructions.

.. code::

  $ virtualenv3 ~./virtualenvs/nikola
  $ source ~/.virtualenvs/nikola/bin/activate
  $ pip install --upgrade pip setuptools wheel
  $ pip install --upgrade "Nikola[extras]"

Initializing a site
===================

Simply run `nikola init <directory_name>`, then tell the wizard what you need.

Build the site
==============

Type `nikola build`, then `nikola serve` to check the site locally.

Create a first post
===================

Type `nikola new_post -e`, and have at it.
If you're unfamiliar with reStructuredText, you can also configure Nikola to
use Markdown instead.

Rebuild the site
================

Once more, type `nikola build`, followed by `nikola serve --browser`, or
`nikola auto --browser` to start the development server.

