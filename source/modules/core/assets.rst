.. index:: Core; Assets

Assets
^^^^^^

Assets are common JS libraries like jquery_, bootstrap_ or select2_. It makes sense to manage these assets by npm_. This
means, all needed JS libraries are listed in `package.json`. If an additional library is needed, it can be added via
``npm i --save-dev <packagename>``. This will update the `package.json` and download the package to the `node_modules`
directory. Our `bin/install-assets.sh` copies all needed javascript, css, fonts, etc. files to the ``public/assets``
directory, which is accessable by the web server.

You can download all required JS files and copy them to their location in the assets dir with:


.. code-block:: sh

  npm install
  bin/install-assets.sh

You can allways remove and reinstall assets with

.. code-block:: sh

  rm -R public/assets/*
  npm install
  bin/install-assets.sh

this will copy all needed JS files into ``public/assets``.

.. _jquery: https://www.npmjs.com/package/jquery
.. _bootstrap: https://www.npmjs.com/package/bootstrap
.. _select2: https://www.npmjs.com/package/select2
.. _npm: https://www.npmjs.com/