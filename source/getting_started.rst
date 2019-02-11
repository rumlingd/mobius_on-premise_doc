.. _installation-label:

Getting started
==================

All you need in order to use our test API is the Mobius Key. To get the key contact our sales team by e-mail sales@mobius.ml.

The Mobius Key
--------------

The Mobius Key have to be passed as an argument by adding a `?MOBIUS_KEY=<your_key>` after the command.

For example:
::

  curl http://webdemo.mobius.ml/test_api/predict/concepts?MOBIUS_KEY=<your_key>
        -X POST -F "data=@./your_image.jpg"


In case of error message please visit troubleshooting section.
