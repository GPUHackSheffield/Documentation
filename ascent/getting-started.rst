.. _getting-started:

Getting Started
===============

Once you have access to Ascent, log in

.. code-block:: bash

	ssh USERNAME@login1.ascent.olcf.ornl.gov

From your ``/ccsopen/home/userid`` directory:

.. code-block:: bash

	git clone https://code.ornl.gov/t4p/Hello_jsrun.git
	cd Hello_jsrun
	
Load CUDA Toolkit

.. code-block:: bash

	module load cuda

Compile the code

.. code-block:: bash

	make
	
Grab a Single Node in an Interactive Job Using LSF and load the CUDA Toolkit

.. code-block:: bash

	bsub –P GEN132 –nnodes 1 –W 30 –alloc_flags “gpumps” –Is /bin/bash
	
GEN132 is the project ID provided for the Hackathon.

The ``-alloc_flags “gpumps”`` enables the MPS server – essentially allowing multiple processes (e.g., MPI ranks) to access the same GPU concurrently. Whether or not to include it depends on your application, but it is included here since (when testing different layouts) you might attempt to target the same GPU with multiple MPI ranks. If you do so without MPS, this program will hang.

Launch a Simple Job Configuration with jsrun by setting the number of OpenMP threads to ``1`` (for simplicity)

.. code-block:: bash

	export OMP_NUM_THREADS=1

Launch the job

.. code-block:: bash

	jsrun –n6 –c1 –g1 ./hello_jsrun | sort
	########################################################################
	*** MPI Ranks: 6, OpenMP Threads: 1, GPUs per Resource Set: 1 ***
	========================================================================
	MPI Rank 000, OMP_thread 00 on HWThread 000 of Node h49n16 - RT_GPU_id 0 : GPU_id 0
	MPI Rank 001, OMP_thread 00 on HWThread 005 of Node h49n16 - RT_GPU_id 0 : GPU_id 1
	MPI Rank 002, OMP_thread 00 on HWThread 009 of Node h49n16 - RT_GPU_id 0 : GPU_id 2
	MPI Rank 003, OMP_thread 00 on HWThread 089 of Node h49n16 - RT_GPU_id 0 : GPU_id 3
	MPI Rank 004, OMP_thread 00 on HWThread 093 of Node h49n16 - RT_GPU_id 0 : GPU_id 4
	MPI Rank 005, OMP_thread 00 on HWThread 097 of Node h49n16 - RT_GPU_id 0 : GPU_id 5
	
Summit Node Diagram
-------------------

Use the `Summit node diagram <https://code.ornl.gov/t4p/Hello_jsrun/blob/master/node_images/Summit_Node.pdf>`_ to understand how your MPI ranks are being assigned to the hardware.

Also, see the Hardware Threads section of the `Summit User Guide <https://goo.gl/Fj8bTE>`_ to understand the difference between the 42 physical coresper node versus the 4 hardware threads per physical core.