How To
===================


Release
-----------

Publish process is based on `sbt-sonatype <https://github.com/xerial/sbt-sonatype>`_ plugn 

Export credentials for sonatype repository:

.. code-block:: bash
	export SONATYPE_USERNAME=???
	export SONATYPE_PASSWORD=???

To publish signed artifacts to sonatype repository use

.. code-block:: bash
	sbt publishSigned

After that close taging repository and release to central using

.. code-block:: bash
	sbt sonatypeRelease





