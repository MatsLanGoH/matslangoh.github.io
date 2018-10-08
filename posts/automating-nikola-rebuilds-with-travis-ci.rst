.. title: Automating Nikola rebuilds with Travis CI
.. slug: automating-nikola-rebuilds-with-travis-ci
.. date: 2018-10-08 21:53:15 UTC+09:00
.. tags: nikola, blog
.. category: blog
.. link: https://getnikola.com/blog/automating-nikola-rebuilds-with-travis-ci.html
.. description: Automatically update your blog using the magic of CI
.. type: text

The ``github_deploy`` command included with Nikola is nice to have, but you
need to have a working build environment to update your blog.

Wouldn't it be much more convenient if we could just write or update a post and
see the changes automagically appear on our website? Using continuous
integration, we can do just that.

.. TEASER_END

Setting up Nikola
=================

We need to make **one important change** to our ``config.py``. 

.. code::

  GITHUB_COMMIT_SOURCE = False

Without this change, Travis CI is going to get trapped in an infinite loop.

Setting up Travis CI
====================

First, let's install ``ruby`` and ``gem`` if we don't have them.

Next, let's get ``travis.yml`` from https://getnikola.com/blog/automating-nikola-rebuilds-with-travis-ci.html and save it as ``.travis.yml``
Then, update these lines

  .. code::

    git config --global user.name 'Your Username'
    git config --global user.email 'Your email'
    git remote add origin git@github.com:YOUR_USERNAME/YOUR_REPO.git

If you want extra languages, add the correct packages under the following
section.

  .. code::

    addons:
      apt:
        packages:
        - language-pack-en-base

Next, let's generate a SSH key for Travis CI

  .. code::

    echo id_rsa >> .gitignore
    echo id_rsa.pub >> .gitignore
    ssh-keygen -C TravisCI -f id_rsa -N ''

Copy the contents of ``id_rsa.pub`` and add them to `Github -> Your Page
Repository -> Settings -> Deploy keys`. Make sure, `Allow write access` is checked.

Playing nice with Ruby
======================

Install the ``travis`` gem.

  .. code::

    gem install --user-install travis

We can now use the Travis CI command-line client to `log in`, `enable the repository`, and `encrypt our SSH key`.

  .. code::

    $ travis login

    We need your GitHub login to identify you.
    This information will not be sent to Travis CI, only to api.github.com.
    The password will not be displayed.

    Try running with --github-token or --auto if you don't want to enter your password anyway.

    Username: MyUsername 
    Password for MyUsername: ********************************************************
    Successfully logged in as MyUsername!

    $ travis enable

    Detected repository as MyUsername/myusername.github.io, is this correct? |yes| yes
    MyUsername/myusername.github.io: enabled :)

    $ travis encrypt-file id_rsa --add

    encrypting id_rsa for MyUsername/myusername.github.io
    storing result as id_rsa.enc
    storing secure env variables for decryption

    Make sure to add id_rsa.enc to the git repository.
    Make sure not to add id_rsa to the git repository.
    Commit all changes to your .travis.yml.

Finally, commit everything to GitHub.

  .. code::

    $ git add .
    $ git commit -am "Automate builds with Travis CI"
    $ git push


Watch Travis CI do its job
==========================

After a couple of minutes, your site should be good to go.

Check the status of your builds at `<https://travis-ci.org/>`_


