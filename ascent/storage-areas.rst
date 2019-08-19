.. _storage-areas:

Storage Areas
=============

The Ascent has the following storage areas available.

NFS Directories
---------------

This is where you might want to keep source code and build your application.

NOTE: These directories are read-only from the compute nodes!

.. code-block:: bash

	/ccsopen/home/userid

Your personal home directory

.. code-block:: bash

	/ccsopen/proj/gen132

Can be accessed by all participants of this event

You can create a directory here with your application name to collaborate with others (source code, scripts, etc.)



GPFS Directories (parallel file system)
---------------------------------------

This is where you should write data when running on Ascent’s compute nodes.

.. code-block:: bash

	/gpfs/wolf/gen132/scratch/userid

Your personal GPFS scratch directory

 
.. code-block:: bash

	/gpfs/wolf/gen132/proj-shared

Can be accessed by all participants of the event

You can create a directory here with your application name to collaborate with others (data written from compute nodes)
