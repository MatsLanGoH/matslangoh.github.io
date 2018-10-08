.. title: Deploying Nikola to GitHub
.. slug: deploying-nikola-to-github
.. date: 2018-10-08 21:32:45 UTC+09:00
.. tags: nikola, blog
.. category: blog
.. link: https://getnikola.com/handbook.html#deploying-to-github
.. description: How to deploy a Nikola blog to Github Pages
.. type: text

Alright, so this new shiny blog is running nicely on our development machine,
but we'd like to share it with the rest of the world. For now, let's go with
Github Pages.

.. TEASER_END

Create a personal Github Pages Repository
=========================================

From the `Github Page <https://www.github.com>`_, create repository with the
following name: ``<Your Github Username>.github.io``

Initialize a git repository in your Nikola source directory
===========================================================

Now go to your Nikola source directory and run the following commands.

.. code::

  $ git init .
  $ git remote add origin git@github.com:<Your Github Username>/<Your Github
  Username>.github.io.git

Setup branches and remotes in ``conf.py``
=========================================

For a github user page (`user.github.io`), the default settings should be good
to go, but have a look at the following items in `conf.py`.

- ``GITHUB_DEPLOY_BRANCH``
- ``GITHUB_SOURCE_BRANCH``
- ``GITHUB_REMOTE_NAME``
- ``GITHUB_COMMIT_SOURCE``

Create a ``.gitignore`` file
============================

Add at least the following entries.

.. code::

  cache
  .doit.db
  __pycache__
  output  

And finally, deploy
===================

Run ``nikola github_deploy``. This should build the site, commit the output
folder to the deploy branche, and push to GitHub. Your website should be up and
running very soon.
